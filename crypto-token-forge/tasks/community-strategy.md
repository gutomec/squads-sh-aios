---
task: communityStrategy()
responsavel: "Pulse"
responsavel_type: Agente
atomic_layer: Molecule
elicit: true

Entrada:
  - campo: projectInfo
    tipo: object
    origen: "fullTokenLaunch() ou Usuário"
    obrigatorio: true
  - campo: tokenAddress
    tipo: string
    origen: "createSplToken() output"
    obrigatorio: true
  - campo: poolAddress
    tipo: string
    origen: "createLiquidityPool() output"
    obrigatorio: false
  - campo: auditReport
    tipo: file
    origen: "securityAudit() output"
    obrigatorio: false
  - campo: tokenomicsYaml
    tipo: file
    origen: "designTokenomics() output"
    obrigatorio: false

Saida:
  - campo: growthPlan
    tipo: file
    destino: "growth-plan.md"
    persistido: true
  - campo: airdropStrategy
    tipo: object
    destino: "growth-plan.md"
    persistido: true
  - campo: channelLinks
    tipo: object
    destino: "launch-summary.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Token criado e negociável"
    - "[ ] Audit report com score PASSED ou CONCERNS"
    - "[ ] Pool de liquidez ativo (se aplicável)"
  post-conditions:
    - "[ ] growth-plan.md gerado"
    - "[ ] Canais de comunicação definidos"
    - "[ ] Estratégia de airdrop definida (se aplicável)"
    - "[ ] Plano de verificação Jupiter definido"
  acceptance-criteria:
    - blocker: true
      criteria: "growth-plan.md gerado com estratégia completa"
    - blocker: false
      criteria: "Canais de comunicação criados"
    - blocker: false
      criteria: "Primeira campanha de awareness planejada"

Performance:
  duration_expected: "20-40 minutos"
  cost_estimated: "~0 SOL (planejamento off-chain)"
  cacheable: true
  parallelizable: true

Metadata:
  version: "1.0.0"
  dependencies:
    - createSplToken()
    - securityAudit()
  author: "crypto-token-forge"
  created_at: "2026-02-24T00:00:00Z"
---

# Community Strategy

## Flow

```
1. Analisar projeto, token e público-alvo
2. Definir canais de comunicação
3. Projetar estratégia de airdrop
4. Planejar campanhas de awareness
5. Definir cronograma de verificações (Jupiter, CoinGecko)
6. Gerar growth-plan.md
```

## Elicitation

- "Qual o público-alvo do token? (devs, traders, comunidade geral)"
- "Já tem comunidade existente? (Discord, Telegram, Twitter)"
- "Budget para marketing? (0 = orgânico puro)"
- "Deseja fazer airdrop? Se sim, que % do supply?"
- "Tem influenciadores ou parceiros identificados?"

## Estratégia por Tipo de Token

### Memecoin
- Foco: viralidade, memes, cultura
- Canais: Twitter/X, Telegram, Reddit
- Tática: airdrop amplo, meme contests, influenciadores
- Timeline: 1-2 semanas de buzz pré-lançamento

### Utility Token
- Foco: valor do produto, cases de uso
- Canais: Discord (dev community), Twitter, Medium
- Tática: early adopter program, docs, demos
- Timeline: 1-3 meses de construção de comunidade

### Governance Token
- Foco: descentralização, participação
- Canais: Discord (governance forum), Snapshot
- Tática: propostas iniciais, delegados, grants
- Timeline: 3-6 meses de governança progressiva

## Plataformas de Verificação

| Plataforma | Processo | Custo |
|---|---|---|
| Jupiter VRFD | Standard (gratuito) ou Express (1000 JUP) | 0 ou ~$1000 |
| CoinGecko | Formulário manual | Gratuito |
| CoinMarketCap | Formulário manual | Gratuito |
| DexScreener | Automático | Gratuito |
| Birdeye | Automático | Gratuito |
