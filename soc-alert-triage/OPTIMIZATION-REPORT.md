# Optimization Report — soc-alert-triage

## Squad: soc-alert-triage
## Version: 1.0.0
## Date: 2026-02-24

---

## Agent Analysis

### Total Agents Proposed: 5
### Total Agents Retained: 5
### Agents Dropped: 0

---

## Agent Justification

### 1. Classifier (`alert-classifier`)
- **Status:** RETAINED
- **Archetype:** Guardian
- **Justification:** Responsabilidade distinta e essencial. A classificação de alertas de múltiplas fontes (SIEM, IDS/IPS, EDR, cloud) por tipo, severidade e mapeamento MITRE ATT&CK é o primeiro passo crítico de qualquer triagem. Nenhum outro agente cobre essa função. A normalização de formatos diferentes e aplicação de taxonomia consistente requer expertise especializada.
- **Overlap:** Nenhum. Único agente que categoriza alertas crus.

### 2. FPFilter (`false-positive-filter`)
- **Status:** RETAINED
- **Archetype:** Guardian
- **Justification:** Responsabilidade distinta e de alto impacto. A filtragem de falsos positivos usando baselines comportamentais, whitelists contextuais e padrões históricos é essencial para reduzir o volume de alertas em até 80%. Sem esse agente, analistas seriam sobrecarregados com ruído. A geração de recomendações de tuning para SIEM também é competência única.
- **Overlap:** Nenhum. O Classifier categoriza; o FPFilter filtra ruído baseado em contexto e baselines.

### 3. Prioritizer (`threat-prioritizer`)
- **Status:** RETAINED
- **Archetype:** Balancer
- **Justification:** Responsabilidade distinta e estratégica. O cálculo de risk scores baseados em exploitability, blast radius, criticidade de ativos e impacto no negócio é competência única deste agente. Também orquestra o pipeline completo (`fullAlertTriage()`). A priorização garante que o SOC foque nas ameaças mais perigosas primeiro.
- **Overlap:** Nenhum. O FPFilter separa real de FP; o Prioritizer ordena ameaças reais por urgência.

### 4. Enricher (`context-enricher`)
- **Status:** RETAINED
- **Archetype:** Builder
- **Justification:** Responsabilidade distinta e técnica. O enriquecimento com IOCs, consulta a feeds de threat intel (VirusTotal, AbuseIPDB, MISP, OTX), mapeamento MITRE ATT&CK completo, geolocalização e correlação histórica transforma alertas em inteligência acionável. Nenhum outro agente tem acesso e competência para integrar múltiplos feeds.
- **Overlap:** Nenhum. O Prioritizer define urgência; o Enricher adiciona contexto técnico detalhado.

### 5. BriefGen (`analyst-brief-generator`)
- **Status:** RETAINED
- **Archetype:** Builder
- **Justification:** Responsabilidade distinta e orientada ao analista. A síntese de toda a análise em um brief acionável com timeline, playbook recomendado, sumário de IOCs e ações de resposta priorizadas é o produto final do pipeline. Sem esse agente, o analista precisaria navegar múltiplos relatórios para entender o contexto completo.
- **Overlap:** Nenhum. Único agente focado em output consumível pelo analista humano.

---

## Overlap Analysis

| Par de Agentes | Overlap | Decisão |
|---|---|---|
| Classifier ↔ FPFilter | Mínimo (classificação vs filtragem) | Mantidos — funções sequenciais complementares |
| FPFilter ↔ Prioritizer | Zero (filtragem vs priorização) | Mantidos — responsabilidades distintas |
| Prioritizer ↔ Enricher | Zero (scoring vs enriquecimento) | Mantidos — responsabilidades distintas |
| Enricher ↔ BriefGen | Mínimo (dados vs síntese) | Mantidos — Enricher coleta, BriefGen sintetiza |
| Classifier ↔ BriefGen | Zero (input vs output do pipeline) | Mantidos — extremos opostos do pipeline |

---

## Conclusion

Todos os 5 agentes são **distintos e necessários**. Cada um cobre uma fase diferente do pipeline de triagem de alertas SOC com responsabilidades bem definidas e sem overlap significativo. A remoção de qualquer agente resultaria em perda de capacidade crítica:

- Sem Classifier: impossível categorizar alertas de múltiplas fontes consistentemente
- Sem FPFilter: analistas sobrecarregados com 80%+ de ruído (alert fatigue)
- Sem Prioritizer: ameaças críticas perdidas entre alertas de baixa prioridade
- Sem Enricher: alertas sem contexto — IOCs, threat intel e MITRE ATT&CK ausentes
- Sem BriefGen: analistas navegando múltiplos relatórios sem síntese acionável
