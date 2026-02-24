# saas-onboarding-activator

Squad especialista em ativação e onboarding de usuários SaaS.

## Visão Geral

O **saas-onboarding-activator** é um squad completo que cobre todo o pipeline de ativação de onboarding:

1. **Rastreamento Comportamental** — Monitoramento de ações, detecção de abandono, segmentação por cohort e feature adoption
2. **Checklists Personalizados** — Checklists dinâmicos por segmento, plano e comportamento com gamificação e progressão visual
3. **Identificação de Aha Moment** — Correlação ação-retenção para descobrir o momento mágico e otimizar o caminho até ele
4. **Tooltips Contextuais** — Guided tours, hotspots, beacons e in-app messages no momento certo, no lugar certo
5. **Outreach Proativo** — Emails, push notifications e mensagens baseadas em comportamento para re-engajar e ativar

**Pain Point:** 75% dos usuários abandonam na primeira semana; 90% de churn ocorre se o usuário não engajar em 3 dias.

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 📊 Tracker | `user-behavior-tracker` | Rastreador de comportamento e analytics |
| ✅ ChecklistBuilder | `checklist-builder` | Construtor de checklists personalizados |
| 💡 AhaFinder | `aha-moment-identifier` | Identificador de aha moment e path optimizer |
| 💬 TooltipGen | `tooltip-generator` | Gerador de tooltips e guided tours |
| 📧 Outreach | `proactive-outreach` | Especialista em outreach e re-engajamento |

## Workflows

| Workflow | Comando | Descrição | Duração |
|---|---|---|---|
| Full Onboarding Activation | `*activate-users` | Pipeline completo: do tracking ao outreach | 90-150 min |
| Quick Engagement Boost | `*quick-engage` | Boost rápido: tracking, aha moment, outreach | 30-45 min |

## Comandos Disponíveis

| Comando | Agente | Descrição |
|---|---|---|
| `*track-behavior` | Tracker | Rastrear comportamento de onboarding |
| `*detect-churn-signals` | Tracker | Detectar sinais de abandono |
| `*build-checklist` | ChecklistBuilder | Criar checklist personalizado |
| `*optimize-checklist` | ChecklistBuilder | Otimizar checklist existente |
| `*find-aha` | AhaFinder | Identificar aha moment |
| `*optimize-path` | AhaFinder | Otimizar caminho até o aha moment |
| `*generate-tooltips` | TooltipGen | Gerar tooltips para onboarding |
| `*create-tour` | TooltipGen | Criar guided tour interativo |
| `*send-outreach` | Outreach | Enviar comunicação proativa |
| `*create-sequence` | Outreach | Criar sequência de emails |
| `*activate-users` | Outreach | Pipeline completo de ativação |

## Quick Start

```
# Ativar o orquestrador de outreach
/soa:agents:proactive-outreach

# Pipeline completo de ativação de onboarding
*activate-users

# Boost rápido de engajamento
*quick-engage

# Apenas rastreamento comportamental
*track-behavior

# Apenas identificar aha moment
*find-aha
```

## Público Alvo

- Product Managers e Product Owners
- Growth Engineers e Growth Hackers
- Customer Success Managers
- UX Designers focados em onboarding
- Marketing de Produto e Lifecycle Marketing

## Requisitos

- Acesso a ferramentas de analytics (Mixpanel, Amplitude, Segment, PostHog)
- Acesso a plataformas de onboarding (Appcues, Pendo, Userpilot)
- Acesso a ferramentas de email (Customer.io, Iterable, Braze)
- Dados de tracking configurados no produto
