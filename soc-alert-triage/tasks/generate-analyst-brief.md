---
task: generateAnalystBrief()
responsavel: "BriefGen"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: enrichedAlerts
    tipo: array
    origen: "enrichContext() — alertas enriquecidos com contexto"
    obrigatorio: true
  - campo: format
    tipo: string
    origen: "Usuário — formato do brief (standard, executive, detailed)"
    obrigatorio: false

Saida:
  - campo: analystBrief
    tipo: file
    destino: "analyst-brief.md, SOC analyst"
    persistido: true
  - campo: actionItems
    tipo: array
    destino: "SOC analyst — ações de resposta priorizadas"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Alertas enriquecidos disponíveis"
  post-conditions:
    - "[ ] Brief gerado com timeline, ameaças e recomendações"
    - "[ ] Playbook recomendado"
    - "[ ] Ações de resposta priorizadas"
    - "[ ] analyst-brief.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Brief com timeline completa do incidente"
    - blocker: true
      criteria: "Playbook específico recomendado por tipo de ameaça"
    - blocker: false
      criteria: "Executive summary para gestão"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "~0 (processamento local)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se dados incompletos, gerar brief parcial com indicação de informações faltantes"
  notification: "SOC analyst"

Metadata:
  version: "1.0.0"
  dependencies:
    - enrichContext()
  author: "soc-alert-triage"
  created_at: "2026-02-24T00:00:00Z"
---

# Generate Analyst Brief

## Flow

```
1. Receber alertas enriquecidos do @context-enricher
2. Construir timeline cronológica do incidente
3. Sintetizar avaliação de ameaça com risk score
4. Selecionar playbook recomendado baseado no tipo de ameaça
5. Listar IOCs relevantes com reputation scores
6. Priorizar ações de resposta (P1, P2, P3)
7. Formatar brief no formato solicitado (standard, executive, detailed)
8. Incluir links para evidências e fontes de dados
9. Gerar analyst-brief.md final
```

## Elicitation

- "Qual o formato de brief desejado? (standard, executive, detailed)"
- "Quem é o público alvo do brief? (L1, L2, L3, gestão)"
- "Há playbooks específicos da organização a referenciar?"
