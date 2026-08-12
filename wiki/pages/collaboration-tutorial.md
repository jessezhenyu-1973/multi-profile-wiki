# 多 Profile Wiki 协作使用教程

## 一句话说明

这是一个 **AI 团队管理系统**。你把不同任务分配给不同角色的 AI，它们各自专注自己的事，互不干扰，最后由协调者汇总成完整结果。

---

## 核心概念（3 分钟看懂）

### 1. 四个角色

| 角色 | 职责 | 类比 |
|------|------|------|
| **coordinator**（协调者） | 拆任务、分配、汇总、防污染 | 项目经理 |
| **researcher**（研究员） | 查资料、分析数据、验证来源 | 数据分析师 |
| **narrative**（叙事者） | 搭结构、写大纲、设计路径 | 内容架构师 |
| **builder**（构建者） | 写代码、生成报告、最终交付 | 工程师 |

### 2. 三个工作区

```
Hermes-Team/
├── profiles/          ← 角色定义区
│   ├── coordinator/   ← 协调者的"人设"
│   ├── researcher/    ← 研究员的"人设"
│   ├── narrative/     ← 叙事者的"人设"
│   └── builder/       ← 构建者的"人设"
│
├── wiki/              ← 共享工作空间
│   ├── system/        ← 全局总控（只有一份）
│   │   ├── dashboard.md    ← 项目看板
│   │   ├── agent-log.md    ← 行为日志
│   │   └── ...
│   ├── projects/      ← 每个项目一个文件夹
│   │   └── quant-research/   ← 你的第一个项目
│   │       ├── AGENTS.md     ← 项目规则
│   │       ├── context.md    ← 项目背景
│   │       ├── tasks.md      ← 任务池
│   │       ├── log.md        ← 项目日志
│   │       ├── decisions.md  ← 决策记录
│   │       ├── inbox/        ← 中间材料（研究员/叙事者输出）
│   │       └── outputs/      ← 正式产出（构建者输出）
│   └── pages/         ← 通用方法论
│
└── [更多项目...]
```

### 3. 一句话流程

```
coordinator 拆任务 → researcher/narrative 执行 → builder 生成产出 → coordinator 汇总
```

---

## 实际操作：手把手教你用

### 第一步：启动项目

当你需要开始一个项目时，对 coordinator 说：

> 你现在扮演 coordinator。
> 项目名称是：{项目名称}
> 项目目标是：{项目目标}
> 当前最重要的问题是：{当前问题}
> 请输出当前项目状态和下一步建议。

coordinator 会读取项目文件，告诉你：
- 当前状态
- 下一步做什么
- 该调用哪个 profile
- 给该 profile 的交接单

### 第二步：分配任务给研究员

当你的项目需要查资料、做分析时：

> 你现在扮演 researcher。
> 进入项目：{项目名称}
> 项目文件已读取（AGENTS.md, context.md, tasks.md, decisions.md）
>
> 本次任务：{具体研究任务}
> 请输出 Markdown 内容，写入：
> inbox/{output-file-name}.md

researcher 会输出研究材料到 inbox/ 目录。

### 第三步：分配任务给叙事者

当研究员完成后，需要整理结构：

> 你现在扮演 narrative。
> 进入项目：{项目名称}
> 项目文件已读取
> 研究员材料在：inbox/{research-output}.md
>
> 本次任务：{结构设计任务}
> 请输出 Markdown 内容，写入：
> inbox/{output-file-name}.md

narrative 会输出结构稿到 inbox/ 目录。

### 第四步：分配任务给构建者

当结构确定后，生成最终产出：

> 你现在扮演 builder。
> 进入项目：{项目名称}
> 项目文件已读取
> 结构稿在：inbox/{narrative-output}.md
>
> 本次任务：{最终构建任务}
> 请输出 Markdown 内容，写入：
> outputs/{output-file-name}.md

builder 会输出正式交付物到 outputs/ 目录。

### 第五步：Coordinator 汇总

每轮完成后，让 coordinator 汇总：

> 你现在扮演 coordinator。
> 汇总项目：{项目名称} 本轮任务。
> 本轮产出：
> - inbox/ 新增：{文件内容}
> - outputs/ 新增：{文件内容}
>
> 请输出：
> 1. 本轮完成总结
> 2. tasks.md 更新建议
> 3. log.md 更新建议
> 4. agent-log.md 更新建议
> 5. dashboard.md 更新建议
> 6. 下一轮任务

---

## 实际案例：数据源调研

以你当前的量化研究项目为例：

**协调者分配任务：**
```
你现在扮演 coordinator。
项目名称：quant-research
请分配数据源调研任务给 researcher。
```

**研究员执行任务：**
```
你现在扮演 researcher。
进入项目：quant-research
项目文件已读取（AGENTS.md, context.md, tasks.md, decisions.md）

本次任务：对比同花顺 MCP、baostock、akshare、通达信 4 个数据源，
调研维度包括：数据类型、更新频率、历史深度、API 限制、适用场景。

请输出 Markdown 内容，写入：
inbox/data-source-research-20260812.md
```

**构建者生成报告：**
```
你现在扮演 builder。
进入项目：quant-research
项目文件已读取
研究员材料在：inbox/data-source-research-20260812.md

本次任务：基于研究结果，编写数据整合代码。
请输出代码和说明，写入：
outputs/data-integration-plan.md
```

---

## 关键规则

### ✅ 应该做的事

1. **每次任务从 coordinator 开始** — 它负责拆解和分配
2. **研究员/叙事者输出到 inbox/** — 中间材料区
3. **构建者输出到 outputs/** — 正式产出区
4. **coordinator 更新 system/ 和项目文件** — 全局状态
5. **简单任务直接给对应角色** — 不用每次都走完整流程

### ❌ 禁止做的事

1. **不要直接让 AI 修改 system/** — 只有 coordinator 可以
2. **不要修改 SOUL.md / USER.md / MEMORY.md** — 这些是角色定义
3. **不要把 A 项目的结论写进 B 项目** — 防止记忆污染
4. **不要让多个 AI 同时改同一个文件** — 会冲突
5. **不要跳过 coordinator** — 它会帮你检查优先级和依赖

---

## 常见场景

### 场景 1：快速问答

> 你现在扮演 researcher。
> 项目：quant-research
> 请调研：同花顺 MCP 的 get_a_share_prices_snapshot 接口支持哪些参数？

### 场景 2：写代码

> 你现在扮演 builder。
> 项目：quant-research
> 请帮我写一个 Python 函数，用于批量获取 A 股历史 K 线数据。

### 场景 3：写报告

> 你现在扮演 narrative。
> 项目：quant-research
> 请设计一份量化策略研究报告的结构。

### 场景 4：多项目并行

当有多个项目时，明确指定项目名：

```
你现在扮演 coordinator。
项目 A 的任务：...
项目 B 的任务：...
请分别给出两个项目的下一步建议。
```

---

## 项目创建流程

当你想创建新项目时：

1. **创建项目文件夹**
   ```bash
   mkdir -p wiki/projects/新项目名/{inbox,outputs}
   touch wiki/projects/新项目名/{AGENTS.md,context.md,tasks.md,log.md,decisions.md}
   ```

2. **生成项目文件内容**
   对 AI 说：
   > 我正在搭建多 Profile Wiki 协作系统，请帮我生成以下文件：
   > - AGENTS.md
   > - context.md
   > - tasks.md
   > - decisions.md
   > - log.md
   >
   > 项目信息：
   > - 名称：{项目名称}
   > - 类型：{项目类型}
   > - 目标：{项目目标}
   > - 当前阶段：{当前阶段}
   > - 限制条件：{限制条件}

3. **登记到 Dashboard**
   让 coordinator 把新项目添加到 dashboard.md

---

## 维护规则

### 日常维护

- **每次任务后**：让 coordinator 更新 tasks.md 和 log.md
- **每周一次**：让 coordinator 做周复盘（weekly-review.md）
- **每月一次**：检查 memory-routing.md，清理过期的临时材料

### 备份建议

```bash
# 定期 git commit
cd Hermes-Team && git add -A && git commit -m "更新项目进度" && git push
```

---

## 快速参考卡

### 角色分工

| 你要做什么 | 调用哪个角色 |
|-----------|-------------|
| 拆任务、分配、汇总 | coordinator |
| 查资料、分析数据、验证 | researcher |
| 写大纲、设计结构、做规划 | narrative |
| 写代码、生成报告、做交付 | builder |

### 文件位置

| 文件类型 | 位置 |
|---------|------|
| 中间材料 | projects/{项目}/inbox/ |
| 正式产出 | projects/{项目}/outputs/ |
| 项目日志 | projects/{项目}/log.md |
| 任务列表 | projects/{项目}/tasks.md |
| 决策记录 | projects/{项目}/decisions.md |
| 全局看板 | system/dashboard.md |
| 行为日志 | system/agent-log.md |

### 常用提示词

**启动项目：**
> 你现在扮演 coordinator。项目名称：{项目名}。请分析当前状态并给出下一步建议。

**分配任务：**
> 你现在扮演 {角色}。进入项目：{项目名}。本次任务：{具体任务}。

**汇总结果：**
> 你现在扮演 coordinator。汇总项目：{项目名}。请输出更新建议。

---

## 进阶用法

### 1. 使用团队专家技能

builder profile 已挂载：
- **Claude Code**: 复杂代码重构、PR review
- **Codex**: 快速编码、并行任务
- **Computer Use**: 桌面自动化、截图分析

### 2. 多项目并行

```
coordinator 同时管理多个项目：
- 项目 A: researcher 查资料
- 项目 B: builder 写代码
- coordinator 更新两个项目的 tasks.md
```

### 3. 定期自动化

可以设置 Cron 任务，让 coordinator 每天/每周自动：
- 检查项目进度
- 生成周报
- 提醒待办事项

---

## 常见问题

**Q: 为什么要用 4 个角色，不能直接让一个 AI 做？**
A: 角色分离防止 AI"自己骗自己"。研究员专注查资料，不急着写结论；构建者专注产出，不擅改方向。就像真实团队一样，各司其职。

**Q: 文件很多，怎么管理？**
A: 记住三个核心：
- inbox/ 放中间材料
- outputs/ 放正式产出
- coordinator 管全局

**Q: 怎么防止 AI 记混了？**
A: memory-routing.md 定义了写入规则。每个项目有自己的 context.md 和 decisions.md，AI 必须遵守。

**Q: 可以只用部分角色吗？**
A: 可以。简单任务直接调用对应角色，不用走完整流程。

---

## 总结

这套系统的核心是 **分工 + 防污染**。

```
coordinator 拆任务 → researcher/narrative 执行 → builder 产出 → coordinator 汇总
```

记住这个循环，你就掌握了多 Profile Wiki 协作的精髓。
