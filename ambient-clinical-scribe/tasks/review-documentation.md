---
task: reviewDocumentation()
responsavel: "QualityReviewer"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: clinicalNote
    tipo: file
    origen: "clinical-note-drafter (draftClinicalNote())"
    obrigatorio: true
  - campo: assignedCodes
    tipo: object
    origen: "medical-coder (assignMedicalCodes())"
    obrigatorio: true
  - campo: complianceRules
    tipo: file
    origen: "Base de conhecimento (HIPAA, CMS documentation guidelines)"
    obrigatorio: false

Saida:
  - campo: reviewReport
    tipo: file
    destino: "Usuário, clinical-note-drafter, medical-coder"
    persistido: true
  - campo: issuesFound
    tipo: array
    destino: "clinical-note-drafter, medical-coder"
    persistido: true
  - campo: qualityScore
    tipo: number
    destino: "Usuário"
    persistido: true
  - campo: complianceStatus
    tipo: string
    destino: "Usuário"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Nota clínica disponível para revisão"
    - "[ ] Códigos ICD-10/CPT atribuídos"
    - "[ ] Regras de compliance carregadas"
  post-conditions:
    - "[ ] Todas as seções SOAP revisadas para completude"
    - "[ ] Consistência entre nota e códigos verificada"
    - "[ ] Compliance HIPAA verificado"
    - "[ ] Quality score calculado"
    - "[ ] Issues documentados com severidade e recomendação"
  acceptance-criteria:
    - blocker: true
      criteria: "Relatório de qualidade gerado com quality score"
    - blocker: true
      criteria: "Compliance HIPAA verificado — sem violações"
    - blocker: false
      criteria: "Quality score >= 90% para aprovação automática"

Performance:
  duration_expected: "1-2 minutos"
  cost_estimated: "Custo de API LLM para análise"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 2
    delay: "exponential(base=2s, max=15s)"
  fallback: "Gerar relatório parcial com checks disponíveis"
  notification: "clinical-note-drafter"

Metadata:
  version: "1.0.0"
  dependencies:
    - draftClinicalNote()
    - assignMedicalCodes()
  author: "ambient-clinical-scribe"
  created_at: "2026-02-24T00:00:00Z"
---

# Review Documentation

## Flow

```
1. Receber nota clínica e códigos atribuídos
2. Verificar completude das seções SOAP
   - Chief Complaint presente?
   - HPI adequado?
   - Exame físico documentado?
   - Assessment com diagnóstico?
   - Plan com próximos passos?
3. Validar consistência interna
   - Assessment consistente com S + O?
   - Plan consistente com Assessment?
4. Validar códigos contra documentação
   - ICD-10 suportados pela nota?
   - CPT consistentes com procedimentos?
   - Nível E/M justificado?
5. Verificar compliance HIPAA
   - PHI protegido adequadamente?
   - Consentimento documentado?
6. Verificar CMS documentation guidelines
7. Calcular quality score (0-100%)
8. Documentar issues com severidade
9. Gerar relatório de qualidade
10. Aprovar (>= 90%) ou retornar para correção
```

## Categorias de Issues

| Severidade | Descrição | Ação |
|---|---|---|
| CRITICAL | Violação HIPAA ou erro que afeta segurança do paciente | Bloqueia aprovação — correção imediata |
| HIGH | Seção SOAP faltante ou código não suportado pela nota | Correção obrigatória |
| MEDIUM | Especificidade insuficiente ou documentação incompleta | Correção recomendada |
| LOW | Melhorias de formatação ou clareza | Sugestão opcional |
| INFO | Observação informativa | Apenas registro |

## Formato do Relatório

```markdown
# Quality Review Report

**Quality Score:** 92/100 — APPROVED
**Compliance Status:** COMPLIANT

## Issues Found

### HIGH — Missing vitals in Objective
- **Seção:** O (Objective)
- **Descrição:** Sinais vitais não documentados
- **Recomendação:** Adicionar PA, FC, Temp, SpO2

### LOW — Improve specificity
- **Seção:** A (Assessment)
- **Descrição:** Diagnóstico poderia ser mais específico
- **Recomendação:** Especificar localização e lateralidade

## Summary
- Completeness: 18/20
- Accuracy: 19/20
- Compliance: 20/20
- Coding Support: 17/20
- Audit Readiness: 18/20
```
