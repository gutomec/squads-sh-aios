---
task: fullCodeReview()
responsavel: "SummaryWriter"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: code
    tipo: string
    origen: "Usuário — código, PR URL ou commit para review"
    obrigatorio: true
  - campo: prUrl
    tipo: string
    origen: "Usuário — URL do Pull Request (opcional)"
    obrigatorio: false

Saida:
  - campo: fullReviewResult
    tipo: object
    destino: "Usuário — resultado completo do review"
    persistido: true
  - campo: securityReport
    tipo: file
    destino: "security-review-report.md"
    persistido: true
  - campo: logicReport
    tipo: file
    destino: "logic-review-report.md"
    persistido: true
  - campo: architectureReport
    tipo: file
    destino: "architecture-review-report.md"
    persistido: true
  - campo: styleReport
    tipo: file
    destino: "style-review-report.md"
    persistido: true
  - campo: reviewSummary
    tipo: file
    destino: "review-summary.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Código ou PR disponível para review"
    - "[ ] Linguagem de programação identificada"
    - "[ ] Nível de rigor definido (standard, strict, relaxed)"
  post-conditions:
    - "[ ] Segurança revisada — vulnerabilidades OWASP Top 10 verificadas"
    - "[ ] Lógica analisada — edge cases e corretude verificados"
    - "[ ] Arquitetura verificada — padrões e acoplamento analisados"
    - "[ ] Estilo enforçado — naming e formatação validados"
    - "[ ] Summary gerado com verdict e findings priorizados"
  acceptance-criteria:
    - blocker: true
      criteria: "Pipeline completo de review executado"
    - blocker: true
      criteria: "Verdict definido"
    - blocker: false
      criteria: "Todos os findings com fix sugerido"

Performance:
  duration_expected: "30-60 minutos"
  cost_estimated: "~0 (análise estática)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: escalate
  retry:
    max_attempts: 2
    delay: "exponential(base=10s, max=60s)"
  fallback: "Se qualquer fase falhar, gerar summary parcial com findings disponíveis e sinalizar fases incompletas"
  notification: "developer/author"

Metadata:
  version: "1.0.0"
  dependencies:
    - reviewSecurity()
    - reviewLogic()
    - checkArchitecture()
    - enforceStyle()
    - writeReviewSummary()
  author: "automated-code-review-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Full Code Review

## Pipeline

```
Fase 1: Segurança      → @security-reviewer      → reviewSecurity()
Fase 2: Lógica         → @logic-reviewer          → reviewLogic()
Fase 3: Arquitetura    → @architecture-checker     → checkArchitecture()
Fase 4: Estilo         → @style-enforcer           → enforceStyle()
Fase 5: Summary        → @review-summary-writer    → writeReviewSummary()
```

## Elicitation

### Fase 1 — Código
- "Qual o código/PR/commit para review?"
- "Qual a linguagem de programação principal?"

### Fase 2 — Contexto
- "Há padrões arquiteturais específicos do projeto?"
- "Existe configuração de linter/formatter?"

### Fase 3 — Rigor
- "Qual o nível de rigor desejado? (standard, strict, relaxed)"
- "Deseja formato de PR comment para GitHub?"

### Fase 4 — Foco
- "Há alguma área de maior preocupação? (segurança, performance, lógica)"
- "Há acceptance criteria ou requisitos de negócio para validar?"

## Níveis de Rigor

| Nível | Descrição | Comportamento |
|---|---|---|
| strict | Revisão rigorosa, todas as categorias | Todos os findings reportados, threshold baixo |
| standard | Revisão padrão, foco em bloqueantes | Findings MEDIUM+ reportados |
| relaxed | Revisão leve, apenas críticos | Apenas CRITICAL e HIGH reportados |
