# automated-code-review-squad

Specialist squad for automated code review.

## Overview

The **automated-code-review-squad** is a complete squad covering the entire automated code review pipeline:

1. **Security Review** — OWASP Top 10, injection flaws, XSS, secrets exposure, dependencies with CVEs
2. **Logic Analysis** — Edge cases, race conditions, null handling, off-by-one errors, business logic
3. **Architecture Verification** — SOLID, DRY, separation of concerns, layer violations, coupling/cohesion
4. **Style Enforcement** — Naming conventions, formatting, documentation, imports, project rules
5. **Review Summary** — Prioritized findings synthesis with verdict (APPROVE/REQUEST_CHANGES/BLOCK)

**Pain Point:** Code reviews consume enormous blocks of senior developer time; merge bottleneck in PRs with long review queues.

## Agents

| Agent | ID | Role |
|---|---|---|
| 🔒 SecurityReviewer | `security-reviewer` | Vulnerability detection and security review |
| 🧠 LogicReviewer | `logic-reviewer` | Logic, correctness, and edge case review |
| 🏗️ ArchChecker | `architecture-checker` | Architectural pattern and design verification |
| ✅ StyleEnforcer | `style-enforcer` | Coding standards and style enforcement |
| 📝 SummaryWriter | `review-summary-writer` | Findings synthesis and approval recommendation |

## Workflows

| Workflow | Command | Description | Duration |
|---|---|---|---|
| Full Code Review | `*full-review` | Full pipeline: security, logic, architecture, style and summary | 30-60 min |
| Quick Security Check | `*quick-security` | Quick check focused on security | 10-20 min |

## Available Commands

| Command | Agent | Description |
|---|---|---|
| `*review-security` | SecurityReviewer | Review code for security vulnerabilities |
| `*check-secrets` | SecurityReviewer | Check for secrets exposure in code |
| `*review-logic` | LogicReviewer | Review code logic and correctness |
| `*find-edge-cases` | LogicReviewer | Identify unhandled edge cases |
| `*check-architecture` | ArchChecker | Verify architectural patterns |
| `*analyze-coupling` | ArchChecker | Analyze coupling and cohesion |
| `*check-style` | StyleEnforcer | Verify coding standards adherence |
| `*fix-style` | StyleEnforcer | Suggest style fixes |
| `*write-summary` | SummaryWriter | Generate prioritized review summary |
| `*full-review` | SummaryWriter | Full automated code review pipeline |

## Quick Start

```
# Activate the synthesizer (main orchestrator)
/acr:agents:review-summary-writer

# Full code review pipeline
*full-review

# Quick security check
*quick-security

# Security review only
*review-security

# Logic review only
*review-logic
```

## Target Users

- Senior developers and leads
- Security engineers (AppSec)
- Software architects
- Tech leads and engineering managers
- Teams with high PR volume

## Requirements

- Accessible source code (local repository or PR URL)
- Project linter configuration (optional, improves accuracy)
- GitHub CLI access for PR integration (optional)
