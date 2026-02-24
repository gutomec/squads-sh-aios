# soc-alert-triage

Specialist squad for SOC alert triage in cybersecurity.

## Overview

The **soc-alert-triage** is a complete squad covering the entire security alert triage pipeline:

1. **Alert Classification** — Automated categorization by type, severity, and MITRE ATT&CK mapping from multiple sources (SIEM, IDS, EDR, cloud)
2. **False Positive Filtering** — FP identification and filtering using historical patterns, behavioral baselines, and contextual whitelists
3. **Threat Prioritization** — Risk scoring based on exploitability, blast radius, asset criticality, and business impact
4. **Threat Intel Enrichment** — IOCs, complete MITRE ATT&CK mapping, reputation scores, and historical correlation
5. **Brief Generation** — Actionable documents with timeline, recommended playbook, IOCs, and prioritized response actions

**Pain Point:** SOC analysts face 4,000+ alerts/day, with 80%+ being false positives — causing alert fatigue, burnout, and risk of missing real threats.

## Agents

| Agent | ID | Role |
|---|---|---|
| 🏷️ Classifier | `alert-classifier` | Alert classifier by type, severity, and MITRE ATT&CK |
| 🛡️ FPFilter | `false-positive-filter` | False positive filter with baselines and heuristics |
| ⚡ Prioritizer | `threat-prioritizer` | Threat prioritizer by composite risk score |
| 🔍 Enricher | `context-enricher` | Context enricher with IOCs and threat intel |
| 📊 BriefGen | `analyst-brief-generator` | Actionable brief generator for SOC analysts |

## Workflows

| Workflow | Command | Description | Duration |
|---|---|---|---|
| Full Alert Triage | `*triage-full` | Full pipeline: from classification to brief | 30-60 min |
| Rapid Classification | `*rapid-classify` | Quick classification: classify, filter, and brief | 10-20 min |

## Available Commands

| Command | Agent | Description |
|---|---|---|
| `*classify-alerts` | Classifier | Classify batch of security alerts |
| `*classify-single` | Classifier | Classify a specific alert |
| `*filter-fps` | FPFilter | Filter false positives from a batch |
| `*check-fp` | FPFilter | Check if alert is a false positive |
| `*prioritize` | Prioritizer | Prioritize threats by risk score |
| `*risk-score` | Prioritizer | Calculate risk score for specific threat |
| `*triage-full` | Prioritizer | Full triage pipeline |
| `*enrich` | Enricher | Enrich alerts with context and threat intel |
| `*ioc-lookup` | Enricher | Look up IOC in threat intel feeds |
| `*generate-brief` | BriefGen | Generate brief for SOC analyst |
| `*incident-summary` | BriefGen | Generate executive incident summary |

## Quick Start

```
# Activate the prioritizer (main orchestrator)
/sat:agents:threat-prioritizer

# Full alert triage pipeline
*triage-full

# Rapid classification
*rapid-classify

# Alert classification only
*classify-alerts

# Brief generation only
*generate-brief
```

## Target Users

- SOC Analysts (L1, L2, L3)
- Security Engineers
- Threat Hunters
- CISOs and Security Leaders
- Incident Response Teams

## Requirements

- Access to SIEM (Splunk, QRadar, Sentinel, Elastic SIEM)
- Access to threat intel feeds (VirusTotal, AbuseIPDB, MISP)
- Access to EDR tools (CrowdStrike, SentinelOne, Defender)
- MITRE ATT&CK framework as taxonomy reference
