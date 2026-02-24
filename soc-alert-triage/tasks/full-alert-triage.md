---
task: fullAlertTriage()
responsavel: "Prioritizer"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: alerts
    tipo: array
    origen: "Usuário ou SIEM — alertas de segurança para triagem"
    obrigatorio: true
  - campo: timeWindow
    tipo: string
    origen: "Usuário — janela de tempo (1h, 4h, 24h)"
    obrigatorio: false

Saida:
  - campo: triageResult
    tipo: object
    destino: "Usuário — resultado completo da triagem"
    persistido: true
  - campo: classificationReport
    tipo: file
    destino: "classification-report.md"
    persistido: true
  - campo: fpReport
    tipo: file
    destino: "fp-analysis-report.md"
    persistido: true
  - campo: riskScoreReport
    tipo: file
    destino: "risk-score-report.md"
    persistido: true
  - campo: iocReport
    tipo: file
    destino: "ioc-report.md"
    persistido: true
  - campo: analystBrief
    tipo: file
    destino: "analyst-brief.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Alertas disponíveis"
    - "[ ] Janela de tempo definida"
  post-conditions:
    - "[ ] Alertas classificados e filtrados"
    - "[ ] Ameaças priorizadas com risk score"
    - "[ ] Contexto enriquecido com threat intel"
    - "[ ] Brief para analista gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Pipeline completo executado da classificação ao brief"
    - blocker: true
      criteria: "Zero alertas ignorados sem classificação"
    - blocker: false
      criteria: "Métricas de eficiência (FP ratio, tempo médio)"

Performance:
  duration_expected: "30-60 minutos"
  cost_estimated: "Variável conforme volume de alertas"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: escalate
  retry:
    max_attempts: 2
    delay: "exponential(base=10s, max=60s)"
  fallback: "Se qualquer fase falhar, gerar brief parcial e escalar para analista sênior"
  notification: "analyst-brief-generator"

Metadata:
  version: "1.0.0"
  dependencies:
    - classifyAlerts()
    - filterFalsePositives()
    - prioritizeThreats()
    - enrichContext()
    - generateAnalystBrief()
  author: "soc-alert-triage"
  created_at: "2026-02-24T00:00:00Z"
---

# Full Alert Triage

## Pipeline

```
Fase 1: Classificação       → @alert-classifier         → classifyAlerts()
Fase 2: Filtragem de FPs    → @false-positive-filter     → filterFalsePositives()
Fase 3: Priorização          → @threat-prioritizer        → prioritizeThreats()
Fase 4: Enriquecimento       → @context-enricher          → enrichContext()
Fase 5: Geração de Brief     → @analyst-brief-generator   → generateAnalystBrief()
```

## Elicitation

### Fase 1 — Fonte
- "De qual fonte vêm os alertas? (Splunk, QRadar, Sentinel, Elastic SIEM)"
- "Qual a janela de tempo para análise? (1h, 4h, 24h)"

### Fase 2 — Contexto
- "Há whitelists ou baselines específicos da organização?"
- "Existe janela de manutenção ativa?"

### Fase 3 — Priorização
- "Há ativos específicos de alta criticidade a priorizar?"
- "Existem ameaças com exploitability ativa conhecida?"

### Fase 4 — Enriquecimento
- "Qual o nível de detalhe desejado no enriquecimento? (basic, standard, deep)"
- "Quais feeds de threat intel estão disponíveis?"

### Fase 5 — Brief
- "Qual o formato do brief? (standard, executive, detailed)"
- "Quem é o público alvo do brief?"

## Métricas de Eficiência

| Métrica | Target | Descrição |
|---|---|---|
| FP Ratio | > 50% filtrado | Percentual de alertas filtrados como FP |
| Classification Rate | 100% | Todos os alertas classificados |
| Mean Risk Score Accuracy | > 85% | Precisão do risk score vs avaliação manual |
| Brief Generation Time | < 15 min | Tempo para gerar brief completo |
| End-to-End Triage Time | < 60 min | Tempo total do pipeline |
