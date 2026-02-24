---
task: buildOnboardingChecklist()
responsavel: "ChecklistBuilder"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: segment
    tipo: string
    origen: "trackUserBehavior() ou Usuário — segmento de usuários"
    obrigatorio: true
  - campo: plan
    tipo: string
    origen: "Projeto — plano de assinatura (free, pro, enterprise)"
    obrigatorio: false
  - campo: goals
    tipo: array
    origen: "Usuário — objetivos de ativação"
    obrigatorio: false
  - campo: behaviorReport
    tipo: file
    origen: "trackUserBehavior() — relatório comportamental"
    obrigatorio: false

Saida:
  - campo: onboardingChecklist
    tipo: file
    destino: "onboarding-checklist.md, tooltip-generator, proactive-outreach"
    persistido: true
  - campo: milestones
    tipo: array
    destino: "user-behavior-tracker, proactive-outreach"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Segmento definido"
    - "[ ] Dados comportamentais disponíveis (ou padrões)"
    - "[ ] Objetivo de ativação claro"
  post-conditions:
    - "[ ] Checklist personalizado criado"
    - "[ ] Milestones definidos com critérios"
    - "[ ] Progressão visual configurada"
    - "[ ] onboarding-checklist.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Checklist com 5-7 itens máximo"
    - blocker: true
      criteria: "Primeiro item completável em < 2 minutos"
    - blocker: false
      criteria: "Personalização por plano de assinatura"

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
  fallback: "Se dados comportamentais indisponíveis, usar checklist padrão do segmento"
  notification: "tooltip-generator"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "saas-onboarding-activator"
  created_at: "2026-02-24T00:00:00Z"
---

# Build Onboarding Checklist

## Flow

```
1. Receber segmento e dados comportamentais
2. Definir objetivo de ativação para o segmento
3. Mapear etapas do onboarding do início à ativação
4. Priorizar por impacto na ativação (aha moment primeiro)
5. Criar checklist com 5-7 itens e progressão
6. Definir milestones com critérios de conclusão
7. Adicionar gamificação (barra de progresso, celebrações)
8. Gerar onboarding-checklist.md
9. Enviar para tooltip-generator e proactive-outreach
```

## Elicitation

- "Qual o segmento de usuários? (admin, end-user, developer)"
- "Qual o plano de assinatura? (free, pro, enterprise)"
- "Quais são os objetivos de ativação?"
- "Qual a ação principal que gera valor no produto?"
