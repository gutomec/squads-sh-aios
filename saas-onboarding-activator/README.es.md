# saas-onboarding-activator

Squad especialista en activación y onboarding de usuarios SaaS.

## Descripción General

El **saas-onboarding-activator** es un squad completo que cubre todo el pipeline de activación de onboarding:

1. **Rastreo Comportamental** — Monitoreo de acciones, detección de abandono, segmentación por cohorte y feature adoption
2. **Checklists Personalizados** — Checklists dinámicos por segmento, plan y comportamiento con gamificación y progresión visual
3. **Identificación de Aha Moment** — Correlación acción-retención para descubrir el momento mágico y optimizar el camino hasta él
4. **Tooltips Contextuales** — Guided tours, hotspots, beacons e in-app messages en el momento correcto, en el lugar correcto
5. **Outreach Proactivo** — Emails, push notifications y mensajes basados en comportamiento para re-enganchar y activar

**Pain Point:** El 75% de los usuarios abandonan en la primera semana; el 90% de churn ocurre si el usuario no se engancha en 3 días.

## Agentes

| Agente | ID | Rol |
|---|---|---|
| 📊 Tracker | `user-behavior-tracker` | Rastreador de comportamiento y analytics |
| ✅ ChecklistBuilder | `checklist-builder` | Constructor de checklists personalizados |
| 💡 AhaFinder | `aha-moment-identifier` | Identificador de aha moment y path optimizer |
| 💬 TooltipGen | `tooltip-generator` | Generador de tooltips y guided tours |
| 📧 Outreach | `proactive-outreach` | Especialista en outreach y re-enganche |

## Flujos de Trabajo

| Workflow | Comando | Descripción | Duración |
|---|---|---|---|
| Full Onboarding Activation | `*activate-users` | Pipeline completo: del tracking al outreach | 90-150 min |
| Quick Engagement Boost | `*quick-engage` | Boost rápido: tracking, aha moment, outreach | 30-45 min |

## Comandos Disponibles

| Comando | Agente | Descripción |
|---|---|---|
| `*track-behavior` | Tracker | Rastrear comportamiento de onboarding |
| `*detect-churn-signals` | Tracker | Detectar señales de abandono |
| `*build-checklist` | ChecklistBuilder | Crear checklist personalizado |
| `*optimize-checklist` | ChecklistBuilder | Optimizar checklist existente |
| `*find-aha` | AhaFinder | Identificar aha moment |
| `*optimize-path` | AhaFinder | Optimizar camino al aha moment |
| `*generate-tooltips` | TooltipGen | Generar tooltips para onboarding |
| `*create-tour` | TooltipGen | Crear guided tour interactivo |
| `*send-outreach` | Outreach | Enviar comunicación proactiva |
| `*create-sequence` | Outreach | Crear secuencia de emails |
| `*activate-users` | Outreach | Pipeline completo de activación |

## Inicio Rápido

```
# Activar el orquestador de outreach
/soa:agents:proactive-outreach

# Pipeline completo de activación de onboarding
*activate-users

# Boost rápido de enganche
*quick-engage

# Solo rastreo comportamental
*track-behavior

# Solo identificar aha moment
*find-aha
```

## Usuarios Objetivo

- Product Managers y Product Owners
- Growth Engineers y Growth Hackers
- Customer Success Managers
- UX Designers enfocados en onboarding
- Marketing de Producto y Lifecycle Marketing

## Requisitos

- Acceso a herramientas de analytics (Mixpanel, Amplitude, Segment, PostHog)
- Acceso a plataformas de onboarding (Appcues, Pendo, Userpilot)
- Acceso a herramientas de email (Customer.io, Iterable, Braze)
- Datos de tracking configurados en el producto
