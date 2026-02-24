---
task: rankCandidates()
responsavel: "Ranker"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: matchedCandidates
    tipo: array
    origen: "matchSkills() — candidatos com fit score"
    obrigatorio: true
  - campo: biasFlags
    tipo: array
    origen: "auditBias() — flags de viés para ajuste"
    obrigatorio: false
  - campo: shortlistSize
    tipo: number
    origen: "Usuário — tamanho da shortlist (5, 10, 20)"
    obrigatorio: false

Saida:
  - campo: rankedShortlist
    tipo: array
    destino: "candidate-summary-agent"
    persistido: true
  - campo: rankingReport
    tipo: file
    destino: "ranking-report.md, candidate-summary-agent"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Candidatos com fit score disponíveis"
    - "[ ] Bias flags recebidos (se disponíveis)"
  post-conditions:
    - "[ ] Candidatos ranqueados com justificativa"
    - "[ ] Shortlist gerada com tamanho configurado"
    - "[ ] Hidden gems identificados"
    - "[ ] ranking-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Ranking com justificativa para cada posição"
    - blocker: true
      criteria: "Bias flags incorporados no ranking"
    - blocker: false
      criteria: "Hidden gems identificados e destacados"

Performance:
  duration_expected: "5-10 minutos"
  cost_estimated: "~0 (processamento local)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=20s)"
  fallback: "Se bias flags indisponíveis, gerar ranking com aviso de auditoria pendente"
  notification: "candidate-summary-agent"

Metadata:
  version: "1.0.0"
  dependencies: [matchSkills(), auditBias()]
  author: "resume-screener-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Rank Candidates

## Flow

```
1. Receber candidatos com fit scores e bias flags
2. Ajustar scores incorporando feedback de bias
3. Combinar fit score + experiência + potencial + diversidade
4. Ranquear candidatos pela pontuação composta
5. Identificar hidden gems (potencial alto, score médio)
6. Gerar shortlist com tamanho configurável
7. Documentar justificativa para cada posição
8. Gerar ranking-report.md
9. Enviar shortlist para @candidate-summary-agent
```

## Elicitation

- "Qual o tamanho desejado da shortlist? (5, 10, 20)"
- "Há peso diferente para experiência vs potencial?"
- "Deseja incluir hidden gems na shortlist?"
- "Há tiers de prioridade para entrevistas?"
