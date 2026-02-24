---
task: fullDataQualityAudit()
responsavel: "QualityReporter"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: dataset
    tipo: string
    origen: "Usuário — dataset para auditoria"
    obrigatorio: true
  - campo: depth
    tipo: string
    origen: "Usuário — profundidade (quick, standard, deep)"
    obrigatorio: false

Saida:
  - campo: auditResult
    tipo: object
    destino: "Usuário — resultado completo da auditoria"
    persistido: true
  - campo: profilingReport
    tipo: file
    destino: "profiling-report.md"
    persistido: true
  - campo: anomalyReport
    tipo: file
    destino: "anomaly-report.md"
    persistido: true
  - campo: schemaReport
    tipo: file
    destino: "schema-validation-report.md"
    persistido: true
  - campo: qualityReport
    tipo: file
    destino: "quality-report.md"
    persistido: true
  - campo: remediationPlan
    tipo: file
    destino: "remediation-plan.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Dataset identificado e acessível"
    - "[ ] Profundidade definida"
  post-conditions:
    - "[ ] Profiling completo realizado"
    - "[ ] Anomalias detectadas e classificadas"
    - "[ ] Schema validado"
    - "[ ] Relatório de qualidade gerado com score"
    - "[ ] Remediações sugeridas com scripts"
  acceptance-criteria:
    - blocker: true
      criteria: "Pipeline completo do profiling à remediação executado"
    - blocker: true
      criteria: "Score de qualidade calculado com 6 dimensões"
    - blocker: false
      criteria: "Scripts de correção prontos para execução"

Performance:
  duration_expected: "30-60 minutos"
  cost_estimated: "Variável conforme tamanho do dataset"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: escalate
  retry:
    max_attempts: 2
    delay: "exponential(base=10s, max=60s)"
  fallback: "Se qualquer fase falhar, continuar com fases seguintes e reportar gaps no relatório final"
  notification: "data-quality-reporter"

Metadata:
  version: "1.0.0"
  dependencies:
    - profileDataset()
    - detectAnomalies()
    - validateSchema()
    - generateQualityReport()
    - suggestRemediation()
  author: "data-quality-guardian"
  created_at: "2026-02-24T00:00:00Z"
---

# Full Data Quality Audit

## Pipeline

```
Fase 1: Profiling         → @data-profiler         → profileDataset()
Fase 2: Anomalias         → @anomaly-detector      → detectAnomalies()
Fase 3: Schema            → @schema-validator       → validateSchema()
Fase 4: Relatório         → @data-quality-reporter  → generateQualityReport()
Fase 5: Remediação        → @remediation-suggester  → suggestRemediation()
```

## Elicitation

### Fase 1 — Dataset
- "Qual o dataset ou tabela para auditar?"
- "Qual o formato dos dados? (CSV, Parquet, JSON, SQL table)"
- "Qual a profundidade desejada? (quick, standard, deep)"

### Fase 2 — Contexto
- "Há um schema esperado documentado?"
- "Existem regras de negócio específicas para validar?"
- "Há um baseline anterior para comparação?"

### Fase 3 — Remediação
- "Deseja gerar scripts de correção automatizados?"
- "Qual a linguagem preferida para scripts? (Python, SQL, dbt)"
- "Há restrições de janela de execução?"

## Profundidade da Auditoria

| Profundidade | Profiling | Anomalias | Schema | Relatório | Remediação |
|---|---|---|---|---|---|
| quick | Básico (nulls, types) | Rule-based only | Tipos e nulls | Standard | Críticos apenas |
| standard | Completo | Statistical + rules | Full + constraints | Detailed | Todos priorizados |
| deep | Deep (distribuições, correlações) | Statistical + ML | Full + referential | Executive + detailed | Todos + prevenção |
