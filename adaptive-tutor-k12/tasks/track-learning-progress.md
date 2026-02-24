---
task: trackLearningProgress()
responsavel: "ProgressTracker"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: student
    tipo: string
    origen: "Usuário — identificação do aluno"
    obrigatorio: true
  - campo: period
    tipo: string
    origen: "Usuário — período de análise (week, month, quarter)"
    obrigatorio: false
  - campo: sessionReports
    tipo: array
    origen: "deliverTutoringSession() — relatórios de sessões"
    obrigatorio: false

Saida:
  - campo: progressReport
    tipo: file
    destino: "progress-report.md, parent-report-agent, curriculum-mapper"
    persistido: true
  - campo: stagnationAlerts
    tipo: array
    destino: "curriculum-mapper, tutor-agent"
    persistido: true
  - campo: masteryMap
    tipo: object
    destino: "curriculum-mapper"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Dados de sessões disponíveis"
    - "[ ] Aluno identificado"
  post-conditions:
    - "[ ] Progresso por tópico calculado"
    - "[ ] Tendências identificadas"
    - "[ ] Estagnação detectada (se houver)"
    - "[ ] Mastery map atualizado"
  acceptance-criteria:
    - blocker: true
      criteria: "Progresso calculado por tópico com percentual de mastery"
    - blocker: true
      criteria: "Tendência de desempenho identificada (improving/stable/declining)"
    - blocker: false
      criteria: "Alertas de estagnação com recomendações"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "~0 (análise de dados)"
  cacheable: true
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se dados insuficientes, gerar relatório parcial com indicação de dados faltantes"
  notification: "parent-report-agent"

Metadata:
  version: "1.0.0"
  dependencies:
    - deliverTutoringSession()
  author: "adaptive-tutor-k12"
  created_at: "2026-02-24T00:00:00Z"
---

# Track Learning Progress

## Flow

```
1. Coletar dados de sessões de tutoria do período
2. Calcular mastery por tópico e habilidade
3. Analisar tendência de desempenho (improving/stable/declining)
4. Comparar progresso atual com baseline do aluno
5. Detectar sinais de estagnação (flat mastery, declining accuracy)
6. Mapear tópicos dominados vs pendentes
7. Gerar alertas de estagnação se necessário
8. Gerar relatório de progresso consolidado
9. Enviar para @parent-report-agent e @curriculum-mapper
```

## Elicitation

- "Qual o aluno a ser analisado?"
- "Qual o período de análise? (última semana, mês, trimestre)"
- "Há preocupações específicas sobre o progresso?"
