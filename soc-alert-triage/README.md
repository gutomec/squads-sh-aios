# soc-alert-triage

Squad especialista em triagem de alertas SOC para cybersecurity.

## Visão Geral

O **soc-alert-triage** é um squad completo que cobre todo o pipeline de triagem de alertas de segurança:

1. **Classificação de Alertas** — Categorização automatizada por tipo, severidade e mapeamento MITRE ATT&CK de múltiplas fontes (SIEM, IDS, EDR, cloud)
2. **Filtragem de Falsos Positivos** — Identificação e filtragem de FPs usando padrões históricos, baselines comportamentais e whitelists contextuais
3. **Priorização de Ameaças** — Risk scoring baseado em exploitability, blast radius, criticidade de ativos e impacto no negócio
4. **Enriquecimento com Threat Intel** — IOCs, mapeamento MITRE ATT&CK completo, reputation scores e correlação histórica
5. **Geração de Briefs** — Documentos acionáveis com timeline, playbook recomendado, IOCs e ações de resposta priorizadas

**Pain Point:** Analistas SOC enfrentam +4.000 alertas/dia, com 80%+ sendo falsos positivos — gerando alert fatigue, burnout e risco de miss de ameaças reais.

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 🏷️ Classifier | `alert-classifier` | Classificador de alertas por tipo, severidade e MITRE ATT&CK |
| 🛡️ FPFilter | `false-positive-filter` | Filtro de falsos positivos com baselines e heurísticas |
| ⚡ Prioritizer | `threat-prioritizer` | Priorizador de ameaças por risk score composto |
| 🔍 Enricher | `context-enricher` | Enriquecedor de contexto com IOCs e threat intel |
| 📊 BriefGen | `analyst-brief-generator` | Gerador de briefs acionáveis para analistas SOC |

## Workflows

| Workflow | Comando | Descrição | Duração |
|---|---|---|---|
| Full Alert Triage | `*triage-full` | Pipeline completo: da classificação ao brief | 30-60 min |
| Rapid Classification | `*rapid-classify` | Classificação rápida: classificação, filtragem e brief | 10-20 min |

## Comandos Disponíveis

| Comando | Agente | Descrição |
|---|---|---|
| `*classify-alerts` | Classifier | Classificar batch de alertas de segurança |
| `*classify-single` | Classifier | Classificar um alerta específico |
| `*filter-fps` | FPFilter | Filtrar falsos positivos de um batch |
| `*check-fp` | FPFilter | Verificar se alerta é falso positivo |
| `*prioritize` | Prioritizer | Priorizar ameaças por risk score |
| `*risk-score` | Prioritizer | Calcular risk score de ameaça específica |
| `*triage-full` | Prioritizer | Pipeline completo de triagem |
| `*enrich` | Enricher | Enriquecer alertas com contexto e threat intel |
| `*ioc-lookup` | Enricher | Buscar IOC em feeds de threat intel |
| `*generate-brief` | BriefGen | Gerar brief para analista SOC |
| `*incident-summary` | BriefGen | Gerar sumário executivo de incidente |

## Quick Start

```
# Ativar o priorizador (orquestrador principal)
/sat:agents:threat-prioritizer

# Pipeline completo de triagem de alertas
*triage-full

# Classificação rápida
*rapid-classify

# Apenas classificação de alertas
*classify-alerts

# Apenas geração de brief
*generate-brief
```

## Público Alvo

- Analistas SOC (L1, L2, L3)
- Engenheiros de Segurança
- Threat Hunters
- CISOs e líderes de segurança
- Equipes de Incident Response

## Requisitos

- Acesso a SIEM (Splunk, QRadar, Sentinel, Elastic SIEM)
- Acesso a feeds de threat intel (VirusTotal, AbuseIPDB, MISP)
- Acesso a ferramentas de EDR (CrowdStrike, SentinelOne, Defender)
- Framework MITRE ATT&CK como referência de taxonomia
