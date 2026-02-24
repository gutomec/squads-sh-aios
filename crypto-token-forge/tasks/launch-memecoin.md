---
task: launchMemecoin()
responsavel: "Forge"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: name
    tipo: string
    origen: "Usuário"
    obrigatorio: true
  - campo: ticker
    tipo: string
    origen: "Usuário"
    obrigatorio: true
  - campo: description
    tipo: string
    origen: "Usuário"
    obrigatorio: true
  - campo: image
    tipo: file
    origen: "Usuário ou gerada via AI"
    obrigatorio: true
  - campo: platform
    tipo: string
    origen: "Usuário (pumpfun ou manual, padrão: pumpfun)"
    obrigatorio: false

Saida:
  - campo: tokenAddress
    tipo: string
    destino: "Usuário"
    persistido: true
  - campo: tradingLink
    tipo: string
    destino: "Usuário, community-growth"
    persistido: true
  - campo: launchSummary
    tipo: file
    destino: "launch-summary.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Nome e ticker definidos"
    - "[ ] Imagem/logo disponível"
    - "[ ] Phantom Wallet conectada com SOL"
  post-conditions:
    - "[ ] Token criado na plataforma"
    - "[ ] Token negociável (bonding curve ou pool)"
    - "[ ] Link de trading gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Token criado e negociável"
    - blocker: true
      criteria: "Link de trading funcional"
    - blocker: false
      criteria: "Token com metadados visíveis"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "0 SOL (Pump.fun gratuito) + SOL para comprar na curve"
  cacheable: false
  parallelizable: false

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "crypto-token-forge"
  created_at: "2026-02-24T00:00:00Z"
---

# Launch Memecoin

## Flow

### Via Pump.fun (Recomendado)

```
1. Acessar pump.fun
2. Conectar Phantom Wallet
3. Clicar "Start a new coin"
4. Preencher: nome, ticker, descrição
5. Upload da imagem
6. (Opcional) Adicionar links sociais
7. Clicar "Create Coin"
8. Aprovar transação na Phantom
9. Token criado na bonding curve!
10. Compartilhar link para comunidade comprar
```

### Via Manual (Controle Total)

```
1. designTokenomics() — supply 1B, comunidade 80-90%
2. createSplToken() — SPL Token clássico, 6 decimais
3. setupMetadata() — nome, logo, descrição
4. securityAudit() — revogar mint + freeze
5. createLiquidityPool() — Raydium CPMM com SOL
```

## Elicitation

- "Nome da memecoin:"
- "Ticker/símbolo:"
- "Descrição curta (1 frase):"
- "Tem imagem? (Se não, posso gerar via AI)"
- "Plataforma: Pump.fun (gratuito, fácil) ou manual (controle total)?"
- "Se Pump.fun: quanto SOL quer comprar na bonding curve inicialmente?"

## Graduação Pump.fun

O token criado no Pump.fun inicia na bonding curve. Quando atinge ~$69K market cap:
- Migra automaticamente para PumpSwap (DEX)
- Pool de liquidez criado automaticamente
- Indexado no Jupiter
- Visível na Phantom para swap

> A maioria dos tokens NUNCA gradua. Sucesso depende de comunidade e narrativa.
