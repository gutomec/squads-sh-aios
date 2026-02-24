---
task: securityAudit()
responsavel: "Sentinel"
responsavel_type: Agente
atomic_layer: Molecule
elicit: true

Entrada:
  - campo: tokenMintAddress
    tipo: string
    origen: "createSplToken() output"
    obrigatorio: true
  - campo: lpTokenAddress
    tipo: string
    origen: "createLiquidityPool() output (se pool já existe)"
    obrigatorio: false
  - campo: tokenomicsYaml
    tipo: file
    origen: "designTokenomics() output"
    obrigatorio: false

Saida:
  - campo: auditReport
    tipo: file
    destino: "audit-report.md"
    persistido: true
  - campo: securityScore
    tipo: string
    destino: "launch-summary.md (PASSED, CONCERNS, FAILED)"
    persistido: true
  - campo: revokedAuthorities
    tipo: array
    destino: "audit-report.md"
    persistido: true
  - campo: lpLockProof
    tipo: string
    destino: "audit-report.md, community-growth"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Token mint address válido"
    - "[ ] Acesso à wallet com authority sobre o token"
  post-conditions:
    - "[ ] Todas as autoridades verificadas"
    - "[ ] Autoridades perigosas revogadas (com confirmação do usuário)"
    - "[ ] Distribuição de supply analisada"
    - "[ ] LP tokens locked (se aplicável)"
    - "[ ] Audit report gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Freeze Authority revogada"
    - blocker: true
      criteria: "Audit report gerado com score"
    - blocker: false
      criteria: "Mint Authority revogada (recomendado)"
    - blocker: false
      criteria: "LP tokens locked por mínimo 1 ano"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0.01-2 SOL (revogações + LP lock)"
  cacheable: false
  parallelizable: false

Metadata:
  version: "1.0.0"
  dependencies:
    - createSplToken()
  author: "crypto-token-forge"
  created_at: "2026-02-24T00:00:00Z"
---

# Security Audit

## Flow

```
1. Verificar autoridades ativas do token
   - spl-token display <TOKEN>
2. Analisar distribuição de supply
   - Top holders e concentração
3. Recomendar revogações ao usuário
4. Executar revogações aprovadas:
   - spl-token authorize <TOKEN> mint --disable
   - spl-token authorize <TOKEN> freeze --disable
5. Lock LP tokens (se pool existe):
   - Via Smithii (0.01 SOL) ou Streamflow
6. Verificar no RugCheck.xyz
7. Gerar audit-report.md
```

## Elicitation

- "Deseja revogar Mint Authority? (Recomendado — impede criação de novos tokens)"
- "Deseja revogar Freeze Authority? (OBRIGATÓRIO para pools no Raydium)"
- "Deseja revogar Update Authority? (Só após metadados 100% finais)"
- "Deseja travar LP tokens? Por quanto tempo? (1y, 2y, 5y, permanente)"

## Security Scoring

| Score | Critérios |
|-------|-----------|
| **PASSED** | Todas as autoridades revogadas + LP locked + supply descentralizado |
| **CONCERNS** | 1-2 autoridades ativas mas com justificativa + LP locked |
| **FAILED** | Mint + Freeze ativas sem justificativa OU LP não locked |

## Comandos de Verificação

```bash
# Ver autoridades do token
spl-token display <TOKEN>

# Revogar mint authority
spl-token authorize <TOKEN> mint --disable

# Revogar freeze authority
spl-token authorize <TOKEN> freeze --disable

# Verificar supply e distribuição
spl-token supply <TOKEN>
spl-token accounts
```
