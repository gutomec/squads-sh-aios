---
task: parseResumes()
responsavel: "Parser"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: resumes
    tipo: array
    origen: "Usuário ou fullResumeScreening() — currículos em qualquer formato"
    obrigatorio: true
  - campo: jobDescription
    tipo: string
    origen: "Usuário — descrição da vaga para contexto"
    obrigatorio: false

Saida:
  - campo: parsedResumes
    tipo: array
    destino: "skills-matcher, bias-auditor, shortlist-ranker"
    persistido: true
  - campo: parsingReport
    tipo: file
    destino: "parsing-report.md, candidate-summary-agent"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Currículos disponíveis em formato legível"
    - "[ ] Formatos suportados (PDF, DOCX, texto)"
  post-conditions:
    - "[ ] Dados estruturados extraídos de todos os CVs"
    - "[ ] Campos normalizados e padronizados"
    - "[ ] Inconsistências cronológicas sinalizadas"
    - "[ ] parsing-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Dados extraídos de 100% dos currículos fornecidos"
    - blocker: true
      criteria: "Skills e experiências normalizadas"
    - blocker: false
      criteria: "Inconsistências cronológicas sinalizadas"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "~0 (processamento local)"
  cacheable: false
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se formato de CV ilegível, alertar usuário e prosseguir com CVs legíveis"
  notification: "skills-matcher"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "resume-screener-squad"
  created_at: "2026-02-24T00:00:00Z"
---

# Parse Resumes

## Flow

```
1. Receber currículos em formato bruto
2. Identificar formato de cada CV (PDF, DOCX, texto)
3. Extrair dados estruturados (experiência, skills, educação)
4. Normalizar títulos de cargo para taxonomia padrão
5. Normalizar skills para vocabulário controlado
6. Detectar inconsistências cronológicas (gaps, sobreposições)
7. Gerar dados padronizados (parsedResumes)
8. Gerar parsing-report.md com estatísticas e alertas
9. Enviar dados para @skills-matcher
```

## Elicitation

- "Quantos currículos deseja processar?"
- "Em qual formato estão os currículos? (PDF, DOCX, texto)"
- "Há uma descrição de vaga para contextualizar a extração?"
- "Deseja sinalizar inconsistências cronológicas?"
