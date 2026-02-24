# ambient-clinical-scribe

> AI-powered ambient clinical documentation squad — from consultation audio to complete medical records with SOAP notes, ICD-10/CPT codes, and quality review. 69.5% reduction in physician administrative time.

## Installation

```bash
npx squads add gutomec/squads-sh-aios/ambient-clinical-scribe
```

## What It Does

**ambient-clinical-scribe** is a squad that automates the entire clinical documentation pipeline:

1. **Capture** — Real-time transcription of medical consultations with speaker diarization
2. **Documentation** — Generation of structured clinical notes in SOAP format
3. **Coding** — Automatic assignment of ICD-10 and CPT codes
4. **Quality** — Review of completeness, accuracy, and HIPAA/CMS compliance

Physicians spend 3+ extra hours per week on administrative documentation. This squad reduces that time by 69.5%, allowing more focus on patient care.

## Agents

| Agent | ID | Role |
|---|---|---|
| 🎙️ AmbientListener | `ambient-listener` | Real-time consultation transcription |
| 📋 NoteDrafter | `clinical-note-drafter` | Structured SOAP note generation |
| 🏥 MedicalCoder | `medical-coder` | ICD-10 and CPT coding |
| ✅ QualityReviewer | `quality-reviewer` | Quality review and compliance |

## Workflows

| Workflow | Command | Description | Duration |
|---|---|---|---|
| Full Documentation | `*document-visit` | Complete pipeline (transcription + note + coding + review) | 5-15 min |
| Quick Note | `*quick-note` | Fast SOAP note without coding | 3-8 min |

## Quick Start

```
# Activate the scribe and document a complete visit
/acs:agents:ambient-listener
*document-visit

# Generate a quick note without coding
*quick-note

# Just generate a SOAP note
/acs:agents:clinical-note-drafter
*draft-note --format=soap

# Just medical coding
/acs:agents:medical-coder
*assign-codes

# Quality review
/acs:agents:quality-reviewer
*review-note
```

## Available Commands

| Command | Agent | Description |
|---|---|---|
| `*start-listening` | AmbientListener | Start real-time capture |
| `*transcribe-session` | AmbientListener | Transcribe audio file |
| `*draft-note` | NoteDrafter | Generate structured clinical note |
| `*format-soap` | NoteDrafter | Format data into SOAP |
| `*assign-codes` | MedicalCoder | Assign ICD-10/CPT codes |
| `*validate-codes` | MedicalCoder | Validate assigned codes |
| `*review-note` | QualityReviewer | Review clinical note |
| `*compliance-check` | QualityReviewer | Check HIPAA/CMS compliance |
| `*document-visit` | Pipeline | Complete documentation |
| `*full-documentation` | Pipeline | Complete documentation (alias) |
| `*quick-note` | Pipeline | Quick note without coding |
| `*draft-visit` | Pipeline | Quick note (alias) |

## Compliance

This squad is designed with compliance in mind:

- **HIPAA** — PHI (Protected Health Information) protection at every stage
- **CMS Guidelines** — Adherence to documentation guidelines for coding and reimbursement
- **OIG Compliance** — Prevention of upcoding/downcoding and coding fraud

**IMPORTANT:** Actual compliance implementation depends on deployment infrastructure. This squad provides checks and validations, but data security (encryption, access control, audit trail) must be implemented at the infrastructure layer.

## Author

**Luiz Gustavo Vieira Rodrigues** ([@gutomec](https://github.com/gutomec))

## License

MIT
