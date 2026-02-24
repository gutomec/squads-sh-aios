---
task: identifyAhaMoment()
responsavel: "AhaFinder"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: product
    tipo: string
    origen: "Usuário — nome/descrição do produto SaaS"
    obrigatorio: true
  - campo: retentionData
    tipo: object
    origen: "trackUserBehavior() — dados de retenção por feature"
    obrigatorio: false
  - campo: segment
    tipo: string
    origen: "Usuário — segmento específico para análise"
    obrigatorio: false

Saida:
  - campo: ahaMomentReport
    tipo: file
    destino: "aha-moment-report.md, checklist-builder, tooltip-generator, proactive-outreach"
    persistido: true
  - campo: optimizedPath
    tipo: array
    destino: "tooltip-generator, checklist-builder"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Produto SaaS identificado"
    - "[ ] Dados comportamentais disponíveis (ou hipóteses)"
    - "[ ] Features do produto mapeadas"
  post-conditions:
    - "[ ] Aha moment identificado com dados"
    - "[ ] Caminho otimizado definido"
    - "[ ] Time-to-value calculado"
    - "[ ] aha-moment-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Aha moment identificado com correlação de retenção"
    - blocker: true
      criteria: "Caminho otimizado com máximo 5 etapas até o aha moment"
    - blocker: false
      criteria: "Variações por segmento identificadas"

Performance:
  duration_expected: "15-25 minutos"
  cost_estimated: "~0 (análise de dados existentes)"
  cacheable: true
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=20s)"
  fallback: "Se dados de retenção indisponíveis, usar hipóteses baseadas em benchmarks do setor"
  notification: "checklist-builder"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "saas-onboarding-activator"
  created_at: "2026-02-24T00:00:00Z"
---

# Identify Aha Moment

## Flow

```
1. Receber dados do produto e segmento
2. Mapear features e ações disponíveis no produto
3. Analisar correlação entre cada ação e retenção D7/D30/D90
4. Identificar aha moment candidatos (top 3-5 ações)
5. Validar com dados de cohort (quem fez vs quem não fez)
6. Selecionar aha moment principal por segmento
7. Mapear caminho atual vs caminho otimizado
8. Calcular time-to-value atual e projetado
9. Gerar aha-moment-report.md
10. Enviar para checklist-builder e tooltip-generator
```

## Elicitation

- "Qual o produto SaaS alvo?"
- "Quais são as principais features do produto?"
- "Existem dados de retenção por feature disponíveis?"
- "Qual o segmento de usuários para análise?"
- "Qual a taxa de ativação atual?"
