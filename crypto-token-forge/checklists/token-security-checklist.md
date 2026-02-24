# Token Security Checklist

Checklist completo de segurança para tokens crypto na Solana.

## Autoridades do Token

- [ ] **Mint Authority** — Verificar se está ativa
  - [ ] Revogar se supply deve ser fixo: `spl-token authorize <TOKEN> mint --disable`
  - [ ] Documentar decisão se mantida ativa (justificativa obrigatória)
- [ ] **Freeze Authority** — Verificar se está ativa
  - [ ] OBRIGATÓRIO revogar antes de criar pool no Raydium
  - [ ] `spl-token authorize <TOKEN> freeze --disable`
- [ ] **Update Authority** — Verificar se está ativa
  - [ ] Revogar SOMENTE após metadados 100% finais
  - [ ] Confirmar nome, símbolo e imagem corretos antes de revogar

## Distribuição de Supply

- [ ] Nenhuma carteira individual detém > 10% do supply (exceto pools e vesting contracts)
- [ ] Alocação do time <= 20% com vesting
- [ ] Time + investidores combinados <= 40%
- [ ] Liquidez pool contém alocação adequada

## Liquidez

- [ ] Pool de liquidez criado em DEX confiável (Raydium, Orca, Meteora)
- [ ] LP tokens locked por mínimo 1 ano OU burned
  - [ ] Plataforma de lock: Smithii / Streamflow / StakePoint
  - [ ] Transaction hash do lock documentado
- [ ] Liquidez suficiente para trading (mínimo recomendado: $500+)

## Metadados

- [ ] Metadados on-chain corretos (nome, símbolo, URI)
- [ ] JSON off-chain acessível e válido
- [ ] Imagem hospedada em armazenamento permanente (Arweave/IPFS)
- [ ] tokenStandard = Fungible (para aparecer na aba Home da Phantom)

## Verificação Externa

- [ ] Token verificado no RugCheck.xyz — score: ___________
- [ ] Token visível no Solscan com informações corretas
- [ ] Token listado no DexScreener (automático após pool)
- [ ] Token listado no Birdeye (automático após DEX)
- [ ] (Opcional) Verificação Jupiter VRFD solicitada

## Smart Contract (se aplicável)

- [ ] Código auditado (se custom program)
- [ ] Sem funções de backdoor ou admin keys
- [ ] Sem lógica de honeypot (restrições de venda)

## Documentação

- [ ] Tokenomics público e transparente
- [ ] Audit report disponível para comunidade
- [ ] Roadmap publicado
- [ ] Equipe identificável (ou justificativa para anonimato)

---

**Score Final:**
- [ ] PASSED — Todos os blockers atendidos
- [ ] CONCERNS — 1-2 itens pendentes com justificativa
- [ ] FAILED — Blockers não atendidos

**Auditor:** @security-auditor (Sentinel)
**Data:** ___________
**Token:** ___________
