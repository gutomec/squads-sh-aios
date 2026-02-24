---
task: reviewSecurity()
responsavel: "SecurityReviewer"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: code
    tipo: string
    origen: "Usuário ou fullCodeReview() — código/PR/commit para review"
    obrigatorio: true
  - campo: language
    tipo: string
    origen: "Detectado ou Usuário — linguagem de programação"
    obrigatorio: false
  - campo: framework
    tipo: string
    origen: "Detectado ou Usuário — framework utilizado"
    obrigatorio: false

Saida:
  - campo: securityFindings
    tipo: array
    destino: "review-summary-writer"
    persistido: true
  - campo: securityReport
    tipo: file
    destino: "security-review-report.md, review-summary-writer"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Código disponível para review"
    - "[ ] Linguagem identificada (automática ou manual)"
  post-conditions:
    - "[ ] OWASP Top 10 verificado"
    - "[ ] Secrets escaneados"
    - "[ ] Dependências auditadas"
    - "[ ] Findings classificados por severidade"
    - "[ ] security-review-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "OWASP Top 10 verificado"
    - blocker: true
      criteria: "Zero secrets expostos"
    - blocker: false
      criteria: "Dependências com CVEs sinalizadas"

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

# Review Security

## Flow

```
1. Receber código para review
2. Identificar linguagem e framework (automático ou informado)
3. Verificar OWASP Top 10 (Injection, Broken Auth, XSS, SSRF, IDOR, etc.)
4. Escanear por secrets expostos (API keys, passwords, tokens, private keys)
5. Auditar dependências por CVEs conhecidas
6. Verificar padrões de criptografia inseguros
7. Classificar findings por severidade (CRITICAL, HIGH, MEDIUM, LOW)
8. Sugerir remediação para cada finding
9. Gerar security-review-report.md
10. Enviar securityFindings[] para @review-summary-writer
```

## Elicitation

- "Qual o código/PR/commit para revisão de segurança?"
- "Qual a linguagem de programação? (será detectada automaticamente se omitida)"
- "Qual o framework utilizado? (será detectado automaticamente se omitido)"
- "Há alguma área de maior preocupação? (autenticação, API, dados sensíveis)"
