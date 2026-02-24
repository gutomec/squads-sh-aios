---
task: generateImageBrief()
responsavel: "ImageBriefer"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: content
    tipo: file
    origen: "writeLongForm() ou adaptForSocial() — conteúdo para criar visuais"
    obrigatorio: true
  - campo: platform
    tipo: string
    origen: "social-media-adapter — plataforma alvo"
    obrigatorio: false
  - campo: style
    tipo: string
    origen: "Usuário ou brand guidelines — estilo visual"
    obrigatorio: false

Saida:
  - campo: imageBriefs
    tipo: array
    destino: "designer/AI tool, publishing-scheduler"
    persistido: true
  - campo: aiPrompts
    tipo: array
    destino: "nano-banana ou dalle3 — prompts para geração AI"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Conteúdo disponível"
    - "[ ] Plataforma alvo definida"
  post-conditions:
    - "[ ] Brief de imagem gerado com especificações completas"
    - "[ ] Prompts de AI incluídos"
    - "[ ] Dimensões corretas para plataforma"
  acceptance-criteria:
    - blocker: true
      criteria: "Brief com dimensões, composição e estilo definidos"
    - blocker: true
      criteria: "Prompt de AI generation funcional"
    - blocker: false
      criteria: "Variações de estilo propostas"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "~0 (criação de brief)"
  cacheable: false
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se brand guidelines indisponíveis, usar estilo genérico profissional"
  notification: "image-brief-generator"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "content-factory-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Generate Image Brief

## Flow

```
1. Receber conteúdo e contexto da plataforma
2. Definir dimensões corretas para a plataforma
3. Especificar composição e layout (rule of thirds, focal point)
4. Definir paleta de cores alinhada à marca
5. Especificar tipografia e texto overlay
6. Gerar prompts otimizados para AI image generation
7. Incluir instruções detalhadas para designer humano
8. Enviar briefs para produção e scheduler
```

## Elicitation

- "Qual o conteúdo para o qual criar visuais?"
- "Para qual plataforma? (Instagram, LinkedIn, Twitter/X, Blog, YouTube)"
- "Há estilo visual preferido? (flat, 3D, photorealistic, illustration)"
- "Há brand guidelines ou paleta de cores definida?"
