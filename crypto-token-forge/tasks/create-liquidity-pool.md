---
task: createLiquidityPool()
responsavel: "Orbit"
responsavel_type: Agente
atomic_layer: Organism
elicit: true

Entrada:
  - campo: tokenMintAddress
    tipo: string
    origen: "createSplToken() output"
    obrigatorio: true
  - campo: pairToken
    tipo: string
    origen: "Usuário (SOL ou USDC, padrão: SOL)"
    obrigatorio: false
  - campo: poolType
    tipo: string
    origen: "Usuário (cpmm, clmm, amm-v4, padrão: cpmm)"
    obrigatorio: false
  - campo: tokenAmount
    tipo: number
    origen: "tokenomics-strategist (alocação de liquidez)"
    obrigatorio: true
  - campo: solAmount
    tipo: number
    origen: "Usuário (quanto SOL depositar)"
    obrigatorio: true
  - campo: feeTier
    tipo: number
    origen: "Usuário (0.25% padrão)"
    obrigatorio: false

Saida:
  - campo: poolAddress
    tipo: string
    destino: "community-growth, launch-summary.md"
    persistido: true
  - campo: lpTokenAddress
    tipo: string
    destino: "security-auditor (para lock)"
    persistido: true
  - campo: initialPrice
    tipo: number
    destino: "launch-summary.md"
    persistido: true
  - campo: transactionHash
    tipo: string
    destino: "audit-report.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Token criado e supply mintado"
    - "[ ] Metadados on-chain configurados"
    - "[ ] Freeze Authority REVOGADA (obrigatório para Raydium)"
    - "[ ] SOL suficiente para taxas + liquidez"
    - "[ ] Token amount disponível na wallet"
  post-conditions:
    - "[ ] Pool criado no Raydium"
    - "[ ] LP tokens recebidos"
    - "[ ] Token swappable via Raydium"
    - "[ ] Token indexado no Jupiter (pode levar alguns minutos)"
    - "[ ] Preço inicial confirmado"
  acceptance-criteria:
    - blocker: true
      criteria: "Pool ativo e funcional no Raydium"
    - blocker: true
      criteria: "Token swappable (compra e venda funcionando)"
    - blocker: false
      criteria: "Token visível no Jupiter para swap"
    - blocker: false
      criteria: "Token listado no DexScreener"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "0.15-0.7 SOL (taxa de criação) + liquidez depositada"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "fixed(30s)"
  fallback: "Verificar se freeze authority foi revogada, verificar saldo SOL"
  notification: "crypto-orchestrator"

Metadata:
  version: "1.0.0"
  dependencies:
    - createSplToken()
    - setupMetadata()
    - securityAudit()
  author: "crypto-token-forge"
  created_at: "2026-02-24T00:00:00Z"
---

# Create Liquidity Pool

## Flow

```
1. Verificar pré-condições (freeze revogada, SOL suficiente)
2. Calcular preço inicial: solAmount / tokenAmount
3. Apresentar resumo ao usuário para confirmação
4. Acessar Raydium (raydium.io/liquidity/create-pool/)
5. Configurar pool (tipo, par, amounts, fee tier)
6. Confirmar transação
7. Registrar pool address e LP token address
8. Verificar swap funciona
9. Aguardar indexação no Jupiter
```

## Elicitation

- "Quanto SOL deseja depositar como liquidez? (mais SOL = menos slippage)"
- "Par de trading: SOL (recomendado) ou USDC?"
- "Tipo de pool: CPMM/Standard AMM (recomendado) ou CLMM?"
- "Taxa do pool: 0.25% (padrão) ou 1%?"

## Cálculo de Preço Inicial

```
Preço = SOL depositado / Tokens depositados

Exemplo:
  5 SOL + 1.000.000 tokens
  Preço = 5 / 1.000.000 = 0.000005 SOL por token
  Se SOL = $13 → preço do token = $0.000065
```

## Custos por Tipo de Pool

| Tipo | Taxa Protocolo | Taxa Rede | Total |
|------|---------------|-----------|-------|
| CPMM | 0.15 SOL | ~0.01 SOL | ~0.16 SOL |
| CLMM | 0 SOL | ~0.1 SOL | ~0.1 SOL |
| AMM V4 | ~0.3 SOL | ~0.3 SOL | ~0.6 SOL |
