# 🚀 Lakehouse Medalhão com Databricks

## 📖 Sobre o Projeto

Este projeto implementa uma arquitetura **Lakehouse Medalhão** utilizando:

- Apache Spark
- Delta Lake
- Databricks
- PySpark

O pipeline segue o padrão moderno de engenharia de dados dividido em:

- 🥉 Bronze Layer
- 🥈 Silver Layer
- 🥇 Gold Layer

---

## 🏗 Arquitetura Geral

```mermaid
flowchart TB
    A[Landing Zone] -->|Ingestão|   B[Bronze Layer]
    B[Bronze Layer] -->|Tratamento| C[Silver Layer]
    C[Silver Layer] -->|Agregação|  D[Gold Layer]
```

---

## 🎯 Objetivos

- Criar pipeline escalável
- Garantir qualidade dos dados
- Aplicar arquitetura moderna
- Implementar boas práticas de engenharia de dados

---

## ⚙️ Tecnologias Utilizadas

| Tecnologia | Finalidade |
|---|---|
| Databricks | Processamento distribuído |
| Apache Spark | ETL |
| Delta Lake | Armazenamento transacional |
| Python | Desenvolvimento |
| MkDocs | Documentação |

---

## 📂 Estrutura do Projeto

```bash
.
├── docs/
│   ├── arquitetura.md
│   ├── bronze.md
│   ├── databricks.md
│   ├── delta-lake.md
│   ├── gold.md
│   ├── index.md
│   ├── silver.md
│   └── stylesheets/
└── notebooks/
    ├── 000_-_Atividade_Pratica_-_Lakehouse_-_Preparando_ambiente.ipynb
    ├── 001_- Atividade Pratica - Lakehouse - Extracao.ipynb
    ├── 002_-_Atividade_Pratica_-_Lakehouse_-_Bronze.ipynb
    ├── 003_-_Atividade_Pratica_-_Lakehouse_-_Silver.ipynb
    ├── 004_-_Atividade_Pratica_-_Lakehouse_-_Gold.ipynb
    └── 005_-_Atifidade_Pratica_-_Lakehouse_-_Destruindo_ambiente.ipynb
```