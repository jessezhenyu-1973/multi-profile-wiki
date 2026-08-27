# 记忆系统管理规范

> 本文件说明 Jesse 的记忆系统如何分层、各自职责，以及维护约定。由 Hermes Agent 在 2026-08-27 整理。

## 三层记忆架构

| 层 | 位置 | 职责 | 维护者 |
|---|---|---|---|
| **Hermes 内置记忆** | `~/.hermes/memories/MEMORY.md` + `USER.md` | 每轮注入的**高信号事实**：环境事实、项目路径指针、长期约定。保持精简（目标 <1.5KB），详情下沉 Wiki。 | Hermes Agent |
| **Multi-Profile Wiki** | `/home/jesse/Hermes-Team/wiki/` | **项目级知识**：策略文档、回测报告、任务/日志、多 Profile 协作上下文。有 git 版本控制。 | BOSS 工作流 / 各 Profile |
| **Obsidian 知识库** | `/home/jesse/llm-wiki/` | **通用知识**：概念、实体、MOC 主题地图，双链知识飞轮。唯一 canonical vault（原 Hermes-Wiki 已并入删除）。 | Hermes Agent |

## 分工原则

1. **MEMORY.md 只放"指针+环境事实"**，不放过程/细节。任何可长到几 KB 的内容都属于 Wiki。
2. **项目知识** → `Hermes-Team/wiki/projects/<name>/`（README 入口 + outputs 交付脚本）。
3. **通用/跨项目知识**（如 agency-agents-zh 268 角色、AI 工作流）→ `llm-wiki/`。
4. **脏工作树处理**：Hermes-Team 的 `outputs/` 中 scratch（v1-v16、debug_*、test_*、*.csv）已被 `.gitignore` 排除；仅最终交付脚本（如 `run_135_position_backtest_v17.py`）纳入版本控制。
5. **破坏性操作前先备份**：`~/.hermes-backup/` 保留 Hermes-Wiki 归档、MEMORY/USER .bak、outputs scratch tar，可恢复。

## 当前状态（2026-08-27）

- MEMORY.md: 2022B（精简完成）；USER.md: 874B
- Hermes-Team: git 干净，3 个清理提交
- Obsidian: 仅 `llm-wiki` 一个 vault，obsidian.json 已重定向
- 备份: `~/.hermes-backup/`（Hermes-Wiki-*.tar.gz、135-strategy-outputs-*.tar.gz、MEMORY/USER/obsidian.json .bak）
