---
task: detectAnomalies()
responsavel: "AnomalyDetector"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: dataset
    tipo: string
    origen: "Usuário ou fullDataQualityAudit() — dataset para análise"
    obrigatorio: true
  - campo: profilingReport
    tipo: file
    origen: "profileDataset() — relatório de profiling"
    obrigatorio: false
  - campo: sensitivity
    tipo: string
    origen: "Usuário — sensibilidade (low, medium, high)"
    obrigatorio: false

Saida:
  - campo: anomalyReport
    tipo: file
    destino: "anomaly-report.md, data-quality-reporter, remediation-suggester"
    persistido: true
  - campo: anomalyList
    tipo: array
    destino: "data-quality-reporter, remediation-suggester"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Dataset disponível"
    - "[ ] Profiling concluído (ou baseline disponível)"
  post-conditions:
    - "[ ] Anomalias detectadas e classificadas"
    - "[ ] Outliers identificados"
    - "[ ] Data drift avaliado"
    - "[ ] anomaly-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Anomalias classificadas por severidade (critical, warning, info)"
    - blocker: true
      criteria: "Cada anomalia documentada com evidência e localização"
    - blocker: false
      criteria: "Taxa de falso positivo estimada"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0 (análise local de dados)"
  cacheable: false
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se profiling não disponível, executar detecção com métodos rule-based apenas"
  notification: "data-quality-reporter"

Metadata:
  version: "1.0.0"
  dependencies:
    - profileDataset()
  author: "data-quality-guardian"
  created_at: "2026-02-24T00:00:00Z"
---

# Detect Anomalies

## Flow

```
1. Receber dataset e relatório de profiling
2. Aplicar detecção estatística (Z-score, IQR, MAD)
3. Verificar regras de negócio e domínio
4. Comparar distribuições com baseline
5. Identificar data drift temporal
6. Classificar anomalias por severidade (critical, warning, info)
7. Documentar evidências para cada anomalia
8. Gerar anomaly-report.md
9. Enviar para @data-quality-reporter
```

## Elicitation

- "Qual o dataset para análise de anomalias?"
- "Qual a sensibilidade desejada? (low, medium, high)"
- "Há regras de negócio específicas para validar?"
- "Existe um baseline de referência para comparação?"
