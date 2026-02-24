# adaptive-tutor-k12

Squad especialista en tutoría adaptativa K-12.

## Descripción General

El **adaptive-tutor-k12** es un squad completo que cubre todo el ciclo de tutoría personalizada:

1. **Evaluación Diagnóstica** — Diagnóstico adaptativo para mapear brechas de conocimiento, nivel de competencia y estilo de aprendizaje
2. **Mapeo Curricular** — Rutas de aprendizaje personalizadas alineadas con BNCC/Common Core, con progresión gradual y repetición espaciada
3. **Tutoría Adaptativa** — Sesiones personalizadas con múltiples enfoques pedagógicos, ejercicios adaptativos y retroalimentación inmediata
4. **Seguimiento de Progreso** — Monitoreo de dominio por tema, detección de estancamiento y análisis de tendencias
5. **Informes para Padres** — Informes accesibles celebrando logros, explicando áreas de mejora y con recomendaciones prácticas para el hogar

**Pain Point:** La tutoría individual genera un 98% de mejora en el rendimiento vs 20% en aula convencional (Bloom, 1984), pero es inaccesible para la mayoría de las familias por su alto costo.

## Agentes

| Agente | ID | Rol |
|---|---|---|
| 📋 Assessor | `diagnostic-assessor` | Evaluación diagnóstica y detección de brechas |
| 🗺️ CurriculumMapper | `curriculum-mapper` | Mapeo curricular y rutas personalizadas |
| 🎓 Tutor | `tutor-agent` | Tutoría adaptativa y enseñanza personalizada |
| 📊 ProgressTracker | `progress-tracker` | Seguimiento de progreso y análisis de tendencias |
| 📧 ParentReporter | `parent-report-agent` | Generación de informes para padres y educadores |

## Flujos de Trabajo

| Workflow | Comando | Descripción | Duración |
|---|---|---|---|
| Full Tutoring Cycle | `*full-tutoring` | Ciclo completo: del diagnóstico al informe para padres | 60-90 min |
| Quick Practice Session | `*quick-practice` | Práctica rápida: tutoría con seguimiento | 20-40 min |

## Comandos Disponibles

| Comando | Agente | Descripción |
|---|---|---|
| `*assess-student` | Assessor | Evaluar nivel de conocimiento del alumno |
| `*identify-gaps` | Assessor | Identificar brechas específicas de conocimiento |
| `*map-curriculum` | CurriculumMapper | Crear ruta de aprendizaje personalizada |
| `*adjust-path` | CurriculumMapper | Ajustar ruta basado en progreso |
| `*tutor-session` | Tutor | Iniciar sesión de tutoría personalizada |
| `*practice` | Tutor | Generar ejercicios de práctica |
| `*full-tutoring` | Tutor | Ciclo completo de tutoría adaptativa |
| `*track-progress` | ProgressTracker | Analizar progreso de aprendizaje |
| `*detect-stagnation` | ProgressTracker | Detectar señales de estancamiento |
| `*parent-report` | ParentReporter | Generar informe de progreso para padres |
| `*educator-report` | ParentReporter | Generar informe para educador/profesor |

## Inicio Rápido

```
# Activar el tutor (orquestador principal)
/atk:agents:tutor-agent

# Ciclo completo de tutoría adaptativa
*full-tutoring

# Práctica rápida
*quick-practice

# Solo evaluación diagnóstica
*assess-student

# Solo informe para padres
*parent-report
```

## Usuarios Objetivo

- Padres buscando tutoría personalizada
- Estudiantes K-12 (Primaria y Secundaria)
- Profesores y pedagogos
- Escuelas e instituciones educativas
- Plataformas de EdTech

## Requisitos

- Definición de materia y nivel escolar del alumno
- Información sobre dificultades específicas (opcional)
- Disponibilidad para sesiones de tutoría (20-90 min)
- Consentimiento de los padres para recopilación de datos de menores (LGPD/COPPA)
