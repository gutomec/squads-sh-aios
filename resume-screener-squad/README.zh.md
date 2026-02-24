# resume-screener-squad

招聘简历筛选专家小组。

## 概述

**resume-screener-squad** 是一个完整的小组，涵盖整个简历筛选流水线：

1. **简历解析** — 从任何格式（PDF、DOCX、文本）的简历中自动提取结构化数据
2. **技能匹配** — 将技能与职位要求进行比较，计算加权匹配分数，识别可转移技能
3. **偏见审计** — 检测性别、年龄、种族、教育背景和姓名偏见，确保公平性
4. **候选人排名** — 透明排名并附带理由，识别隐藏宝石，可配置候选名单
5. **高管摘要** — 为招聘经理提供可操作的简报，包括优势、关注点、比较矩阵和面试问题

**痛点：** 每次招聘平均成本4,700美元，周期44天；手动筛选容易产生无意识偏见并错失合格候选人。

## 代理

| 代理 | ID | 角色 |
|---|---|---|
| 📋 Parser | `resume-parser` | 简历解析和数据提取 |
| 🔍 SkillsMatcher | `skills-matcher` | 技能匹配和匹配分数计算 |
| 🛡️ BiasAuditor | `bias-auditor` | 偏见审计和公平性 |
| ⚡ Ranker | `shortlist-ranker` | 排名和候选名单生成 |
| 📊 SummaryWriter | `candidate-summary-agent` | 高管摘要和简报 |

## 工作流

| 工作流 | 命令 | 描述 | 持续时间 |
|---|---|---|---|
| 完整简历筛选 | `*triage-full` | 完整流水线：从解析到高管摘要 | 30-60分钟 |
| 快速技能匹配 | `*quick-match` | 快速匹配：解析、匹配和简化摘要 | 10-20分钟 |

## 可用命令

| 命令 | 代理 | 描述 |
|---|---|---|
| `*parse-resumes` | Parser | 从简历中提取结构化数据 |
| `*parse-single` | Parser | 从特定简历中提取数据 |
| `*match-skills` | SkillsMatcher | 计算候选人匹配分数 |
| `*analyze-gaps` | SkillsMatcher | 分析技能差距 |
| `*audit-bias` | BiasAuditor | 审计筛选过程中的偏见 |
| `*check-fairness` | BiasAuditor | 验证排名公平性 |
| `*rank-candidates` | Ranker | 排名候选人并生成候选名单 |
| `*triage-full` | Ranker | 完整筛选流水线 |
| `*candidate-summary` | SummaryWriter | 生成候选人高管摘要 |
| `*comparison-matrix` | SummaryWriter | 生成比较矩阵 |

## 快速开始

```
# 激活排名器（主编排器）
/rss:agents:shortlist-ranker

# 完整筛选流水线
*triage-full

# 快速技能匹配
*quick-match

# 仅简历解析
*parse-resumes

# 仅偏见审计
*audit-bias
```

## 目标用户

- 招聘经理和猎头
- 人力资源和人才获取团队
- DEI（多元化、公平和包容）专家
- CTO和为团队招聘的技术领导者

## 要求

- 可读格式的简历（PDF、DOCX、文本）
- 职位描述及要求（必备和加分项）
- 期望的候选名单大小定义
