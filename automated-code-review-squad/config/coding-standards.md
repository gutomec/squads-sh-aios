# Coding Standards — automated-code-review-squad

## Linguagem
- TypeScript/JavaScript para análise e scripts
- YAML para configurações de regras
- Markdown para relatórios e summaries
- JSON para dados estruturados (findings, métricas)

## Convenções de Nomes
- Variáveis e funções: camelCase (`securityFindings`, `reviewSecurity`)
- Constantes: UPPER_SNAKE_CASE (`MAX_SEVERITY_SCORE`, `OWASP_TOP_10`)
- Arquivos: kebab-case (`review-security.md`, `check-architecture.md`)
- Classes/Agentes: PascalCase (`SecurityReviewer`, `ArchChecker`)
- Workflows: snake_case (`full_code_review`, `quick_security_check`)
- Comandos: *kebab-case (`*review-security`, `*check-architecture`)

## Findings
- Cada finding deve ter: id, categoria, severidade, descrição, localização, fix sugerido
- Severidades: CRITICAL, HIGH, MEDIUM, LOW, INFO
- Categorias: security, logic, architecture, style
- Fix sugerido é obrigatório — review sem sugestão é incompleto
- Referências externas quando aplicável (OWASP, CWE, CVE)

## Segurança
- NUNCA logar código fonte de clientes em relatórios públicos
- Sanitizar dados sensíveis antes de armazenar findings
- Secrets encontrados devem ser reportados sem expor o valor completo
- Mascarar chaves e tokens nos relatórios (ex: `sk-...xxxx`)
- CVEs devem incluir link para NVD (National Vulnerability Database)

## Relatórios
- UTF-8 para todos os arquivos
- Português (PT-BR) para descrições e relatórios
- Inglês para nomes de variáveis, IDs e termos técnicos padrão
- Acentuação correta obrigatória (análise, lógica, segurança, etc.)
- Summary deve ser priorizado — bloqueantes primeiro

## Verdicts
- BLOCK: ao menos um finding CRITICAL ou HIGH de segurança
- REQUEST_CHANGES: findings MEDIUM ou edge cases em caminhos críticos
- APPROVE: apenas findings LOW e INFO
- Verdict deve ser justificado com referência aos findings
