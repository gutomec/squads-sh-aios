# content-factory-squad

Squad especialista em produção de conteúdo em escala para marketing.

## Visão Geral

O **content-factory-squad** é um squad completo que cobre todo o pipeline de produção de conteúdo:

1. **Planejamento Editorial** — Calendários editoriais multi-canal, definição de temas, mapeamento de buyer journey e pilares de conteúdo
2. **Criação de Conteúdo Longo** — Artigos, blog posts, whitepapers, e-books e case studies otimizados para SEO com storytelling
3. **Adaptação para Redes Sociais** — Transformação de conteúdo longo em carrosséis Instagram, threads Twitter/X, posts LinkedIn e scripts TikTok
4. **Briefs de Imagem** — Direção visual com especificações de dimensão, composição, estilo e prompts para geração AI
5. **Agendamento Multicanal** — Publicações agendadas em horários ótimos por plataforma com gestão de fila e cadência

**Pain Point:** Produzir conteúdo de qualidade em escala para múltiplos canais exige coordenação entre estratégia, escrita, design e publicação — um processo que normalmente leva dias pode ser acelerado com orquestração de agentes.

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 📋 Strategist | `content-strategist` | Estrategista de conteúdo e planejamento editorial |
| ✍️ Writer | `long-form-writer` | Escritor de conteúdo longo e SEO |
| 📱 SocialAdapter | `social-media-adapter` | Adaptador de conteúdo para redes sociais |
| 🎨 ImageBriefer | `image-brief-generator` | Gerador de briefs de imagem e direção visual |
| ⏰ Scheduler | `publishing-scheduler` | Agendador de publicações multicanal |

## Workflows

| Workflow | Comando | Descrição | Duração |
|---|---|---|---|
| Full Content Pipeline | `*content-pipeline` | Pipeline completo: do planejamento ao agendamento | 60-120 min |
| Quick Social Blast | `*social-blast` | Produção rápida: do tema ao post agendado | 15-30 min |

## Comandos Disponíveis

| Comando | Agente | Descrição |
|---|---|---|
| `*plan-calendar` | Strategist | Planejar calendário editorial mensal/trimestral |
| `*content-pipeline` | Strategist | Pipeline completo de produção de conteúdo |
| `*write-article` | Writer | Escrever artigo ou blog post |
| `*write-whitepaper` | Writer | Escrever whitepaper ou e-book |
| `*adapt-social` | SocialAdapter | Adaptar conteúdo para redes sociais |
| `*create-thread` | SocialAdapter | Criar thread Twitter/X |
| `*generate-brief` | ImageBriefer | Gerar brief de imagem para conteúdo |
| `*batch-briefs` | ImageBriefer | Gerar briefs para múltiplas peças |
| `*schedule` | Scheduler | Agendar publicação de conteúdo |
| `*optimize-times` | Scheduler | Otimizar horários de publicação |

## Quick Start

```
# Ativar o estrategista (orquestrador principal)
/cfs:agents:content-strategist

# Pipeline completo de produção de conteúdo
*content-pipeline

# Social blast rápido
*social-blast

# Apenas escrever um artigo
*write-article

# Apenas adaptar para redes sociais
*adapt-social
```

## Público Alvo

- Gerentes de Marketing de Conteúdo
- Social Media Managers
- Content Strategists
- Copywriters e Redatores
- Marketing Digital Managers

## Requisitos

- Acesso a plataforma de blog (WordPress, HubSpot, Ghost)
- Acesso a ferramentas de social media (Buffer, Hootsuite, Later)
- Brand guidelines definidos (tom de voz, paleta de cores)
- Buyer personas mapeadas
