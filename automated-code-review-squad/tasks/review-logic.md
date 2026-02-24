---
task: reviewLogic()
responsavel: "LogicReviewer"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: code
    tipo: string
    origen: "Usuário ou fullCodeReview() — código para review"
    obrigatorio: true
  - campo: context
    tipo: string
    origen: "Usuário — contexto de negócio ou acceptance criteria"
    obrigatorio: false

Saida:
  - campo: logicFindings
    tipo: array
    destino: "review-summary-writer"
    persistido: true
  - campo: logicReport
    tipo: file
    destino: "logic-review-report.md, review-summary-writer"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Código disponível para review"
    - "[ ] Contexto de negócio informado (quando disponível)"
  post-conditions:
    - "[ ] Edge cases identificados"
    - "[ ] Race conditions verificadas"
    - "[ ] Error handling revisado"
    - "[ ] Complexidade avaliada"
    - "[ ] logic-review-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Edge cases nos limites verificados"
    - blocker: true
      criteria: "Error handling em todos os caminhos de falha"
    - blocker: false
      criteria: "Complexidade ciclomática avaliada"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0 (análise estática)"
  cacheable: false
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se análise parcial falhar, reportar findings já identificados e sinalizar análise incompleta"
  notification: "review-summary-writer"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "automated-code-review-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Review Logic

## Flow

```
1. Receber código e contexto de negócio
2. Analisar fluxo lógico principal (happy path)
3. Identificar edge cases nos limites (0, null, empty, max, negative)
4. Verificar null/undefined handling
5. Checar race conditions em código concorrente/async
6. Avaliar error handling e caminhos de falha
7. Medir complexidade ciclomática e cognitiva
8. Verificar correspondência com lógica de negócio/requisitos
9. Gerar logic-review-report.md
10. Enviar logicFindings[] para @review-summary-writer
```

## Elicitation

- "Qual o código para revisão de lógica?"
- "Qual o contexto de negócio ou acceptance criteria?"
- "Há alguma função/método específico que merece atenção?"
- "O código lida com concorrência ou operações assíncronas?"
