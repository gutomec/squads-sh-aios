# ambient-clinical-scribe

> Squad de documentación clínica automatizada con IA ambient — del audio de la consulta al expediente completo con notas SOAP, códigos ICD-10/CPT y revisión de calidad. Reducción del 69.5% en el tiempo administrativo de los médicos.

## Instalación

```bash
npx squads add gutomec/squads-sh-aios/ambient-clinical-scribe
```

## Qué Hace

**ambient-clinical-scribe** es un squad que automatiza todo el pipeline de documentación clínica:

1. **Captura** — Transcripción en tiempo real de consultas médicas con diarización de hablantes
2. **Documentación** — Generación de notas clínicas estructuradas en formato SOAP
3. **Codificación** — Asignación automática de códigos ICD-10 y CPT
4. **Calidad** — Revisión de completitud, precisión y cumplimiento HIPAA/CMS

Los médicos dedican más de 3 horas extra por semana a la documentación administrativa. Este squad reduce ese tiempo en un 69.5%, permitiendo mayor enfoque en la atención al paciente.

## Agentes

| Agente | ID | Rol |
|---|---|---|
| 🎙️ AmbientListener | `ambient-listener` | Transcripción de consultas en tiempo real |
| 📋 NoteDrafter | `clinical-note-drafter` | Generación de notas SOAP estructuradas |
| 🏥 MedicalCoder | `medical-coder` | Codificación ICD-10 y CPT |
| ✅ QualityReviewer | `quality-reviewer` | Revisión de calidad y cumplimiento |

## Workflows

| Workflow | Comando | Descripción | Duración |
|---|---|---|---|
| Full Documentation | `*document-visit` | Pipeline completo (transcripción + nota + codificación + revisión) | 5-15 min |
| Quick Note | `*quick-note` | Nota SOAP rápida sin codificación | 3-8 min |

## Inicio Rápido

```
# Activar el scribe y documentar una visita completa
/acs:agents:ambient-listener
*document-visit

# Generar nota rápida sin codificación
*quick-note

# Solo generar nota SOAP
/acs:agents:clinical-note-drafter
*draft-note --format=soap

# Solo codificación médica
/acs:agents:medical-coder
*assign-codes

# Revisión de calidad
/acs:agents:quality-reviewer
*review-note
```

## Comandos Disponibles

| Comando | Agente | Descripción |
|---|---|---|
| `*start-listening` | AmbientListener | Iniciar captura en tiempo real |
| `*transcribe-session` | AmbientListener | Transcribir archivo de audio |
| `*draft-note` | NoteDrafter | Generar nota clínica estructurada |
| `*format-soap` | NoteDrafter | Formatear datos en SOAP |
| `*assign-codes` | MedicalCoder | Asignar códigos ICD-10/CPT |
| `*validate-codes` | MedicalCoder | Validar códigos asignados |
| `*review-note` | QualityReviewer | Revisar nota clínica |
| `*compliance-check` | QualityReviewer | Verificar cumplimiento HIPAA/CMS |
| `*document-visit` | Pipeline | Documentación completa |
| `*full-documentation` | Pipeline | Documentación completa (alias) |
| `*quick-note` | Pipeline | Nota rápida sin codificación |
| `*draft-visit` | Pipeline | Nota rápida (alias) |

## Cumplimiento

Este squad fue diseñado con el cumplimiento normativo en mente:

- **HIPAA** — Protección de PHI (Protected Health Information) en todas las etapas
- **CMS Guidelines** — Adherencia a las guías de documentación para codificación y reembolso
- **OIG Compliance** — Prevención de upcoding/downcoding y fraude de codificación

**IMPORTANTE:** La implementación real de cumplimiento depende de la infraestructura de despliegue. Este squad proporciona las verificaciones y validaciones, pero la seguridad de datos (encriptación, control de acceso, auditoría) debe implementarse en la capa de infraestructura.

## Autor

**Luiz Gustavo Vieira Rodrigues** ([@gutomec](https://github.com/gutomec))

## Licencia

MIT
