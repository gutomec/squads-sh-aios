---
task: fullOnboardingActivation()
responsavel: "Outreach"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: product
    tipo: string
    origen: "Usuário — nome/descrição do produto SaaS"
    obrigatorio: true
  - campo: segment
    tipo: string
    origen: "Usuário — segmento de usuários alvo"
    obrigatorio: false

Saida:
  - campo: activationResult
    tipo: object
    destino: "Usuário — resultado completo da ativação"
    persistido: true
  - campo: behaviorReport
    tipo: file
    destino: "behavior-report.md"
    persistido: true
  - campo: onboardingChecklist
    tipo: file
    destino: "onboarding-checklist.md"
    persistido: true
  - campo: ahaMomentReport
    tipo: file
    destino: "aha-moment-report.md"
    persistido: true
  - campo: tooltipSet
    tipo: file
    destino: "tooltip-set.md"
    persistido: true
  - campo: outreachPlan
    tipo: file
    destino: "outreach-plan.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Produto SaaS identificado"
    - "[ ] Dados de tracking disponíveis ou configuráveis"
    - "[ ] Canais de comunicação acessíveis"
  post-conditions:
    - "[ ] Comportamento rastreado e analisado"
    - "[ ] Checklist de onboarding criado"
    - "[ ] Aha moment identificado"
    - "[ ] Tooltips e guided tours gerados"
    - "[ ] Outreach proativo configurado"
    - "[ ] Todos os artefatos gerados"
  acceptance-criteria:
    - blocker: true
      criteria: "Pipeline completo executado do tracking ao outreach"
    - blocker: true
      criteria: "Aha moment identificado e caminho otimizado"
    - blocker: false
      criteria: "Métricas de baseline definidas para comparação"

Performance:
  duration_expected: "90-150 minutos"
  cost_estimated: "Variável conforme complexidade do produto"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: escalate
  retry:
    max_attempts: 2
    delay: "exponential(base=10s, max=60s)"
  fallback: "Se qualquer fase falhar, entregar artefatos parciais e reportar status"
  notification: "user-behavior-tracker"

Metadata:
  version: "1.0.0"
  dependencies:
    - trackUserBehavior()
    - buildOnboardingChecklist()
    - identifyAhaMoment()
    - generateTooltips()
    - executeProactiveOutreach()
  author: "saas-onboarding-activator"
  created_at: "2026-02-24T00:00:00Z"
---

# Full Onboarding Activation

## Pipeline

```
Fase 1: Rastreamento      → @user-behavior-tracker   → trackUserBehavior()
Fase 2: Checklist          → @checklist-builder        → buildOnboardingChecklist()
Fase 3: Aha Moment         → @aha-moment-identifier    → identifyAhaMoment()
Fase 4: Tooltips           → @tooltip-generator        → generateTooltips()
Fase 5: Outreach           → @proactive-outreach       → executeProactiveOutreach()
```

## Elicitation

### Fase 1 — Produto
- "Qual o produto SaaS alvo?"
- "Qual o segmento de usuários? (new_signup, trial, free_to_paid)"
- "Quais as principais features do produto?"

### Fase 2 — Contexto
- "Qual a taxa de ativação atual?"
- "Quais canais de comunicação estão disponíveis? (email, push, in-app)"
- "Quais ferramentas de analytics estão em uso?"

### Fase 3 — Objetivos
- "Qual a meta de ativação? (% de usuários ativados em D7)"
- "Qual o time-to-value atual?"
- "Existem dados de churn da primeira semana?"

## Métricas de Sucesso

| Métrica | Baseline | Meta |
|---|---|---|
| Taxa de ativação D7 | Atual | +20% |
| Time-to-value | Atual | -30% |
| Churn primeira semana | Atual | -25% |
| Completion rate do checklist | N/A | > 60% |
| Email open rate | N/A | > 40% |
