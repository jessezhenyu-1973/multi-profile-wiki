# Wiki Schema

## 这个 Wiki 的作用

本 Wiki 用于管理多 Profile 协作。

它负责：
- 管理长期项目
- 管理任务、日志、决策和产出
- 防止记忆污染
- 沉淀跨项目方法论

## 核心原则

只有一个 system/。

system/ 是全局总控层，不属于任何单独项目。

可以有多个 projects/。

每个长期项目都应该在 projects/ 下面有一个独立文件夹。

## 写入原则

- 项目规则写入 projects/{project}/AGENTS.md
- 项目背景写入 projects/{project}/context.md
- 项目任务写入 projects/{project}/tasks.md
- 项目过程写入 projects/{project}/log.md
- 项目决策写入 projects/{project}/decisions.md
- 临时材料写入 projects/{project}/inbox/
- 正式产出写入 projects/{project}/outputs/
- 跨项目方法论写入 pages/
- 原始资料写入 raw/
- 素材附件写入 assets/
- 归档内容写入 archive/

## 禁止事项

- 禁止把项目状态写进 profile 的 SOUL.md
- 禁止把临时任务写进 MEMORY.md
- 禁止把未经验证的信息直接写进 pages/
- 禁止多个 profile 同时修改同一个正式文件
- 禁止把密钥写进任何 Markdown 文件
