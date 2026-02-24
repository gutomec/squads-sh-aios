# ambient-clinical-scribe

> AI 驱动的环境临床文档 squad — 从问诊音频到完整病历，包含 SOAP 病历、ICD-10/CPT 编码和质量审核。减少医生 69.5% 的行政时间。

## 安装

```bash
npx squads add gutomec/squads-sh-aios/ambient-clinical-scribe
```

## 功能介绍

**ambient-clinical-scribe** 是一个自动化整个临床文档流程的 squad：

1. **采集** — 实时转录医疗问诊，支持说话人分离
2. **文档** — 生成 SOAP 格式的结构化临床病历
3. **编码** — 自动分配 ICD-10 和 CPT 编码
4. **质量** — 审核完整性、准确性和 HIPAA/CMS 合规性

医生每周在行政文档上花费超过 3 小时。此 squad 将该时间减少 69.5%，让医生更专注于患者护理。

## 智能体

| 智能体 | ID | 职责 |
|---|---|---|
| 🎙️ AmbientListener | `ambient-listener` | 实时问诊转录 |
| 📋 NoteDrafter | `clinical-note-drafter` | 结构化 SOAP 病历生成 |
| 🏥 MedicalCoder | `medical-coder` | ICD-10 和 CPT 编码 |
| ✅ QualityReviewer | `quality-reviewer` | 质量审核与合规 |

## 工作流

| 工作流 | 命令 | 描述 | 时长 |
|---|---|---|---|
| 完整文档 | `*document-visit` | 完整流程（转录 + 病历 + 编码 + 审核） | 5-15 分钟 |
| 快速病历 | `*quick-note` | 快速 SOAP 病历（跳过编码） | 3-8 分钟 |

## 快速开始

```
# 激活 scribe 并记录完整就诊
/acs:agents:ambient-listener
*document-visit

# 生成快速病历（无编码）
*quick-note

# 仅生成 SOAP 病历
/acs:agents:clinical-note-drafter
*draft-note --format=soap

# 仅医学编码
/acs:agents:medical-coder
*assign-codes

# 质量审核
/acs:agents:quality-reviewer
*review-note
```

## 可用命令

| 命令 | 智能体 | 描述 |
|---|---|---|
| `*start-listening` | AmbientListener | 开始实时采集 |
| `*transcribe-session` | AmbientListener | 转录音频文件 |
| `*draft-note` | NoteDrafter | 生成结构化临床病历 |
| `*format-soap` | NoteDrafter | 格式化为 SOAP |
| `*assign-codes` | MedicalCoder | 分配 ICD-10/CPT 编码 |
| `*validate-codes` | MedicalCoder | 验证已分配编码 |
| `*review-note` | QualityReviewer | 审核临床病历 |
| `*compliance-check` | QualityReviewer | 检查 HIPAA/CMS 合规性 |
| `*document-visit` | 流程 | 完整文档 |
| `*full-documentation` | 流程 | 完整文档（别名） |
| `*quick-note` | 流程 | 快速病历（无编码） |
| `*draft-visit` | 流程 | 快速病历（别名） |

## 合规

此 squad 以合规为设计理念：

- **HIPAA** — 每个环节保护 PHI（受保护健康信息）
- **CMS 指南** — 遵循编码和报销的文档指南
- **OIG 合规** — 防止高编码/低编码和编码欺诈

**重要：** 实际合规实施取决于部署基础设施。此 squad 提供检查和验证，但数据安全（加密、访问控制、审计追踪）必须在基础设施层实现。

## 作者

**Luiz Gustavo Vieira Rodrigues** ([@gutomec](https://github.com/gutomec))

## 许可证

MIT
