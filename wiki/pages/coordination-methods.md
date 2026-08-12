# Coordination Methods

## 多 Profile 任务流

常规复杂任务流程：

coordinator → researcher → narrative → builder → coordinator

## 文件写入原则

- researcher 写项目 inbox/
- narrative 写项目 inbox/
- builder 写项目 outputs/
- coordinator 汇总写 system/ 和项目 log/tasks

## 多项目流程

1. 每个项目放在 projects/{project}/
2. system/ 只保留一个
3. dashboard.md 记录所有项目状态
4. agent-log.md 记录所有 profile 行为
5. 每个项目的细节写入自己的项目文件夹
