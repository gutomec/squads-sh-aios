# adaptive-tutor-k12

Specialist squad for K-12 adaptive tutoring.

## Overview

The **adaptive-tutor-k12** is a complete squad covering the entire personalized tutoring cycle:

1. **Diagnostic Assessment** — Adaptive diagnostics to map knowledge gaps, proficiency level, and learning style
2. **Curriculum Mapping** — Personalized learning paths aligned with BNCC/Common Core, with gradual progression and spaced repetition
3. **Adaptive Tutoring** — Personalized sessions with multiple pedagogical approaches, adaptive exercises, and immediate feedback
4. **Progress Tracking** — Topic-level mastery monitoring, stagnation detection, and trend analysis
5. **Parent Reports** — Accessible reports celebrating achievements, explaining improvement areas, and providing practical home recommendations

**Pain Point:** Individual tutoring yields 98% performance improvement vs 20% in conventional classrooms (Bloom, 1984), but is inaccessible to most families due to high cost.

## Agents

| Agent | ID | Role |
|---|---|---|
| 📋 Assessor | `diagnostic-assessor` | Diagnostic assessment and gap detection |
| 🗺️ CurriculumMapper | `curriculum-mapper` | Curriculum mapping and personalized paths |
| 🎓 Tutor | `tutor-agent` | Adaptive tutoring and personalized teaching |
| 📊 ProgressTracker | `progress-tracker` | Progress tracking and trend analysis |
| 📧 ParentReporter | `parent-report-agent` | Parent and educator report generation |

## Workflows

| Workflow | Command | Description | Duration |
|---|---|---|---|
| Full Tutoring Cycle | `*full-tutoring` | Complete cycle: from diagnostic to parent report | 60-90 min |
| Quick Practice Session | `*quick-practice` | Quick practice: tutoring with tracking | 20-40 min |

## Available Commands

| Command | Agent | Description |
|---|---|---|
| `*assess-student` | Assessor | Assess student knowledge level |
| `*identify-gaps` | Assessor | Identify specific knowledge gaps |
| `*map-curriculum` | CurriculumMapper | Create personalized learning path |
| `*adjust-path` | CurriculumMapper | Adjust path based on progress |
| `*tutor-session` | Tutor | Start personalized tutoring session |
| `*practice` | Tutor | Generate practice exercises |
| `*full-tutoring` | Tutor | Full adaptive tutoring cycle |
| `*track-progress` | ProgressTracker | Analyze learning progress |
| `*detect-stagnation` | ProgressTracker | Detect stagnation signals |
| `*parent-report` | ParentReporter | Generate progress report for parents |
| `*educator-report` | ParentReporter | Generate report for educator/teacher |

## Quick Start

```
# Activate the tutor (main orchestrator)
/atk:agents:tutor-agent

# Full adaptive tutoring cycle
*full-tutoring

# Quick practice
*quick-practice

# Diagnostic assessment only
*assess-student

# Parent report only
*parent-report
```

## Target Users

- Parents seeking personalized tutoring
- K-12 Students (Elementary through High School)
- Teachers and pedagogues
- Schools and educational institutions
- EdTech platforms

## Requirements

- Subject and grade level definition
- Information about specific difficulties (optional)
- Availability for tutoring sessions (20-90 min)
- Parental consent for minor data collection (LGPD/COPPA)
