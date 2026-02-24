# ambient-clinical-scribe

> Squad especialista em documentação clínica automatizada por IA ambient — do áudio da consulta ao prontuário completo com nota SOAP, códigos ICD-10/CPT e revisão de qualidade. Redução de 69.5% no tempo administrativo de médicos.

## Instalação

```bash
npx squads add gutomec/squads-sh-aios/ambient-clinical-scribe
```

## O que Faz

O **ambient-clinical-scribe** é um squad que automatiza todo o pipeline de documentação clínica:

1. **Captura** — Transcrição em tempo real de consultas médicas com diarização de speakers
2. **Documentação** — Geração de notas clínicas estruturadas em formato SOAP
3. **Codificação** — Atribuição automática de códigos ICD-10 e CPT
4. **Qualidade** — Revisão de completude, precisão e compliance HIPAA/CMS

Médicos gastam 3+ horas extras por semana em documentação administrativa. Este squad reduz esse tempo em 69.5%, permitindo mais foco no atendimento ao paciente.

## Agentes

| Agente | ID | Papel |
|---|---|---|
| 🎙️ AmbientListener | `ambient-listener` | Transcrição de consultas em tempo real |
| 📋 NoteDrafter | `clinical-note-drafter` | Geração de notas SOAP estruturadas |
| 🏥 MedicalCoder | `medical-coder` | Codificação ICD-10 e CPT |
| ✅ QualityReviewer | `quality-reviewer` | Revisão de qualidade e compliance |

## Workflows

| Workflow | Comando | Descrição | Duração |
|---|---|---|---|
| Full Documentation | `*document-visit` | Pipeline completo (transcrição + nota + codificação + revisão) | 5-15 min |
| Quick Note | `*quick-note` | Nota SOAP rápida sem codificação | 3-8 min |

## Quick Start

```
# Ativar o scribe e documentar uma visita completa
/acs:agents:ambient-listener
*document-visit

# Gerar nota rápida sem codificação
*quick-note

# Apenas gerar nota SOAP
/acs:agents:clinical-note-drafter
*draft-note --format=soap

# Apenas codificação médica
/acs:agents:medical-coder
*assign-codes

# Revisão de qualidade
/acs:agents:quality-reviewer
*review-note
```

## Comandos Disponíveis

| Comando | Agente | Descrição |
|---|---|---|
| `*start-listening` | AmbientListener | Iniciar captura em tempo real |
| `*transcribe-session` | AmbientListener | Transcrever arquivo de áudio |
| `*draft-note` | NoteDrafter | Gerar nota clínica estruturada |
| `*format-soap` | NoteDrafter | Formatar dados em SOAP |
| `*assign-codes` | MedicalCoder | Atribuir códigos ICD-10/CPT |
| `*validate-codes` | MedicalCoder | Validar códigos atribuídos |
| `*review-note` | QualityReviewer | Revisar nota clínica |
| `*compliance-check` | QualityReviewer | Verificar compliance HIPAA/CMS |
| `*document-visit` | Pipeline | Documentação completa |
| `*full-documentation` | Pipeline | Documentação completa (alias) |
| `*quick-note` | Pipeline | Nota rápida sem codificação |
| `*draft-visit` | Pipeline | Nota rápida (alias) |

## Compliance

Este squad foi projetado com compliance em mente:

- **HIPAA** — Proteção de PHI (Protected Health Information) em todas as etapas
- **CMS Guidelines** — Aderência a documentation guidelines para codificação e reembolso
- **OIG Compliance** — Prevenção de upcoding/downcoding e fraude de codificação

**IMPORTANTE:** A implementação de compliance real depende da infraestrutura de deploy. Este squad fornece as verificações e validações, mas a segurança de dados (encriptação, controle de acesso, audit trail) deve ser implementada na camada de infraestrutura.

## Autor

**Luiz Gustavo Vieira Rodrigues** ([@gutomec](https://github.com/gutomec))

## Licença

MIT
