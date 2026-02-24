---
task: fullClinicalDocumentation()
responsavel: "NoteDrafter"
responsavel_type: Agente
atomic_layer: Page
elicit: true

Entrada:
  - campo: consultationSource
    tipo: file
    origen: "Usuário (arquivo de áudio, transcrição existente, ou stream)"
    obrigatorio: true
  - campo: patientContext
    tipo: object
    origen: "Usuário ou EHR (patient ID, histórico, medicações, alergias)"
    obrigatorio: true
  - campo: noteFormat
    tipo: string
    origen: "Usuário (SOAP, DAP, narrative — padrão: SOAP)"
    obrigatorio: false
  - campo: specialty
    tipo: string
    origen: "Usuário (clínica geral, cardiologia, etc.)"
    obrigatorio: false

Saida:
  - campo: documentationPackage
    tipo: object
    destino: "Usuário, EHR"
    persistido: true
  - campo: clinicalNote
    tipo: file
    destino: "documentationPackage"
    persistido: true
  - campo: codingReport
    tipo: file
    destino: "documentationPackage"
    persistido: true
  - campo: qualityReport
    tipo: file
    destino: "documentationPackage"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Fonte da consulta disponível (áudio ou transcrição)"
    - "[ ] Dados do paciente informados (ID, contexto clínico)"
    - "[ ] Engine de transcrição configurado"
    - "[ ] Formato de nota definido"
  post-conditions:
    - "[ ] Transcrição gerada com speakers identificados"
    - "[ ] Nota clínica SOAP gerada e completa"
    - "[ ] Códigos ICD-10 e CPT atribuídos"
    - "[ ] Revisão de qualidade com score >= 90%"
    - "[ ] Pacote de documentação completo gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "Nota clínica SOAP gerada com todas as seções preenchidas"
    - blocker: true
      criteria: "Códigos ICD-10 e CPT atribuídos com confidence >= 80%"
    - blocker: true
      criteria: "Quality review score >= 90%"
    - blocker: false
      criteria: "Compliance HIPAA verificado sem violações"
    - blocker: false
      criteria: "Documentação pronta para integração com EHR"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "Variável (STT + LLM APIs)"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=60s)"
  fallback: "Pausar pipeline, reportar erro com contexto e sugerir correção"
  notification: "quality-reviewer"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "ambient-clinical-scribe"
  created_at: "2026-02-24T00:00:00Z"
---

# Full Clinical Documentation

## Pipeline

```
Fase 1: Transcrição    → @ambient-listener      → transcribeConsultation()
Fase 2: Nota Clínica   → @clinical-note-drafter  → draftClinicalNote()
Fase 3: Codificação    → @medical-coder          → assignMedicalCodes()
Fase 4: Revisão        → @quality-reviewer        → reviewDocumentation()
```

## Elicitation

### Fase 0 — Contexto
- "Qual a fonte da consulta? (arquivo de áudio, transcrição existente)"
- "Qual o ID do paciente?"
- "Qual a especialidade? (clínica geral, cardiologia, ortopedia, etc.)"
- "Formato de nota preferido? (SOAP, DAP, narrative — padrão: SOAP)"

### Fase 1 — Transcrição
- "Idioma da consulta? (pt-BR, en-US, es — padrão: pt-BR)"
- "Quantos participantes na consulta? (médico + paciente + acompanhante?)"

### Fase 4 — Revisão
- "Quality score mínimo aceitável? (padrão: 90%)"
- "Deseja incluir codificação médica (ICD-10/CPT)? (padrão: sim)"

### Fase Final — Entrega
- "Deseja exportar para formato EHR (HL7 FHIR)?"
- "Deseja salvar no prontuário eletrônico?"

## Pacote de Documentação Final

```
documentation-package/
├── clinical-note.md          # Nota clínica SOAP
├── transcription.json        # Transcrição com timestamps
├── coding-report.json        # Códigos ICD-10/CPT
├── quality-report.md         # Relatório de qualidade
└── metadata.json             # Metadados da sessão
```
