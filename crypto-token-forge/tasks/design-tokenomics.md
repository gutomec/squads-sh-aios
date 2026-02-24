---
task: designTokenomics()
responsavel: "Nomics"
responsavel_type: Agente
atomic_layer: Molecule
elicit: true

Entrada:
  - campo: projectConcept
    tipo: string
    origen: "Usuário ou fullTokenLaunch() fase 1"
    obrigatorio: true
  - campo: tokenType
    tipo: string
    origen: "Usuário (memecoin, utility, governance)"
    obrigatorio: true
  - campo: totalSupply
    tipo: number
    origen: "Usuário (opcional — sugestão automática por tipo)"
    obrigatorio: false

Saida:
  - campo: tokenomicsYaml
    tipo: file
    destino: "tokenomics.yaml, token-architect, defi-launcher"
    persistido: true
  - campo: distributionChart
    tipo: object
    destino: "launch-summary.md"
    persistido: true
  - campo: vestingSchedule
    tipo: object
    destino: "tokenomics.yaml"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Conceito do projeto definido"
    - "[ ] Tipo de token escolhido"
  post-conditions:
    - "[ ] tokenomics.yaml gerado com todas as categorias"
    - "[ ] Distribuição soma 100%"
    - "[ ] Time + investidores <= 40%"
    - "[ ] Comunidade >= 30%"
    - "[ ] Vesting schedule definido para time e investidores"
  acceptance-criteria:
    - blocker: true
      criteria: "Distribuição completa soma exatamente 100%"
    - blocker: true
      criteria: "Time + investidores não excedem 40%"
    - blocker: true
      criteria: "Vesting para time com cliff >= 12 meses"

Performance:
  duration_expected: "15-30 minutos"
  cost_estimated: "~0 SOL (off-chain design)"
  cacheable: true
  parallelizable: false

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "crypto-token-forge"
  created_at: "2026-02-24T00:00:00Z"
---

# Design Tokenomics

## Flow

```
1. Receber conceito e tipo do token
2. Sugerir supply total baseado no tipo
3. Projetar distribuição por categoria
4. Definir vesting schedules
5. Calcular projeções de circulação
6. Gerar tokenomics.yaml
7. Apresentar para aprovação do usuário
```

## Elicitation

- "Qual o conceito/propósito do seu token?"
- "Tipo: memecoin, utility ou governance?"
- "Supply total desejado? (sugestão: 1B para memecoin, 100M para utility, 10M para governance)"
- "Vai ter staking rewards? Se sim, qual APY desejado?"
- "Vai ter mecanismo de burn?"
- "Haverá pré-venda ou rodadas de investimento?"
