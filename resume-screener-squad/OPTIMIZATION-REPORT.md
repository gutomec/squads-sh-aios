# Optimization Report — resume-screener-squad

## Squad: resume-screener-squad
## Version: 1.0.0
## Date: 2026-02-24

---

## Agent Analysis

### Total Agents Proposed: 5
### Total Agents Retained: 5
### Agents Dropped: 0

---

## Agent Justification

### 1. Parser (`resume-parser`)
- **Status:** RETAINED
- **Archetype:** Builder
- **Justification:** Responsabilidade distinta e essencial. O parsing de currículos em múltiplos formatos (PDF, DOCX, texto) com extração de dados estruturados, normalização de títulos e skills, e detecção de inconsistências cronológicas é o primeiro passo crítico de qualquer triagem. Nenhum outro agente cobre essa função.
- **Overlap:** Nenhum. Único agente que interage diretamente com currículos brutos.

### 2. SkillsMatcher (`skills-matcher`)
- **Status:** RETAINED
- **Archetype:** Builder
- **Justification:** Responsabilidade distinta e analítica. A comparação de skills com requisitos da vaga, cálculo de fit score ponderado, identificação de gaps e reconhecimento de skills transferíveis são competências únicas deste agente. O Parser extrai dados; o SkillsMatcher os analisa contra os requisitos.
- **Overlap:** Mínimo com Parser. O Parser extrai dados brutos; o SkillsMatcher os compara com requisitos — funções complementares e sequenciais.

### 3. BiasAuditor (`bias-auditor`)
- **Status:** RETAINED
- **Archetype:** Guardian
- **Justification:** Responsabilidade distinta e mandatória. A auditoria de vieses (gênero, idade, etnia, pedigree educacional, nome) é uma função de compliance e ética que deve ser independente do matching e ranking. Misturar auditoria com avaliação comprometeria a integridade de ambas.
- **Overlap:** Nenhum. Único agente focado em fairness e compliance DEI.

### 4. Ranker (`shortlist-ranker`)
- **Status:** RETAINED
- **Archetype:** Balancer
- **Justification:** Responsabilidade distinta e decisória. O ranking de candidatos combina múltiplos fatores (fit score, experiência, potencial, diversidade), incorpora feedback do bias-auditor, identifica hidden gems e gera shortlist com justificativas transparentes. Essa função de síntese e decisão é diferente do matching analítico.
- **Overlap:** Mínimo com SkillsMatcher. O SkillsMatcher calcula fit scores individuais; o Ranker combina múltiplos fatores para decisão de ranking — funções complementares.

### 5. SummaryWriter (`candidate-summary-agent`)
- **Status:** RETAINED
- **Archetype:** Builder
- **Justification:** Responsabilidade distinta e orientada ao consumidor final. A geração de resumos executivos, matriz comparativa e perguntas de entrevista requer habilidade de síntese e comunicação para hiring managers. É a camada de apresentação que torna os dados acionáveis.
- **Overlap:** Nenhum. Único agente focado em output para o consumidor final (hiring manager).

---

## Overlap Analysis

| Par de Agentes | Overlap | Decisão |
|---|---|---|
| Parser ↔ SkillsMatcher | Mínimo (extração vs análise) | Mantidos — domínios complementares e sequenciais |
| SkillsMatcher ↔ Ranker | Mínimo (scoring individual vs ranking composto) | Mantidos — granularidades diferentes |
| SkillsMatcher ↔ BiasAuditor | Zero (avaliação vs auditoria) | Mantidos — independência é essencial |
| Ranker ↔ SummaryWriter | Mínimo (decisão vs comunicação) | Mantidos — públicos alvo diferentes |
| BiasAuditor ↔ Ranker | Zero (auditoria vs ranking) | Mantidos — BiasAuditor alimenta Ranker com flags |

---

## Conclusion

Todos os 5 agentes são **distintos e necessários**. Cada um cobre uma fase diferente do pipeline de triagem de currículos com responsabilidades bem definidas e sem overlap significativo. A remoção de qualquer agente resultaria em perda de capacidade crítica:

- Sem Parser: impossível extrair dados estruturados de CVs
- Sem SkillsMatcher: impossível calcular fit scores e identificar gaps
- Sem BiasAuditor: sem garantia de fairness — risco de discriminação
- Sem Ranker: impossível gerar shortlist priorizada com justificativas
- Sem SummaryWriter: sem output acionável para hiring managers
