---
task: checkArchitecture()
responsavel: "ArchChecker"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: code
    tipo: string
    origen: "Usuário ou fullCodeReview() — código para review"
    obrigatorio: true
  - campo: expectedPatterns
    tipo: array
    origen: "Projeto — padrões arquiteturais esperados"
    obrigatorio: false

Saida:
  - campo: architectureFindings
    tipo: array
    destino: "review-summary-writer"
    persistido: true
  - campo: architectureReport
    tipo: file
    destino: "architecture-review-report.md, review-summary-writer"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Código disponível para review"
    - "[ ] Padrões arquiteturais do projeto identificados (quando disponíveis)"
  post-conditions:
    - "[ ] SOLID verificado"
    - "[ ] Layer violations detectadas"
    - "[ ] Acoplamento analisado"
    - "[ ] Design patterns validados"
    - "[ ] architecture-review-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Layer violations identificadas"
    - blocker: true
      criteria: "SOLID principles verificados"
    - blocker: false
      criteria: "Design patterns validados"

Performance:
  duration_expected: "10-15 minutos"
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

# Check Architecture

## Flow

```
1. Receber código para review
2. Identificar arquitetura do projeto (MVC, Clean, Hexagonal, etc.)
3. Verificar princípios SOLID (SRP, OCP, LSP, ISP, DIP)
4. Detectar layer violations (controller acessando DB, etc.)
5. Analisar acoplamento entre módulos (afferent, efferent)
6. Avaliar coesão dentro de módulos
7. Validar uso correto de design patterns
8. Verificar DRY (duplicação de lógica)
9. Gerar architecture-review-report.md
10. Enviar architectureFindings[] para @review-summary-writer
```

## Elicitation

- "Qual o código para verificação arquitetural?"
- "Quais padrões arquiteturais são esperados? (MVC, Clean Architecture, Hexagonal, etc.)"
- "Há restrições de layer boundary definidas no projeto?"
- "Qual o contexto do projeto? (startup MVP, enterprise, microservice)"
