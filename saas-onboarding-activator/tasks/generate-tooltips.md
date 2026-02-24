---
task: generateTooltips()
responsavel: "TooltipGen"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: flow
    tipo: string
    origen: "checklist-builder ou identifyAhaMoment() — fluxo de onboarding"
    obrigatorio: true
  - campo: steps
    tipo: array
    origen: "checklist-builder — etapas do checklist"
    obrigatorio: false
  - campo: tone
    tipo: string
    origen: "Usuário — tom de voz (friendly, professional, playful)"
    obrigatorio: false

Saida:
  - campo: tooltipSet
    tipo: file
    destino: "tooltip-set.md, proactive-outreach"
    persistido: true
  - campo: guidedTours
    tipo: array
    destino: "frontend team — tours para implementação"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Fluxo de onboarding definido"
    - "[ ] Etapas mapeadas"
    - "[ ] Tom de voz definido"
  post-conditions:
    - "[ ] Tooltips gerados para cada etapa"
    - "[ ] Guided tours criados"
    - "[ ] Variações A/B incluídas"
    - "[ ] tooltip-set.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Tooltip para cada etapa do onboarding"
    - blocker: true
      criteria: "Guided tour com máximo 5 steps"
    - blocker: false
      criteria: "Variações A/B para testing"

Performance:
  duration_expected: "10-15 minutos"
  cost_estimated: "~0 (geração de conteúdo)"
  cacheable: true
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=20s)"
  fallback: "Se etapas não definidas, gerar tooltips genéricos para fluxo padrão"
  notification: "proactive-outreach"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "saas-onboarding-activator"
  created_at: "2026-02-24T00:00:00Z"
---

# Generate Tooltips

## Flow

```
1. Receber fluxo e etapas do onboarding
2. Definir contexto de cada tooltip (quando, onde, por quê)
3. Escrever copy contextual, amigável e conciso
4. Criar guided tour principal com 3-5 steps
5. Definir hotspots e beacons para features não-descobertas
6. Adicionar variações A/B para testing
7. Formatar tooltips para implementação (Appcues, Pendo, Userpilot)
8. Gerar tooltip-set.md
9. Enviar para frontend team e proactive-outreach
```

## Elicitation

- "Qual o fluxo de onboarding alvo? (signup, first-use, activation)"
- "Quais são as etapas do checklist?"
- "Qual o tom de voz desejado? (friendly, professional, playful)"
- "Qual ferramenta de in-app messaging será usada? (Appcues, Pendo, Userpilot)"
