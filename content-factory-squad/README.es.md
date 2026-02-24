# content-factory-squad

Squad especialista en producción de contenido a escala para marketing.

## Descripción General

El **content-factory-squad** es un squad completo que cubre todo el pipeline de producción de contenido:

1. **Planificación Editorial** — Calendarios editoriales multicanal, definición de temas, mapeo de buyer journey y pilares de contenido
2. **Creación de Contenido Largo** — Artículos, blog posts, whitepapers, e-books y case studies optimizados para SEO con storytelling
3. **Adaptación para Redes Sociales** — Transformación de contenido largo en carruseles Instagram, hilos Twitter/X, posts LinkedIn y scripts TikTok
4. **Briefs de Imagen** — Dirección visual con especificaciones de dimensión, composición, estilo y prompts para generación AI
5. **Programación Multicanal** — Publicaciones programadas en horarios óptimos por plataforma con gestión de cola y cadencia

**Pain Point:** Producir contenido de calidad a escala para múltiples canales requiere coordinación entre estrategia, escritura, diseño y publicación — un proceso que normalmente toma días puede acelerarse con orquestación de agentes.

## Agentes

| Agente | ID | Rol |
|---|---|---|
| 📋 Strategist | `content-strategist` | Estratega de contenido y planificación editorial |
| ✍️ Writer | `long-form-writer` | Escritor de contenido largo y SEO |
| 📱 SocialAdapter | `social-media-adapter` | Adaptador de contenido para redes sociales |
| 🎨 ImageBriefer | `image-brief-generator` | Generador de briefs de imagen y dirección visual |
| ⏰ Scheduler | `publishing-scheduler` | Programador de publicaciones multicanal |

## Flujos de Trabajo

| Workflow | Comando | Descripción | Duración |
|---|---|---|---|
| Full Content Pipeline | `*content-pipeline` | Pipeline completo: de la planificación a la programación | 60-120 min |
| Quick Social Blast | `*social-blast` | Producción rápida: del tema al post programado | 15-30 min |

## Comandos Disponibles

| Comando | Agente | Descripción |
|---|---|---|
| `*plan-calendar` | Strategist | Planificar calendario editorial mensual/trimestral |
| `*content-pipeline` | Strategist | Pipeline completo de producción de contenido |
| `*write-article` | Writer | Escribir artículo o blog post |
| `*write-whitepaper` | Writer | Escribir whitepaper o e-book |
| `*adapt-social` | SocialAdapter | Adaptar contenido para redes sociales |
| `*create-thread` | SocialAdapter | Crear hilo Twitter/X |
| `*generate-brief` | ImageBriefer | Generar brief de imagen para contenido |
| `*batch-briefs` | ImageBriefer | Generar briefs para múltiples piezas |
| `*schedule` | Scheduler | Programar publicación de contenido |
| `*optimize-times` | Scheduler | Optimizar horarios de publicación |

## Inicio Rápido

```
# Activar el estratega (orquestador principal)
/cfs:agents:content-strategist

# Pipeline completo de producción de contenido
*content-pipeline

# Social blast rápido
*social-blast

# Solo escribir un artículo
*write-article

# Solo adaptar para redes sociales
*adapt-social
```

## Usuarios Objetivo

- Gerentes de Marketing de Contenido
- Social Media Managers
- Content Strategists
- Copywriters y Redactores
- Gerentes de Marketing Digital

## Requisitos

- Acceso a plataforma de blog (WordPress, HubSpot, Ghost)
- Acceso a herramientas de social media (Buffer, Hootsuite, Later)
- Brand guidelines definidas (tono de voz, paleta de colores)
- Buyer personas mapeadas
