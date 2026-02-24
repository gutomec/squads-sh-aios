# resume-screener-squad

Squad especialista en triaje de currículos para reclutamiento.

## Descripción General

El **resume-screener-squad** es un squad completo que cubre todo el pipeline de triaje de currículos:

1. **Parsing de Currículos** — Extracción automatizada de datos estructurados de CVs en cualquier formato (PDF, DOCX, texto)
2. **Matching de Skills** — Comparación de skills con requisitos del puesto, cálculo de fit score ponderado e identificación de skills transferibles
3. **Auditoría de Sesgos** — Detección de sesgos de género, edad, etnia, pedigrí educativo y nombre, garantizando equidad
4. **Ranking de Candidatos** — Ranking transparente con justificaciones, identificación de hidden gems y shortlist configurable
5. **Resúmenes Ejecutivos** — Briefs accionables para hiring managers con fortalezas, preocupaciones, matriz comparativa y preguntas de entrevista

**Pain Point:** Costo promedio de US$ 4.700 por contratación con ciclo de 44 días; el triaje manual es propenso a sesgos inconscientes y pérdida de candidatos calificados.

## Agentes

| Agente | ID | Rol |
|---|---|---|
| 📋 Parser | `resume-parser` | Parser de currículos y extracción de datos |
| 🔍 SkillsMatcher | `skills-matcher` | Matching de skills y cálculo de fit score |
| 🛡️ BiasAuditor | `bias-auditor` | Auditoría de sesgos y fairness |
| ⚡ Ranker | `shortlist-ranker` | Ranking y generación de shortlist |
| 📊 SummaryWriter | `candidate-summary-agent` | Resúmenes ejecutivos y briefs |

## Flujos de Trabajo

| Workflow | Comando | Descripción | Duración |
|---|---|---|---|
| Full Resume Screening | `*triage-full` | Pipeline completo: del parsing al resumen ejecutivo | 30-60 min |
| Quick Skills Match | `*quick-match` | Match rápido: parsing, matching y resumen simplificado | 10-20 min |

## Comandos Disponibles

| Comando | Agente | Descripción |
|---|---|---|
| `*parse-resumes` | Parser | Extraer datos estructurados de currículos |
| `*parse-single` | Parser | Extraer datos de un currículo específico |
| `*match-skills` | SkillsMatcher | Calcular fit score de candidatos |
| `*analyze-gaps` | SkillsMatcher | Analizar gaps de skills |
| `*audit-bias` | BiasAuditor | Auditar proceso de triaje por sesgos |
| `*check-fairness` | BiasAuditor | Verificar fairness del ranking |
| `*rank-candidates` | Ranker | Rankear candidatos y generar shortlist |
| `*triage-full` | Ranker | Pipeline completo de triaje |
| `*candidate-summary` | SummaryWriter | Generar resumen ejecutivo de candidatos |
| `*comparison-matrix` | SummaryWriter | Generar matriz comparativa |

## Inicio Rápido

```
# Activar el ranker (orquestador principal)
/rss:agents:shortlist-ranker

# Pipeline completo de triaje
*triage-full

# Match rápido de skills
*quick-match

# Solo parsing de CVs
*parse-resumes

# Solo auditoría de sesgo
*audit-bias
```

## Usuarios Objetivo

- Hiring Managers y Reclutadores
- Equipos de RRHH y Talent Acquisition
- Especialistas en DEI (Diversidad, Equidad e Inclusión)
- CTOs y líderes técnicos contratando para sus equipos

## Requisitos

- Currículos en formato legible (PDF, DOCX, texto)
- Descripción del puesto con requisitos (must-have y nice-to-have)
- Definición del tamaño de shortlist deseado
