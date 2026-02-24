# Launch Readiness Checklist

Checklist pré-lançamento para tokens crypto na Solana.

## Token

- [ ] Token criado na rede correta (devnet para testes / mainnet para produção)
- [ ] Supply mintado e verificado: `spl-token supply <TOKEN>`
- [ ] Decimais configurados corretamente
- [ ] Token account criada e com saldo

## Metadados

- [ ] Nome exibido corretamente na Phantom
- [ ] Símbolo exibido corretamente
- [ ] Logo/imagem visível
- [ ] Descrição presente no JSON off-chain
- [ ] Links sociais incluídos (se aplicável)
- [ ] tokenStandard = Fungible

## Segurança

- [ ] Security audit com score PASSED ou CONCERNS
- [ ] Freeze Authority revogada
- [ ] Mint Authority revogada (ou justificativa documentada)
- [ ] LP tokens locked ou burned

## Liquidez

- [ ] Pool de liquidez criado no Raydium
- [ ] Par de trading definido (Token/SOL ou Token/USDC)
- [ ] Liquidez inicial depositada
- [ ] Preço inicial calculado e documentado
- [ ] Swap testado (compra e venda funcionando)

## Indexação

- [ ] Token indexado no Jupiter (pode levar minutos após pool)
- [ ] Token visível no DexScreener
- [ ] Token listado no Birdeye
- [ ] Token verificável no Solscan

## Comunidade

- [ ] growth-plan.md definido
- [ ] Canal principal de comunicação criado (Discord/Telegram)
- [ ] Twitter/X configurado
- [ ] Material de marketing preparado (tokenomics visual, roadmap)
- [ ] Anúncio de lançamento redigido

## Documentação

- [ ] tokenomics.yaml completo e público
- [ ] audit-report.md gerado
- [ ] launch-summary.md com todos os endereços e links
- [ ] README do projeto atualizado

---

**Status:** [ ] READY TO LAUNCH / [ ] NOT READY (pendências listadas abaixo)

**Pendências:**
1. ___________
2. ___________

**Responsável:** @crypto-orchestrator (Forge)
**Data:** ___________
