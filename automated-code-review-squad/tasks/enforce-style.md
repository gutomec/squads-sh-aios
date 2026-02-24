---
task: enforceStyle()
responsavel: "StyleEnforcer"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: code
    tipo: string
    origen: "Usuário ou fullCodeReview() — código para review"
    obrigatorio: true
  - campo: config
    tipo: object
    origen: "Projeto — configuração de linter/formatter"
    obrigatorio: false

Saida:
  - campo: styleFindings
    tipo: array
    destino: "review-summary-writer"
    persistido: true
  - campo: styleReport
    tipo: file
    destino: "style-review-report.md, review-summary-writer"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Código disponível para review"
    - "[ ] Configuração de linter identificada (quando disponível)"
  post-conditions:
    - "[ ] Naming conventions verificadas"
    - "[ ] Formatação validada"
    - "[ ] Documentação checada"
    - "[ ] Imports verificados"
    - "[ ] style-review-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Naming conventions de public APIs consistentes"
    - blocker: false
      criteria: "Formatação seguindo configuração do projeto"
    - blocker: false
      criteria: "Documentação presente em funções públicas"

Performance:
  duration_expected: "5-10 minutos"
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

# Enforce Style

## Flow

```
1. Receber código e configuração do projeto
2. Verificar naming conventions (camelCase, PascalCase, snake_case, etc.)
3. Validar formatação (indentação, line length, whitespace)
4. Checar documentação (JSDoc, docstrings em funções públicas)
5. Verificar ordenação de imports (externos → internos → relativos)
6. Detectar imports não utilizados
7. Aplicar regras específicas do projeto
8. Gerar style-review-report.md
9. Enviar styleFindings[] para @review-summary-writer
```

## Elicitation

- "Qual o código para verificação de estilo?"
- "Há configuração de linter/formatter no projeto? (.eslintrc, .prettierrc, etc.)"
- "Quais naming conventions são usadas no projeto?"
- "Documentação é obrigatória para funções públicas?"
