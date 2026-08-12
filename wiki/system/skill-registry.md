# Skill Registry — 技能注册表

> **来源**: 多 Profile Wiki 协作系统 + agency-agents-zh 268 专家
> **最后更新**: 2026-08-12

## 架构概览

```
coordinator (95 skills)    → 项目管理、HR、法务、财务、供应链、产品、支持
researcher  (49 skills)    → 学术研究、金融、GIS、法务、安全、测试
narrative   (72 skills)    → 设计、营销、付费媒体、产品、销售
builder     (94 skills)    → 工程、设计、游戏开发、GIS、安全、空间计算、测试
```

---

## Shared Skills（共享技能）

### memory-routing
- **类型**: shared
- **安装到**: coordinator, researcher, narrative, builder
- **用途**: 判断信息应该写入哪里
- **风险**: low

### research-methods
- **类型**: shared
- **安装到**: researcher, coordinator
- **用途**: 指导资料搜集、验证、分析
- **风险**: low

### structure-design
- **类型**: shared
- **安装到**: narrative, builder
- **用途**: 内容/产品结构、大纲设计
- **风险**: low

---

## Role Skills（角色专属技能）

### Coordinator Skills
| Skill | 用途 | 风险 |
|-------|------|------|
| task-decomposition | 拆解复杂任务为可执行步骤 | low |
| memory-audit | 检查记忆污染、数据一致性 | medium |
| dashboard-management | 维护 dashboard.md 项目状态 | low |

### Researcher Skills
| Skill | 用途 | 风险 |
|-------|------|------|
| data-research | A 股数据源调研、验证、对比 | low |
| competitor-analysis | 竞品策略、产品、市场研究 | low |

### Narrative Skills
| Skill | 用途 | 风险 |
|-------|------|------|
| report-structure | 研究报告、回测报告结构设计 | low |

### Builder Skills
| Skill | 用途 | 风险 |
|-------|------|------|
| coding-agents | 使用 Claude Code / Codex 进行编码 | medium |
| desktop-automation | 桌面应用自动化、UI 截图分析 | low |
| final-output-builder | 生成最终交付物（代码、报告、文档） | medium |
| quant-implementation | 量化策略实现、回测脚本编写 | medium |

---

## agency-agents-zh 专家技能（按部门映射）

> **来源**: [jnMetaCode/agency-agents-zh](https://github.com/jnMetaCode/agency-agents-zh)
> **安装日期**: 2026-08-12
> **总技能数**: 310（268 个原始智能体 + 部分重复）

### 📊 部门 → Profile 映射

| 部门 | Coordinator | Researcher | Narrative | Builder |
|------|:-----------:|:----------:|:---------:|:-------:|
| project-management | ✅ 7 | | | |
| hr | ✅ 2 | | | |
| legal | ✅ 2 | ✅ 2 | | |
| finance | ✅ 9 | ✅ 9 | | |
| supply-chain | ✅ 5 | | | |
| product | ✅ 5 | | ✅ 5 | |
| support | ✅ 7 | | | |
| specialized | ✅ 58 | | | |
| academic | | ✅ 6 | | |
| gis | | ✅ 13 | | ✅ 13 |
| security | | ✅ 10 | | ✅ 10 |
| testing | | ✅ 9 | | ✅ 9 |
| marketing | | | ✅ 42 | |
| paid-media | | | ✅ 7 | |
| sales | | | ✅ 9 | |
| design | | | ✅ 9 | ✅ 9 |
| engineering | | | | ✅ 42 |
| game-development | | | | ✅ 5 |
| spatial-computing | | | | ✅ 6 |

---

### 📋 各 Profile 详细技能清单

#### coordinator — 95 skills

**project-management (7)**
- 项目管理实验追踪器
- Jira 工作流主管
- 会议纪要专员
- 项目牧羊人
- 工作室运营
- 工作室制片人
- 高级项目经理

**hr (2)**
- HR 专家

**legal (2)**
- 法务专家

**finance (9)**
- 金融分析师（9个金融专家技能）

**supply-chain (5)**
- 供应链专家（5个供应链技能）

**product (5)**
- 产品经理（5个产品技能）

**support (7)**
- 客户支持专家（7个支持技能）

**specialized (58)**
- 20+ 个专项技能（包括 Blender、Godot、Unity、Roblox 等专业领域）

---

#### researcher — 49 skills

**academic (6)**
- 学术研究专家（6个学术技能）

**finance (9)**
- 金融分析师（9个金融技能）

**gis (13)**
- GIS 专家（13个地理信息系统技能）

**legal (2)**
- 法务专家（2个法务技能）

**security (10)**
- 安全专家（10个安全技能）

**testing (9)**
- 测试专家（9个测试技能）

---

#### narrative — 72 skills

**marketing (42)**
- 营销专家（42个营销技能，含小红书、抖音、微信、飞书等中国市场智能体）

**paid-media (7)**
- 付费媒体专家（7个付费媒体技能）

**sales (9)**
- 销售专家（9个销售技能）

**design (9)**
- 设计专家（9个设计技能）

**product (5)**
- 产品经理（5个产品技能）

---

#### builder — 94 skills

**engineering (42)**
- 工程专家（42个工程技能，涵盖前端、后端、全栈、移动端等）

**design (9)**
- 设计专家（9个设计技能）

**game-development (5)**
- 游戏开发专家（5个游戏开发技能）

**gis (13)**
- GIS 专家（13个地理信息系统技能）

**security (10)**
- 安全专家（10个安全技能）

**spatial-computing (6)**
- 空间计算专家（6个空间计算技能，含 Apple Vision Pro 等）

**testing (9)**
- 测试专家（9个测试技能）

---

## 编排器配置（ao compose）

### 使用方式

在 Hermes 中执行多专家协作时，使用 `ao compose` 语法：

```
ao compose:
  - role: coordinator
    skills: [task-decomposition, memory-audit]
    agents: [project-manager-senior, meeting-notes-specialist]
    
  - role: researcher
    skills: [data-research, competitor-analysis]
    agents: [finance-analyst, gis-specialist]
    
  - role: narrative
    skills: [report-structure]
    agents: [marketing-strategist, social-media-manager]
    
  - role: builder
    skills: [coding-agents, desktop-automation]
    agents: [full-stack-developer, security-auditor]
```

### 跨角色协作示例

```
ao compose:
  - coordinator: task-decomposition → 分配 T001 数据调研任务
  - researcher: finance-analyst → 执行 T001，输出研究报告
  - narrative: marketing-strategist → 将研究报告转化为市场洞察
  - builder: quant-implementation → 实现策略代码
```

---

## 安装维护

### 更新专家技能

```bash
cd ~/agency-agents-zh
# 1. 重新转换
bash scripts/convert.sh --tool hermes

# 2. 重新安装到各 Profile
bash scripts/install.sh --tool hermes --profile coordinator --no-interactive
bash scripts/install.sh --tool hermes --profile researcher --no-interactive
bash scripts/install.sh --tool hermes --profile narrative --no-interactive
bash scripts/install.sh --tool hermes --profile builder --no-interactive
```

### 添加新部门

```bash
cd ~/agency-agents-zh
# 1. 安装新部门到指定 Profile
bash scripts/install.sh --tool hermes --profile <profile> --category <新分类> --no-interactive

# 2. 更新本文件
```

### 验证安装

```bash
# 查看每个 Profile 的技能数量
find ~/.hermes/profiles/coordinator/skills -type f | wc -l  # 95
find ~/.hermes/profiles/researcher/skills -type f | wc -l   # 49
find ~/.hermes/profiles/narrative/skills -type f | wc -l    # 72
find ~/.hermes/profiles/builder/skills -type f | wc -l      # 94
```

---

## Wiki 索引

> 相关 Wiki 页面位于 `Hermes-Wiki/concepts/` 和 `Hermes-Wiki/entities/`

- [[agency-agents-zh]] — 268 专家角色系统介绍
- [[多Profile协作]] — 多 Profile Wiki 协作系统
- [[skill-registry]] — 技能注册表（本文件）
- [[ao-compose]] — 编排器语法
