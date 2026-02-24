# soc-alert-triage

Squad especialista en triaje de alertas SOC para ciberseguridad.

## Descripcion General

El **soc-alert-triage** es un squad completo que cubre todo el pipeline de triaje de alertas de seguridad:

1. **Clasificacion de Alertas** — Categorizacion automatizada por tipo, severidad y mapeo MITRE ATT&CK de multiples fuentes (SIEM, IDS, EDR, cloud)
2. **Filtrado de Falsos Positivos** — Identificacion y filtrado de FPs usando patrones historicos, baselines comportamentales y whitelists contextuales
3. **Priorizacion de Amenazas** — Risk scoring basado en exploitability, blast radius, criticidad de activos e impacto en el negocio
4. **Enriquecimiento con Threat Intel** — IOCs, mapeo MITRE ATT&CK completo, reputation scores y correlacion historica
5. **Generacion de Briefs** — Documentos accionables con timeline, playbook recomendado, IOCs y acciones de respuesta priorizadas

**Pain Point:** Los analistas SOC enfrentan +4.000 alertas/dia, con 80%+ siendo falsos positivos — generando alert fatigue, burnout y riesgo de perder amenazas reales.

## Agentes

| Agente | ID | Rol |
|---|---|---|
| 🏷️ Classifier | `alert-classifier` | Clasificador de alertas por tipo, severidad y MITRE ATT&CK |
| 🛡️ FPFilter | `false-positive-filter` | Filtro de falsos positivos con baselines y heuristicas |
| ⚡ Prioritizer | `threat-prioritizer` | Priorizador de amenazas por risk score compuesto |
| 🔍 Enricher | `context-enricher` | Enriquecedor de contexto con IOCs y threat intel |
| 📊 BriefGen | `analyst-brief-generator` | Generador de briefs accionables para analistas SOC |

## Flujos de Trabajo

| Workflow | Comando | Descripcion | Duracion |
|---|---|---|---|
| Full Alert Triage | `*triage-full` | Pipeline completo: de la clasificacion al brief | 30-60 min |
| Rapid Classification | `*rapid-classify` | Clasificacion rapida: clasificar, filtrar y brief | 10-20 min |

## Comandos Disponibles

| Comando | Agente | Descripcion |
|---|---|---|
| `*classify-alerts` | Classifier | Clasificar batch de alertas de seguridad |
| `*classify-single` | Classifier | Clasificar una alerta especifica |
| `*filter-fps` | FPFilter | Filtrar falsos positivos de un batch |
| `*check-fp` | FPFilter | Verificar si alerta es falso positivo |
| `*prioritize` | Prioritizer | Priorizar amenazas por risk score |
| `*risk-score` | Prioritizer | Calcular risk score de amenaza especifica |
| `*triage-full` | Prioritizer | Pipeline completo de triaje |
| `*enrich` | Enricher | Enriquecer alertas con contexto y threat intel |
| `*ioc-lookup` | Enricher | Buscar IOC en feeds de threat intel |
| `*generate-brief` | BriefGen | Generar brief para analista SOC |
| `*incident-summary` | BriefGen | Generar resumen ejecutivo de incidente |

## Inicio Rapido

```
# Activar el priorizador (orquestador principal)
/sat:agents:threat-prioritizer

# Pipeline completo de triaje de alertas
*triage-full

# Clasificacion rapida
*rapid-classify

# Solo clasificacion de alertas
*classify-alerts

# Solo generacion de brief
*generate-brief
```

## Usuarios Objetivo

- Analistas SOC (L1, L2, L3)
- Ingenieros de Seguridad
- Threat Hunters
- CISOs y lideres de seguridad
- Equipos de Incident Response

## Requisitos

- Acceso a SIEM (Splunk, QRadar, Sentinel, Elastic SIEM)
- Acceso a feeds de threat intel (VirusTotal, AbuseIPDB, MISP)
- Acceso a herramientas de EDR (CrowdStrike, SentinelOne, Defender)
- Framework MITRE ATT&CK como referencia de taxonomia
