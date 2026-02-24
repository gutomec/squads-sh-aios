---
task: schedulePublishing()
responsavel: "Scheduler"
responsavel_type: Agente
atomic_layer: Atom
elicit: false

Entrada:
  - campo: content
    tipo: array
    origen: "adaptForSocial() ou writeLongForm() — conteúdo a publicar"
    obrigatorio: true
  - campo: channels
    tipo: array
    origen: "content-strategist — canais de publicação"
    obrigatorio: true
  - campo: preferredDate
    tipo: string
    origen: "Usuário ou calendário — data preferida"
    obrigatorio: false

Saida:
  - campo: publishingSchedule
    tipo: file
    destino: "publishing-schedule.md, content-strategist"
    persistido: true
  - campo: queueStatus
    tipo: object
    destino: "content-strategist"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Conteúdo pronto para publicação"
    - "[ ] Canais definidos"
  post-conditions:
    - "[ ] Publicações agendadas com horários ótimos"
    - "[ ] Fila de publicação atualizada"
    - "[ ] Calendário sincronizado"
  acceptance-criteria:
    - blocker: true
      criteria: "Publicações agendadas em horários ótimos por plataforma"
    - blocker: true
      criteria: "Sem conflitos de agendamento"
    - blocker: false
      criteria: "Cadência semanal consistente"

Performance:
  duration_expected: "5-10 minutos"
  cost_estimated: "~0 (agendamento)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se horário ótimo indisponível, agendar no próximo slot disponível"
  notification: "publishing-scheduler"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "content-factory-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Schedule Publishing

## Flow

```
1. Receber conteúdo pronto e canais alvo
2. Consultar horários ótimos por plataforma e timezone
3. Verificar conflitos no calendário existente
4. Agendar publicações nos horários ótimos
5. Atualizar fila de publicação por canal
6. Confirmar agendamento com resumo detalhado
7. Reportar status ao content-strategist
```

## Elicitation

- "Qual conteúdo deseja agendar?"
- "Em quais canais publicar? (blog, Instagram, LinkedIn, Twitter/X, TikTok)"
- "Há data/horário preferido para publicação?"
- "Qual o timezone do público-alvo?"
