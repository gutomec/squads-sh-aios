# Coding Standards — resume-screener-squad

## Linguagem
- JSON para dados estruturados de candidatos (parsed resumes, fit scores)
- YAML para configurações e requisitos de vaga
- Markdown para relatórios e resumos executivos
- Python para scripts de parsing e matching
- SQL para queries em ATS e databases de candidatos

## Convenções de Nomes
- Variáveis e funções: camelCase (`fitScore`, `parseResumes`, `matchSkills`)
- Constantes: UPPER_SNAKE_CASE (`MAX_SHORTLIST_SIZE`, `MIN_FIT_SCORE`)
- Arquivos: kebab-case (`parse-resumes.md`, `fit-score-report.md`)
- IDs de candidato: `CAND-YYYY-NNNN` (`CAND-2026-0042`)
- IDs de vaga: `JOB-YYYY-NNNN` (`JOB-2026-0015`)

## Encoding
- SEMPRE usar UTF-8 para todos os arquivos
- Preservar acentuação em nomes de candidatos e descrições
- Suportar caracteres especiais de múltiplos idiomas

## Privacidade & Compliance
- LGPD/GDPR compliance obrigatório para dados de candidatos
- Consent management: consentimento explícito para processamento
- Minimização de dados: processar apenas o necessário
- Retenção: definir prazo de retenção de dados de candidatos
- NUNCA incluir dados sensíveis em logs ou relatórios de debug
- Mascarar PII em outputs de desenvolvimento/teste
- Direito ao esquecimento: suportar exclusão de dados do candidato

## DEI (Diversidade, Equidade e Inclusão)
- Linguagem inclusiva em todas as comunicações
- Sem proxies discriminatórios em critérios de avaliação
- Auditoria de viés mandatória em todo pipeline de triagem
- Relatórios de diversidade em cada shortlist

## Relatórios
- Markdown para relatórios legíveis por humanos
- JSON para dados estruturados entre agentes
- Tabelas para comparações e matrizes
- Linguagem neutra e baseada em evidências
- Sem adjetivos subjetivos em avaliações de candidatos

## Testes
- Validar parsing com CVs em múltiplos formatos
- Testar matching com requisitos variados
- Simular cenários de viés para validar detecção
- Verificar compliance com LGPD/GDPR em cada output
- Testar edge cases (CVs incompletos, formatos exóticos)
