# resume-screener-squad

Specialist squad for resume screening in recruitment.

## Overview

The **resume-screener-squad** is a complete squad covering the entire resume screening pipeline:

1. **Resume Parsing** — Automated structured data extraction from CVs in any format (PDF, DOCX, text)
2. **Skills Matching** — Comparing skills with job requirements, weighted fit score calculation, and transferable skills identification
3. **Bias Auditing** — Detection of gender, age, ethnicity, education pedigree, and name biases, ensuring fairness
4. **Candidate Ranking** — Transparent ranking with justifications, hidden gems identification, and configurable shortlist
5. **Executive Summaries** — Actionable briefs for hiring managers with strengths, concerns, comparison matrix, and interview questions

**Pain Point:** Average cost of $4,700 per hire with a 44-day cycle; manual screening is prone to unconscious biases and loss of qualified candidates.

## Agents

| Agent | ID | Role |
|---|---|---|
| 📋 Parser | `resume-parser` | Resume parser and data extraction |
| 🔍 SkillsMatcher | `skills-matcher` | Skills matching and fit score calculator |
| 🛡️ BiasAuditor | `bias-auditor` | Bias auditing and fairness |
| ⚡ Ranker | `shortlist-ranker` | Ranking and shortlist generation |
| 📊 SummaryWriter | `candidate-summary-agent` | Executive summaries and briefs |

## Workflows

| Workflow | Command | Description | Duration |
|---|---|---|---|
| Full Resume Screening | `*triage-full` | Complete pipeline: from parsing to executive summary | 30-60 min |
| Quick Skills Match | `*quick-match` | Quick match: parsing, matching and simplified summary | 10-20 min |

## Available Commands

| Command | Agent | Description |
|---|---|---|
| `*parse-resumes` | Parser | Extract structured data from resumes |
| `*parse-single` | Parser | Extract data from a specific resume |
| `*match-skills` | SkillsMatcher | Calculate candidate fit scores |
| `*analyze-gaps` | SkillsMatcher | Analyze skill gaps |
| `*audit-bias` | BiasAuditor | Audit screening process for biases |
| `*check-fairness` | BiasAuditor | Verify ranking fairness |
| `*rank-candidates` | Ranker | Rank candidates and generate shortlist |
| `*triage-full` | Ranker | Complete screening pipeline |
| `*candidate-summary` | SummaryWriter | Generate candidate executive summaries |
| `*comparison-matrix` | SummaryWriter | Generate comparison matrix |

## Quick Start

```
# Activate the ranker (main orchestrator)
/rss:agents:shortlist-ranker

# Full screening pipeline
*triage-full

# Quick skills match
*quick-match

# Resume parsing only
*parse-resumes

# Bias audit only
*audit-bias
```

## Target Users

- Hiring Managers and Recruiters
- HR and Talent Acquisition Teams
- DEI (Diversity, Equity and Inclusion) Specialists
- CTOs and Technical Leaders hiring for their teams

## Requirements

- Resumes in readable format (PDF, DOCX, text)
- Job description with requirements (must-have and nice-to-have)
- Desired shortlist size definition
