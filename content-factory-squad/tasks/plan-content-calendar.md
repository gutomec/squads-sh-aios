---
task: planContentCalendar()
responsavel: "Strategist"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: period
    tipo: string
    origen: "Usuário — mensal/trimestral/anual"
    obrigatorio: true
  - campo: channels
    tipo: array
    origen: "Usuário — lista de canais alvo"
    obrigatorio: false
  - campo: personas
    tipo: array
    origen: "Usuário — buyer personas"
    obrigatorio: false
  - campo: brandGuidelines
    tipo: object
    origen: "Projeto — tom de voz, visual identity"
    obrigatorio: false

Saida:
  - campo: contentCalendar
    tipo: file
    destino: "content-calendar.md, long-form-writer, social-media-adapter, publishing-scheduler"
    persistido: true
  - campo: themeMap
    tipo: object
    destino: "long-form-writer, social-media-adapter"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Período definido"
    - "[ ] Ao menos um canal alvo identificado"
  post-conditions:
    - "[ ] Calendário editorial gerado com temas e datas"
    - "[ ] Temas mapeados ao buyer journey"
    - "[ ] Formatos definidos para cada canal"
  acceptance-criteria:
    - blocker: true
      criteria: "Calendário com pelo menos 4 semanas de conteúdo planejado"
    - blocker: true
      criteria: "Cada tema alinhado com fase do buyer journey"
    - blocker: false
      criteria: "Mix de formatos diversificado"

Performance:
  duration_expected: "15-30 minutos"
  cost_estimated: "~0 (planejamento estratégico)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se dados de persona indisponíveis, usar persona genérica baseada no segmento"
  notification: "content-strategist"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "content-factory-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Plan Content Calendar

## Flow

```
1. Definir período e objetivos de marketing
2. Mapear buyer personas e etapas do funil
3. Identificar pilares de conteúdo (3-5 temas principais)
4. Distribuir temas por semana do período
5. Definir formatos por canal (blog, social, email, vídeo)
6. Atribuir prioridades e datas de publicação
7. Gerar calendário editorial em content-calendar.md
8. Enviar calendário para writers e scheduler
```

## Elicitation

- "Qual o período do calendário? (mensal, trimestral, anual)"
- "Quais canais serão utilizados? (blog, Instagram, LinkedIn, Twitter/X, TikTok, email)"
- "Quais são as buyer personas do público-alvo?"
- "Há brand guidelines ou tom de voz definido?"
