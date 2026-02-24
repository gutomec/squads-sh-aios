# Coding Standards — soc-alert-triage

## Linguagem
- YAML para configurações de regras, playbooks e workflows
- JSON para IOCs e dados estruturados (alertas, risk scores)
- Markdown para briefs, relatórios e documentação
- Python para scripts de automação SOC
- KQL/SPL para queries de SIEM (Sentinel/Splunk)

## Convenções de Nomes
- Variáveis e funções: camelCase (`classifiedAlerts`, `filterFalsePositives`)
- Constantes: UPPER_SNAKE_CASE (`MAX_RISK_SCORE`, `DEFAULT_TIME_WINDOW`)
- Arquivos: kebab-case (`classify-alerts.md`, `fp-analysis-report.md`)
- IDs de alerta: `ALT-YYYY-NNNN` (`ALT-2026-0042`)
- IOC identifiers: tipo:valor (`ip:185.220.101.45`, `hash:a1b2c3d4...`)

## Timestamps
- SEMPRE usar UTC para todos os timestamps
- Formato: ISO 8601 (`2026-02-24T14:30:00Z`)
- Incluir timezone quando reportar para analistas
- Normalizar timestamps entre fontes diferentes (SIEM, IDS, EDR)

## Segurança
- NUNCA logar dados sensíveis (credenciais, tokens, API keys)
- Sanitizar IOCs antes de compartilhar externamente
- Mascarar PII em relatórios (nomes de usuário, emails internos)
- Usar variáveis de ambiente para credenciais de feeds de threat intel
- Validar integridade de IOCs antes de consultar feeds externos
- Logs de auditoria para todas as decisões de filtragem

## Briefs e Relatórios
- JSON/Markdown em UTF-8
- Sumário executivo sempre em 3-5 linhas
- Action items com prioridade (P1, P2, P3) e responsável
- Timeline com timestamps precisos em UTC
- IOCs formatados em tabela com reputation score

## Classificação
- Usar taxonomia MITRE ATT&CK para categorização
- Severidade padronizada: critical, high, medium, low, info
- Tipo padronizado: malware, phishing, brute_force, lateral_movement, exfiltration, etc.
- Justificativa documentada para cada classificação

## Testes
- Testar regras de classificação com alertas de amostra
- Validar baselines de FP periodicamente
- Simular cenários de triagem (tabletop exercises)
- Verificar precisão de risk scores vs avaliação manual
