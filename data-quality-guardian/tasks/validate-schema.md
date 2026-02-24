---
task: validateSchema()
responsavel: "SchemaValidator"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: dataset
    tipo: string
    origen: "Usuário ou fullDataQualityAudit() — dataset para validação"
    obrigatorio: true
  - campo: expectedSchema
    tipo: object
    origen: "Projeto ou Usuário — schema esperado"
    obrigatorio: false
  - campo: references
    tipo: array
    origen: "Projeto — tabelas/entidades de referência para integridade"
    obrigatorio: false

Saida:
  - campo: schemaReport
    tipo: file
    destino: "schema-validation-report.md, data-quality-reporter, remediation-suggester"
    persistido: true
  - campo: breakingChanges
    tipo: array
    destino: "data-quality-reporter, remediation-suggester"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Dataset disponível"
    - "[ ] Schema esperado definido (ou inferido)"
  post-conditions:
    - "[ ] Schema validado campo a campo"
    - "[ ] Breaking changes identificadas"
    - "[ ] Integridade referencial verificada"
    - "[ ] schema-validation-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "100% dos campos validados contra schema esperado"
    - blocker: true
      criteria: "Breaking changes listadas com impacto downstream"
    - blocker: false
      criteria: "Integridade referencial verificada entre entidades"

Performance:
  duration_expected: "5-10 minutos"
  cost_estimated: "~0 (validação local)"
  cacheable: true
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se schema esperado não disponível, inferir schema do dataset e reportar como baseline"
  notification: "data-quality-reporter"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "data-quality-guardian"
  created_at: "2026-02-24T00:00:00Z"
---

# Validate Schema

## Flow

```
1. Receber dataset e schema esperado
2. Inferir ou carregar schema esperado
3. Validar tipos de dados campo a campo
4. Verificar constraints (not null, unique, check)
5. Checar integridade referencial entre tabelas/entidades
6. Detectar breaking changes vs versão anterior do schema
7. Avaliar compatibilidade backward/forward
8. Gerar schema-validation-report.md
9. Enviar para @data-quality-reporter
```

## Elicitation

- "Qual o dataset para validação de schema?"
- "Há um schema esperado documentado? (JSON Schema, Avro, DDL)"
- "Quais tabelas/entidades devem ser verificadas para integridade referencial?"
- "Qual a versão anterior do schema para detecção de breaking changes?"
