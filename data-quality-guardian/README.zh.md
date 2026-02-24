# data-quality-guardian

数据管道数据质量专家小组。

## 概述

**data-quality-guardian** 是一个完整的小组，涵盖整个数据质量管道：

1. **数据画像** — 分布分析、数据类型、基数、空值率、唯一性和描述性统计
2. **异常检测** — 异常值识别、数据漂移、异常模式和基线偏差
3. **模式验证** — 类型检查、约束、参照完整性和破坏性变更检测
4. **质量报告** — 6个维度的综合评分、趋势、SLA比较和执行摘要
5. **修复建议** — 自动化清理脚本、管道修复和治理建议

**痛点：** 89%的数据团队报告质量问题；61%将数据质量列为组织中的首要挑战。

## 代理

| 代理 | ID | 角色 |
|---|---|---|
| 📋 Profiler | `data-profiler` | 数据画像和统计 |
| 🔍 AnomalyDetector | `anomaly-detector` | 异常和异常值检测器 |
| 🛡️ SchemaValidator | `schema-validator` | 模式和完整性验证器 |
| 📊 QualityReporter | `data-quality-reporter` | 质量报告和指标 |
| ⚡ RemediationSuggester | `remediation-suggester` | 修复和预防建议器 |

## 工作流

| 工作流 | 命令 | 描述 | 持续时间 |
|---|---|---|---|
| 完整数据质量审计 | `*full-audit` | 完整管道：从画像到修复 | 30-60分钟 |
| 快速数据检查 | `*quick-check` | 快速检查：画像、模式和报告 | 10-20分钟 |

## 可用命令

| 命令 | 代理 | 描述 |
|---|---|---|
| `*profile-data` | Profiler | 完整数据集画像 |
| `*compare-baseline` | Profiler | 将当前画像与基线比较 |
| `*detect-anomalies` | AnomalyDetector | 检测数据集中的异常 |
| `*check-drift` | AnomalyDetector | 检查期间之间的数据漂移 |
| `*validate-schema` | SchemaValidator | 验证数据集模式 |
| `*check-integrity` | SchemaValidator | 检查参照完整性 |
| `*quality-report` | QualityReporter | 生成质量报告 |
| `*quality-score` | QualityReporter | 计算质量评分 |
| `*full-audit` | QualityReporter | 完整数据质量审计 |
| `*suggest-fix` | RemediationSuggester | 建议修复方案 |
| `*generate-script` | RemediationSuggester | 生成清理脚本 |

## 快速开始

```
# 激活质量报告器（主编排器）
/dqg:agents:data-quality-reporter

# 完整数据质量审计
*full-audit

# 快速数据检查
*quick-check

# 仅数据画像
*profile-data

# 仅异常检测
*detect-anomalies
```

## 目标用户

- 数据工程师
- 数据分析师
- 数据治理团队
- 分析工程师
- CTO和数据负责人

## 要求

- 访问待分析的数据集（CSV、Parquet、JSON、SQL）
- 预期模式文档（可选，可推断）
- 用于比较的先前基线（可选）
- 质量SLA定义（可选）
