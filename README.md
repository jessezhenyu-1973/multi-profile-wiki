# 多 Profile + Wiki 协作系统

> AI 项目协作系统 — 多 Profile 隔离 + Wiki 共享上下文 + BOSS 模式任务编排

## 项目概述

这是一个为 Hermes Agent 多 Profile 环境设计的协作系统，通过 Wiki 实现 Profile 之间的知识共享和任务编排，解决多 Profile 间的"记忆污染"问题。

## 核心架构

### 三层设计

```
┌─────────────────────────────────────────────────────┐
│                   BOSS 模式 (老板)                     │
│           需求澄清 → 任务拆解 → 自动执行 → 汇总交付         │
├─────────────────────────────────────────────────────┤
│                     Wiki 层                           │
│   shared/ 共享上下文  │  wiki/ 知识文档  │  outputs/   │
│       任务记录          │  协作协议          │   产出物     │
├──────────────┬────────────────┬──────────────────────┤
│   协调者       │   研究员         │    执行者              │
│  Coordinator  │   Analyst      │    Executor            │
│  (SOUL.md)   │  (SOUL.md)     │   (SOUL.md)            │
└──────────────┴────────────────┴──────────────────────┘
```

### Profile 隔离

- 每个 Profile 有独立的 `SOUL.md`（人格/角色定义）
- 通过 Wiki 的 `shared/` 目录共享上下文和任务记录
- 各 Profile 的 `memory/`、`cron/`、`skills/` 完全隔离

## 目录结构

```
multi-profile-wiki/
├── profiles/                    # Profile 配置目录
│   ├── coordinator/             # 协调者 Profile (BOSS 模式)
│   │   └── SOUL.md              # 角色定义
│   ├── analyst/                 # 研究员 Profile
│   │   └── SOUL.md
│   └── executor/                # 执行者 Profile
│       └── SOUL.md
├── wiki/                        # Wiki 知识库
│   ├── pages/                   # 知识页面
│   │   ├── boss-mode.md         # BOSS 模式工作流文档
│   │   └── ...
│   └── ...
├── scripts/                     # 可复用脚本
│   └── a_stock_morning_analysis.py  # A 股上午盘分析脚本
├── outputs/                     # 产出物
│   └── TASK-20260812-001_A股市场分析.md  # 示例任务报告
├── skills/                      # 技能定义
│   └── boss-mode-workflow/
│       └── SKILL.md             # BOSS 模式技能定义
├── SCHEMA.md                    # Wiki Schema (规则定义)
├── agent-log.md                 # Agent 操作日志
└── README.md                    # 本文件
```

## BOSS 模式

BOSS 模式是老板驱动的多 Profile 协作工作流：

1. **需求澄清** — BOSS 下达需求，系统拆解为可执行任务
2. **任务分配** — 协调者将任务分发给研究员/执行者 Profile
3. **自动执行** — 各 Profile 独立执行，结果写入 Wiki
4. **汇总交付** — 协调者汇总所有结果，BOSS 审核

### 快速启动 BOSS 模式

在 Hermes Agent 中加载 `boss-mode-workflow` 技能即可开始：

```
技能名称: boss-mode-workflow
位置: skills/boss-mode-workflow/SKILL.md
```

## 使用示例

### 示例 1: A 股上午盘分析 (TASK-001)

2026-08-12 完成了第一个 BOSS 模式任务：

- **分析对象**: A 股上午盘市场
- **发现主线**: CPO/光通信、机器人、半导体、AI 应用、低空经济
- **涨停分析**: 70 家涨停，百花医药 7 连板，秦安股份 4 连板
- **大单成交**: 中际旭创 195 亿，长鑫科技 203 亿

完整报告: [TASK-20260812-001](outputs/TASK-20260812-001_A股市场分析.md)

## 更新历史

| 日期 | 版本 | 更新内容 | 原因 |
|------|------|----------|------|
| 2026-08-12 | v1.1 | 添加 BOSS 模式技能、A 股分析示例 | 搭建完整多 Profile 协作流程 |
| 2026-08-11 | v1.0 | 初始搭建，4 个 Profile + Wiki 基础结构 | 解决多 Profile 记忆污染问题 |

## 许可

MIT License — 可以自由修改和分发

## 作者

Jesse (jessezhenyu-1973)
