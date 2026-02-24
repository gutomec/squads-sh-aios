---
task: transcribeConsultation()
responsavel: "AmbientListener"
responsavel_type: Agente
atomic_layer: Organism
elicit: false

Entrada:
  - campo: audioSource
    tipo: file
    origen: "Usuário (arquivo de áudio ou stream da consulta)"
    obrigatorio: true
  - campo: sessionMetadata
    tipo: object
    origen: "Usuário (patient ID, date, provider)"
    obrigatorio: true
  - campo: language
    tipo: string
    origen: "Usuário (pt-BR, en-US, es — padrão: pt-BR)"
    obrigatorio: false

Saida:
  - campo: rawTranscription
    tipo: file
    destino: "clinical-note-drafter"
    persistido: true
  - campo: speakerSegments
    tipo: array
    destino: "clinical-note-drafter"
    persistido: true
  - campo: medicalTermsIdentified
    tipo: array
    destino: "clinical-note-drafter, medical-coder"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Fonte de áudio disponível e acessível"
    - "[ ] Metadados da sessão informados (patient ID, data, provider)"
    - "[ ] Engine de speech-to-text configurado"
    - "[ ] Idioma da consulta definido"
  post-conditions:
    - "[ ] Transcrição gerada com timestamps"
    - "[ ] Speakers identificados e segmentados (médico, paciente)"
    - "[ ] Termos médicos identificados e listados"
    - "[ ] Qualidade da transcrição verificada"
  acceptance-criteria:
    - blocker: true
      criteria: "Transcrição gerada com segmentos de speaker distintos"
    - blocker: true
      criteria: "Termos médicos identificados e preservados corretamente"

Performance:
  duration_expected: "2-5 minutos (para consulta de 15-30 min)"
  cost_estimated: "Variável por engine de STT utilizado"
  cacheable: false
  parallelizable: false

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=2s, max=30s)"
  fallback: "Verificar qualidade do áudio, tentar engine alternativo"
  notification: "clinical-note-drafter"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "ambient-clinical-scribe"
  created_at: "2026-02-24T00:00:00Z"
---

# Transcribe Consultation

## Flow

```
1. Receber áudio da consulta (arquivo ou stream)
2. Configurar engine de speech-to-text
3. Processar áudio com transcrição
4. Realizar diarização de speakers
5. Identificar termos médicos via NER
6. Mapear termos para UMLS/SNOMED
7. Gerar transcrição estruturada com timestamps
8. Validar qualidade da transcrição
9. Entregar ao pipeline (clinical-note-drafter)
```

## Engines Suportados

### OpenAI Whisper (batch)
```
whisper audio.wav --model large-v3 --language pt --task transcribe
```

### Azure Speech Services (real-time)
```
Configurar SpeechConfig com medical vocabulary
Ativar diarization via ConversationTranscriber
```

### Formato de Saída

```json
{
  "sessionId": "sess-2024-01-15-001",
  "duration": "00:22:15",
  "speakers": ["Dr. Silva", "Paciente"],
  "segments": [
    {
      "speaker": "Dr. Silva",
      "start": "00:00:05",
      "end": "00:00:12",
      "text": "Bom dia, como você está se sentindo?"
    },
    {
      "speaker": "Paciente",
      "start": "00:00:13",
      "end": "00:00:28",
      "text": "Doutor, estou com uma dor de cabeça forte há 3 dias..."
    }
  ],
  "medicalTerms": [
    { "term": "cefaleia", "code": "UMLS:C0018681", "context": "dor de cabeça forte" }
  ]
}
```
