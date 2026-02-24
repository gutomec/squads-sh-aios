# Coding Standards — adaptive-tutor-k12

## Linguagem
- Markdown para conteúdo educacional e relatórios
- YAML para configurações e trilhas de aprendizagem
- JSON para dados de progresso, avaliações e perfis de aluno
- Convenções de nomenclatura padrão AIOS

## Convenções de Nomes
- Variáveis e funções: camelCase (`diagnosticReport`, `learningPath`, `masteryScore`)
- Constantes: UPPER_SNAKE_CASE (`MAX_DIFFICULTY_LEVEL`, `MIN_MASTERY_THRESHOLD`)
- Arquivos: kebab-case (`run-diagnostic-assessment.md`, `learning-path.md`)
- IDs de aluno: `STU-YYYYMMDD-NNNN` (`STU-20260224-0001`)
- Relatórios: kebab-case com prefixo tipo (`diagnostic-report.md`, `progress-report.md`)

## Pedagogia
- Linguagem inclusiva e sem estereótipos de gênero, raça ou classe
- Acessível para diferentes idades — adaptar vocabulário ao nível do aluno
- Tom encorajador e positivo — celebrar acertos, guiar nos erros
- Exemplos diversos e representativos (nomes, contextos, culturas)
- Feedback construtivo — nunca punitivo ou desmotivador

## Privacidade e Compliance
- **COPPA** (Children's Online Privacy Protection Act) — Proteção de dados de menores nos EUA
- **LGPD** (Lei Geral de Proteção de Dados) — Proteção de dados pessoais no Brasil
- NUNCA armazenar dados sensíveis de menores sem consentimento
- Mascarar dados de identificação em logs e relatórios compartilhados
- Consentimento dos pais/responsáveis obrigatório para coleta de dados
- Dados de alunos menores de 13 anos requerem tratamento especial

## Acessibilidade
- Suportar múltiplos estilos de aprendizagem em todo conteúdo
- Explicações alternativas para alunos com dificuldades de aprendizagem
- Contraste e legibilidade adequados em conteúdo visual
- Linguagem clara e objetiva — evitar jargão desnecessário

## Conteúdo Educacional
- Alinhamento com padrões curriculares (BNCC/Common Core) obrigatório
- Exercícios com feedback imediato e explicação do raciocínio
- Múltiplas abordagens para cada conceito (visual, verbal, prática)
- Dificuldade adaptativa — nunca exercícios aleatórios sem propósito
- Revisão espaçada incorporada em toda trilha de aprendizagem

## Testes
- Validar adaptação de dificuldade com cenários de acerto/erro
- Testar acessibilidade de linguagem em relatórios para pais
- Verificar alinhamento curricular com base BNCC/Common Core
- Simular diferentes perfis de aluno (alto desempenho, lacunas, estagnação)
