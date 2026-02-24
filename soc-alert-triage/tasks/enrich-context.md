---
task: enrichContext()
responsavel: "Enricher"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: prioritizedAlerts
    tipo: array
    origen: "prioritizeThreats() — alertas priorizados por risk score"
    obrigatorio: true
  - campo: depth
    tipo: string
    origen: "Usuário — nível de enriquecimento (basic, standard, deep)"
    obrigatorio: false

Saida:
  - campo: enrichedAlerts
    tipo: array
    destino: "analyst-brief-generator"
    persistido: true
  - campo: iocReport
    tipo: file
    destino: "ioc-report.md, analyst-brief-generator"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Alertas priorizados disponíveis"
    - "[ ] Acesso a feeds de threat intel"
  post-conditions:
    - "[ ] IOCs extraídos e correlacionados"
    - "[ ] MITRE ATT&CK mapping completo"
    - "[ ] Contexto histórico adicionado"
    - "[ ] ioc-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "IOCs extraídos para todos os alertas critical/high"
    - blocker: true
      criteria: "MITRE ATT&CK mapping completo (tactic + technique + sub-technique)"
    - blocker: false
      criteria: "Correlação com threat intel feeds externos"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0 (consulta a feeds de threat intel)"
  cacheable: true
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se feed de threat intel indisponível, usar feeds alternativos disponíveis"
  notification: "analyst-brief-generator"

Metadata:
  version: "1.0.0"
  dependencies:
    - prioritizeThreats()
  author: "soc-alert-triage"
  created_at: "2026-02-24T00:00:00Z"
---

# Enrich Context

## Flow

```
1. Receber alertas priorizados do @threat-prioritizer
2. Extrair IOCs (IPs, hashes, domínios, URLs)
3. Consultar threat intel feeds (VirusTotal, AbuseIPDB, MISP, OTX)
4. Verificar reputation scores em múltiplas fontes
5. Mapear MITRE ATT&CK completo (tática + técnica + sub-técnica)
6. Adicionar geolocalização e ASN para IPs suspeitos
7. Correlacionar com histórico de incidentes anteriores
8. Gerar ioc-report.md com todas as correlações
9. Enviar alertas enriquecidos para @analyst-brief-generator
```

## Elicitation

- "Quais feeds de threat intel estão disponíveis?"
- "Qual o nível de detalhe desejado? (basic, standard, deep)"
- "Há IOCs específicos já conhecidos para correlacionar?"
