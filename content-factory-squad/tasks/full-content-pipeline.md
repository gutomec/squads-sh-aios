---
task: fullContentPipeline()
responsavel: "Strategist"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: topic
    tipo: string
    origen: "Usuário — tema principal"
    obrigatorio: true
  - campo: channels
    tipo: array
    origen: "Usuário — canais alvo"
    obrigatorio: true
  - campo: format
    tipo: string
    origen: "Usuário — formato do conteúdo principal"
    obrigatorio: false

Saida:
  - campo: completePipeline
    tipo: object
    destino: "Usuário — resultado completo do pipeline"
    persistido: true
  - campo: contentCalendar
    tipo: file
    destino: "content-calendar.md"
    persistido: true
  - campo: longFormContent
    tipo: file
    destino: "long-form-content.md"
    persistido: true
  - campo: socialPosts
    tipo: array
    destino: "social-posts.json"
    persistido: true
  - campo: imageBriefs
    tipo: array
    destino: "image-briefs.json"
    persistido: true
  - campo: publishingSchedule
    tipo: file
    destino: "publishing-schedule.md"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Tema definido"
    - "[ ] Ao menos 2 canais alvo"
    - "[ ] Acesso a plataformas de publicação"
  post-conditions:
    - "[ ] Conteúdo longo escrito"
    - "[ ] Adaptações sociais geradas"
    - "[ ] Briefs de imagem criados"
    - "[ ] Publicações agendadas"
  acceptance-criteria:
    - blocker: true
      criteria: "Pipeline completo executado do planejamento ao agendamento"
    - blocker: true
      criteria: "Conteúdo adaptado para todos os canais solicitados"
    - blocker: false
      criteria: "Variações A/B geradas"

Performance:
  duration_expected: "60-120 minutos"
  cost_estimated: "Variável conforme número de canais e formatos"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: escalate
  retry:
    max_attempts: 2
    delay: "exponential(base=10s, max=60s)"
  fallback: "Se qualquer fase falhar, entregar resultado parcial e indicar fase pendente"
  notification: "content-strategist"

Metadata:
  version: "1.0.0"
  dependencies:
    - planContentCalendar()
    - writeLongForm()
    - adaptForSocial()
    - generateImageBrief()
    - schedulePublishing()
  author: "content-factory-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Full Content Pipeline

## Pipeline

```
Fase 1: Planejamento      → @content-strategist    → planContentCalendar()
Fase 2: Escrita            → @long-form-writer      → writeLongForm()
Fase 3: Adaptação Social   → @social-media-adapter  → adaptForSocial()
Fase 4: Briefs de Imagem   → @image-brief-generator → generateImageBrief()
Fase 5: Agendamento        → @publishing-scheduler  → schedulePublishing()
```

## Elicitation

### Fase 1 — Tema e Canais
- "Qual o tema principal do conteúdo?"
- "Para quais canais deseja produzir? (blog, LinkedIn, Instagram, Twitter/X, TikTok)"
- "Qual o formato principal? (artigo, whitepaper, e-book)"
- "Há keywords de SEO específicas?"
- "Qual a data desejada para publicação?"

### Fase 2 — Detalhamento
- "Qual a buyer persona alvo?"
- "Há referências ou fontes obrigatórias?"
- "Qual o tom de voz desejado?"

### Fase 3 — Adaptação
- "Alguma plataforma com prioridade para adaptação?"
- "Deseja variações A/B para teste?"

### Fase 5 — Agendamento
- "Qual o timezone do público-alvo?"
- "Há restrições de data ou horário?"
