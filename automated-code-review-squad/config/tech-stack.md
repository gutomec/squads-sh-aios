# Tech Stack — automated-code-review-squad

## SAST (Static Application Security Testing)
- **SonarQube** — Análise estática de segurança e qualidade de código
- **Semgrep** — Análise estática baseada em padrões (lightweight, open-source)
- **CodeQL** — Análise semântica de segurança (GitHub)
- **Snyk Code** — SAST integrado ao pipeline de CI/CD

## Linting & Formatting
- **ESLint** — Linter para JavaScript/TypeScript
- **Prettier** — Formatter opinativo para JS/TS/CSS/HTML
- **Pylint** — Linter para Python
- **Black** — Formatter opinativo para Python
- **RuboCop** — Linter para Ruby
- **Clippy** — Linter para Rust
- **golangci-lint** — Linter agregador para Go

## Segurança & Dependências
- **OWASP ZAP** — Scanner de segurança web dinâmico (DAST)
- **Snyk** — Auditoria de dependências e vulnerabilidades
- **Dependabot** — Atualização automática de dependências (GitHub)
- **Trivy** — Scanner de vulnerabilidades para containers e dependências
- **npm audit** — Auditoria de dependências Node.js nativa
- **pip-audit** — Auditoria de dependências Python

## Code Quality & Métricas
- **SonarCloud** — Qualidade de código na nuvem
- **Code Climate** — Análise de manutenibilidade e cobertura
- **Codacy** — Revisão de código automatizada
- **Codecov** — Cobertura de testes

## CI/CD Integration
- **GitHub Actions** — Pipelines de CI/CD nativos do GitHub
- **GitLab CI** — Pipelines de CI/CD nativos do GitLab
- **Jenkins** — Servidor de CI/CD open-source
- **CircleCI** — Plataforma de CI/CD cloud

## Linguagens Suportadas
- **TypeScript** — Análise completa (ESLint, Prettier, SonarQube)
- **JavaScript** — Análise completa (ESLint, Prettier, SonarQube)
- **Python** — Análise completa (Pylint, Black, Bandit)
- **Go** — Análise completa (golangci-lint, go vet)
- **Java** — Análise completa (Checkstyle, SpotBugs, PMD)
- **Rust** — Análise completa (Clippy, rustfmt)
- **Ruby** — Análise parcial (RuboCop, Brakeman)
- **C#** — Análise parcial (StyleCop, Roslyn Analyzers)
