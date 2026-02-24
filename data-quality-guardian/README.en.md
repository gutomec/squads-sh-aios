# data-quality-guardian

Specialist squad for data quality in data pipelines.

## Overview

The **data-quality-guardian** is a complete squad covering the entire data quality pipeline:

1. **Data Profiling** — Distribution analysis, data types, cardinality, null rates, uniqueness, and descriptive statistics
2. **Anomaly Detection** — Outlier identification, data drift, unusual patterns, and baseline deviations
3. **Schema Validation** — Type checking, constraints, referential integrity, and breaking change detection
4. **Quality Reports** — Composite scores across 6 dimensions, trends, SLA comparisons, and executive summaries
5. **Remediation Suggestions** — Automated cleaning scripts, pipeline fixes, and governance recommendations

**Pain Point:** 89% of data teams report quality issues; 61% list data quality as the top challenge in their organizations.

## Agents

| Agent | ID | Role |
|---|---|---|
| 📋 Profiler | `data-profiler` | Data profiler and statistics |
| 🔍 AnomalyDetector | `anomaly-detector` | Anomaly and outlier detector |
| 🛡️ SchemaValidator | `schema-validator` | Schema and integrity validator |
| 📊 QualityReporter | `data-quality-reporter` | Quality reporter and metrics |
| ⚡ RemediationSuggester | `remediation-suggester` | Remediation and prevention suggester |

## Workflows

| Workflow | Command | Description | Duration |
|---|---|---|---|
| Full Data Quality Audit | `*full-audit` | Full pipeline: from profiling to remediation | 30-60 min |
| Quick Data Check | `*quick-check` | Quick check: profiling, schema, and report | 10-20 min |

## Available Commands

| Command | Agent | Description |
|---|---|---|
| `*profile-data` | Profiler | Profile complete dataset |
| `*compare-baseline` | Profiler | Compare current profile with baseline |
| `*detect-anomalies` | AnomalyDetector | Detect anomalies in dataset |
| `*check-drift` | AnomalyDetector | Check data drift between periods |
| `*validate-schema` | SchemaValidator | Validate dataset schema |
| `*check-integrity` | SchemaValidator | Check referential integrity |
| `*quality-report` | QualityReporter | Generate quality report |
| `*quality-score` | QualityReporter | Calculate quality score |
| `*full-audit` | QualityReporter | Full data quality audit |
| `*suggest-fix` | RemediationSuggester | Suggest remediations |
| `*generate-script` | RemediationSuggester | Generate cleaning script |

## Quick Start

```
# Activate the quality reporter (main orchestrator)
/dqg:agents:data-quality-reporter

# Full data quality audit
*full-audit

# Quick data check
*quick-check

# Profiling only
*profile-data

# Anomaly detection only
*detect-anomalies
```

## Target Users

- Data Engineers
- Data Analysts
- Data Governance Teams
- Analytics Engineers
- CTOs and Data Leaders

## Requirements

- Access to the dataset for analysis (CSV, Parquet, JSON, SQL)
- Expected schema documented (optional, can be inferred)
- Previous baseline for comparison (optional)
- Quality SLA definitions (optional)
