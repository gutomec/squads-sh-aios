---
task: fullTutoringCycle()
responsavel: "Tutor"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: subject
    tipo: string
    origen: "Usuário — disciplina"
    obrigatorio: true
  - campo: student
    tipo: string
    origen: "Usuário — nome/perfil do aluno"
    obrigatorio: false

Saida:
  - campo: fullCycleResult
    tipo: object
    destino: "Usuário — resultado completo do ciclo"
    persistido: true
  - campo: diagnosticReport
    tipo: file
    destino: "diagnostic-report.md"
    persistido: true
  - campo: learningPath
    tipo: file
    destino: "learning-path.md"
    persistido: true
  - campo: sessionReport
    tipo: file
    destino: "session-report.md"
    persistido: true
  - campo: progressReport
    tipo: file
    destino: "progress-report.md"
    persistido: true
  - campo: parentReport
    tipo: file
    destino: "parent-report.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Disciplina definida"
    - "[ ] Aluno identificado (nome ou perfil)"
  post-conditions:
    - "[ ] Diagnóstico completo realizado"
    - "[ ] Trilha personalizada criada"
    - "[ ] Sessão de tutoria entregue"
    - "[ ] Progresso rastreado"
    - "[ ] Relatório para pais gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Ciclo completo do diagnóstico ao relatório"
    - blocker: true
      criteria: "Trilha personalizada criada e sessão entregue"
    - blocker: false
      criteria: "Relatório para pais com recomendações"

Performance:
  duration_expected: "60-90 minutos"
  cost_estimated: "Variável conforme extensão de cada fase"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: escalate
  retry:
    max_attempts: 2
    delay: "exponential(base=10s, max=60s)"
  fallback: "Se qualquer fase falhar, entregar resultado parcial e indicar fase pendente"
  notification: "progress-tracker"

Metadata:
  version: "1.0.0"
  dependencies:
    - runDiagnosticAssessment()
    - mapCurriculumPath()
    - deliverTutoringSession()
    - trackLearningProgress()
    - generateParentReport()
  author: "adaptive-tutor-k12"
  created_at: "2026-02-24T00:00:00Z"
---

# Full Tutoring Cycle

## Pipeline

```
Fase 1: Avaliação Diagnóstica → @diagnostic-assessor → runDiagnosticAssessment()
Fase 2: Mapeamento Curricular → @curriculum-mapper    → mapCurriculumPath()
Fase 3: Sessão de Tutoria     → @tutor-agent          → deliverTutoringSession()
Fase 4: Rastreamento          → @progress-tracker     → trackLearningProgress()
Fase 5: Relatório para Pais   → @parent-report-agent  → generateParentReport()
```

## Elicitation

### Fase 1 — Disciplina e Aluno
- "Qual a disciplina? (Matemática, Português, Ciências, História, Inglês, etc.)"
- "Qual o ano escolar do aluno? (1º ao 12º)"
- "Qual o nome do aluno (para personalização)?"

### Fase 2 — Contexto
- "Há tópicos específicos com dificuldade?"
- "Há algum prazo ou objetivo específico? (prova, vestibular, etc.)"

### Fase 3 — Tutoria
- "O aluno prefere explicações visuais, verbais ou práticas?"
- "Quanto tempo disponível para a sessão?"

### Fase 5 — Relatório
- "Deseja relatório para pais ao final? (sim/não)"
- "Qual o formato preferido? (breve resumo ou relatório detalhado)"
