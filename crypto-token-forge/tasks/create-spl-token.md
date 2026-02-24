---
task: createSplToken()
responsavel: "Helix"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: tokenSpec
    tipo: object
    origen: "token-architect (token-spec.yaml) ou fullTokenLaunch()"
    obrigatorio: true
  - campo: program
    tipo: string
    origen: "token-architect (spl ou token-2022)"
    obrigatorio: true
  - campo: decimals
    tipo: number
    origen: "token-architect (padrão: 6)"
    obrigatorio: true
  - campo: supply
    tipo: number
    origen: "tokenomics-strategist (supply total)"
    obrigatorio: true
  - campo: network
    tipo: string
    origen: "crypto-orchestrator (devnet ou mainnet)"
    obrigatorio: true
  - campo: extensions
    tipo: array
    origen: "token-architect (extensões Token-2022)"
    obrigatorio: false

Saida:
  - campo: tokenMintAddress
    tipo: string
    destino: "metadata-artist, security-auditor, defi-launcher"
    persistido: true
  - campo: tokenAccountAddress
    tipo: string
    destino: "security-auditor"
    persistido: true
  - campo: transactionSignatures
    tipo: array
    destino: "audit-report.md"
    persistido: true
  - campo: supplyConfirmation
    tipo: object
    destino: "launch-summary.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Solana CLI configurado para rede correta (devnet/mainnet)"
    - "[ ] Wallet com SOL suficiente"
    - "[ ] spl-token-cli instalado"
    - "[ ] Especificação do token definida (programa, decimais, supply)"
  post-conditions:
    - "[ ] Token criado — mint address confirmado"
    - "[ ] Token account criada"
    - "[ ] Supply mintado e verificado"
    - "[ ] Transaction signatures logadas"
  acceptance-criteria:
    - blocker: true
      criteria: "Token mint address válido e verificável no explorer"
    - blocker: true
      criteria: "Supply mintado corresponde ao especificado"

Performance:
  duration_expected: "5-10 minutos"
  cost_estimated: "~0.01 SOL (devnet: grátis)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=2s, max=30s)"
  fallback: "Verificar saldo SOL, verificar rede, retry manual"
  notification: "crypto-orchestrator"

Metadata:
  version: "1.0.0"
  dependencies:
    - designTokenomics()
  author: "crypto-token-forge"
  created_at: "2026-02-24T00:00:00Z"
---

# Create SPL Token

## Flow

```
1. Verificar pré-condições (CLI, SOL, rede)
2. Criar token (spl-token create-token)
3. Criar token account (spl-token create-account)
4. Mintar supply (spl-token mint)
5. Verificar supply (spl-token supply)
6. Logar transaction signatures
7. Reportar mint address ao pipeline
```

## Comandos por Programa

### SPL Token (clássico)
```bash
spl-token create-token --decimals {decimals}
spl-token create-account {TOKEN}
spl-token mint {TOKEN} {SUPPLY}
```

### Token-2022
```bash
spl-token create-token \
  --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb \
  --enable-metadata \
  --decimals {decimals}

spl-token initialize-metadata {TOKEN} "{NAME}" "{SYMBOL}" "{URI}"
spl-token create-account {TOKEN}
spl-token mint {TOKEN} {SUPPLY}
```

### Token-2022 com Transfer Fee
```bash
spl-token create-token \
  --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb \
  --enable-metadata \
  --transfer-fee {BASIS_POINTS} {MAX_FEE} \
  --decimals {decimals}
```
