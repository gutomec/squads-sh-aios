# Optimization Report — data-quality-guardian

## Squad: data-quality-guardian
## Version: 1.0.0
## Date: 2026-02-24

---

## Agent Analysis

### Total Agents Proposed: 5
### Total Agents Retained: 5
### Agents Dropped: 0

---

## Agent Justification

### 1. Profiler (`data-profiler`)
- **Status:** RETAINED
- **Archetype:** Builder
- **Justification:** Responsabilidade distinta e fundamental. O profiling de datasets — cálculo de estatísticas descritivas, taxas de nulos, unicidade, distribuições e baselines — é o primeiro passo crítico de qualquer avaliação de qualidade de dados. Nenhum outro agente cobre essa função analítica de base. Sem profiling, os demais agentes não teriam dados de entrada para trabalhar.
- **Overlap:** Nenhum. Único agente que calcula estatísticas descritivas e baselines.

### 2. AnomalyDetector (`anomaly-detector`)
- **Status:** RETAINED
- **Archetype:** Guardian
- **Justification:** Responsabilidade distinta e especializada. A detecção de anomalias — outliers estatísticos, data drift, padrões incomuns e valores impossíveis — requer métodos especializados (Z-score, IQR, KS-test, PSI) que vão além do profiling básico. Enquanto o Profiler descreve os dados, o AnomalyDetector identifica o que está errado nos dados.
- **Overlap:** Mínimo com Profiler (ambos analisam dados, mas com focos diferentes: descrição vs detecção de problemas).

### 3. SchemaValidator (`schema-validator`)
- **Status:** RETAINED
- **Archetype:** Guardian
- **Justification:** Responsabilidade distinta e estrutural. A validação de schemas — tipos de dados, constraints, integridade referencial e breaking changes — é uma dimensão de qualidade completamente diferente da análise estatística. Enquanto Profiler e AnomalyDetector focam em valores, o SchemaValidator foca na estrutura e contratos de dados.
- **Overlap:** Nenhum. Único agente que valida integridade referencial e detecta breaking changes.

### 4. QualityReporter (`data-quality-reporter`)
- **Status:** RETAINED
- **Archetype:** Builder
- **Justification:** Responsabilidade distinta e integradora. A geração de relatórios com scores compostos por 6 dimensões, comparações com SLAs, tendências temporais e sumários executivos é uma competência única. O QualityReporter integra outputs de todos os outros agentes em uma narrativa acionável para stakeholders e times de governança.
- **Overlap:** Nenhum. Único agente que calcula scores compostos e gera relatórios executivos.

### 5. RemediationSuggester (`remediation-suggester`)
- **Status:** RETAINED
- **Archetype:** Balancer
- **Justification:** Responsabilidade distinta e orientada a ação. A sugestão de remediações — scripts de limpeza, correções de pipeline, políticas de governança e recomendações de prevenção — transforma diagnóstico em ação. Sem este agente, a auditoria seria apenas descritiva, sem prescriçoes para correção. A priorização por impacto × esforço e geração de scripts prontos é uma competência única.
- **Overlap:** Nenhum. Único agente que gera scripts de correção e recomendações de governança.

---

## Overlap Analysis

| Par de Agentes | Overlap | Decisão |
|---|---|---|
| Profiler ↔ AnomalyDetector | Mínimo (estatísticas vs detecção de anomalias) | Mantidos — domínios complementares |
| Profiler ↔ SchemaValidator | Zero (valores vs estrutura) | Mantidos — dimensões diferentes |
| AnomalyDetector ↔ SchemaValidator | Zero (valores anômalos vs schema/constraints) | Mantidos — responsabilidades distintas |
| QualityReporter ↔ RemediationSuggester | Zero (diagnóstico/relatório vs ação/correção) | Mantidos — responsabilidades distintas |
| Profiler ↔ QualityReporter | Mínimo (dados brutos vs relatório integrado) | Mantidos — pipeline producer/consumer |

---

## Conclusion

Todos os 5 agentes são **distintos e necessários**. Cada um cobre uma fase diferente do pipeline de qualidade de dados com responsabilidades bem definidas e sem overlap significativo. A remoção de qualquer agente resultaria em perda de capacidade crítica:

- Sem Profiler: impossível calcular estatísticas e baselines de qualidade
- Sem AnomalyDetector: impossível detectar outliers, drift e padrões anômalos
- Sem SchemaValidator: impossível validar integridade estrutural e detectar breaking changes
- Sem QualityReporter: impossível gerar relatórios integrados com scores e tendências
- Sem RemediationSuggester: auditoria apenas descritiva, sem ações corretivas
