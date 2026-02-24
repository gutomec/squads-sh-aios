---
task: runDiagnosticAssessment()
responsavel: "Assessor"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: subject
    tipo: string
    origen: "Usuário ou fullTutoringCycle() — disciplina para avaliação"
    obrigatorio: true
  - campo: grade
    tipo: string
    origen: "Usuário — ano escolar do aluno (1-12)"
    obrigatorio: false
  - campo: student
    tipo: string
    origen: "Usuário — nome/perfil do aluno"
    obrigatorio: false

Saida:
  - campo: diagnosticReport
    tipo: file
    destino: "diagnostic-report.md, curriculum-mapper, tutor-agent, progress-tracker"
    persistido: true
  - campo: learningProfile
    tipo: object
    destino: "curriculum-mapper, tutor-agent"
    persistido: true
  - campo: gapMap
    tipo: array
    destino: "curriculum-mapper"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Disciplina definida"
    - "[ ] Nível escolar aproximado identificado"
  post-conditions:
    - "[ ] Nível de proficiência avaliado"
    - "[ ] Lacunas identificadas por tópico"
    - "[ ] Estilo de aprendizagem determinado"
    - "[ ] Relatório diagnóstico gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Nível de proficiência determinado com confiança >= 70%"
    - blocker: true
      criteria: "Ao menos 3 lacunas específicas identificadas"
    - blocker: false
      criteria: "Estilo de aprendizagem identificado"

Performance:
  duration_expected: "15-25 minutos"
  cost_estimated: "~0 (processamento de avaliação)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se avaliação adaptativa falhar, usar avaliação padrão baseada no nível escolar"
  notification: "curriculum-mapper"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "adaptive-tutor-k12"
  created_at: "2026-02-24T00:00:00Z"
---

# Run Diagnostic Assessment

## Flow

```
1. Definir disciplina e nível escolar aproximado
2. Selecionar questões adaptativas iniciais (nível médio para o ano)
3. Aplicar questões ajustando dificuldade baseado nas respostas
4. Analisar padrões de acerto/erro por tópico
5. Identificar lacunas específicas com mapeamento de pré-requisitos
6. Determinar estilo de aprendizagem preferencial
7. Calcular nível de proficiência com score de confiança
8. Gerar relatório diagnóstico completo
9. Enviar para @curriculum-mapper
```

## Elicitation

- "Qual a disciplina a ser avaliada? (Matemática, Português, Ciências, História, Inglês, etc.)"
- "Qual o ano escolar do aluno? (1º ao 12º)"
- "Qual o nome do aluno? (para personalização)"
- "Há tópicos específicos que gostaria de avaliar?"
