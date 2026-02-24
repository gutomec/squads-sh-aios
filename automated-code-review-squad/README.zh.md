# automated-code-review-squad

自动化代码审查专家小组。

## 概述

**automated-code-review-squad** 是一个完整的小组，涵盖整个自动化代码审查流水线：

1. **安全审查** — OWASP Top 10、注入漏洞、XSS、密钥泄露、含CVE的依赖
2. **逻辑分析** — 边界情况、竞态条件、空值处理、差一错误、业务逻辑
3. **架构验证** — SOLID、DRY、关注点分离、层违规、耦合/内聚
4. **风格执行** — 命名规范、格式化、文档、导入、项目规则
5. **审查摘要** — 带裁决的优先级发现摘要（APPROVE/REQUEST_CHANGES/BLOCK）

**痛点：** 代码审查消耗高级开发人员大量时间；PR合并因审查队列过长而形成瓶颈。

## 代理

| 代理 | ID | 角色 |
|---|---|---|
| 🔒 SecurityReviewer | `security-reviewer` | 漏洞检测和安全审查 |
| 🧠 LogicReviewer | `logic-reviewer` | 逻辑、正确性和边界情况审查 |
| 🏗️ ArchChecker | `architecture-checker` | 架构模式和设计验证 |
| ✅ StyleEnforcer | `style-enforcer` | 编码标准和风格执行 |
| 📝 SummaryWriter | `review-summary-writer` | 发现摘要和审批建议 |

## 工作流

| 工作流 | 命令 | 描述 | 持续时间 |
|---|---|---|---|
| 完整代码审查 | `*full-review` | 完整流水线：安全、逻辑、架构、风格和摘要 | 30-60分钟 |
| 快速安全检查 | `*quick-security` | 专注安全的快速检查 | 10-20分钟 |

## 可用命令

| 命令 | 代理 | 描述 |
|---|---|---|
| `*review-security` | SecurityReviewer | 审查代码安全漏洞 |
| `*check-secrets` | SecurityReviewer | 检查代码中的密钥泄露 |
| `*review-logic` | LogicReviewer | 审查代码逻辑和正确性 |
| `*find-edge-cases` | LogicReviewer | 识别未处理的边界情况 |
| `*check-architecture` | ArchChecker | 验证架构模式 |
| `*analyze-coupling` | ArchChecker | 分析耦合和内聚 |
| `*check-style` | StyleEnforcer | 验证编码标准遵循 |
| `*fix-style` | StyleEnforcer | 建议风格修复 |
| `*write-summary` | SummaryWriter | 生成优先级审查摘要 |
| `*full-review` | SummaryWriter | 完整自动化代码审查流水线 |

## 快速开始

```
# 激活合成器（主编排器）
/acr:agents:review-summary-writer

# 完整代码审查流水线
*full-review

# 快速安全检查
*quick-security

# 仅安全审查
*review-security

# 仅逻辑审查
*review-logic
```

## 目标用户

- 高级开发人员和技术负责人
- 安全工程师（AppSec）
- 软件架构师
- 技术主管和工程经理
- PR量大的团队

## 要求

- 可访问的源代码（本地仓库或PR URL）
- 项目linter配置（可选，提高准确性）
- GitHub CLI访问以集成PR（可选）
