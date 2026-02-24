---
task: classifyAlerts()
responsavel: "Classifier"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: alerts
    tipo: array
    origen: "SIEM/IDS/EDR ou fullAlertTriage() — alertas crus de segurança"
    obrigatorio: true
  - campo: source
    tipo: string
    origen: "Pipeline — fonte dos alertas (splunk, qradar, sentinel)"
    obrigatorio: false
  - campo: timeWindow
    tipo: string
    origen: "Usuário — janela de tempo (1h, 4h, 24h)"
    obrigatorio: false

Saida:
  - campo: classifiedAlerts
    tipo: array
    destino: "false-positive-filter, threat-prioritizer"
    persistido: true
  - campo: classificationReport
    tipo: file
    destino: "classification-report.md, analyst-brief-generator"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Alertas crus disponíveis"
    - "[ ] Fonte de alertas identificada"
  post-conditions:
    - "[ ] Alertas classificados por tipo e severidade"
    - "[ ] Mapeamento MITRE ATT&CK aplicado"
    - "[ ] Relatório de classificação gerado"
    - "[ ] classification-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "100% dos alertas classificados com tipo e severidade"
    - blocker: true
      criteria: "Mapeamento MITRE ATT&CK para alertas de severidade high/critical"
    - blocker: false
      criteria: "Métricas de distribuição por categoria"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "~0 (processamento local)"
  cacheable: false
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se formato de alerta desconhecido, classificar como 'unclassified' com severidade medium e escalar"
  notification: "false-positive-filter"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "soc-alert-triage"
  created_at: "2026-02-24T00:00:00Z"
---

# Classify Alerts

## Flow

```
1. Receber batch de alertas crus
2. Normalizar formato de diferentes fontes (SIEM, IDS, EDR, cloud)
3. Classificar por tipo (malware, phishing, brute force, lateral movement, etc.)
4. Atribuir severidade (critical, high, medium, low, info)
5. Mapear MITRE ATT&CK tactic e technique para alertas high/critical
6. Gerar métricas de distribuição por categoria
7. Gerar classification-report.md
8. Enviar alertas classificados para @false-positive-filter
```

## Elicitation

- "De qual fonte vêm os alertas? (Splunk, QRadar, Sentinel, Elastic SIEM)"
- "Qual a janela de tempo para análise? (1h, 4h, 24h)"
- "Há algum tipo específico de alerta a priorizar?"
