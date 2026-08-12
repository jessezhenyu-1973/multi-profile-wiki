# Skill Registry

## Shared Skills

### memory-routing

- type: shared
- installed_to:
  - coordinator
  - researcher
  - narrative
  - builder
- purpose: 判断信息应该写入哪里
- risk: low

### research-methods

- type: shared
- installed_to:
  - researcher
  - coordinator
- purpose: 指导资料搜集、验证、分析
- risk: low

### structure-design

- type: shared
- installed_to:
  - narrative
  - builder
- purpose: 内容/产品结构、大纲设计
- risk: low

## Coordinator Skills

### task-decomposition

- type: role
- installed_to:
  - coordinator
- purpose: 拆解复杂任务为可执行步骤
- risk: low

### memory-audit

- type: role
- installed_to:
  - coordinator
- purpose: 检查记忆污染、数据一致性
- risk: medium

### dashboard-management

- type: role
- installed_to:
  - coordinator
- purpose: 维护 dashboard.md 项目状态
- risk: low

## Researcher Skills

### data-research

- type: role
- installed_to:
  - researcher
- purpose: A 股数据源调研、验证、对比
- risk: low

### competitor-analysis

- type: role
- installed_to:
  - researcher
- purpose: 竞品策略、产品、市场研究
- risk: low

## Narrative Skills

### report-structure

- type: role
- installed_to:
  - narrative
- purpose: 研究报告、回测报告结构设计
- risk: low

## Builder Skills

### coding-agents

- type: role
- installed_to:
  - builder
- purpose: 使用 Claude Code / Codex 进行编码
- sub-skills:
  - claude-code: 复杂重构、多步代码修改、PR review
  - codex: 快速实现、并行任务、OpenAI 模型编码
- risk: medium

### desktop-automation

- type: role
- installed_to:
  - builder
- purpose: 桌面应用自动化、UI 截图分析
- sub-skills:
  - computer-use: 后台 GUI 交互、截图、点击
- risk: low

### final-output-builder

- type: role
- installed_to:
  - builder
- purpose: 生成最终交付物（代码、报告、文档）
- risk: medium

### quant-implementation

- type: role
- installed_to:
  - builder
- purpose: 量化策略实现、回测脚本编写
- risk: medium
