# content-factory-squad

Specialist squad for content production at scale for marketing.

## Overview

The **content-factory-squad** is a complete squad covering the entire content production pipeline:

1. **Editorial Planning** — Multi-channel editorial calendars, theme definition, buyer journey mapping and content pillars
2. **Long-Form Content Creation** — Articles, blog posts, whitepapers, e-books and case studies optimized for SEO with storytelling
3. **Social Media Adaptation** — Transforming long-form content into Instagram carousels, Twitter/X threads, LinkedIn posts and TikTok scripts
4. **Image Briefs** — Visual direction with dimension specifications, composition, style and AI generation prompts
5. **Multi-Channel Scheduling** — Publications scheduled at optimal times per platform with queue management and cadence

**Pain Point:** Producing quality content at scale for multiple channels requires coordination between strategy, writing, design and publishing — a process that normally takes days can be accelerated with agent orchestration.

## Agents

| Agent | ID | Role |
|---|---|---|
| 📋 Strategist | `content-strategist` | Content strategist and editorial planning |
| ✍️ Writer | `long-form-writer` | Long-form content writer and SEO |
| 📱 SocialAdapter | `social-media-adapter` | Social media content adapter |
| 🎨 ImageBriefer | `image-brief-generator` | Image brief and visual direction generator |
| ⏰ Scheduler | `publishing-scheduler` | Multi-channel publishing scheduler |

## Workflows

| Workflow | Command | Description | Duration |
|---|---|---|---|
| Full Content Pipeline | `*content-pipeline` | Full pipeline: from planning to scheduling | 60-120 min |
| Quick Social Blast | `*social-blast` | Quick production: from theme to scheduled post | 15-30 min |

## Available Commands

| Command | Agent | Description |
|---|---|---|
| `*plan-calendar` | Strategist | Plan monthly/quarterly editorial calendar |
| `*content-pipeline` | Strategist | Full content production pipeline |
| `*write-article` | Writer | Write article or blog post |
| `*write-whitepaper` | Writer | Write whitepaper or e-book |
| `*adapt-social` | SocialAdapter | Adapt content for social media |
| `*create-thread` | SocialAdapter | Create Twitter/X thread |
| `*generate-brief` | ImageBriefer | Generate image brief for content |
| `*batch-briefs` | ImageBriefer | Generate briefs for multiple pieces |
| `*schedule` | Scheduler | Schedule content publishing |
| `*optimize-times` | Scheduler | Optimize publishing times |

## Quick Start

```
# Activate the strategist (main orchestrator)
/cfs:agents:content-strategist

# Full content production pipeline
*content-pipeline

# Quick social blast
*social-blast

# Write an article only
*write-article

# Adapt for social media only
*adapt-social
```

## Target Users

- Content Marketing Managers
- Social Media Managers
- Content Strategists
- Copywriters and Writers
- Digital Marketing Managers

## Requirements

- Access to blog platform (WordPress, HubSpot, Ghost)
- Access to social media tools (Buffer, Hootsuite, Later)
- Defined brand guidelines (tone of voice, color palette)
- Mapped buyer personas
