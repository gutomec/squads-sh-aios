---
task: matchSkills()
responsavel: "SkillsMatcher"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: parsedResumes
    tipo: array
    origen: "parseResumes() — dados estruturados dos candidatos"
    obrigatorio: true
  - campo: jobDescription
    tipo: string
    origen: "Usuário — descrição da vaga com requisitos"
    obrigatorio: true

Saida:
  - campo: matchedCandidates
    tipo: array
    destino: "bias-auditor, shortlist-ranker, candidate-summary-agent"
    persistido: true
  - campo: fitScoreReport
    tipo: file
    destino: "fit-score-report.md, shortlist-ranker"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Dados de candidatos extraídos (parseResumes())"
    - "[ ] Descrição da vaga disponível com requisitos"
  post-conditions:
    - "[ ] Fit score calculado para cada candidato"
    - "[ ] Gap analysis por candidato gerado"
    - "[ ] Skills transferíveis identificadas"
    - "[ ] fit-score-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Fit score calculado para 100% dos candidatos"
    - blocker: true
      criteria: "Cada requisito ponderado por importância (must-have vs nice-to-have)"
    - blocker: false
      criteria: "Skills transferíveis reconhecidas"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "~0 (processamento local)"
  cacheable: false
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se job description incompleta, usar requisitos explícitos disponíveis"
  notification: "bias-auditor"

Metadata:
  version: "1.0.0"
  dependencies: [parseResumes()]
  author: "resume-screener-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Match Skills

## Flow

```
1. Receber dados estruturados e job description
2. Extrair requisitos da vaga (must-have e nice-to-have)
3. Ponderar cada requisito por importância
4. Comparar skills de cada candidato com requisitos
5. Identificar skills transferíveis e experiência adjacente
6. Calcular fit score ponderado por candidato
7. Gerar gap analysis detalhado por candidato
8. Gerar fit-score-report.md
9. Enviar resultados para @bias-auditor e @shortlist-ranker
```

## Elicitation

- "Qual a descrição completa da vaga?"
- "Quais são os requisitos must-have?"
- "Quais são os nice-to-have?"
- "Há peso diferente para skills técnicas vs comportamentais?"
