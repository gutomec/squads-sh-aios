# adaptive-tutor-k12

Squad especialista em tutoria adaptativa K-12.

## Visão Geral

O **adaptive-tutor-k12** é um squad completo que cobre todo o ciclo de tutoria personalizada:

1. **Avaliação Diagnóstica** — Diagnóstico adaptativo para mapear lacunas de conhecimento, nível de proficiência e estilo de aprendizagem
2. **Mapeamento Curricular** — Trilhas de aprendizagem personalizadas alinhadas com BNCC/Common Core, com progressão gradual e spaced repetition
3. **Tutoria Adaptativa** — Sessões personalizadas com múltiplas abordagens pedagógicas, exercícios adaptativos e feedback imediato
4. **Rastreamento de Progresso** — Monitoramento de mastery por tópico, detecção de estagnação e análise de tendências
5. **Relatórios para Pais** — Relatórios acessíveis celebrando conquistas, explicando áreas de melhoria e com recomendações práticas para casa

**Pain Point:** Tutoria individual gera 98% de melhoria no desempenho vs 20% em sala de aula convencional (Bloom, 1984), mas é inacessível para a maioria das famílias pelo custo elevado.

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 📋 Assessor | `diagnostic-assessor` | Avaliação diagnóstica e detecção de lacunas |
| 🗺️ CurriculumMapper | `curriculum-mapper` | Mapeamento curricular e trilhas personalizadas |
| 🎓 Tutor | `tutor-agent` | Tutoria adaptativa e ensino personalizado |
| 📊 ProgressTracker | `progress-tracker` | Rastreamento de progresso e análise de tendências |
| 📧 ParentReporter | `parent-report-agent` | Geração de relatórios para pais e educadores |

## Workflows

| Workflow | Comando | Descrição | Duração |
|---|---|---|---|
| Full Tutoring Cycle | `*full-tutoring` | Ciclo completo: diagnóstico ao relatório para pais | 60-90 min |
| Quick Practice Session | `*quick-practice` | Prática rápida: tutoria com rastreamento | 20-40 min |

## Comandos Disponíveis

| Comando | Agente | Descrição |
|---|---|---|
| `*assess-student` | Assessor | Avaliar nível de conhecimento do aluno |
| `*identify-gaps` | Assessor | Identificar lacunas específicas de conhecimento |
| `*map-curriculum` | CurriculumMapper | Criar trilha de aprendizagem personalizada |
| `*adjust-path` | CurriculumMapper | Ajustar trilha baseado em progresso |
| `*tutor-session` | Tutor | Iniciar sessão de tutoria personalizada |
| `*practice` | Tutor | Gerar exercícios de prática |
| `*full-tutoring` | Tutor | Ciclo completo de tutoria adaptativa |
| `*track-progress` | ProgressTracker | Analisar progresso de aprendizagem |
| `*detect-stagnation` | ProgressTracker | Detectar sinais de estagnação |
| `*parent-report` | ParentReporter | Gerar relatório de progresso para pais |
| `*educator-report` | ParentReporter | Gerar relatório para educador/professor |

## Quick Start

```
# Ativar o tutor (orquestrador principal)
/atk:agents:tutor-agent

# Ciclo completo de tutoria adaptativa
*full-tutoring

# Prática rápida
*quick-practice

# Apenas avaliação diagnóstica
*assess-student

# Apenas relatório para pais
*parent-report
```

## Público Alvo

- Pais e responsáveis buscando tutoria personalizada
- Estudantes K-12 (Ensino Fundamental e Médio)
- Professores e pedagogos
- Escolas e instituições de ensino
- Plataformas de EdTech

## Requisitos

- Definição de disciplina e nível escolar do aluno
- Informações sobre dificuldades específicas (opcional)
- Disponibilidade para sessões de tutoria (20-90 min)
- Consentimento dos pais para coleta de dados de menores (LGPD/COPPA)
