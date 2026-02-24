---
task: deliverTutoringSession()
responsavel: "Tutor"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: topic
    tipo: string
    origen: "mapCurriculumPath() ou Usuário — tópico da sessão"
    obrigatorio: true
  - campo: difficulty
    tipo: string
    origen: "curriculum-mapper ou progress-tracker — nível de dificuldade"
    obrigatorio: false
  - campo: learningStyle
    tipo: string
    origen: "runDiagnosticAssessment() — estilo de aprendizagem preferido"
    obrigatorio: false
  - campo: learningPath
    tipo: file
    origen: "mapCurriculumPath() — trilha de aprendizagem"
    obrigatorio: false

Saida:
  - campo: sessionReport
    tipo: file
    destino: "session-report.md, progress-tracker"
    persistido: true
  - campo: exerciseResults
    tipo: array
    destino: "progress-tracker"
    persistido: true
  - campo: adaptiveFeedback
    tipo: object
    destino: "progress-tracker, curriculum-mapper"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Tópico definido"
    - "[ ] Nível de dificuldade conhecido ou padrão"
  post-conditions:
    - "[ ] Conceito explicado com abordagem adaptada"
    - "[ ] Exercícios realizados com feedback"
    - "[ ] Dificuldade ajustada baseada em desempenho"
    - "[ ] session-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Conceito explicado com ao menos 2 abordagens diferentes"
    - blocker: true
      criteria: "Mínimo 3 exercícios com feedback individualizado"
    - blocker: false
      criteria: "Dificuldade adaptada em tempo real"

Performance:
  duration_expected: "20-40 minutos"
  cost_estimated: "~0 (sessão de tutoria)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se adaptação de dificuldade falhar, manter nível padrão com exercícios variados"
  notification: "progress-tracker"

Metadata:
  version: "1.0.0"
  dependencies:
    - mapCurriculumPath()
  author: "adaptive-tutor-k12"
  created_at: "2026-02-24T00:00:00Z"
---

# Deliver Tutoring Session

## Flow

```
1. Receber tópico e contexto (trilha, estilo, dificuldade)
2. Preparar explicação adaptada ao estilo de aprendizagem do aluno
3. Apresentar conceito com exemplos concretos e analogias
4. Verificar compreensão com perguntas socráticas
5. Gerar exercícios de prática com dificuldade adaptativa
6. Fornecer feedback imediato e encorajador para cada exercício
7. Adaptar dificuldade baseada nas respostas (subir/manter/descer)
8. Revisar pontos de dificuldade com abordagem alternativa
9. Gerar relatório de sessão com resultados
10. Enviar para @progress-tracker
```

## Elicitation

- "Qual o tópico da sessão de tutoria?"
- "Há alguma dificuldade específica que o aluno tem relatado?"
- "O aluno prefere explicações visuais, verbais ou práticas?"
- "Quantos exercícios de prática deseja? (padrão: 5)"
