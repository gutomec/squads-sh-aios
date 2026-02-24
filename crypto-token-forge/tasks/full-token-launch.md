---
task: fullTokenLaunch()
responsavel: "Forge"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: projectConcept
    tipo: string
    origen: "Usuário (descrição do projeto e propósito do token)"
    obrigatorio: true
  - campo: tokenName
    tipo: string
    origen: "Usuário"
    obrigatorio: true
  - campo: tokenSymbol
    tipo: string
    origen: "Usuário"
    obrigatorio: true
  - campo: tokenType
    tipo: string
    origen: "Usuário (memecoin, utility, governance)"
    obrigatorio: true
  - campo: network
    tipo: string
    origen: "Usuário (devnet ou mainnet, padrão: devnet)"
    obrigatorio: false

Saida:
  - campo: tokenMintAddress
    tipo: string
    destino: "Usuário, audit-report.md"
    persistido: true
  - campo: poolAddress
    tipo: string
    destino: "Usuário, growth-plan.md"
    persistido: true
  - campo: tokenomicsYaml
    tipo: file
    destino: "tokenomics.yaml"
    persistido: true
  - campo: auditReport
    tipo: file
    destino: "audit-report.md"
    persistido: true
  - campo: launchSummary
    tipo: file
    destino: "launch-summary.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Solana CLI instalado e configurado"
    - "[ ] spl-token-cli instalado"
    - "[ ] Metaboss instalado"
    - "[ ] Wallet com SOL suficiente (devnet: airdrop / mainnet: SOL real)"
    - "[ ] Conceito do projeto definido"
  post-conditions:
    - "[ ] Token criado com mint address confirmado"
    - "[ ] Metadados on-chain — token exibe nome/logo na Phantom"
    - "[ ] Autoridades revogadas (mint, freeze)"
    - "[ ] Pool de liquidez ativo no Raydium"
    - "[ ] Token swappable via Jupiter"
    - "[ ] Audit report gerado com status PASSED"
    - "[ ] Estratégia de growth definida"
  acceptance-criteria:
    - blocker: true
      criteria: "Token criado e mintado com supply correto"
    - blocker: true
      criteria: "Metadados visíveis na Phantom (nome, símbolo, logo)"
    - blocker: true
      criteria: "Autoridades de mint e freeze revogadas"
    - blocker: true
      criteria: "Pool de liquidez ativo e token swappable"
    - blocker: false
      criteria: "LP tokens locked ou burned"
    - blocker: false
      criteria: "Token verificado no Jupiter"

Performance:
  duration_expected: "1-3 horas (devnet) / 2-4 horas (mainnet)"
  cost_estimated: "~1-5 SOL (taxas) + liquidez depositada"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=60s)"
  fallback: "Pausar pipeline, reportar erro com transaction hash e contexto"
  notification: "crypto-orchestrator"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "crypto-token-forge"
  created_at: "2026-02-24T00:00:00Z"
---

# Full Token Launch

## Pipeline

```
Fase 1: Tokenomics     → @tokenomics-strategist → designTokenomics()
Fase 2: Arquitetura     → @token-architect       → (design decisions)
Fase 3: Desenvolvimento → @solana-dev            → createSplToken()
Fase 4: Metadados       → @metadata-artist       → setupMetadata()
Fase 5: Segurança       → @security-auditor      → securityAudit()
Fase 6: Mainnet Deploy  → @solana-dev            → (deploy mainnet)
Fase 7: Liquidez        → @defi-launcher         → createLiquidityPool()
Fase 8: Comunidade      → @community-growth      → communityStrategy()
```

## Elicitation

### Fase 1 — Conceito
- "Qual o propósito/conceito do token?"
- "Qual o tipo? (memecoin, utility, governance)"
- "Nome e símbolo desejados?"

### Fase 2 — Arquitetura
- "Precisa de transfer fees? (Token-2022)"
- "Supply fixo ou inflacionário?"
- "Quantos decimais? (6 padrão)"

### Fase 7 — Liquidez
- "Quanto SOL deseja depositar como liquidez inicial?"
- "Par de trading: SOL ou USDC?"
- "Tipo de pool: CPMM (recomendado) ou CLMM?"

### Fase Final — Confirmação
- "Deseja deployar na mainnet? (confirmar com SOL real)"
