# incident-response-squad

Squad especialista em resposta a incidentes para DevOps/SRE.

## Visão Geral

O **incident-response-squad** é um squad completo que cobre todo o pipeline de resposta a incidentes:

1. **Análise de Logs** — Agregação e análise de logs de múltiplas fontes (CloudWatch, ELK, Splunk, Datadog)
2. **Correlação de Causa Raiz** — Correlação de sinais de 20-45 ferramentas de monitoramento, mapeamento de blast radius
3. **Execução de Runbooks** — Runbooks automatizados para rollback, scaling, restart e remediação
4. **Comunicação de Status** — Atualização de status pages e notificação de stakeholders
5. **Post-Mortem** — Geração de documentos blameless com timeline, action items e lições aprendidas

**Pain Point:** 65% do tempo de resolução é gasto diagnosticando a causa raiz; empresas gerenciam 20-45 ferramentas de monitoramento.

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 📋 LogAnalyzer | `log-analyzer` | Analisador de logs multi-source |
| 🔍 Correlator | `root-cause-correlator` | Correlacionador de causa raiz e blast radius |
| ⚡ RunbookExec | `runbook-executor` | Executor de runbooks de remediação |
| 📢 StatusUpdater | `status-page-updater` | Gestor de comunicação e status page |
| 📝 PostMortem | `postmortem-writer` | Gerador de post-mortem blameless |

## Workflows

| Workflow | Comando | Descrição | Duração |
|---|---|---|---|
| Full Incident Response | `*respond-incident` | Pipeline completo: do alerta ao post-mortem | 30-90 min |
| Rapid Triage | `*triage-incident` | Triagem rápida: análise, causa raiz, comunicação | 10-20 min |

## Comandos Disponíveis

| Comando | Agente | Descrição |
|---|---|---|
| `*analyze-logs` | LogAnalyzer | Analisar logs de um incidente |
| `*search-logs` | LogAnalyzer | Buscar padrão específico nos logs |
| `*correlate-signals` | Correlator | Correlacionar sinais de múltiplas fontes |
| `*find-root-cause` | Correlator | Identificar causa raiz mais provável |
| `*execute-runbook` | RunbookExec | Executar runbook de remediação |
| `*list-runbooks` | RunbookExec | Listar runbooks disponíveis |
| `*update-status` | StatusUpdater | Atualizar status page |
| `*notify-stakeholders` | StatusUpdater | Notificar stakeholders |
| `*write-postmortem` | PostMortem | Gerar post-mortem blameless |
| `*generate-timeline` | PostMortem | Gerar timeline do incidente |

## Quick Start

```
# Ativar o correlacionador (orquestrador principal)
/irs:agents:root-cause-correlator

# Pipeline completo de resposta a incidente
*respond-incident

# Triagem rápida
*triage-incident

# Apenas análise de logs
*analyze-logs

# Apenas post-mortem
*write-postmortem
```

## Público Alvo

- SREs (Site Reliability Engineers)
- Engenheiros de DevOps
- Engenheiros de on-call
- CTOs e líderes técnicos

## Requisitos

- Acesso a ferramentas de monitoramento (Datadog, Prometheus, Grafana)
- Acesso a plataformas de log (ELK, Splunk, CloudWatch)
- Acesso ao status page (Statuspage.io, Atlassian)
- Canal de comunicação configurado (Slack #incidents)
