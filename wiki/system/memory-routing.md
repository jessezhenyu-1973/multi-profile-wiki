# Memory Routing

## 写入规则

角色身份 → profiles/{profile}/SOUL.md

用户长期偏好 → profiles/{profile}/USER.md 或 system/user-profile.md

角色通用经验 → profiles/{profile}/MEMORY.md

项目规则 → projects/{project}/AGENTS.md

项目背景 → projects/{project}/context.md

项目任务 → projects/{project}/tasks.md

项目过程 → projects/{project}/log.md

项目决策 → projects/{project}/decisions.md

临时材料 → projects/{project}/inbox/

正式产出 → projects/{project}/outputs/

跨项目方法论 → pages/

原始资料 → raw/

素材附件 → assets/

归档内容 → archive/

## 判断原则

只属于当前项目的信息，写入 projects/{project}/。

影响所有项目的信息，写入 system/。

很多项目都能复用的方法，写入 pages/。

## 禁止事项

- 禁止把项目状态写进 SOUL.md
- 禁止把临时任务写进 MEMORY.md
- 禁止把未经验证的信息写进 pages/
- 禁止多个 profile 同时修改同一个正式文件
