# Coding Standards — saas-onboarding-activator

## Linguagem
- TypeScript para SDKs de tracking e integrações
- JSON para eventos, configurações e dados estruturados
- Markdown para relatórios, checklists e documentação
- YAML para configurações de workflows e automações
- HTML/CSS para tooltips e guided tours inline

## Convenções de Nomes
- Variáveis e funções: camelCase (`userSegment`, `trackUserBehavior`)
- Constantes: UPPER_SNAKE_CASE (`MAX_CHECKLIST_ITEMS`, `DEFAULT_TIME_WINDOW`)
- Arquivos: kebab-case (`track-user-behavior.md`, `aha-moment-report.md`)
- Eventos de tracking: camelCase (`signupComplete`, `featureUsed`, `checklistItemCompleted`)
- Segmentos: snake_case (`new_signup`, `trial_user`, `free_to_paid`)

## Eventos de Tracking
- SEMPRE incluir timestamp em UTC (ISO 8601)
- SEMPRE incluir user_id e session_id
- SEMPRE incluir context (page, source, referrer)
- Nomear eventos com verbo_objeto: `signup_complete`, `feature_used`, `checklist_started`
- Propriedades em camelCase: `planType`, `onboardingStep`, `completionRate`

## Privacidade & Compliance
- GDPR/LGPD compliance em todos os rastreamentos
- Anonimizar PII (Personally Identifiable Information) em relatórios
- Consent management — só rastrear com consentimento explícito
- Data retention policy — definir tempo de retenção de dados
- NUNCA rastrear dados sensíveis (senhas, cartões, documentos)
- Implementar opt-out em todas as comunicações

## Tooltips & In-App Messages
- Máximo 2 linhas de texto por tooltip
- Máximo 5 steps por guided tour
- Sempre incluir botão de dismiss/skip
- Tom de voz consistente com a marca do produto
- Incluir variações A/B em todos os tooltips

## Emails & Outreach
- Subject line com máximo 50 caracteres
- Preview text com máximo 90 caracteres
- Personalizar com nome e progresso do usuário
- Incluir unsubscribe em todos os emails
- Respeitar frequência máxima (1 email/dia, 3/semana)
- NUNCA usar urgência falsa ou guilt-tripping

## Testes
- Testar variações A/B antes de deploy em 100%
- Validar rendering de tooltips em mobile e desktop
- Testar sequências de email end-to-end
- Verificar GDPR/LGPD compliance em novos rastreamentos
- Testar edge cases: usuário sem nome, sem email, sem dados
