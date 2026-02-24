# Token Specification — {TOKEN_NAME} ({TOKEN_SYMBOL})

## Identidade

| Campo | Valor |
|-------|-------|
| Nome | {TOKEN_NAME} |
| Símbolo | {TOKEN_SYMBOL} |
| Descrição | {DESCRIPTION} |
| Tipo | {memecoin / utility / governance} |

## Arquitetura Técnica

| Campo | Valor |
|-------|-------|
| Blockchain | Solana |
| Programa | {SPL Token / Token-2022} |
| Program ID | {PROGRAM_ID} |
| Decimais | {DECIMALS} |
| Supply Total | {TOTAL_SUPPLY} |

## Extensões Token-2022 (se aplicável)

| Extensão | Configuração |
|----------|-------------|
| transfer-fee | {basis_points} bps, max {max_fee} |
| metadata-pointer | {enabled/disabled} |
| {outras} | {config} |

## Autoridades

| Autoridade | Status | Ação Planejada |
|-----------|--------|----------------|
| Mint Authority | {Ativa/Revogada} | {Revogar após mint / Manter para inflação} |
| Freeze Authority | {Ativa/Revogada} | {Revogar antes do pool} |
| Update Authority | {Ativa/Revogada} | {Revogar após metadados finais} |

## Metadados

| Campo | Valor |
|-------|-------|
| Nome on-chain | {TOKEN_NAME} |
| Símbolo on-chain | {TOKEN_SYMBOL} |
| URI | {ARWEAVE_URI} |
| tokenStandard | Fungible |
| Imagem | {IMAGE_URI} |
| Storage | {Arweave / IPFS} |

## Links Sociais

| Plataforma | URL |
|-----------|-----|
| Website | {URL} |
| Twitter/X | {URL} |
| Telegram | {URL} |
| Discord | {URL} |

## Liquidez

| Campo | Valor |
|-------|-------|
| DEX | {Raydium / Orca / Meteora} |
| Tipo de Pool | {CPMM / CLMM / AMM V4} |
| Par | {TOKEN/SOL ou TOKEN/USDC} |
| Tokens no Pool | {amount} |
| SOL no Pool | {amount} |
| Preço Inicial | {price} SOL por token |
| Fee Tier | {0.25% / 1%} |

## Endereços (preenchido após deploy)

| Item | Endereço |
|------|----------|
| Token Mint | {MINT_ADDRESS} |
| Pool Address | {POOL_ADDRESS} |
| LP Token | {LP_TOKEN_ADDRESS} |

## Rede

| Ambiente | Status |
|----------|--------|
| Devnet | {Deployed / Pending} |
| Mainnet | {Deployed / Pending} |

---

*Gerado por @token-architect (Archon) — crypto-token-forge*
*Data: {DATE}*
