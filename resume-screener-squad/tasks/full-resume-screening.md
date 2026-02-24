---
task: fullResumeScreening()
responsavel: "Ranker"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: resumes
    tipo: array
    origen: "Usuário — currículos para triagem"
    obrigatorio: true
  - campo: jobDescription
    tipo: string
    origen: "Usuário — descrição da vaga"
    obrigatorio: true

Saida:
  - campo: screeningResult
    tipo: object
    destino: "Usuário — resultado completo da triagem"
    persistido: true
  - campo: parsedResumes
    tipo: array
    destino: "parsed-resumes.json"
    persistido: true
  - campo: fitScoreReport
    tipo: file
    destino: "fit-score-report.md"
    persistido: true
  - campo: biasReport
    tipo: file
    destino: "bias-audit-report.md"
    persistido: true
  - campo: rankingReport
    tipo: file
    destino: "ranking-report.md"
    persistido: true
  - campo: candidateSummaries
    tipo: file
    destino: "candidate-summaries.md"
    persistido: true
  - campo: comparisonMatrix
    tipo: file
    destino: "comparison-matrix.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Currículos disponíveis em formato legível"
    - "[ ] Descrição da vaga completa com requisitos"
    - "[ ] Tamanho da shortlist definido"
  post-conditions:
    - "[ ] Currículos parseados com dados estruturados"
    - "[ ] Skills matched com fit scores calculados"
    - "[ ] Vieses auditados sem disparidades críticas"
    - "[ ] Candidatos ranqueados com justificativas"
    - "[ ] Resumos executivos e matriz comparativa gerados"
  acceptance-criteria:
    - blocker: true
      criteria: "Pipeline completo do parsing ao resumo executivo"
    - blocker: true
      criteria: "Auditoria de viés realizada"
    - blocker: false
      criteria: "Perguntas de entrevista geradas"

Performance:
  duration_expected: "30-60 minutos"
  cost_estimated: "Variável conforme volume de currículos"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: escalate
  retry:
    max_attempts: 2
    delay: "exponential(base=10s, max=60s)"
  fallback: "Se qualquer fase falhar, entregar resultado parcial com indicação da fase interrompida"
  notification: "candidate-summary-agent"

Metadata:
  version: "1.0.0"
  dependencies: [parseResumes(), matchSkills(), auditBias(), rankCandidates(), generateCandidateSummary()]
  author: "resume-screener-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Full Resume Screening

## Pipeline

```
Fase 1: Parsing        → @resume-parser          → parseResumes()
Fase 2: Matching        → @skills-matcher          → matchSkills()
Fase 3: Auditoria       → @bias-auditor            → auditBias()
Fase 4: Ranking          → @shortlist-ranker        → rankCandidates()
Fase 5: Resumos          → @candidate-summary-agent → generateCandidateSummary()
```

## Elicitation

### Fase 1 — Currículos
- "Quantos currículos deseja triar?"
- "Em qual formato estão os currículos? (PDF, DOCX, texto)"

### Fase 2 — Vaga
- "Qual a descrição completa da vaga (título, requisitos, nice-to-haves)?"
- "Quais são os requisitos must-have?"

### Fase 3 — Configuração
- "Qual o tamanho desejado da shortlist? (5, 10, 20)"
- "Há requisitos de diversidade específicos?"

### Fase 4 — Saída
- "Qual formato de resumo preferido? (standard, executive, detailed)"
- "Deseja perguntas de entrevista personalizadas?"
