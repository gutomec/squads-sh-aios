---
task: assignMedicalCodes()
responsavel: "MedicalCoder"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: clinicalNote
    tipo: file
    origen: "clinical-note-drafter (draftClinicalNote())"
    obrigatorio: true
  - campo: codingGuidelines
    tipo: file
    origen: "Base de conhecimento de coding (ICD-10-CM, CPT guidelines)"
    obrigatorio: false
  - campo: patientHistory
    tipo: object
    origen: "EHR (diagnósticos prévios, histórico de codificação)"
    obrigatorio: false

Saida:
  - campo: icd10Codes
    tipo: array
    destino: "quality-reviewer"
    persistido: true
  - campo: cptCodes
    tipo: array
    destino: "quality-reviewer"
    persistido: true
  - campo: codingConfidenceScores
    tipo: object
    destino: "quality-reviewer"
    persistido: true
  - campo: codingRationale
    tipo: string
    destino: "quality-reviewer"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Nota clínica estruturada disponível"
    - "[ ] Base de códigos ICD-10-CM atualizada"
    - "[ ] Base de códigos CPT atualizada"
    - "[ ] Guidelines de codificação carregados"
  post-conditions:
    - "[ ] Códigos ICD-10 atribuídos com especificidade máxima"
    - "[ ] Códigos CPT atribuídos para procedimentos documentados"
    - "[ ] Confidence scores calculados para cada código"
    - "[ ] Rationale documentado para cada atribuição"
    - "[ ] Sem riscos de upcoding detectados"
  acceptance-criteria:
    - blocker: true
      criteria: "Pelo menos 1 código ICD-10 atribuído com confidence >= 80%"
    - blocker: true
      criteria: "Pelo menos 1 código CPT atribuído para E/M"
    - blocker: true
      criteria: "Todos os códigos suportados pela documentação clínica"

Performance:
  duration_expected: "1-2 minutos"
  cost_estimated: "Custo de API LLM + lookup de coding databases"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=2s, max=15s)"
  fallback: "Atribuir código genérico com flag para revisão manual"
  notification: "quality-reviewer"

Metadata:
  version: "1.0.0"
  dependencies:
    - draftClinicalNote()
  author: "ambient-clinical-scribe"
  created_at: "2026-02-24T00:00:00Z"
---

# Assign Medical Codes

## Flow

```
1. Receber nota clínica estruturada do clinical-note-drafter
2. Analisar seção Assessment para diagnósticos
3. Mapear cada diagnóstico para ICD-10-CM mais específico
4. Verificar lateralidade e especificidade dos códigos
5. Analisar seções Objective e Plan para procedimentos
6. Mapear procedimentos para códigos CPT
7. Determinar nível de E/M (99211-99215) baseado na complexidade
8. Calcular confidence score para cada código
9. Verificar riscos de upcoding/downcoding
10. Documentar rationale para cada atribuição
11. Entregar relatório de codificação para quality-reviewer
```

## Formato de Saída

```json
{
  "icd10": [
    {
      "code": "J06.9",
      "description": "Acute upper respiratory infection, unspecified",
      "type": "primary",
      "confidence": 0.92,
      "rationale": "Paciente relata dor de garganta e congestão nasal há 3 dias. Exame mostra hiperemia de orofaringe.",
      "supportingEvidence": ["S: dor de garganta", "O: hiperemia orofaringe"]
    }
  ],
  "cpt": [
    {
      "code": "99213",
      "description": "Office visit, established patient, low complexity",
      "confidence": 0.88,
      "rationale": "Problema agudo sem complicação, decisão médica de baixa complexidade.",
      "emLevel": 3
    }
  ],
  "risks": {
    "upcoding": false,
    "downcoding": false,
    "missingSpecificity": false
  }
}
```
