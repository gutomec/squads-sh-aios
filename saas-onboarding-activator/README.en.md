# saas-onboarding-activator

Specialist squad for SaaS user activation and onboarding.

## Overview

The **saas-onboarding-activator** is a complete squad covering the entire onboarding activation pipeline:

1. **Behavioral Tracking** — Action monitoring, abandonment detection, cohort segmentation, and feature adoption tracking
2. **Personalized Checklists** — Dynamic checklists by segment, plan, and behavior with gamification and visual progression
3. **Aha Moment Identification** — Action-retention correlation to discover the magic moment and optimize the path to it
4. **Contextual Tooltips** — Guided tours, hotspots, beacons, and in-app messages at the right time, in the right place
5. **Proactive Outreach** — Emails, push notifications, and behavior-based messages to re-engage and activate

**Pain Point:** 75% of users abandon in the first week; 90% churn if users don't engage within 3 days.

## Agents

| Agent | ID | Role |
|---|---|---|
| 📊 Tracker | `user-behavior-tracker` | Behavior tracking and analytics |
| ✅ ChecklistBuilder | `checklist-builder` | Personalized checklist builder |
| 💡 AhaFinder | `aha-moment-identifier` | Aha moment identifier and path optimizer |
| 💬 TooltipGen | `tooltip-generator` | Tooltip and guided tour generator |
| 📧 Outreach | `proactive-outreach` | Outreach and re-engagement specialist |

## Workflows

| Workflow | Command | Description | Duration |
|---|---|---|---|
| Full Onboarding Activation | `*activate-users` | Full pipeline: from tracking to outreach | 90-150 min |
| Quick Engagement Boost | `*quick-engage` | Quick boost: tracking, aha moment, outreach | 30-45 min |

## Available Commands

| Command | Agent | Description |
|---|---|---|
| `*track-behavior` | Tracker | Track onboarding behavior |
| `*detect-churn-signals` | Tracker | Detect abandonment signals |
| `*build-checklist` | ChecklistBuilder | Create personalized checklist |
| `*optimize-checklist` | ChecklistBuilder | Optimize existing checklist |
| `*find-aha` | AhaFinder | Identify aha moment |
| `*optimize-path` | AhaFinder | Optimize path to aha moment |
| `*generate-tooltips` | TooltipGen | Generate onboarding tooltips |
| `*create-tour` | TooltipGen | Create interactive guided tour |
| `*send-outreach` | Outreach | Send proactive communication |
| `*create-sequence` | Outreach | Create email sequence |
| `*activate-users` | Outreach | Full activation pipeline |

## Quick Start

```
# Activate the outreach orchestrator
/soa:agents:proactive-outreach

# Full onboarding activation pipeline
*activate-users

# Quick engagement boost
*quick-engage

# Behavioral tracking only
*track-behavior

# Identify aha moment only
*find-aha
```

## Target Users

- Product Managers and Product Owners
- Growth Engineers and Growth Hackers
- Customer Success Managers
- UX Designers focused on onboarding
- Product Marketing and Lifecycle Marketing

## Requirements

- Access to analytics tools (Mixpanel, Amplitude, Segment, PostHog)
- Access to onboarding platforms (Appcues, Pendo, Userpilot)
- Access to email tools (Customer.io, Iterable, Braze)
- Tracking data configured in the product
