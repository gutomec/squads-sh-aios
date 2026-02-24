# Coding Standards — data-quality-guardian

## Linguagem
- SQL para consultas e validações de dados
- Python para scripts de profiling, detecção de anomalias e remediação
- YAML para configurações de regras, thresholds e data quality checks
- JSON para schemas e dados estruturados (profiling results, anomaly lists)
- Markdown para relatórios de qualidade e documentação

## Convenções de Nomes
- Variáveis e funções: camelCase (`profilingReport`, `detectAnomalies`)
- Constantes: UPPER_SNAKE_CASE (`MAX_NULL_RATE`, `DEFAULT_SENSITIVITY`)
- Arquivos: kebab-case (`profile-dataset.md`, `quality-report.md`)
- Datasets: snake_case (`sales_2026`, `customer_orders`)
- Métricas: snake_case (`null_rate`, `unique_rate`, `completeness_score`)

## Formatos de Dados
- SEMPRE usar UTF-8 para todos os arquivos
- Datas em ISO 8601 (`2026-02-24T14:30:00Z`)
- Números decimais com ponto (`.`) como separador
- Percentuais com 2 casas decimais (`98.45%`)
- Scores de qualidade de 0.00 a 100.00

## Segurança
- NUNCA logar dados sensíveis (PII) em relatórios
- Mascarar dados sensíveis em exemplos e outputs (ex: `j***@email.com`)
- Usar variáveis de ambiente para credenciais de conexão
- Validar permissões de acesso ao dataset antes de profilar
- Relatórios não devem conter amostras de dados sensíveis sem mascaramento

## Relatórios de Qualidade
- Scores de 0 a 100 para cada dimensão
- Cores: verde (>= threshold_green), amarelo (>= threshold_yellow), vermelho (< threshold_yellow)
- Incluir timestamp de geração em UTC
- Incluir versão do dataset e período analisado
- Sumário executivo com no máximo 5 bullet points

## Scripts de Remediação
- Incluir cabeçalho com propósito, autor, data e dataset alvo
- Incluir validação de pré-condições antes de executar
- Incluir plano de rollback quando aplicável
- Logar cada ação com timestamp
- Estimar impacto (registros afetados) antes de executar

## Testes
- Testar scripts de remediação em amostra antes de executar em full dataset
- Validar profiling em datasets de teste com anomalias conhecidas
- Verificar scores de qualidade contra valores esperados
- Testar detecção de anomalias com datasets sintéticos
