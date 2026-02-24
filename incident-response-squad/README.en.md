# incident-response-squad

Specialist squad for incident response in DevOps/SRE.

## Overview

The **incident-response-squad** is a complete squad covering the entire incident response pipeline:

1. **Log Analysis** — Aggregation and analysis of logs from multiple sources (CloudWatch, ELK, Splunk, Datadog)
2. **Root Cause Correlation** — Signal correlation from 20-45 monitoring tools, blast radius mapping
3. **Runbook Execution** — Automated runbooks for rollback, scaling, restart and remediation
4. **Status Communication** — Status page updates and stakeholder notifications
5. **Post-Mortem** — Blameless document generation with timeline, action items and lessons learned

**Pain Point:** 65% of resolution time is spent diagnosing root cause; companies manage 20-45 monitoring tools.

## Agents

| Agent | ID | Role |
|---|---|---|
| 📋 LogAnalyzer | `log-analyzer` | Multi-source log analyzer |
| 🔍 Correlator | `root-cause-correlator` | Root cause correlator and blast radius mapper |
| ⚡ RunbookExec | `runbook-executor` | Remediation runbook executor |
| 📢 StatusUpdater | `status-page-updater` | Communication and status page manager |
| 📝 PostMortem | `postmortem-writer` | Blameless post-mortem generator |

## Workflows

| Workflow | Command | Description | Duration |
|---|---|---|---|
| Full Incident Response | `*respond-incident` | Full pipeline: from alert to post-mortem | 30-90 min |
| Rapid Triage | `*triage-incident` | Quick triage: analysis, root cause, communication | 10-20 min |

## Available Commands

| Command | Agent | Description |
|---|---|---|
| `*analyze-logs` | LogAnalyzer | Analyze logs for an incident |
| `*search-logs` | LogAnalyzer | Search for a specific pattern in logs |
| `*correlate-signals` | Correlator | Correlate signals from multiple sources |
| `*find-root-cause` | Correlator | Identify most probable root cause |
| `*execute-runbook` | RunbookExec | Execute remediation runbook |
| `*list-runbooks` | RunbookExec | List available runbooks |
| `*update-status` | StatusUpdater | Update status page |
| `*notify-stakeholders` | StatusUpdater | Notify stakeholders |
| `*write-postmortem` | PostMortem | Generate blameless post-mortem |
| `*generate-timeline` | PostMortem | Generate incident timeline |

## Quick Start

```
# Activate the correlator (main orchestrator)
/irs:agents:root-cause-correlator

# Full incident response pipeline
*respond-incident

# Quick triage
*triage-incident

# Log analysis only
*analyze-logs

# Post-mortem only
*write-postmortem
```

## Target Users

- SREs (Site Reliability Engineers)
- DevOps Engineers
- On-call Engineers
- CTOs and Technical Leaders

## Requirements

- Access to monitoring tools (Datadog, Prometheus, Grafana)
- Access to log platforms (ELK, Splunk, CloudWatch)
- Access to status page (Statuspage.io, Atlassian)
- Communication channel configured (Slack #incidents)
