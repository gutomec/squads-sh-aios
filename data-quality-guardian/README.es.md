# data-quality-guardian

Squad especialista en calidad de datos para pipelines de datos.

## Descripcion General

El **data-quality-guardian** es un squad completo que cubre todo el pipeline de calidad de datos:

1. **Profiling de Datos** — Analisis de distribuciones, tipos de datos, cardinalidad, tasas de nulos, unicidad y estadisticas descriptivas
2. **Deteccion de Anomalias** — Identificacion de outliers, data drift, patrones inusuales y desviaciones de baseline
3. **Validacion de Schema** — Verificacion de tipos, constraints, integridad referencial y deteccion de breaking changes
4. **Reportes de Calidad** — Scores compuestos por 6 dimensiones, tendencias, comparaciones con SLAs y resumenes ejecutivos
5. **Sugerencias de Remediacion** — Scripts automatizados de limpieza, correcciones de pipeline y recomendaciones de gobernanza

**Pain Point:** El 89% de los equipos de datos reportan problemas de calidad; el 61% lista la calidad de datos como desafio principal en sus organizaciones.

## Agentes

| Agente | ID | Rol |
|---|---|---|
| 📋 Profiler | `data-profiler` | Profiler de datos y estadisticas |
| 🔍 AnomalyDetector | `anomaly-detector` | Detector de anomalias y outliers |
| 🛡️ SchemaValidator | `schema-validator` | Validador de schema e integridad |
| 📊 QualityReporter | `data-quality-reporter` | Reportador de calidad y metricas |
| ⚡ RemediationSuggester | `remediation-suggester` | Sugeridor de remediacion y prevencion |

## Flujos de Trabajo

| Workflow | Comando | Descripcion | Duracion |
|---|---|---|---|
| Full Data Quality Audit | `*full-audit` | Pipeline completo: del profiling a la remediacion | 30-60 min |
| Quick Data Check | `*quick-check` | Verificacion rapida: profiling, schema y reporte | 10-20 min |

## Comandos Disponibles

| Comando | Agente | Descripcion |
|---|---|---|
| `*profile-data` | Profiler | Profilar dataset completo |
| `*compare-baseline` | Profiler | Comparar perfil actual con baseline |
| `*detect-anomalies` | AnomalyDetector | Detectar anomalias en dataset |
| `*check-drift` | AnomalyDetector | Verificar data drift entre periodos |
| `*validate-schema` | SchemaValidator | Validar schema del dataset |
| `*check-integrity` | SchemaValidator | Verificar integridad referencial |
| `*quality-report` | QualityReporter | Generar reporte de calidad |
| `*quality-score` | QualityReporter | Calcular score de calidad |
| `*full-audit` | QualityReporter | Auditoria completa de calidad |
| `*suggest-fix` | RemediationSuggester | Sugerir remediaciones |
| `*generate-script` | RemediationSuggester | Generar script de limpieza |

## Inicio Rapido

```
# Activar el reportador de calidad (orquestador principal)
/dqg:agents:data-quality-reporter

# Auditoria completa de calidad de datos
*full-audit

# Verificacion rapida
*quick-check

# Solo profiling
*profile-data

# Solo deteccion de anomalias
*detect-anomalies
```

## Usuarios Objetivo

- Data Engineers
- Data Analysts
- Equipos de Data Governance
- Analytics Engineers
- CTOs y lideres de datos

## Requisitos

- Acceso al dataset para analisis (CSV, Parquet, JSON, SQL)
- Schema esperado documentado (opcional, puede ser inferido)
- Baseline anterior para comparacion (opcional)
- Definicion de SLAs de calidad (opcional)
