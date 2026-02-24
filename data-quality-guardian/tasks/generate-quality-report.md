---
task: generateQualityReport()
responsavel: "QualityReporter"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: profilingData
    tipo: file
    origen: "profileDataset() — dados de profiling"
    obrigatorio: true
  - campo: anomalyData
    tipo: file
    origen: "detectAnomalies() — dados de anomalias"
    obrigatorio: false
  - campo: schemaData
    tipo: file
    origen: "validateSchema() — dados de validação de schema"
    obrigatorio: false
  - campo: format
    tipo: string
    origen: "Usuário — formato do relatório (standard, executive, detailed)"
    obrigatorio: false

Saida:
  - campo: qualityReport
    tipo: file
    destino: "quality-report.md, remediation-suggester, stakeholders"
    persistido: true
  - campo: qualityScore
    tipo: object
    destino: "remediation-suggester, stakeholders"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Dados de profiling disponíveis"
    - "[ ] Anomalias analisadas (opcional)"
    - "[ ] Schema validado (opcional)"
  post-conditions:
    - "[ ] Relatório de qualidade gerado"
    - "[ ] Score composto calculado"
    - "[ ] Tendências identificadas"
    - "[ ] quality-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Score de qualidade calculado com 6 dimensões (completude, acurácia, consistência, timeliness, unicidade, validade)"
    - blocker: true
      criteria: "Violações de SLA identificadas e alertadas"
    - blocker: false
      criteria: "Tendência temporal incluída quando dados históricos disponíveis"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "~0 (geração de relatório)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se dados parciais, gerar relatório com dimensões disponíveis e marcar gaps"
  notification: "remediation-suggester"

Metadata:
  version: "1.0.0"
  dependencies:
    - profileDataset()
  author: "data-quality-guardian"
  created_at: "2026-02-24T00:00:00Z"
---

# Generate Quality Report

## Flow

```
1. Receber dados de profiling, anomalias e schema
2. Calcular score por dimensão de qualidade (6 dimensões)
3. Calcular score composto ponderado
4. Comparar com SLAs definidos
5. Identificar tendências temporais
6. Priorizar issues por impacto
7. Gerar sumário executivo
8. Formatar relatório final
9. Enviar para @remediation-suggester
```

## Elicitation

- "Qual o formato desejado do relatório? (standard, executive, detailed)"
- "Há SLAs de qualidade definidos para este dataset?"
- "Deseja incluir comparação com períodos anteriores?"
- "Quem são os stakeholders destinatários do relatório?"
