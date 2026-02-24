---
task: suggestRemediation()
responsavel: "RemediationSuggester"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: qualityReport
    tipo: file
    origen: "generateQualityReport() — relatório de qualidade"
    obrigatorio: true
  - campo: priority
    tipo: string
    origen: "Usuário — foco de remediação (critical-only, all, preventive)"
    obrigatorio: false

Saida:
  - campo: remediationPlan
    tipo: file
    destino: "remediation-plan.md, data engineering team"
    persistido: true
  - campo: cleaningScripts
    tipo: array
    destino: "data engineering team — scripts prontos"
    persistido: true
  - campo: governanceRecommendations
    tipo: array
    destino: "governance team — políticas recomendadas"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Relatório de qualidade disponível"
    - "[ ] Problemas identificados e priorizados"
  post-conditions:
    - "[ ] Plano de remediação criado"
    - "[ ] Scripts de limpeza gerados"
    - "[ ] Recomendações de governança incluídas"
    - "[ ] remediation-plan.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Remediações priorizadas por impacto × esforço"
    - blocker: true
      criteria: "Scripts automatizáveis incluídos quando possível"
    - blocker: false
      criteria: "Recomendações de prevenção para causa raiz"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0 (geração de recomendações)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se relatório incompleto, gerar remediações para problemas com dados suficientes"
  notification: "data-quality-reporter"

Metadata:
  version: "1.0.0"
  dependencies:
    - generateQualityReport()
  author: "data-quality-guardian"
  created_at: "2026-02-24T00:00:00Z"
---

# Suggest Remediation

## Flow

```
1. Receber relatório de qualidade com problemas
2. Analisar problemas por categoria (dados, schema, pipeline, governança)
3. Priorizar por impacto (dados afetados) × esforço (complexidade)
4. Gerar scripts de limpeza automatizados (Python, SQL, dbt)
5. Definir correções manuais quando necessário
6. Recomendar políticas de governança e prevenção
7. Estimar impacto da remediação (% de dados corrigidos)
8. Gerar remediation-plan.md
9. Enviar para equipe de dados
```

## Elicitation

- "Qual o foco de remediação? (critical-only, all, preventive)"
- "Qual a linguagem preferida para scripts? (Python, SQL, dbt)"
- "Há restrições de janela de execução para correções?"
- "Deseja incluir recomendações de governança?"
