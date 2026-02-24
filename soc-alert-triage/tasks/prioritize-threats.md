---
task: prioritizeThreats()
responsavel: "Prioritizer"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: filteredAlerts
    tipo: array
    origen: "filterFalsePositives() — alertas reais filtrados"
    obrigatorio: true
  - campo: assetInventory
    tipo: object
    origen: "Organização — inventário de ativos e criticidade"
    obrigatorio: false

Saida:
  - campo: prioritizedAlerts
    tipo: array
    destino: "context-enricher, analyst-brief-generator"
    persistido: true
  - campo: riskScoreReport
    tipo: file
    destino: "risk-score-report.md, analyst-brief-generator"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Alertas reais filtrados disponíveis"
  post-conditions:
    - "[ ] Ameaças priorizadas por risk score"
    - "[ ] Blast radius mapeado"
    - "[ ] Ordem de resposta recomendada"
    - "[ ] risk-score-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Risk score calculado para cada ameaça"
    - blocker: true
      criteria: "Ameaças com exploitability ativa no topo"
    - blocker: false
      criteria: "Blast radius estimado para ameaças critical"

Performance:
  duration_expected: "5-10 minutos"
  cost_estimated: "~0 (processamento local)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: escalate
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se inventário de ativos indisponível, assumir criticidade média para todos os ativos"
  notification: "context-enricher"

Metadata:
  version: "1.0.0"
  dependencies:
    - filterFalsePositives()
  author: "soc-alert-triage"
  created_at: "2026-02-24T00:00:00Z"
---

# Prioritize Threats

## Flow

```
1. Receber alertas reais do @false-positive-filter
2. Calcular exploitability score para cada ameaça
3. Estimar blast radius (sistemas e usuários potencialmente afetados)
4. Avaliar criticidade do ativo afetado
5. Calcular impacto no negócio
6. Gerar risk score composto (0-10)
7. Ordenar ameaças por prioridade
8. Recomendar ordem de resposta para o SOC
9. Gerar risk-score-report.md
10. Enviar para @context-enricher e @analyst-brief-generator
```

## Elicitation

- "Há inventário de ativos com criticidade definida?"
- "Existem ativos crown jewels a priorizar?"
- "Há alguma ameaça com exploitability ativa conhecida?"
