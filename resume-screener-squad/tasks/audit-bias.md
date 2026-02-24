---
task: auditBias()
responsavel: "BiasAuditor"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: screeningResults
    tipo: array
    origen: "matchSkills() — resultados do matching"
    obrigatorio: true
  - campo: jobDescription
    tipo: string
    origen: "Usuário — descrição da vaga"
    obrigatorio: false

Saida:
  - campo: biasReport
    tipo: file
    destino: "bias-audit-report.md, shortlist-ranker, candidate-summary-agent"
    persistido: true
  - campo: biasFlags
    tipo: array
    destino: "shortlist-ranker — flags para ajuste"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Resultados de matching disponíveis"
    - "[ ] Dados de candidatos com scores calculados"
  post-conditions:
    - "[ ] Vieses potenciais identificados"
    - "[ ] Disparidades reportadas com evidência"
    - "[ ] Recomendações de ajuste geradas"
    - "[ ] bias-audit-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Auditoria cobrindo gênero, idade, educação e nome"
    - blocker: true
      criteria: "Disparidades com evidência estatística"
    - blocker: false
      criteria: "Compliance com EEOC/legislação local"

Performance:
  duration_expected: "5-10 minutos"
  cost_estimated: "~0 (processamento local)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=20s)"
  fallback: "Se dados insuficientes para análise estatística, gerar relatório qualitativo"
  notification: "shortlist-ranker"

Metadata:
  version: "1.0.0"
  dependencies: [matchSkills()]
  author: "resume-screener-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Audit Bias

## Flow

```
1. Receber resultados de matching
2. Analisar distribuição demográfica implícita
3. Detectar proxies de viés (universidade, localização, gaps)
4. Verificar disparidades de score entre grupos
5. Identificar padrões discriminatórios
6. Verificar compliance com legislação
7. Gerar recomendações de ajuste
8. Gerar bias-audit-report.md
9. Enviar flags para @shortlist-ranker
```

## Elicitation

- "Quais categorias de viés devem ser priorizadas?"
- "Há requisitos de diversidade específicos da empresa?"
- "Qual legislação anti-discriminação é aplicável?"
- "Deseja análise qualitativa ou quantitativa?"
