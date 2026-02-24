---
task: writeReviewSummary()
responsavel: "SummaryWriter"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: findings
    tipo: array
    origen: "Todos os reviewers — findings de segurança, lógica, arquitetura e estilo"
    obrigatorio: true
  - campo: format
    tipo: string
    origen: "Usuário — formato (github-pr, standard, detailed)"
    obrigatorio: false

Saida:
  - campo: reviewSummary
    tipo: file
    destino: "review-summary.md, developer/author"
    persistido: true
  - campo: verdict
    tipo: string
    destino: "CI/CD pipeline — APPROVE/REQUEST_CHANGES/BLOCK"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Findings de ao menos um reviewer disponíveis"
    - "[ ] Formato de saída definido (default: standard)"
  post-conditions:
    - "[ ] Findings deduplicados e agrupados"
    - "[ ] Summary priorizado por severidade"
    - "[ ] Verdict definido (APPROVE/REQUEST_CHANGES/BLOCK)"
    - "[ ] Fixes sugeridos para cada finding"
    - "[ ] review-summary.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Findings priorizados por severidade"
    - blocker: true
      criteria: "Verdict claro (APPROVE/REQUEST_CHANGES/BLOCK)"
    - blocker: false
      criteria: "Pontos positivos do código reconhecidos"

Performance:
  duration_expected: "5-10 minutos"
  cost_estimated: "~0 (síntese textual)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se síntese falhar, gerar summary parcial com findings disponíveis"
  notification: "developer/author"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "automated-code-review-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Write Review Summary

## Flow

```
1. Receber findings de todos os reviewers (segurança, lógica, arquitetura, estilo)
2. Deduplicar findings sobrepostos entre revisores
3. Agrupar findings por categoria
4. Priorizar por severidade (CRITICAL > HIGH > MEDIUM > LOW > INFO)
5. Sugerir fix para cada finding
6. Reconhecer pontos positivos do código
7. Definir verdict (APPROVE / REQUEST_CHANGES / BLOCK)
8. Formatar summary no formato solicitado (github-pr, standard, detailed)
9. Gerar review-summary.md
10. Enviar para developer/author
```

## Elicitation

- "Quais findings devem ser incluídos no summary?"
- "Qual o formato desejado? (github-pr, standard, detailed)"
- "Há contexto adicional sobre o PR/commit?"
- "Deseja incluir métricas de cobertura de testes?"
