---
task: draftClinicalNote()
responsavel: "NoteDrafter"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: transcription
    tipo: file
    origen: "ambient-listener (transcribeConsultation())"
    obrigatorio: true
  - campo: noteTemplate
    tipo: string
    origen: "Usuário ou padrão (SOAP, DAP, narrative — padrão: SOAP)"
    obrigatorio: false
  - campo: patientContext
    tipo: object
    origen: "Usuário ou EHR (histórico, medicações, alergias)"
    obrigatorio: false

Saida:
  - campo: structuredClinicalNote
    tipo: file
    destino: "medical-coder, quality-reviewer"
    persistido: true
  - campo: soapSections
    tipo: object
    destino: "medical-coder"
    persistido: true
  - campo: clinicalSummary
    tipo: string
    destino: "quality-reviewer"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Transcrição disponível com segmentos de speaker"
    - "[ ] Formato de nota definido (SOAP/DAP/narrative)"
    - "[ ] Contexto do paciente carregado (se disponível)"
  post-conditions:
    - "[ ] Nota clínica gerada em formato estruturado"
    - "[ ] Todas as seções SOAP preenchidas com dados da transcrição"
    - "[ ] Resumo clínico gerado"
    - "[ ] Nenhum dado clínico inventado — apenas dados da transcrição"
  acceptance-criteria:
    - blocker: true
      criteria: "Nota SOAP gerada com todas as 4 seções preenchidas"
    - blocker: true
      criteria: "Dados clínicos baseados exclusivamente na transcrição"
    - blocker: false
      criteria: "Resumo clínico conciso e preciso"

Performance:
  duration_expected: "1-3 minutos"
  cost_estimated: "Custo de API LLM para geração"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=3s, max=20s)"
  fallback: "Gerar nota parcial com seções disponíveis, flag seções incompletas"
  notification: "quality-reviewer"

Metadata:
  version: "1.0.0"
  dependencies:
    - transcribeConsultation()
  author: "ambient-clinical-scribe"
  created_at: "2026-02-24T00:00:00Z"
---

# Draft Clinical Note

## Flow

```
1. Receber transcrição estruturada do ambient-listener
2. Carregar contexto do paciente (se disponível)
3. Analisar transcrição e categorizar informações (S, O, A, P)
4. Extrair queixa principal (Chief Complaint)
5. Compor HPI (History of Present Illness) a partir do relato
6. Identificar dados de exame físico e sinais vitais
7. Formular Assessment baseado nas informações disponíveis
8. Estruturar Plan (tratamento, meds, referrals, follow-up)
9. Gerar nota SOAP completa
10. Produzir resumo clínico
11. Entregar para codificação (medical-coder)
```

## Template SOAP

```markdown
# Nota Clínica — SOAP

**Paciente:** [ID] | **Data:** [Data] | **Provider:** [Nome]

## S — Subjective
**CC (Chief Complaint):** [Queixa principal]
**HPI:** [History of Present Illness]
**ROS:** [Review of Systems]
**PMH:** [Past Medical History]
**Medications:** [Medicações atuais]
**Allergies:** [Alergias]

## O — Objective
**Vitals:** [Sinais vitais]
**Physical Exam:** [Exame físico]
**Labs/Imaging:** [Resultados de exames]

## A — Assessment
**Diagnosis:** [Diagnóstico/impressão]
**DDx:** [Diagnóstico diferencial]

## P — Plan
**Treatment:** [Tratamento]
**Medications:** [Prescrições]
**Referrals:** [Encaminhamentos]
**Follow-up:** [Retorno]
**Patient Education:** [Orientações]
```
