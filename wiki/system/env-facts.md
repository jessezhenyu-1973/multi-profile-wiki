# 环境与基础设施事实

> 本页承接原 MEMORY.md 中的密集环境事实。记忆文件只保留指向本页的指针，详情在此维护。

## Oracle Cloud VPS
- **公网 IP** `129.80.125.206`，主机名 `3x-ui`，Ubuntu 24，用户 `ubuntu`
- **SSH 私钥**：`~/下载/ssh-key-2026-08-26.key`
- **3x-ui 面板** v3.7：`http://100.75.28.79:1286/1gce3WdCHKSyQx7azV/`（用户 jesse）
  - 代理：`VLESS-Reality@443`，伪装 `yahoo.com`
  - 坑：v3.7 客户端在独立 `clients` 表 + `client_inbounds`（`flow_override` 存 flow），直接写 `inbounds.settings.clients` 无效
- **Tailscale**：VPS `100.75.28.79`；本机 `100.95.78.116`（jesse-gem12）；NAS `100.69.128.20`；手机 `v2436a`
- **系统加固**：BBR + 2G swap；fail2ban；`sudo` 免密已配（`/etc/sudoers.d/jesse`，`SUDO_PASSWORD` 在 `.env`）

## 模型配置（2026-09-10 更新）
- **主模型**：`agnes-3.0-flash @ custom`（`https://apihub.agnes-ai.com/v1`，key 在 `.env` `HERMES_CUSTOM_APIHUB_AGNES_AI_COM_API_KEY`）
  - 实测文本 200/1.4s；**支持视觉**（base64 PNG 识读 OK，content 非空）；reasoning 模型，短输出时 content 可能空、答案在 reasoning_content，给足 max_tokens 即正常
- **fallback 链**（4 条全实测 200，跨供应商冗余）：
  1. `openrouter/nvidia/nemotron-3-ultra-550b-a55b:free`（550B 最强，偶发上游 overload）
  2. `openrouter/nvidia/nemotron-3-super-120b-a12b:free`
  3. `openrouter/z-ai/glm-5.3-flash`
  4. `nous/meituan/longcat-2.0:free`
- **OpenViking VLM/记忆抽取 = 主模型**（2026-09-10 起两机统一指向 `agnes-3.0-flash @ apihub`，见下节）
- **Zen keyless**：`chat/completions` 带 `Bearer` token 反而 401，须**不带 Authorization**，仅 `hermes-cli` UA

## 数据源
- **baostock**：股票代码需 `sh.`/`sz.` 前缀（如 `sh.600519`）；`query_stock_industry` 返回 `code/code_name/industry` 列
- **同花顺**：`hithink-finance` CLI
- **其他 MCP**：akshare、东方财富妙想

## 量化项目交付物
- **135 策略**：`/home/jesse/135-strategy/`
  - V18-ATR 定稿：V17 信号 + `ATR(14)×2.5` 追踪止损，移除一箭穿心，组合层 `10%×5只`
  - 本地领先 `origin/main` 10 个提交，push 被 main 分支保护拦截 → 待 PR 或解保护后直推
  - Hermes-Team 内回测引擎：入口 `wiki/projects/135-strategy/outputs/run_135_position_backtest_v17.py`
- **龙头战法选股 v2.0**：`/home/jesse/leading-stock-strategy/run_leading_stock.py`
  - Cron 任务 `fa180ca066e2`：每周一至周五 16:00 触发，策略执行约 5-10 分钟
- **DMI 多因子最佳**：v4 信号共振（+29.05%，夏普 0.75）

## 长期约定
- 每日记录进展，保证工作连续性。

## 双机热备互探 (2026-09-05 建立)

- **架构**: gem12 (Linux, 100.95.78.116) <-> JesseHomeNAS (fnOS Linux, 100.69.128.20) 互为备份, 保障 135战法选股/持仓盯盘/收盘采集任务单台宕机不中断
- **双向 SSH**: 已打通 (远端公钥已加到本机 ~/.ssh/authorized_keys; 本机->远端原本就有)
- **探测脚本**: `~/135-strategy/outputs/peer_monitor.py` (两边各一份, 按主机名自动识别对端, PEER_HOST 可覆盖)
  - 探测项: 对端/本机 gateway 进程、主模型 59.35.206.146:8000 /v1/models 连通、cron 任务 last_status、135 数据新鲜度(outputs/ 最新 json)、磁盘、**OpenViking 记忆库 /ready**(读各自 ovcli.conf 的 url: gem12 探 100.69.128.20:1933 客户端视角, NAS 探 127.0.0.1:1933 server 本体, 不 ready 报 CRIT)
  - 告警去重: 状态文件 ~/.hermes/peer_monitor_state.json, 相同告警 30min 冷却, 恢复时发一次恢复通知
- **看门狗 cron**: 两边各一个 "双机互探看门狗(135热备)", no_agent 模式, `*/30 9-20 * * 1-5`, 脚本 ~/.hermes/scripts/peer_monitor_watchdog.py (薄包装, 实际逻辑在 135-strategy/outputs/)
  - 有异常才推飞书(本机 oc_ee25c8415ec4a9623907d2b25cb4d646 / 远端 oc_fb67079b7382718648e532bf938cd6fb), 全绿静默, 零 LLM 成本
  - 本机 job_id 6d2650365493, 远端 job_id c45cddbe316d
- **注意**: 远端 hermes 版本较旧, cron 改任务用 `hermes cron edit <id>` 而非 `update`

## OpenViking 长期记忆 (2026-09-05 部署)

> 解决"老是忘记"：中心化记忆库 + 自动语义召回。两个 Hermes 共享同一记忆空间。

- **Server**: NAS `100.69.128.20:1933`（host 网络），Docker 容器 `openviking`，镜像 `ghcr.io/volcengine/openviking:latest`
  - 数据卷 `~/.openviking`（挂载到容器 `/app/.openviking`），配置 `~/.openviking/ov.conf`
  - root key `~/.openviking/.root_key`；租户 user key `~/.openviking/.user_key`（account=jesse, user=hermes）
  - 记忆空间：`viking://user/hermes/...`（两机共享同一空间）
- **模型**：
  - embedding：NAS 本地 ollama 容器（host 网络 :11434）+ `nomic-embed-text`（768 维）
  - VLM/记忆抽取（2026-09-10 更新）：**两机统一指向主模型 `agnes-3.0-flash @ https://apihub.agnes-ai.com/v1`**（key 在各自 `~/.hermes/.env` 的 `HERMES_CUSTOM_APIHUB_AGNES_AI_COM_API_KEY`）；实测支持视觉、reasoning 模型 content 正常
  - 历史：此前 NAS 用 `qwen3.8-27b-vision @ 59.35.206.146:8000/v1`、gem12 用 `openrouter/nemotron-3-super-120b:free`，均已被 agnes 替换
  - 改配置：NAS 改 `~/.openviking/ov.conf` 的 `vlm` 块后 `docker restart openviking`；gem12 同文件后 `systemctl --user restart openviking.service`（两机部署不同：NAS 是 Docker 容器，gem12 是 uv + systemd user service）
- **两个 Hermes 接入**（都指向同一 server + 同一 user key）：
  - 本机 gem12：`memory.provider=openviking`，`memory.openviking.use_ovcli_config=true`，ovcli `~/.openviking/ovcli.conf` → `http://100.69.128.20:1933`
  - NAS：同上，ovcli → `http://127.0.0.1:1933`（同机更快）
  - 改完配置须 `systemctl --user restart hermes-gateway.service` 生效
- **坑**：
  - OpenViking ollama provider 走 OpenAI 兼容接口，`api_base` 必须带 `/v1`（否则 embedding 404）
  - 插件默认**不读** ovcli.conf，须 `use_ovcli_config: true`；api_key 模式下 server 从 key 推导身份，不发 account/user 头
  - 写入 URI 命名空间是 `viking://user/hermes/...`（user 名=key 里的 hermes，不是 default）
  - 召回端点 `/api/v1/search/find`，写入端点 `/api/v1/content/write`
- **验证**：本机插件 client 写入 → NAS 侧召回命中（score 0.99+），共享确认
- **markdown wiki 不受影响**：llm-wiki / Hermes-Team/wiki 仍各机各一份，OpenViking 只加"自动召回"层

## multi-profile-wiki 推送流程 (2026-09-10 修订, 实测)

- **仓库**: github.com/jessezhenyu-1973/multi-profile-wiki；`main` 受保护: `enforce_admins=true`（owner 可绕过直推）
- **实测事实（2026-09-10）**: 该仓库旧版 branch-protection 的 **review 子端点写操作全部 404**（DELETE/PUT 子端点都 Not Found），主端点 PUT 整体 422（"No subschema matched"，`-f required_status_checks=null` 等字段类型校验失败）——旧 API 在此仓库基本只读。而 owner 用 gh token 直推 `main` **成功**（`enforce_admins` 允许 admin 绕过保护，b5e941b→f8ac643 均如此）。**结论: 不需要"解保护→推→恢复保护"三步，直接带 token 推即可。**
- **标准流程** (NAS 无 GitHub 直连, 须经 GEM12 中转):
  1. 改动的机器上 `git commit`
  2. 传改动到 GEM12: `git bundle create /tmp/x.bundle main` → `scp` → GEM12 上 `git fetch /tmp/x.bundle main && git merge FETCH_HEAD --no-edit`
  3. **GEM12 推送必须带 token，否则挂起**（实测坑）: GEM12 的 `git credential.helper=store` 无凭据时 `git push origin main` / `git ls-remote` 会卡交互提示直到超时。正确姿势:
     ```bash
     TOK=$(gh auth token)
     git push "https://x-access-token:${TOK}@github.com/jessezhenyu-1973/multi-profile-wiki.git" main
     ```
     诊断挂起先 `git ls-remote origin main`（会立刻挂），别盲目重试 push
  4. 对齐: 改动机 `git fetch origin && git reset --hard origin/main`，三方 `git log -1` 核对一致
- **已知遗留**: 09-05 记录的"1 approving review"保护现已不可读/写（API 404，可能在 rulesets 体系下）；当前可验证的保护 = `enforce_admins=true` + `required_conversation_resolution=true`。owner admin token 推不受阻。
- **OpenViking 灌库**: llm-wiki + 135-strategy 项目 wiki 已于 2026-09-05 灌入 `viking://resources/` (两机共享可检索); 重复入队会产生 `_1` 后缀目录, 用容器内 `ov rm -r` 删 (处理中会 CONFLICT, 等解锁)
