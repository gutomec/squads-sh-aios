---
task: profileDataset()
responsavel: "Profiler"
responsavel_type: Agente
atomic_layer: Molecule
elicit: false

Entrada:
  - campo: dataset
    tipo: string
    origen: "Usuário ou fullDataQualityAudit() — caminho ou referência do dataset"
    obrigatorio: true
  - campo: format
    tipo: string
    origen: "Usuário — formato dos dados (csv, parquet, json, sql)"
    obrigatorio: false
  - campo: depth
    tipo: string
    origen: "Usuário — profundidade do profiling (quick, standard, deep)"
    obrigatorio: false

Saida:
  - campo: profilingReport
    tipo: file
    destino: "profiling-report.md, anomaly-detector, schema-validator, data-quality-reporter"
    persistido: true
  - campo: columnStats
    tipo: object
    destino: "anomaly-detector, data-quality-reporter"
    persistido: true
  - campo: baselineProfile
    tipo: object
    destino: "anomaly-detector — baseline para comparação futura"
    persistido: true

Checklist:
  pre-conditions:
    - "[ ] Dataset acessível"
    - "[ ] Formato identificado"
  post-conditions:
    - "[ ] Profiling completo de todas as colunas"
    - "[ ] Estatísticas descritivas calculadas"
    - "[ ] Baseline estabelecido"
    - "[ ] profiling-report.md gerado"
  acceptance-criteria:
    - blocker: true
      criteria: "100% das colunas profiladas com tipo, nulls e distribuição"
    - blocker: true
      criteria: "Estatísticas descritivas para colunas numéricas (min, max, mean, median, std)"
    - blocker: false
      criteria: "Comparação com baseline anterior quando disponível"

Performance:
  duration_expected: "5-15 minutos"
  cost_estimated: "~0 (análise local de dados)"
  cacheable: true
  parallelizable: true

Error Handling:
  strategy: retry
  retry:
    max_attempts: 3
    delay: "exponential(base=5s, max=30s)"
  fallback: "Se dataset inacessível, solicitar caminho alternativo ou formato diferente"
  notification: "data-quality-reporter"

Metadata:
  version: "1.0.0"
  dependencies: []
  author: "data-quality-guardian"
  created_at: "2026-02-24T00:00:00Z"
---

# Profile Dataset

## Flow

```
1. Receber dataset e identificar formato
2. Inferir ou carregar schema existente
3. Calcular estatísticas por coluna (count, nulls, unique)
4. Analisar distribuições para colunas numéricas
5. Calcular taxas de nulos e unicidade
6. Identificar tipos de dados inconsistentes
7. Estabelecer baseline de qualidade
8. Gerar profiling-report.md
9. Enviar para @anomaly-detector
```

## Elicitation

- "Qual o dataset ou caminho para profilar?"
- "Qual o formato dos dados? (CSV, Parquet, JSON, SQL table)"
- "Qual a profundidade desejada? (quick, standard, deep)"
- "Há um baseline anterior para comparação?"
