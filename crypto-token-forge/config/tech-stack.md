# Tech Stack — crypto-token-forge

## Blockchain
- **Solana** — Blockchain principal (alta velocidade, baixo custo)
- **SPL Token Program** — Programa padrão de tokens (`TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA`)
- **Token-2022 Program** — Programa estendido com extensions (`TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb`)

## CLI Tools
- **Solana CLI** (solana-cli 3.x) — Gestão de wallets, config, rede
- **SPL Token CLI** (spl-token-cli) — Criação e gestão de tokens
- **Metaboss** — Criação e update de metadados Metaplex
- **Anchor CLI** — Framework de smart contracts Solana (opcional)

## SDKs & Libraries
- **@metaplex-foundation/umi** — Framework universal de interação Metaplex
- **@metaplex-foundation/mpl-token-metadata** — Metadados de tokens
- **@solana/web3.js** — SDK JavaScript para Solana
- **@solana/spl-token** — SDK para interação com Token Program

## Armazenamento Descentralizado
- **Arweave** (via Irys/Bundlr) — Armazenamento permanente (metadados, imagens)
- **IPFS** (via Pinata) — Armazenamento descentralizado alternativo

## DEXs & DeFi
- **Raydium** — DEX principal para criação de pools de liquidez
- **Jupiter** — Agregador DEX dominante na Solana
- **PumpSwap** — DEX nativa do Pump.fun (pós-graduação)
- **Orca** — DEX alternativa
- **Meteora** — DEX com pools dinâmicos

## Wallets
- **Phantom** — Wallet principal do ecossistema Solana
- **Solflare** — Wallet alternativa

## Explorers & Analytics
- **Solscan** — Explorer principal
- **DexScreener** — Rastreamento de trading em DEXs
- **Birdeye** — Analytics de tokens Solana
- **RugCheck** — Verificação de segurança de tokens

## Plataformas No-Code
- **Pump.fun** — Launchpad de memecoins (gratuito)
- **Smithii** — Criação de tokens e lock de LP
- **CoinFactory** — Gerador de tokens SPL

## Lock & Vesting
- **Streamflow** — Lock de LP tokens e vesting
- **Smithii Token Locker** — Lock simples (0.01 SOL)
- **StakePoint** — Lock de LP Raydium/Meteora
