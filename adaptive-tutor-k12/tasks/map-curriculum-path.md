---
task: mapCurriculumPath()
responsavel: "CurriculumMapper"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: diagnosticReport
    tipo: file
    origen: "runDiagnosticAssessment() — relatório diagnóstico do aluno"
    obrigatorio: true
  - campo: subject
    tipo: string
    origen: "Usuário — disciplina"
    obrigatorio: true
  - campo: targetGrade
    tipo: string
    origen: "Usuário — nível alvo (ano escolar)"
    obrigatorio: false

Saida:
  - campo: learningPath
    tipo: file
    destino: "learning-path.md, tutor-agent, progress-tracker, parent-report-agent"
    persistido: true
  - campo: milestones
    tipo: array
    destino: "progress-tracker, parent-report-agent"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Diagnóstico completo disponível"
    - "[ ] Disciplina definida"
  post-conditions:
    - "[ ] Trilha personalizada criada"
    - "[ ] Milestones definidos"
    - "[ ] Pré-requisitos mapeados"
    - "[ ] Spaced repetition incluído"
  acceptance-criteria:
    - blocker: true
      criteria: "Trilha cobre todas as lacunas identificadas no diagnóstico"
    - blocker: true
      criteria: "Alinhada com padrões curriculares (BNCC/Common Core)"
    - blocker: false
      criteria: "Milestones com critérios claros de conclusão"

Performance:
  duration_expected: "10-20 minutos"
  cost_estimated: "~0 (mapeamento curricular)"
  cacheable: true
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se mapeamento de padrão curricular falhar, usar sequência pedagógica genérica"
  notification: "tutor-agent"

Metadata:
  version: "1.0.0"
  dependencies:
    - runDiagnosticAssessment()
  author: "adaptive-tutor-k12"
  created_at: "2026-02-24T00:00:00Z"
---

# Map Curriculum Path

## Flow

```
1. Receber diagnóstico com lacunas e perfil de aprendizagem
2. Mapear currículo oficial (BNCC/Common Core) para a disciplina e ano
3. Identificar pré-requisitos faltantes para cada lacuna
4. Sequenciar conteúdos por dependência e Zone of Proximal Development
5. Definir milestones motivadores e alcançáveis
6. Incluir spaced repetition para retenção de longo prazo
7. Gerar trilha de aprendizagem personalizada
8. Enviar trilha para @tutor-agent
```

## Elicitation

- "Qual o nível alvo desejado? (ano escolar ou competência específica)"
- "Há preferência de ritmo? (intensivo, regular, relaxado)"
- "Há restrições de tempo? (prazo para atingir determinado nível)"
