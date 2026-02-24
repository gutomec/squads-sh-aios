---
task: generateParentReport()
responsavel: "ParentReporter"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: student
    tipo: string
    origen: "Usuário — identificação do aluno"
    obrigatorio: true
  - campo: period
    tipo: string
    origen: "Usuário — período do relatório (weekly, biweekly, monthly)"
    obrigatorio: false
  - campo: progressReport
    tipo: file
    origen: "trackLearningProgress() — relatório de progresso"
    obrigatorio: false
  - campo: format
    tipo: string
    origen: "Usuário — formato (parent, educator)"
    obrigatorio: false

Saida:
  - campo: parentReport
    tipo: file
    destino: "parent-report.md, Pais/Educadores"
    persistido: true
  - campo: recommendations
    tipo: array
    destino: "Pais — atividades recomendadas para casa"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Dados de progresso disponíveis"
    - "[ ] Aluno identificado"
  post-conditions:
    - "[ ] Relatório gerado com linguagem acessível"
    - "[ ] Conquistas celebradas"
    - "[ ] Áreas de melhoria explicadas"
    - "[ ] Recomendações práticas incluídas"
  acceptance-criteria:
    - blocker: true
      criteria: "Relatório com seção de conquistas e progressos"
    - blocker: true
      criteria: "Recomendações práticas para apoio em casa"
    - blocker: false
      criteria: "Gráficos de progresso visual"

Performance:
  duration_expected: "5-10 minutos"
  cost_estimated: "~0 (geração de relatório)"
  cacheable: true
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se dados de progresso indisponíveis, gerar relatório qualitativo baseado em sessões recentes"
  notification: "progress-tracker"

Metadata:
  version: "1.0.0"
  dependencies:
    - trackLearningProgress()
  author: "adaptive-tutor-k12"
  created_at: "2026-02-24T00:00:00Z"
---

# Generate Parent Report

## Flow

```
1. Receber dados de progresso do @progress-tracker
2. Selecionar conquistas e milestones alcançados para celebrar
3. Identificar áreas de melhoria com contexto positivo
4. Traduzir métricas em linguagem acessível (para pais) ou pedagógica (para educadores)
5. Gerar recomendações práticas e atividades para apoio em casa
6. Incluir próximos milestones como objetivos motivadores
7. Formatar relatório final no formato solicitado
8. Enviar para pais/educador
```

## Elicitation

- "Qual o aluno para o relatório?"
- "Qual o período desejado? (semanal, quinzenal, mensal)"
- "O relatório é para pais ou educadores?"
- "Há alguma conquista específica a destacar?"
