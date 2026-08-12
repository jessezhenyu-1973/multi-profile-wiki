---
name: boss-mode-workflow
description: BOSS 模式 — 老板驱动协作工作流：需求澄清→任务拆解→多 Profile 自动执行→汇总交付成品
version: 1.0.0
author: agent
created_by: "agent"
metadata:
  hermes:
    tags: [多 Profile 协作，BOSS 模式，任务拆解，自动化工作流，A 股分析]
---

# BOSS 模式 — 老板驱动协作工作流

## 触发条件

用户表达复杂需求，需要多角色协作完成。适用于：分析报告、系统开发、策略研究、文档编写等跨角色任务。

## 核心原则

1. **老板不碰技术细节** — 你只描述目标，coordinator 负责拆解
2. **coordinator 必须先问清楚** — 不清楚就追问，直到所有关键信息到位
3. **全程可追踪** — 每个任务有 ID、分配、进度、输出
4. **最终交付成品** — 不是中间过程，而是可直接使用的结果

## 工作流

```
老板提出需求
    ↓
coordinator 追问（需求澄清阶段）
    ↓
coordinator 输出《任务确认书》
    ↓
coordinator 输出《任务拆解单》
    ↓
自动派发 → researcher / narrative / builder 并行执行
    ↓
coordinator 汇总 → 生成《最终交付物》
    ↓
交付给老板
```

## 执行步骤

### 1. 需求澄清（coordinator 主导）

收到需求后，**必须**追问以下信息：

| # | 问题 | 为什么重要 |
|---|------|-----------|
| 1 | 最终要交付什么？ | 报告？代码？方案？数据？ |
| 2 | 给谁看的？ | 决定语言风格和深度 |
| 3 | 截止时间？ | 决定优先级和并行度 |
| 4 | 有没有参考/模板？ | 避免方向偏离 |
| 5 | 有什么约束？ | 工具限制、数据权限、合规要求 |

### 追问话术模板

```
老板，收到您的需求了。在开始工作前，我需要确认几个关键点：

1. 最终交付物是什么形态？
   - 一份分析报告
   - 一套代码/脚本
   - 一个完整方案文档
   - 其他：____

2. 这份东西给谁看？
   - 自己用
   - 给团队/领导
   - 对外发布

3. 有没有时间要求？什么时候需要？

4. 有没有可以参考的模板/样例？

5. 有什么需要注意的约束？
```

追问完成后，输出《任务确认书》：

```markdown
## 📋 任务确认书

**需求来源**: 老板  
**任务编号**: TASK-{YYYYMMDD}-{NNN}  
**需求描述**: [一句话总结]  
**交付物**: [明确描述]  
**截止时间**: [明确时间]  
**约束条件**: [列出]  
**参考材料**: [列出]  

✅ 已确认，开始任务拆解。
```

### 2. 任务拆解（coordinator 主导）

根据确认需求，拆解为可分配任务：

```markdown
## 📋 任务拆解单 — [任务编号]

### 任务总览
- **任务编号**: TASK-YYYYMMDD-NNN
- **负责人**: coordinator
- **状态**: 已派发

### 子任务分配

| ID | 子任务 | 负责人 | Profile | 交付物 | 依赖 |
|----|--------|--------|---------|--------|------|
| T001 | [描述] | researcher | researcher | [文件路径] | 无 |
| T002 | [描述] | builder | builder | [文件路径] | T001 |
| T003 | [描述] | narrative | narrative | [文件路径] | T001 |

### 并行策略
- 无依赖子任务并行执行
- 有依赖的子任务按依赖顺序执行
```

### 3. 自动化执行（各 profile 独立）

每个 profile 收到任务后：

1. 读取任务描述和交付要求
2. 执行对应工作（研究/开发/写作）
3. 输出到指定路径（`projects/{project}/outputs/` 或 `outputs/`）
4. 记录到 `agent-log.md`

> coordinator 不干预执行过程，只监控进度。

### 4. 汇总交付（coordinator 主导）

所有子任务完成后，coordinator：

1. 读取所有子任务的输出文件
2. 整合为统一的最终交付物
3. 格式为老板可直接使用的形式
4. 提交最终报告

```markdown
## 📦 最终交付报告

**任务编号**: TASK-YYYYMMDD-NNN  
**交付状态**: ✅ 已完成  
**交付物位置**: [文件路径]  

### 交付物摘要
[简要总结交付内容]

### 各子任务完成情况
- T001: ✅ researcher 输出 [文件名]
- T002: ✅ builder 输出 [文件名]
- T003: ✅ narrative 输出 [文件名]

### 下一步
[如需迭代，提出改进建议]
```

## 快速启动方式

### 方式一：直接对 coordinator 说

```
我要做一个 [需求描述]
```

coordinator 会自动启动需求澄清流程。

### 方式二：明确使用 BOSS 模式

```
用 BOSS 模式：我要 [需求描述]
```

coordinator 会严格按照上述流程执行。

### 方式三：复杂任务 + 参考材料

```
用 BOSS 模式处理：[需求描述]

参考资料：
- [文件路径 1]
- [文件路径 2]

截止时间：[时间]
```

## 监控进度

老板可以随时查看进度：

```
当前任务进度如何？
```

coordinator 会回复：

```markdown
## 进度报告 — TASK-YYYYMMDD-NNN

| 子任务 | 状态 | 预计完成 |
|--------|------|---------|
| T001 | ✅ 完成 | 16:30 |
| T002 | 🔄 进行中 | 17:00 |
| T003 | ⏳ 等待中 | 17:30 |

预计全部完成：17:30
```

## 迭代改进

交付后，老板可以直接说：

```
这里需要修改：[具体问题]
```

coordinator 会：
1. 分析修改需求
2. 分配给对应 profile
3. 更新交付物
4. 重新提交

## A 股分析专项 — 数据源参考

当任务为 A 股市场分析时，coordinator 应使用以下 MCP 工具：

| 工具名 | 用途 | 关键参数 |
|--------|------|---------|
| `mcp__fuyao_a_share__get_a_share_special_data_hot_stock_list` | 热股榜 | period=day/hour |
| `mcp__fuyao_a_share__get_a_share_special_data_limit_up_pool` | 涨停池 | date_ms, page, size |
| `mcp__fuyao_a_share__get_a_share_special_data_skyrocket_list` | 飙升榜 | period=day/hour |
| `mcp__fuyao_a_share__get_a_share_prices_snapshot` | 实时行情 | thscodes 逗号分隔 |
| `mcp__fuyao_a_share_index__get_a_share_index_prices_snapshot` | 指数行情 | thscodes |
| `mcp__fuyao_a_share__get_a_share_special_data_anomaly_analysis_stock` | 个股异动 | thscodes |
| `mcp__fuyao_a_share__get_a_share_special_data_limit_up_ladder` | 连板天梯 | 无 |

### A 股分析输出模板

```markdown
# 📊 [日期] A 股市场分析

## 一、市场整体概览
- 涨停家数、跌停家数、连板高度
- 赚钱效应定性（⭐评级）
- 核心主线识别

## 二、热点板块分析
| 板块 | 涨停家数 | 连板高度 | 龙头股 | 驱动逻辑 |

## 三、资金流向分析
| 板块 | 代表股成交额 | 资金方向 |

## 四、龙头股精选
| 股票 | 代码 | 连板 | 题材 | 逻辑 |

## 五、操作建议
- 主线策略
- 风险提示
```

## 注意事项

1. **coordinator 不是执行者** — 它只拆解和调度，不写代码/不做研究
2. **追问是必须的** — 不要怕麻烦，问清楚比返工更高效
3. **交付物是成品** — 不是中间过程，老板拿到就能用
4. **全程可追溯** — 所有任务有编号、有记录、可回溯
5. **文件路径规范** — 输出统一放在 `projects/{project}/outputs/` 或 `outputs/`

## 相关文件

- `wiki/pages/boss-mode.md` — 完整流程文档
- `wiki/system/agent-log.md` — 任务日志记录
- `wiki/system/dashboard.md` — 项目仪表盘
