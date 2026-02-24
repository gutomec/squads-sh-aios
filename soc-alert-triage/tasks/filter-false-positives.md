---
task: filterFalsePositives()
responsavel: "FPFilter"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: classifiedAlerts
    tipo: array
    origen: "classifyAlerts() — alertas classificados"
    obrigatorio: true

Saida:
  - campo: filteredAlerts
    tipo: array
    destino: "threat-prioritizer, context-enricher"
    persistido: true
  - campo: fpReport
    tipo: file
    destino: "fp-analysis-report.md, analyst-brief-generator"
    persistido: true
  - campo: tuningRecommendations
    tipo: array
    destino: "SIEM admin — regras para tuning"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Alertas classificados disponíveis"
  post-conditions:
    - "[ ] Falsos positivos identificados e documentados"
    - "[ ] Alertas reais filtrados e prontos para priorização"
    - "[ ] Recomendações de tuning geradas"
    - "[ ] fp-analysis-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Cada FP com justificativa documentada"
    - blocker: true
      criteria: "Taxa de falso negativo < 1%"
    - blocker: false
      criteria: "Recomendações de tuning para redução futura"

Performance:
  duration_expected: "5-10 minutos"
  cost_estimated: "~0 (processamento local)"
  cacheable: false
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se baseline indisponível, manter todos os alertas como reais (fail-safe)"
  notification: "threat-prioritizer"

Metadata:
  version: "1.0.0"
  dependencies:
    - classifyAlerts()
  author: "soc-alert-triage"
  created_at: "2026-02-24T00:00:00Z"
---

# Filter False Positives

## Flow

```
1. Receber alertas classificados do @alert-classifier
2. Comparar com baselines comportamentais
3. Verificar whitelists e padrões benignos conhecidos
4. Analisar contexto (horário, usuário, ativo)
5. Marcar falsos positivos com justificativa documentada
6. Separar alertas reais dos falsos positivos
7. Gerar recomendações de tuning para regras SIEM
8. Gerar fp-analysis-report.md
9. Enviar alertas reais para @threat-prioritizer
```

## Elicitation

- "Há whitelists ou baselines específicos da organização?"
- "Existe janela de manutenção ativa que possa gerar FPs?"
- "Houve testes de penetração autorizados recentemente?"
