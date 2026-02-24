# soc-alert-triage

SOC告警分诊网络安全专家小组。

## 概述

**soc-alert-triage** 是一个完整的小组，涵盖整个安全告警分诊流水线：

1. **告警分类** — 从多个来源（SIEM、IDS、EDR、云）按类型、严重性和MITRE ATT&CK映射进行自动化分类
2. **误报过滤** — 使用历史模式、行为基线和上下文白名单识别和过滤误报
3. **威胁优先级排序** — 基于可利用性、爆炸半径、资产关键性和业务影响的风险评分
4. **威胁情报丰富** — IOC、完整MITRE ATT&CK映射、信誉评分和历史关联
5. **简报生成** — 包含时间线、推荐剧本、IOC和优先响应操作的可操作文档

**痛点：** SOC分析师每天面临4000+告警，80%以上为误报——导致告警疲劳、倦怠和错过真实威胁的风险。

## 代理

| 代理 | ID | 角色 |
|---|---|---|
| 🏷️ Classifier | `alert-classifier` | 按类型、严重性和MITRE ATT&CK分类告警 |
| 🛡️ FPFilter | `false-positive-filter` | 使用基线和启发式方法过滤误报 |
| ⚡ Prioritizer | `threat-prioritizer` | 按复合风险评分排序威胁优先级 |
| 🔍 Enricher | `context-enricher` | 使用IOC和威胁情报丰富上下文 |
| 📊 BriefGen | `analyst-brief-generator` | 为SOC分析师生成可操作简报 |

## 工作流

| 工作流 | 命令 | 描述 | 持续时间 |
|---|---|---|---|
| 完整告警分诊 | `*triage-full` | 完整流水线：从分类到简报 | 30-60分钟 |
| 快速分类 | `*rapid-classify` | 快速分类：分类、过滤和简报 | 10-20分钟 |

## 可用命令

| 命令 | 代理 | 描述 |
|---|---|---|
| `*classify-alerts` | Classifier | 批量分类安全告警 |
| `*classify-single` | Classifier | 分类特定告警 |
| `*filter-fps` | FPFilter | 批量过滤误报 |
| `*check-fp` | FPFilter | 检查告警是否为误报 |
| `*prioritize` | Prioritizer | 按风险评分排序威胁 |
| `*risk-score` | Prioritizer | 计算特定威胁的风险评分 |
| `*triage-full` | Prioritizer | 完整分诊流水线 |
| `*enrich` | Enricher | 使用上下文和威胁情报丰富告警 |
| `*ioc-lookup` | Enricher | 在威胁情报源中查找IOC |
| `*generate-brief` | BriefGen | 为SOC分析师生成简报 |
| `*incident-summary` | BriefGen | 生成事件执行摘要 |

## 快速开始

```
# 激活优先级排序器（主编排器）
/sat:agents:threat-prioritizer

# 完整告警分诊流水线
*triage-full

# 快速分类
*rapid-classify

# 仅告警分类
*classify-alerts

# 仅生成简报
*generate-brief
```

## 目标用户

- SOC分析师（L1、L2、L3）
- 安全工程师
- 威胁猎人
- CISO和安全负责人
- 事件响应团队

## 要求

- 访问SIEM（Splunk、QRadar、Sentinel、Elastic SIEM）
- 访问威胁情报源（VirusTotal、AbuseIPDB、MISP）
- 访问EDR工具（CrowdStrike、SentinelOne、Defender）
- MITRE ATT&CK框架作为分类参考
