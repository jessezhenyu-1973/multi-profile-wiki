# AGENTS.md — 量化研究团队

## 项目目标

构建 A 股量化研究协作系统，支持多数据源整合、因子分析、回测验证和自动化报告。

## 项目类型

量化研究 / 自动化分析

## 工作规则

1. 所有研究输出写入 `inbox/`
2. 所有正式产出写入 `outputs/`
3. 任务进度实时更新 `tasks.md`
4. 每日工作记录写入 `log.md`
5. 重要决策写入 `decisions.md`

## Profile 职责

### Researcher
- 搜集市场数据
- 分析用户偏好
- 调研竞品策略
- 验证来源可靠性
- 输出研究材料到 `inbox/research-{date}.md`

### Narrative
- 搭建报告结构
- 设计分析框架
- 梳理产品定位
- 设计用户路径
- 输出结构稿到 `inbox/narrative-{date}.md`

### Builder
- 生成正式报告
- 编写代码实现
- 整理最终文档
- 输出交付物到 `outputs/`
- 为后续实现准备说明

### Coordinator
- 判断项目状态
- 拆解复杂任务
- 分配任务给其他 Profile
- 生成交接单
- 汇总各 Profile 输出
- 更新 `tasks.md` 和 `log.md`
- 检查记忆污染

## 文件写入规则

| 文件类型 | 写入位置 | 负责人 |
|---------|---------|--------|
| 研究材料 | `inbox/` | researcher |
| 结构稿 | `inbox/` | narrative |
| 正式产出 | `outputs/` | builder |
| 任务进度 | `tasks.md` | coordinator |
| 项目日志 | `log.md` | coordinator |
| 决策记录 | `decisions.md` | coordinator |

## 禁止事项

- 禁止多个 Profile 同时修改同一个正式文件
- 禁止把项目状态写进 Profile 的 SOUL.md
- 禁止把临时任务写进 MEMORY.md
- 禁止未经验证的信息直接写入 pages/
- 禁止把密钥写进任何 Markdown 文件
