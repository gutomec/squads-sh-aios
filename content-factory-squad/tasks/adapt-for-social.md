---
task: adaptForSocial()
responsavel: "SocialAdapter"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: longFormContent
    tipo: file
    origen: "writeLongForm() — conteúdo original"
    obrigatorio: true
  - campo: platforms
    tipo: array
    origen: "content-strategist ou Usuário — instagram, linkedin, twitter, tiktok"
    obrigatorio: false

Saida:
  - campo: socialPosts
    tipo: array
    destino: "publishing-scheduler, image-brief-generator"
    persistido: true
  - campo: platformVariations
    tipo: object
    destino: "publishing-scheduler"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Conteúdo longo disponível"
    - "[ ] Ao menos uma plataforma alvo"
  post-conditions:
    - "[ ] Posts adaptados para cada plataforma"
    - "[ ] Hooks e hashtags incluídos"
    - "[ ] Formatos específicos respeitados"
  acceptance-criteria:
    - blocker: true
      criteria: "Post adaptado para ao menos 2 plataformas"
    - blocker: true
      criteria: "Limites de caracteres respeitados por plataforma"
    - blocker: false
      criteria: "Variações A/B para teste"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0 (adaptação de conteúdo)"
  cacheable: false
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se conteúdo longo indisponível, adaptar a partir do briefing do strategist"
  notification: "social-media-adapter"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "content-factory-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Adapt For Social

## Flow

```
1. Receber conteúdo longo do long-form-writer
2. Identificar pontos-chave e quotes impactantes
3. Adaptar para LinkedIn (post profissional com dados)
4. Adaptar para Instagram (carrossel/caption visual)
5. Adaptar para Twitter/X (thread concisa e impactante)
6. Adaptar para TikTok (script com hook nos primeiros 3s)
7. Adicionar hashtags e CTAs específicos por plataforma
8. Gerar variações A/B para teste de performance
9. Enviar para publishing-scheduler e image-brief-generator
```

## Elicitation

- "Qual o conteúdo original a ser adaptado?"
- "Para quais plataformas deseja adaptar? (Instagram, LinkedIn, Twitter/X, TikTok)"
- "Há tom ou estilo específico para alguma plataforma?"
- "Deseja variações A/B para teste?"
