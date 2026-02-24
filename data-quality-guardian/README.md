# data-quality-guardian

Squad especialista em qualidade de dados para pipelines de dados.

## Visão Geral

O **data-quality-guardian** é um squad completo que cobre todo o pipeline de qualidade de dados:

1. **Profiling de Dados** — Análise de distribuições, tipos de dados, cardinalidade, taxas de nulos, unicidade e estatísticas descritivas
2. **Detecção de Anomalias** — Identificação de outliers, data drift, padrões incomuns e desvios de baseline
3. **Validação de Schema** — Verificação de tipos, constraints, integridade referencial e detecção de breaking changes
4. **Relatórios de Qualidade** — Scores compostos por 6 dimensões, tendências, comparações com SLAs e sumários executivos
5. **Sugestão de Remediação** — Scripts automatizados de limpeza, correções de pipeline e recomendações de governança

**Pain Point:** 89% das equipes de dados relatam problemas de qualidade; 61% listam qualidade de dados como desafio principal em suas organizações.

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 📋 Profiler | `data-profiler` | Profiler de dados e estatísticas |
| 🔍 AnomalyDetector | `anomaly-detector` | Detector de anomalias e outliers |
| 🛡️ SchemaValidator | `schema-validator` | Validador de schema e integridade |
| 📊 QualityReporter | `data-quality-reporter` | Repórter de qualidade e métricas |
| ⚡ RemediationSuggester | `remediation-suggester` | Sugestor de remediação e prevenção |

## Workflows

| Workflow | Comando | Descrição | Duração |
|---|---|---|---|
| Full Data Quality Audit | `*full-audit` | Pipeline completo: do profiling à remediação | 30-60 min |
| Quick Data Check | `*quick-check` | Verificação rápida: profiling, schema e relatório | 10-20 min |

## Comandos Disponíveis

| Comando | Agente | Descrição |
|---|---|---|
| `*profile-data` | Profiler | Profilar dataset completo |
| `*compare-baseline` | Profiler | Comparar perfil atual com baseline |
| `*detect-anomalies` | AnomalyDetector | Detectar anomalias em dataset |
| `*check-drift` | AnomalyDetector | Verificar data drift entre períodos |
| `*validate-schema` | SchemaValidator | Validar schema do dataset |
| `*check-integrity` | SchemaValidator | Verificar integridade referencial |
| `*quality-report` | QualityReporter | Gerar relatório de qualidade |
| `*quality-score` | QualityReporter | Calcular score de qualidade |
| `*full-audit` | QualityReporter | Auditoria completa de qualidade |
| `*suggest-fix` | RemediationSuggester | Sugerir remediações |
| `*generate-script` | RemediationSuggester | Gerar script de limpeza |

## Quick Start

```
# Ativar o repórter de qualidade (orquestrador principal)
/dqg:agents:data-quality-reporter

# Auditoria completa de qualidade
*full-audit

# Verificação rápida
*quick-check

# Apenas profiling
*profile-data

# Apenas detecção de anomalias
*detect-anomalies
```

## Público Alvo

- Data Engineers
- Data Analysts
- Data Governance Teams
- Analytics Engineers
- CTOs e líderes de dados

## Requisitos

- Acesso ao dataset para análise (CSV, Parquet, JSON, SQL)
- Schema esperado documentado (opcional, pode ser inferido)
- Baseline anterior para comparação (opcional)
- Definição de SLAs de qualidade (opcional)
