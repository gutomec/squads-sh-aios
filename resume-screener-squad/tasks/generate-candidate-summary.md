---
task: generateCandidateSummary()
responsavel: "SummaryWriter"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: shortlist
    tipo: array
    origen: "rankCandidates() — candidatos ranqueados"
    obrigatorio: true
  - campo: format
    tipo: string
    origen: "Usuário — formato (standard, executive, detailed)"
    obrigatorio: false

Saida:
  - campo: candidateSummaries
    tipo: file
    destino: "candidate-summaries.md, hiring manager"
    persistido: true
  - campo: comparisonMatrix
    tipo: file
    destino: "comparison-matrix.md, hiring manager"
    persistido: true
  - campo: interviewQuestions
    tipo: array
    destino: "hiring manager — perguntas sugeridas"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Shortlist disponível (rankCandidates())"
    - "[ ] Dados completos dos candidatos acessíveis"
  post-conditions:
    - "[ ] Resumo executivo por candidato gerado"
    - "[ ] Matriz comparativa gerada"
    - "[ ] Perguntas de entrevista sugeridas"
    - "[ ] candidate-summaries.md gerado"
    - "[ ] comparison-matrix.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Resumo com pontos fortes e pontos de atenção"
    - blocker: true
      criteria: "Matriz comparativa entre candidatos"
    - blocker: false
      criteria: "Perguntas de entrevista específicas por candidato"

Performance:
  duration_expected: "10-15 minutos"
  cost_estimated: "~0 (processamento local)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=20s)"
  fallback: "Se dados de candidato incompletos, gerar resumo parcial com indicação de campos faltantes"
  notification: "shortlist-ranker"

Metadata:
  version: "1.0.0"
  dependencies: [rankCandidates()]
  author: "resume-screener-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Generate Candidate Summary

## Flow

```
1. Receber shortlist ranqueada do @shortlist-ranker
2. Sintetizar perfil de cada candidato
3. Identificar pontos fortes baseados em evidências
4. Identificar pontos de atenção e riscos
5. Gerar matriz comparativa entre candidatos
6. Sugerir perguntas de entrevista técnicas e comportamentais
7. Formatar para o público alvo (hiring manager)
8. Gerar candidate-summaries.md e comparison-matrix.md
9. Entregar relatório final consolidado
```

## Elicitation

- "Qual formato de resumo preferido? (standard, executive, detailed)"
- "Quais critérios priorizar na matriz comparativa?"
- "Deseja perguntas de entrevista técnicas, comportamentais ou ambas?"
- "Há preferência de linguagem para o relatório?"
