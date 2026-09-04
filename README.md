# 🚀 DATA QUALITY FRAMEWORK

Framework genérico e reutilizável para **análise, monitoramento e avaliação da qualidade de dados** desenvolvido em **Databricks com PySpark**.

O projeto foi concebido para analisar diferentes DataFrames e fontes de dados de forma automatizada, sem depender previamente do significado das colunas, do domínio de negócio ou de regras específicas de uma determinada fonte.

A arquitetura foi estruturada de forma **modular, independente e escalável**, permitindo que cada etapa seja desenvolvida, executada e evoluída individualmente.

---

## 🎯 Objetivo do Projeto

O objetivo deste projeto é desenvolver um **framework de Data Quality capaz de avaliar sistematicamente diferentes características dos dados**, desde sua estrutura até seus relacionamentos e possíveis anomalias.

O framework busca transformar análises de qualidade que normalmente são realizadas de maneira manual ou específica para cada dataset em um processo:

* **Genérico**
* **Automatizado**
* **Reutilizável**
* **Modular**
* **Escalável**
* **Independente da fonte**
* **Orientado a métricas**

> **Princípio fundamental:** o framework deve analisar diferentes fontes de dados sem conhecer previamente o significado das colunas ou depender de regras específicas de negócio.

---

# 🏗️ Arquitetura do Framework

A arquitetura foi organizada em camadas, separando **ingestão, preparação, análise e consolidação**.

```text
                         DATA SOURCES
                              │
                              ▼
                 ┌─────────────────────────┐
                 │ 01_DATA_INGESTION       │
                 │                         │
                 │ Leitura da fonte        │
                 │ DataFrame de entrada    │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │ 02_DATA_PREPARATION     │
                 │                         │
                 │ Schema                  │
                 │ Tipos de coluna         │
                 │ Colunas analisáveis     │
                 │ Configurações           │
                 └────────────┬────────────┘
                              │
          ┌───────────────────┼───────────────────┐
          │                   │                   │
          ▼                   ▼                   ▼
   SCHEMA PROFILE     DISTRIBUTION PROFILE   PATTERN PROFILE
          │                   │                   │
          ├───────────────┬───┴───────────────┬───┤
          │               │                   │
          ▼               ▼                   ▼
   DUPLICITY PROFILE  CONSISTENCY PROFILE  OUTLIER PROFILE
          │               │                   │
          └───────────────┼───────────────────┘
                          │
                          ▼
                CORRELATION PROFILE
                          │
                          ▼
                DATA QUALITY SCORE
                          │
                          ▼
             DASHBOARDS / REPORTS / ALERTS
```

Cada Profile possui responsabilidade analítica própria e pode evoluir independentemente dos demais.

---

# 📊 Roadmap dos Profiles

## 01. DATA INGESTION

Camada responsável por disponibilizar os dados de entrada para o framework.

A origem física dos dados pode variar entre diferentes tecnologias e formatos, como arquivos, bancos de dados, APIs, Delta Lake ou outras fontes.

**Responsabilidade principal:**

> Disponibilizar o DataFrame de entrada para o framework.

---

## 02. DATA PREPARATION

Camada intermediária responsável por preparar o DataFrame para as análises de qualidade.

Realiza automaticamente:

* Validação do DataFrame;
* Identificação do schema;
* Classificação dos tipos de coluna;
* Identificação das colunas analisáveis;
* Configuração dos parâmetros do framework;
* Disponibilização do DataFrame preparado.

**Responsabilidade principal:**

> Criar um contrato padronizado entre a ingestão e os Profiles de qualidade.

---

## 03. SCHEMA PROFILE ✅

Analisa a **estrutura técnica do DataFrame**.

Entre as principais características avaliadas estão:

* Tipos de dados;
* Quantidade de colunas;
* Quantidade de registros;
* Valores NULL;
* Valores vazios;
* Valores distintos;
* Cardinalidade;
* Completude;
* Características estruturais do schema.

**Pergunta central:**

> A estrutura dos dados está adequada e completa?

---

## 04. DISTRIBUTION PROFILE 🚧

Analisa como os valores estão **distribuídos dentro das colunas**.

Entre as principais análises estão:

* Resumo da distribuição;
* Frequência dos valores;
* Participação percentual;
* Top valores;
* Concentração dos valores;
* Índice de diversidade;
* Dominância;
* Regularidade da distribuição;
* Visualizações da distribuição.

**Pergunta central:**

> Como os valores estão distribuídos dentro dos dados?

---

## 05. PATTERN PROFILE 🚧

Identifica automaticamente **padrões estruturais presentes nos valores**, sem depender do significado da coluna.

Entre as principais análises estão:

* Comprimento dos valores;
* Variabilidade de comprimento;
* Composição de caracteres;
* Estruturas predominantes;
* Estruturas recorrentes;
* Concentração estrutural;
* Diversidade estrutural;
* Regularidade;
* Desvios de padrão;
* Identificação de estruturas atípicas.

O objetivo é detectar comportamentos como:

```text
123456789
12345678
ABC123456
2026-01-15
XX-999999
```

mesmo quando o framework não conhece o significado da coluna.

**Pergunta central:**

> Os valores seguem padrões estruturais consistentes?

---

## 06. DUPLICITY PROFILE

Analisa a ocorrência de **duplicidade e unicidade dos dados**.

Entre as análises previstas estão:

* Registros duplicados;
* Registros únicos;
* Taxa de duplicidade;
* Cardinalidade;
* Possíveis chaves;
* Repetição de combinações de colunas.

**Pergunta central:**

> Existem registros ou combinações de valores indevidamente repetidos?

---

## 07. CONSISTENCY PROFILE

Avalia a **consistência interna dos dados**, buscando identificar valores ou relações que apresentem comportamentos incoerentes.

A análise poderá considerar:

* Consistência entre colunas;
* Regras estruturais;
* Relações entre atributos;
* Valores incompatíveis;
* Contradições;
* Regras condicionais.

**Pergunta central:**

> Os dados são coerentes entre si?

---

## 08. OUTLIER PROFILE

Identifica **valores estatisticamente atípicos** ou comportamentos que se afastam significativamente do padrão observado.

Entre as abordagens previstas estão:

* Identificação de outliers;
* Distribuição estatística;
* Quartis;
* IQR;
* Z-Score;
* Desvios estatísticos;
* Análise de anomalias.

**Pergunta central:**

> Existem valores que se comportam de maneira significativamente diferente do restante dos dados?

---

## 09. CORRELATION PROFILE

Analisa **relações e associações entre variáveis**, buscando identificar possíveis dependências ou comportamentos relacionados.

Entre as análises previstas estão:

* Correlação entre variáveis numéricas;
* Intensidade das relações;
* Relações positivas e negativas;
* Variáveis potencialmente relacionadas;
* Identificação de possíveis redundâncias.

**Pergunta central:**

> Quais variáveis apresentam relações relevantes entre si?

---

## 10. DATA QUALITY SCORE

Camada responsável por consolidar os resultados produzidos pelos diferentes Profiles.

O objetivo é transformar múltiplas métricas de qualidade em uma **visão consolidada do estado do dataset**.

O Score poderá considerar indicadores relacionados a:

```text
Schema
   +
Distribution
   +
Pattern
   +
Duplicity
   +
Consistency
   +
Outliers
   +
Correlation
        │
        ▼
DATA QUALITY SCORE
```

O resultado permitirá acompanhar:

* Qualidade geral;
* Qualidade por dimensão;
* Principais problemas identificados;
* Colunas críticas;
* Indicadores de degradação;
* Evolução da qualidade ao longo do tempo.

**Pergunta central:**

> Qual é o nível geral de qualidade deste dataset?

---

# 🔄 Fluxo de Evolução

O framework segue uma evolução progressiva das análises:

```text
ESTRUTURA
    ↓
DISTRIBUIÇÃO
    ↓
PADRÕES
    ↓
DUPLICIDADE
    ↓
CONSISTÊNCIA
    ↓
ANOMALIAS
    ↓
RELACIONAMENTOS
    ↓
QUALITY SCORE
```

Essa abordagem permite que o framework evolua de análises mais básicas e estruturais para análises estatísticas e relacionais mais sofisticadas.

---

# 🧩 Princípio de Independência dos Profiles

Um dos principais princípios arquiteturais do projeto é a **independência entre os Profiles**.

Os Profiles não devem depender da origem física dos dados.

Por exemplo, o `DISTRIBUTION_PROFILE` não deve precisar saber se os dados vieram de:

```text
CSV
Parquet
Delta
Oracle
PostgreSQL
API
Kafka
S3
```

Sua única responsabilidade é analisar o DataFrame preparado.

A arquitetura estabelece:

```text
DATA SOURCE
     ↓
DATA INGESTION
     ↓
DATA PREPARATION
     ↓
DATAFRAME PADRONIZADO
     ↓
┌────┴────┬────────┬────────┬─────────┐
│         │        │        │         │
Schema  Distrib. Pattern  Outlier  ...
```

Dessa forma, o mesmo Profile pode ser reutilizado em diferentes datasets.

---

# ▶️ Execução Independente

Cada Profile deverá poder ser executado individualmente.

Por exemplo:

```text
03_SCHEMA_PROFILE
       ↓
02_DATA_PREPARATION
       ↓
01_DATA_INGESTION
```

ou:

```text
05_PATTERN_PROFILE
       ↓
02_DATA_PREPARATION
       ↓
01_DATA_INGESTION
```

Isso permite desenvolver, testar e validar cada componente de forma independente.

A execução integrada do framework será posteriormente coordenada pelo:

```text
00_ORCHESTRATOR
```

---

# 🗂️ Estrutura do Projeto

A estrutura planejada para o projeto é:

```text
DATA_QUALITY_FRAMEWORK/
│
├── 00_ORCHESTRATOR
│
├── 01_DATA_INGESTION
│
├── 02_DATA_PREPARATION
│
├── 03_SCHEMA_PROFILE
│
├── 04_DISTRIBUTION_PROFILE
│
├── 05_PATTERN_PROFILE
│
├── 06_DUPLICITY_PROFILE
│
├── 07_CONSISTENCY_PROFILE
│
├── 08_OUTLIER_PROFILE
│
├── 09_CORRELATION_PROFILE
│
└── 10_DATA_QUALITY_SCORE
```

Essa separação permite que cada notebook tenha uma responsabilidade clara, reduzindo acoplamento e facilitando a manutenção do framework.

---

# 📝 Padrão de Documentação

Todas as etapas analíticas seguem um padrão de documentação técnica dentro dos notebooks.

Cada célula possui quatro componentes principais:

### O QUE FAZ

Descreve o objetivo da operação ou métrica.

### COMO FAZ

Explica tecnicamente como a análise é realizada.

### POR QUE É IMPORTANTE

Apresenta a relevância da análise para Data Quality.

### PERGUNTA RESPONDIDA

Relaciona a métrica com a pergunta de qualidade que está sendo investigada.

Esse padrão permite que o notebook funcione não apenas como código executável, mas também como **documentação técnica e material de auditoria da análise**.

---

# 📈 Visualização dos Resultados

As análises deverão produzir resultados estruturados que possam posteriormente ser utilizados em diferentes camadas de consumo.

```text
PROFILE
   ↓
MÉTRICAS
   ↓
DATAFRAMES DE RESULTADO
   ↓
CONSOLIDAÇÃO
   ↓
DASHBOARD
```

Entre os possíveis consumidores estão:

* Dashboards;
* Relatórios;
* Alertas;
* Monitoramento;
* Processos de auditoria;
* Análises exploratórias;
* Data Quality Score.

---

# 🚧 Roadmap de Desenvolvimento

### Fase 1 — Fundação

* [x] Definição da arquitetura;
* [x] Schema Profile;
* [x] Estrutura do Data Preparation;
* [x] Padronização da documentação;
* [ ] Data Ingestion modular.

### Fase 2 — Perfis Analíticos

* [ ] Distribution Profile;
* [ ] Pattern Profile;
* [ ] Duplicity Profile;
* [ ] Consistency Profile;
* [ ] Outlier Profile;
* [ ] Correlation Profile.

### Fase 3 — Consolidação

* [ ] Padronização das métricas dos Profiles;
* [ ] Data Quality Score;
* [ ] Classificação dos resultados;
* [ ] Identificação das dimensões críticas;
* [ ] Consolidação executiva.

### Fase 4 — Consumo

* [ ] Dashboard de Data Quality;
* [ ] Relatórios automatizados;
* [ ] Sistema de alertas;
* [ ] Histórico dos indicadores;
* [ ] Monitoramento da evolução da qualidade.

### Fase 5 — Orquestração

* [ ] Orchestrator;
* [ ] Execução automatizada;
* [ ] Controle de dependências;
* [ ] Logs de execução;
* [ ] Monitoramento;
* [ ] Integração com Databricks Workflows.

---

# 🛠️ Tecnologias

O framework está sendo desenvolvido utilizando principalmente:

* **Databricks**
* **Apache Spark**
* **PySpark**
* **Python**
* **Delta Lake**
* **Databricks Workflows**
* **Databricks SQL / Visualizations**

---

# 🤝 Contribuições

Contribuições são bem-vindas.

Ao contribuir com o projeto, mantenha os princípios arquiteturais estabelecidos:

* Evitar dependência de domínio;
* Evitar regras específicas de uma única fonte;
* Priorizar reutilização;
* Evitar processamento redundante;
* Documentar as métricas;
* Manter os Profiles independentes;
* Preservar o padrão de nomenclatura e organização do framework.

---

# 📜 Licença

Este projeto está sob a licença **MIT**.

Consulte o arquivo `LICENSE` para obter mais informações.
