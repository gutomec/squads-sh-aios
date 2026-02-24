---
task: executeProactiveOutreach()
responsavel: "Outreach"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: userSegment
    tipo: string
    origen: "trackUserBehavior() ou Usuário — segmento de usuários alvo"
    obrigatorio: true
  - campo: trigger
    tipo: string
    origen: "trackUserBehavior() — trigger comportamental (inactivity, milestone_missed, signup)"
    obrigatorio: true
  - campo: channel
    tipo: string
    origen: "Usuário — canal de comunicação (email, push, inapp)"
    obrigatorio: false

Saida:
  - campo: outreachPlan
    tipo: file
    destino: "outreach-plan.md, user-behavior-tracker"
    persistido: true
  - campo: messageTemplates
    tipo: array
    destino: "marketing team — templates para automação"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Segmento e trigger definidos"
    - "[ ] Canal de comunicação disponível"
    - "[ ] Dados de personalização acessíveis"
  post-conditions:
    - "[ ] Plano de outreach criado"
    - "[ ] Templates de mensagem gerados"
    - "[ ] Sequência de emails configurada"
    - "[ ] outreach-plan.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Mensagem personalizada com nome e próximo passo"
    - blocker: true
      criteria: "Timing definido baseado em comportamento"
    - blocker: false
      criteria: "Sequência de follow-up com 3 touchpoints"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0 (geração de conteúdo)"
  cacheable: true
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=20s)"
  fallback: "Se dados de personalização indisponíveis, usar template genérico do segmento"
  notification: "user-behavior-tracker"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "saas-onboarding-activator"
  created_at: "2026-02-24T00:00:00Z"
---

# Execute Proactive Outreach

## Flow

```
1. Receber segmento e trigger comportamental
2. Definir canal ideal (email, push, in-app)
3. Personalizar mensagem com contexto do usuário
4. Definir timing baseado em comportamento
5. Criar sequência de follow-up com 3 touchpoints
6. Incluir opção de unsubscribe e preferências
7. Gerar templates para automação
8. Gerar outreach-plan.md
9. Enviar para plataforma de marketing automation
```

## Elicitation

- "Qual o segmento de usuários alvo?"
- "Qual o trigger comportamental? (inactivity, milestone_missed, signup, trial_expiry)"
- "Qual o canal de comunicação preferido? (email, push, inapp)"
- "Qual o objetivo da comunicação? (activation, reengagement, trial_conversion)"
