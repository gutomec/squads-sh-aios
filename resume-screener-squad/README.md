# resume-screener-squad

Squad especialista em triagem de currículos para recrutamento.

## Visão Geral

O **resume-screener-squad** é um squad completo que cobre todo o pipeline de triagem de currículos:

1. **Parsing de Currículos** — Extração automatizada de dados estruturados de CVs em qualquer formato (PDF, DOCX, texto)
2. **Matching de Skills** — Comparação de skills com requisitos da vaga, cálculo de fit score ponderado e identificação de skills transferíveis
3. **Auditoria de Vieses** — Detecção de vieses de gênero, idade, etnia, pedigree educacional e nome, garantindo equidade
4. **Ranking de Candidatos** — Ranking transparente com justificativas, identificação de hidden gems e shortlist configurável
5. **Resumos Executivos** — Briefs acionáveis para hiring managers com pontos fortes, atenção, matriz comparativa e perguntas de entrevista

**Pain Point:** Custo médio de US$ 4.700 por contratação com ciclo de 44 dias; triagem manual é propenso a vieses inconscientes e perda de candidatos qualificados.

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 📋 Parser | `resume-parser` | Parser de currículos e extração de dados |
| 🔍 SkillsMatcher | `skills-matcher` | Matching de skills e cálculo de fit score |
| 🛡️ BiasAuditor | `bias-auditor` | Auditoria de vieses e fairness |
| ⚡ Ranker | `shortlist-ranker` | Ranking e geração de shortlist |
| 📊 SummaryWriter | `candidate-summary-agent` | Resumos executivos e briefs |

## Workflows

| Workflow | Comando | Descrição | Duração |
|---|---|---|---|
| Full Resume Screening | `*triage-full` | Pipeline completo: do parsing ao resumo executivo | 30-60 min |
| Quick Skills Match | `*quick-match` | Match rápido: parsing, matching e resumo simplificado | 10-20 min |

## Comandos Disponíveis

| Comando | Agente | Descrição |
|---|---|---|
| `*parse-resumes` | Parser | Extrair dados estruturados de currículos |
| `*parse-single` | Parser | Extrair dados de um currículo específico |
| `*match-skills` | SkillsMatcher | Calcular fit score de candidatos |
| `*analyze-gaps` | SkillsMatcher | Analisar gaps de skills |
| `*audit-bias` | BiasAuditor | Auditar processo de triagem por vieses |
| `*check-fairness` | BiasAuditor | Verificar fairness do ranking |
| `*rank-candidates` | Ranker | Ranquear candidatos e gerar shortlist |
| `*triage-full` | Ranker | Pipeline completo de triagem |
| `*candidate-summary` | SummaryWriter | Gerar resumo executivo de candidatos |
| `*comparison-matrix` | SummaryWriter | Gerar matriz comparativa |

## Quick Start

```
# Ativar o ranker (orquestrador principal)
/rss:agents:shortlist-ranker

# Pipeline completo de triagem
*triage-full

# Match rápido de skills
*quick-match

# Apenas parsing de CVs
*parse-resumes

# Apenas auditoria de viés
*audit-bias
```

## Público Alvo

- Hiring Managers e Recrutadores
- Equipes de RH e Talent Acquisition
- Especialistas em DEI (Diversidade, Equidade e Inclusão)
- CTOs e líderes técnicos contratando para suas equipes

## Requisitos

- Currículos em formato legível (PDF, DOCX, texto)
- Descrição da vaga com requisitos (must-have e nice-to-have)
- Definição do tamanho da shortlist desejada
