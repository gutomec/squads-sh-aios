# Tech Stack — ambient-clinical-scribe

## Speech-to-Text
- **OpenAI Whisper** (large-v3) — Transcrição de alta precisão, suporte multilíngue, batch processing
- **Azure Speech Services** — Transcrição em tempo real, baixa latência, medical vocabulary customizado
- **Google Cloud Speech-to-Text** — Alternativa para streaming, boa precisão geral
- **AWS Transcribe Medical** — Especializado em terminologia médica, vocabulário clínico nativo

## NLP & Medical NER
- **UMLS (Unified Medical Language System)** — Ontologia médica de referência para mapeamento de termos
- **SNOMED CT** — Terminologia clínica padronizada internacional
- **spaCy (en_core_sci_lg / scispacy)** — NER médico para identificação de entidades clínicas
- **Hugging Face Bio-NER** — Modelos pré-treinados para reconhecimento de entidades biomédicas
- **MetaMap / QuickUMLS** — Mapeamento de texto para conceitos UMLS

## Sistemas de Codificação
- **ICD-10-CM** — International Classification of Diseases, 10th Revision, Clinical Modification (diagnósticos)
- **CPT (Current Procedural Terminology)** — Códigos de procedimentos e serviços (AMA)
- **HCPCS Level II** — Healthcare Common Procedure Coding System (suprimentos e serviços)
- **LOINC** — Logical Observation Identifiers Names and Codes (resultados de laboratório)

## Integração EHR
- **HL7 FHIR (R4)** — Standard de interoperabilidade para troca de dados clínicos
- **SMART on FHIR** — Framework de autorização para aplicações em EHR
- **CDA (Clinical Document Architecture)** — Standard de documentos clínicos HL7
- **C-CDA** — Consolidated CDA para troca de dados entre sistemas

## Compliance & Segurança
- **HIPAA** — Health Insurance Portability and Accountability Act (privacidade de dados de saúde)
- **CMS Documentation Guidelines** — Guidelines de documentação para codificação e reembolso
- **OIG Compliance** — Office of Inspector General compliance para codificação médica
- **HITECH Act** — Health Information Technology for Economic and Clinical Health

## LLM & IA
- **Claude / GPT-4** — Geração de notas clínicas estruturadas a partir de transcrições
- **Embedding models** — Similarity search para mapeamento de códigos
- **Fine-tuned medical models** — Modelos especializados em terminologia médica

## Formatos de Dados
- **JSON** — Transcrições, relatórios de codificação, metadados
- **Markdown** — Notas clínicas, relatórios de qualidade
- **YAML** — Configurações e workflows
- **HL7 FHIR JSON** — Integração com prontuários eletrônicos
