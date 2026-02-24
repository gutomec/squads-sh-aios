# crypto-token-forge

Squad especialista em criação, lançamento e gestão de tokens crypto na blockchain Solana.

## Visão Geral

O **crypto-token-forge** é um squad completo que cobre todo o pipeline de criação de tokens:

1. **Concepção** — Design de tokenomics e arquitetura do token
2. **Desenvolvimento** — Criação do token SPL ou Token-2022 via CLI/código
3. **Branding** — Metadados Metaplex (nome, símbolo, logo, descrição)
4. **Segurança** — Auditoria, revogação de autoridades, lock de LP
5. **Lançamento** — Pool de liquidez no Raydium, listagem no Jupiter
6. **Growth** — Estratégia de comunidade, airdrops, verificação

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 🎯 Forge | `crypto-orchestrator` | Orquestrador principal do pipeline |
| 🏗️ Archon | `token-architect` | Arquiteto técnico de tokens |
| 📊 Nomics | `tokenomics-strategist` | Estrategista de tokenomics |
| ⚡ Helix | `solana-dev` | Desenvolvedor Solana |
| 🎨 Meta | `metadata-artist` | Especialista em metadados e branding |
| 🚀 Orbit | `defi-launcher` | Especialista em DeFi e lançamento |
| 🛡️ Sentinel | `security-auditor` | Auditor de segurança crypto |
| 📢 Pulse | `community-growth` | Growth e comunidade |

## Workflows

| Workflow | Comando | Descrição |
|---|---|---|
| Full Token Launch | `*forge-token` | Pipeline completo do zero ao token negociável |
| Memecoin Express | `*forge-memecoin` | Lançamento rápido via Pump.fun |
| Utility Token | `*forge-utility` | Token-2022 com utilidade real |

## Quick Start

```
# Ativar o orquestrador
/ctf:agents:crypto-orchestrator

# Lançar token completo
*forge-token

# Lançar memecoin rápida
*forge-memecoin

# Apenas design de tokenomics
*design-tokenomics

# Auditoria de segurança
*security-audit
```

## Requisitos

- Solana CLI instalado (`solana --version`)
- SPL Token CLI (`cargo install spl-token-cli`)
- Metaboss (`cargo install metaboss`)
- SOL na wallet (devnet para testes, mainnet para produção)
