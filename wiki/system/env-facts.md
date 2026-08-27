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

## 模型配置（2026-08-26 实测）
- **主模型**：`opencode-free/hy3-free`（x-preview-f-free 下架替换）
- **视觉**：hy3 假视觉 → config 声明 `supports_vision:false`，图片走 `vision_analyze`
- **fallback 链**：`qwen38-local/Qwen3.8-27B@59.35.206.146:8000/v1`（真视觉）→ `openrouter/nemotron-3-ultra:free` → `nvidia/nemotron-3-super-120b`
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
