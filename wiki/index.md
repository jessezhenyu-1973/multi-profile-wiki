# Hermes Team Wiki Index

这是多 Profile 协作系统的总入口。

## 系统区

- [[system/dashboard]]：总看板，记录所有项目的状态、优先级、当前重点和下一步。
- [[system/agent-log]]：全局行为日志，记录每个 profile 做过什么、输出放在哪里。
- [[system/weekly-review]]：周复盘文件，用来总结每周项目进展、问题和下周重点。
- [[system/memory-routing]]：写入规则，判断一条信息应该写进哪里，防止记忆污染。
- [[system/skill-registry]]：技能登记表，记录不同 profile 可以使用哪些 skill。
- [[system/user-profile]]：统一用户画像，记录用户长期偏好，供所有 profile 参考。

## 项目区

所有长期项目放在：

- projects/：每个项目一个独立文件夹，用来存放项目背景、任务、日志、决策和产出。

每个项目需要包含：

- AGENTS.md：项目工作规则，告诉各个 profile 在这个项目里该做什么、不能做什么。
- context.md：项目背景，记录项目目标、当前阶段、用户对象和限制条件。
- tasks.md：任务池，记录正在做、待做、已完成的任务。
- log.md：项目日志，记录每轮任务推进情况。
- decisions.md：项目决策，记录已经确定的方向和边界。
- inbox/：中间材料区，放 researcher 和 narrative 的研究材料、结构稿、大纲。
- outputs/：正式产出区，放 builder 生成的最终文章、页面、代码方案、课程讲义等。

## 通用方法论

- [[pages/research-methods]]：研究方法，供 researcher 做资料整理、用户研究、竞品研究时参考。
- [[pages/narrative-methods]]：结构方法，供 narrative 搭文章、课程、产品路径时参考。
- [[pages/building-methods]]：构建方法，供 builder 生成正式产出时参考。
- [[pages/coordination-methods]]：协作方法，供 coordinator 拆任务、分配任务、汇总结果时参考。

## Profile

- coordinator：协调者，负责拆任务、分配任务、汇总结果和检查记忆污染。
- researcher：研究专家，负责查资料、做研究、整理事实和分析信息。
- narrative：叙事架构师，负责搭结构、写大纲、设计路径和组织表达。
- builder：构建者，负责写正文、写代码、做页面、生成最终交付物。
