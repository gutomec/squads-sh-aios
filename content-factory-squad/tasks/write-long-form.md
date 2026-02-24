---
task: writeLongForm()
responsavel: "Writer"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: topic
    tipo: string
    origen: "content-strategist ou Usuário — tema do conteúdo"
    obrigatorio: true
  - campo: format
    tipo: string
    origen: "content-strategist — article/blogpost/whitepaper/ebook"
    obrigatorio: false
  - campo: keywords
    tipo: array
    origen: "content-strategist ou Usuário — SEO keywords"
    obrigatorio: false
  - campo: contentCalendar
    tipo: file
    origen: "planContentCalendar() — calendário editorial"
    obrigatorio: false

Saida:
  - campo: longFormContent
    tipo: file
    destino: "long-form-content.md, social-media-adapter, image-brief-generator"
    persistido: true
  - campo: contentMetadata
    tipo: object
    destino: "publishing-scheduler"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Tema definido"
    - "[ ] Formato escolhido (ou padrão: article)"
  post-conditions:
    - "[ ] Conteúdo escrito com heading structure"
    - "[ ] Otimizado para SEO"
    - "[ ] CTAs incluídos"
  acceptance-criteria:
    - blocker: true
      criteria: "Conteúdo com mínimo 800 palavras para artigos"
    - blocker: true
      criteria: "Heading structure H1-H4 correta"
    - blocker: false
      criteria: "Meta description e keywords incluídos"

Performance:
  duration_expected: "20-45 minutos"
  cost_estimated: "~0 (criação de conteúdo)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se briefing incompleto, solicitar informações adicionais ao content-strategist"
  notification: "long-form-writer"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "content-factory-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Write Long-Form Content

## Flow

```
1. Receber briefing do content-strategist ou usuário
2. Pesquisar tema e referências relevantes
3. Definir estrutura (outline) com H1-H4
4. Escrever headline magnética
5. Desenvolver corpo do artigo com storytelling
6. Incluir CTAs estratégicos alinhados com a fase do funil
7. Otimizar para SEO (keywords, meta description, heading structure)
8. Revisar e polir o texto
9. Gerar metadata de conteúdo (title, description, keywords)
10. Enviar para social-media-adapter e image-brief-generator
```

## Elicitation

- "Qual o tema do conteúdo?"
- "Qual o formato desejado? (artigo, blog post, whitepaper, e-book, case study)"
- "Há keywords de SEO específicas a incluir?"
- "Qual a buyer persona alvo?"
- "Há referências ou fontes obrigatórias?"
