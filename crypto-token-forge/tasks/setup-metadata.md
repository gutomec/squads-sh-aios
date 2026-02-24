---
task: setupMetadata()
responsavel: "Meta"
responsavel_type: Agente
atomic_layer: Organism
elicit: true

Entrada:
  - campo: tokenMintAddress
    tipo: string
    origen: "createSplToken() output"
    obrigatorio: true
  - campo: tokenName
    tipo: string
    origen: "Usuário ou fullTokenLaunch()"
    obrigatorio: true
  - campo: tokenSymbol
    tipo: string
    origen: "Usuário ou fullTokenLaunch()"
    obrigatorio: true
  - campo: tokenDescription
    tipo: string
    origen: "Usuário"
    obrigatorio: true
  - campo: tokenImage
    tipo: file
    origen: "Usuário ou gerada via AI (nano-banana-pro/dalle3)"
    obrigatorio: true
  - campo: socialLinks
    tipo: object
    origen: "Usuário (website, twitter, telegram, discord)"
    obrigatorio: false

Saida:
  - campo: imageUri
    tipo: string
    destino: "JSON de metadados off-chain"
    persistido: true
  - campo: jsonUri
    tipo: string
    destino: "Metaplex on-chain metadata"
    persistido: true
  - campo: metadataTransactionHash
    tipo: string
    destino: "audit-report.md"
    persistido: true
  - campo: offChainJson
    tipo: file
    destino: "Arweave/IPFS"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Token mint address válido"
    - "[ ] Imagem do token disponível (PNG/WebP, < 100KB)"
    - "[ ] Nome e símbolo definidos"
  post-conditions:
    - "[ ] Imagem uploaded para Arweave/IPFS"
    - "[ ] JSON de metadados uploaded para Arweave/IPFS"
    - "[ ] Metadados on-chain via Metaplex"
    - "[ ] Token exibe nome e logo na Phantom"
    - "[ ] tokenStandard = Fungible"
  acceptance-criteria:
    - blocker: true
      criteria: "Token exibe nome correto na Phantom Wallet"
    - blocker: true
      criteria: "Token exibe logo/imagem na Phantom Wallet"
    - blocker: true
      criteria: "Token aparece na aba Home (não Collectibles)"
    - blocker: false
      criteria: "Token visível no Solscan com metadados"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0.01-0.05 SOL (upload + on-chain)"
  cacheable: false
  parallelizable: false

Metadata:
  version: "1.0.0"
  dependencies:
    - createSplToken()
  author: "crypto-token-forge"
  created_at: "2026-02-24T00:00:00Z"
---

# Setup Metadata

## Flow

```
1. Receber token address e informações do projeto
2. Preparar imagem (resize se necessário, < 100KB)
3. Upload imagem → Arweave (via Akord/Irys) ou IPFS (via Pinata)
4. Criar JSON de metadados off-chain com image URI
5. Upload JSON → Arweave/IPFS
6. Deploy metadados on-chain:
   - Token-2022: spl-token initialize-metadata
   - SPL Token: metaboss create metadata
7. Verificar exibição na Phantom e Solscan
```

## Elicitation

- "Tem uma imagem/logo para o token? (Se não, posso gerar via AI)"
- "Descrição do token (1-2 frases):"
- "Links sociais? (website, twitter, telegram, discord)"
- "Onde hospedar metadados? (Arweave recomendado, IPFS alternativa)"

## Formato do JSON Off-Chain

```json
{
  "name": "Token Name",
  "symbol": "TKN",
  "description": "Descrição do token e seu propósito",
  "image": "https://arweave.net/IMAGE_HASH",
  "extensions": {
    "website": "https://example.com",
    "twitter": "https://x.com/token",
    "telegram": "https://t.me/token",
    "discord": "https://discord.gg/token"
  }
}
```
