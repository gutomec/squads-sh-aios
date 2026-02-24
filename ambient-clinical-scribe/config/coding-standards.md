# Coding Standards — ambient-clinical-scribe

## Linguagem
- TypeScript para scripts de automação e integração
- Python para NLP, NER médico e processamento de áudio
- Markdown para notas clínicas e relatórios
- YAML/JSON para configurações, transcrições e dados estruturados

## Convenções de Nomes
- Variáveis e funções: camelCase (`clinicalNote`, `assignMedicalCodes`)
- Constantes: UPPER_SNAKE_CASE (`MAX_QUALITY_SCORE`, `HIPAA_COMPLIANCE_THRESHOLD`)
- Arquivos: kebab-case (`transcribe-consultation.md`, `coding-report.json`)
- Códigos médicos: sempre maiúsculas com pontuação padrão (`J06.9`, `99213`)

## Segurança & Compliance
- NUNCA armazenar PHI (Protected Health Information) em logs ou arquivos temporários
- Sempre encriptar dados de pacientes em trânsito e em repouso
- Anonimizar dados em ambientes de desenvolvimento e teste
- Seguir HIPAA Security Rule para controle de acesso
- Audit trail obrigatório para todas as ações em dados de pacientes
- Consentimento do paciente documentado antes da captura de áudio

## Documentação Clínica
- Notas SOAP devem conter APENAS informações presentes na transcrição
- Terminologia médica padronizada (UMLS/SNOMED)
- Códigos ICD-10 com máxima especificidade (até 7th character)
- Códigos CPT com modificadores quando aplicável
- Data e hora em formato ISO 8601 (UTC)

## Qualidade de Dados
- Transcrições devem incluir timestamps para cada segmento
- Confidence scores obrigatórios para codificação automática
- Quality score mínimo de 90% para aprovação automática
- Issues documentados com severidade (CRITICAL, HIGH, MEDIUM, LOW, INFO)

## Testes
- Testar transcrição com amostras de áudio de diferentes sotaques
- Validar mapeamento de códigos contra bases oficiais (ICD-10-CM, CPT)
- Testar compliance HIPAA com dados anonimizados
- Verificar quality score em cenários edge case
- Testar integração FHIR com sandbox de EHR

## Interoperabilidade
- Saída de dados em formato HL7 FHIR R4 quando integrado com EHR
- IDs de pacientes seguem formato do sistema EHR integrado
- Timestamps em UTC com timezone offset
- Encoding UTF-8 obrigatório em todos os arquivos
