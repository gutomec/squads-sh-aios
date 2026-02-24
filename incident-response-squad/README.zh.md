# incident-response-squad

DevOps/SRE 事件响应专家小组。

## 概述

**incident-response-squad** 是一个完整的小组，涵盖整个事件响应流水线：

1. **日志分析** — 从多个来源（CloudWatch、ELK、Splunk、Datadog）聚合和分析日志
2. **根因关联** — 关联20-45个监控工具的信号，映射爆炸半径
3. **运维手册执行** — 自动化运维手册用于回滚、扩缩容、重启和修复
4. **状态通知** — 更新状态页面并通知相关方
5. **事后总结** — 生成无指责的事后文档，包含时间线、行动项和经验教训

**痛点：** 65%的解决时间花在诊断根本原因上；企业管理着20-45个监控工具。

## 代理

| 代理 | ID | 角色 |
|---|---|---|
| 📋 LogAnalyzer | `log-analyzer` | 多源日志分析器 |
| 🔍 Correlator | `root-cause-correlator` | 根因关联器和爆炸半径映射 |
| ⚡ RunbookExec | `runbook-executor` | 修复运维手册执行器 |
| 📢 StatusUpdater | `status-page-updater` | 通信和状态页面管理器 |
| 📝 PostMortem | `postmortem-writer` | 无指责事后总结生成器 |

## 工作流

| 工作流 | 命令 | 描述 | 持续时间 |
|---|---|---|---|
| 完整事件响应 | `*respond-incident` | 完整流水线：从告警到事后总结 | 30-90分钟 |
| 快速分诊 | `*triage-incident` | 快速分诊：分析、根因、通知 | 10-20分钟 |

## 可用命令

| 命令 | 代理 | 描述 |
|---|---|---|
| `*analyze-logs` | LogAnalyzer | 分析事件日志 |
| `*search-logs` | LogAnalyzer | 在日志中搜索特定模式 |
| `*correlate-signals` | Correlator | 关联多源信号 |
| `*find-root-cause` | Correlator | 识别最可能的根本原因 |
| `*execute-runbook` | RunbookExec | 执行修复运维手册 |
| `*list-runbooks` | RunbookExec | 列出可用运维手册 |
| `*update-status` | StatusUpdater | 更新状态页面 |
| `*notify-stakeholders` | StatusUpdater | 通知相关方 |
| `*write-postmortem` | PostMortem | 生成无指责事后总结 |
| `*generate-timeline` | PostMortem | 生成事件时间线 |

## 快速开始

```
# 激活关联器（主编排器）
/irs:agents:root-cause-correlator

# 完整事件响应流水线
*respond-incident

# 快速分诊
*triage-incident

# 仅日志分析
*analyze-logs

# 仅事后总结
*write-postmortem
```

## 目标用户

- SRE（站点可靠性工程师）
- DevOps工程师
- 值班工程师
- CTO和技术负责人

## 要求

- 访问监控工具（Datadog、Prometheus、Grafana）
- 访问日志平台（ELK、Splunk、CloudWatch）
- 访问状态页面（Statuspage.io、Atlassian）
- 配置通信渠道（Slack #incidents）
