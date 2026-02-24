---
task: trackUserBehavior()
responsavel: "Tracker"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: userSegment
    tipo: string
    origen: "Usuário ou fullOnboardingActivation() — segmento de usuários alvo"
    obrigatorio: true
  - campo: timeWindow
    tipo: string
    origen: "Usuário — janela de análise (24h, 7d, 30d)"
    obrigatorio: false
  - campo: events
    tipo: array
    origen: "Projeto — eventos específicos a rastrear"
    obrigatorio: false

Saida:
  - campo: behaviorReport
    tipo: file
    destino: "behavior-report.md, checklist-builder, aha-moment-identifier, proactive-outreach"
    persistido: true
  - campo: churnSignals
    tipo: array
    destino: "proactive-outreach, aha-moment-identifier"
    persistido: true
  - campo: segmentData
    tipo: object
    destino: "checklist-builder, tooltip-generator"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Segmento de usuários definido"
    - "[ ] Eventos de tracking configurados"
    - "[ ] Ferramentas de analytics acessíveis"
  post-conditions:
    - "[ ] Comportamento rastreado e analisado"
    - "[ ] Sinais de abandono identificados"
    - "[ ] Segmentação atualizada"
    - "[ ] behavior-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Eventos-chave do onboarding rastreados com timestamps"
    - blocker: true
      criteria: "Sinais de abandono identificados com threshold de confiança"
    - blocker: false
      criteria: "Cohort analysis com retenção D1/D3/D7"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0 (consulta a ferramentas de analytics)"
  cacheable: false
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se fonte de analytics indisponível, usar dados de sessão disponíveis"
  notification: "proactive-outreach"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "saas-onboarding-activator"
  created_at: "2026-02-24T00:00:00Z"
---

# Track User Behavior

## Flow

```
1. Definir segmento e janela de análise
2. Coletar eventos de tracking das ferramentas de analytics
3. Analisar padrões de engajamento positivo
4. Identificar sinais de abandono (inatividade, bounce, rage clicks)
5. Calcular métricas de ativação (DAU/MAU, feature adoption, time-to-value)
6. Segmentar usuários por comportamento e cohort
7. Gerar relatório comportamental com insights acionáveis
8. Enviar para checklist-builder e aha-moment-identifier
```

## Elicitation

- "Qual o segmento de usuários a rastrear? (new_signup, trial, free, enterprise)"
- "Qual a janela de análise? (24h, 7d, 30d)"
- "Quais eventos específicos devem ser priorizados?"
- "Quais ferramentas de analytics estão disponíveis? (Mixpanel, Amplitude, Segment)"
