# automated-code-review-squad

Squad especialista en code review automatizado.

## Descripcion General

El **automated-code-review-squad** es un squad completo que cubre todo el pipeline de code review automatizado:

1. **Revision de Seguridad** — OWASP Top 10, injection flaws, XSS, exposicion de secrets, dependencias con CVEs
2. **Analisis Logico** — Edge cases, race conditions, null handling, off-by-one errors, logica de negocio
3. **Verificacion Arquitectural** — SOLID, DRY, separacion de concerns, layer violations, acoplamiento/cohesion
4. **Enforcement de Estilo** — Naming conventions, formateo, documentacion, imports, reglas del proyecto
5. **Review Summary** — Sintesis priorizada de findings con verdict (APPROVE/REQUEST_CHANGES/BLOCK)

**Pain Point:** Las revisiones de codigo consumen enormes bloques de tiempo de desarrolladores senior; cuello de botella de merge en PRs con largas colas de review.

## Agentes

| Agente | ID | Rol |
|---|---|---|
| 🔒 SecurityReviewer | `security-reviewer` | Deteccion de vulnerabilidades y revision de seguridad |
| 🧠 LogicReviewer | `logic-reviewer` | Revision de logica, correccion y edge cases |
| 🏗️ ArchChecker | `architecture-checker` | Verificacion de patrones arquitecturales y diseno |
| ✅ StyleEnforcer | `style-enforcer` | Enforcement de coding standards y estilo |
| 📝 SummaryWriter | `review-summary-writer` | Sintesis de findings y recomendacion de aprobacion |

## Flujos de Trabajo

| Workflow | Comando | Descripcion | Duracion |
|---|---|---|---|
| Full Code Review | `*full-review` | Pipeline completo: seguridad, logica, arquitectura, estilo y summary | 30-60 min |
| Quick Security Check | `*quick-security` | Verificacion rapida enfocada en seguridad | 10-20 min |

## Comandos Disponibles

| Comando | Agente | Descripcion |
|---|---|---|
| `*review-security` | SecurityReviewer | Revisar codigo por vulnerabilidades de seguridad |
| `*check-secrets` | SecurityReviewer | Verificar exposicion de secrets en el codigo |
| `*review-logic` | LogicReviewer | Revisar logica y correccion del codigo |
| `*find-edge-cases` | LogicReviewer | Identificar edge cases no tratados |
| `*check-architecture` | ArchChecker | Verificar patrones arquitecturales |
| `*analyze-coupling` | ArchChecker | Analizar acoplamiento y cohesion |
| `*check-style` | StyleEnforcer | Verificar adherencia a coding standards |
| `*fix-style` | StyleEnforcer | Sugerir correcciones de estilo |
| `*write-summary` | SummaryWriter | Generar sumario priorizado del code review |
| `*full-review` | SummaryWriter | Pipeline completo de code review automatizado |

## Inicio Rapido

```
# Activar el sintetizador (orquestador principal)
/acr:agents:review-summary-writer

# Pipeline completo de code review
*full-review

# Verificacion rapida de seguridad
*quick-security

# Solo revision de seguridad
*review-security

# Solo revision de logica
*review-logic
```

## Usuarios Objetivo

- Desarrolladores senior y leads
- Ingenieros de seguridad (AppSec)
- Arquitectos de software
- Tech leads y engineering managers
- Equipos con alto volumen de PRs

## Requisitos

- Codigo fuente accesible (repositorio local o PR URL)
- Configuracion de linter del proyecto (opcional, mejora precision)
- Acceso al GitHub CLI para integracion con PRs (opcional)
