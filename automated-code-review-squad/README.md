# automated-code-review-squad

Squad especialista em code review automatizado.

## Visão Geral

O **automated-code-review-squad** é um squad completo que cobre todo o pipeline de code review automatizado:

1. **Revisão de Segurança** — OWASP Top 10, injection flaws, XSS, secrets exposure, dependências com CVEs
2. **Análise Lógica** — Edge cases, race conditions, null handling, off-by-one errors, lógica de negócio
3. **Verificação Arquitetural** — SOLID, DRY, separação de concerns, layer violations, acoplamento/coesão
4. **Enforcement de Estilo** — Naming conventions, formatação, documentação, imports, regras do projeto
5. **Review Summary** — Síntese priorizada de findings com verdict (APPROVE/REQUEST_CHANGES/BLOCK)

**Pain Point:** Revisões de código consomem enormes blocos de tempo de desenvolvedores sêniores; gargalo de merge em PRs com filas longas de review.

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 🔒 SecurityReviewer | `security-reviewer` | Detecção de vulnerabilidades e revisão de segurança |
| 🧠 LogicReviewer | `logic-reviewer` | Revisão de lógica, corretude e edge cases |
| 🏗️ ArchChecker | `architecture-checker` | Verificação de padrões arquiteturais e design |
| ✅ StyleEnforcer | `style-enforcer` | Enforcement de coding standards e estilo |
| 📝 SummaryWriter | `review-summary-writer` | Síntese de findings e recomendação de aprovação |

## Workflows

| Workflow | Comando | Descrição | Duração |
|---|---|---|---|
| Full Code Review | `*full-review` | Pipeline completo: segurança, lógica, arquitetura, estilo e summary | 30-60 min |
| Quick Security Check | `*quick-security` | Verificação rápida focada em segurança | 10-20 min |

## Comandos Disponíveis

| Comando | Agente | Descrição |
|---|---|---|
| `*review-security` | SecurityReviewer | Revisar código por vulnerabilidades de segurança |
| `*check-secrets` | SecurityReviewer | Verificar exposição de secrets no código |
| `*review-logic` | LogicReviewer | Revisar lógica e corretude do código |
| `*find-edge-cases` | LogicReviewer | Identificar edge cases não tratados |
| `*check-architecture` | ArchChecker | Verificar padrões arquiteturais do código |
| `*analyze-coupling` | ArchChecker | Analisar acoplamento e coesão |
| `*check-style` | StyleEnforcer | Verificar aderência a coding standards |
| `*fix-style` | StyleEnforcer | Sugerir correções de estilo |
| `*write-summary` | SummaryWriter | Gerar sumário priorizado do code review |
| `*full-review` | SummaryWriter | Pipeline completo de code review automatizado |

## Quick Start

```
# Ativar o sintetizador (orquestrador principal)
/acr:agents:review-summary-writer

# Pipeline completo de code review
*full-review

# Verificação rápida de segurança
*quick-security

# Apenas revisão de segurança
*review-security

# Apenas revisão de lógica
*review-logic
```

## Público Alvo

- Desenvolvedores sêniores e leads
- Engenheiros de segurança (AppSec)
- Arquitetos de software
- Tech leads e engineering managers
- Equipes com alto volume de PRs

## Requisitos

- Código fonte acessível (repositório local ou PR URL)
- Configuração de linter do projeto (opcional, melhora precisão)
- Acesso ao GitHub CLI para integração com PRs (opcional)
