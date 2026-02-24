# Coding Standards — crypto-token-forge

## Linguagem
- TypeScript para SDKs e scripts de automação
- Rust para programas on-chain (smart contracts avançados)
- Bash para comandos CLI e automação simples
- YAML/JSON para configurações e metadados

## Convenções de Nomes
- Variáveis e funções: camelCase (`tokenMintAddress`, `createLiquidityPool`)
- Constantes: UPPER_SNAKE_CASE (`MAX_SUPPLY`, `PROGRAM_ID`)
- Arquivos: kebab-case (`create-spl-token.ts`, `token-metadata.json`)
- Endereços Solana: sempre referenciados como `publicKey` ou `mintAddress`

## Segurança
- NUNCA hardcode private keys em código
- Sempre usar variáveis de ambiente para keys sensíveis
- Validar todos os endereços antes de transações
- Confirmar transações na devnet antes da mainnet
- Logs detalhados de cada operação on-chain

## Transações Solana
- Sempre incluir retry logic (max 3 tentativas)
- Verificar confirmação da transação (`confirmed` ou `finalized`)
- Logar transaction signature para auditoria
- Estimar fees antes de enviar

## Metadados
- JSON de metadados SEMPRE em UTF-8
- Imagens: PNG ou WebP, máximo 100KB
- URI: preferencialmente Arweave (permanente)
- Validar JSON schema antes de upload

## Testes
- Sempre testar na devnet antes da mainnet
- Verificar saldo suficiente antes de operações
- Validar output de cada etapa do pipeline
