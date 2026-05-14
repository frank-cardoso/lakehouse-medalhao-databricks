# 🚀 Lakehouse Medalhão (Databricks)

## 📌 Problema e objetivo de negócio

A seguradora precisa unificar dados de **clientes, carros, apólices, sinistros e endereços** para acelerar análises, melhorar a qualidade dos relatórios e reduzir retrabalho entre times. Este projeto entrega um **Lakehouse completo** com Arquitetura Medallion na plataforma Databricks, garantindo rastreabilidade, governança e performance ao longo do ciclo de vida dos dados.

Objetivos principais:

- Unificar dados operacionais em uma visão confiável
- Garantir qualidade com camadas de tratamento
- Acelerar o consumo por BI e analytics
- Padronizar processos com orquestração automatizada

---

## 🧭 Fluxo ponta a ponta

1. **Extração (MongoDB Atlas)** com proteção de credenciais via `dbutils.widgets`
2. **Landing Zone (CSV)** em `/Volumes/workspace/landing/dados`
3. **Bronze (Delta)** com metadados técnicos
4. **Silver (Delta)** com limpeza, tipagem e padronização
5. **Gold (Delta)** com modelo dimensional e SCD Tipo 1

---

## 🏗 Arquitetura geral

```mermaid
%%{init: {"theme": "dark", "themeVariables": {"edgeLabelBackground": "transparent"}}}%%
flowchart TD
    classDef landing fill:#37474f,stroke:#fff,stroke-width:1px,color:#fff
    classDef bronze fill:#cd7f32,stroke:#fff,stroke-width:1px,color:#fff
    classDef silver fill:#757575,stroke:#fff,stroke-width:1px,color:#fff
    classDef gold fill:#b7791f,stroke:#fff,stroke-width:1px,color:#fff
    classDef step fill:#2d3748,stroke:#4a5568,color:#fff

    S[MongoDB Atlas]:::step -->|Extracao via<br>Pandas| L[Landing Zone<br>CSV]:::landing
    L -->|Ingestao| B[Bronze<br>Delta]:::bronze
    B -->|Qualidade e<br>padronizacao| C[Silver<br>Delta]:::silver
    C -->|Modelagem<br>dimensional| D[Gold<br>Delta]:::gold
    D -->|Consumo| BI[BI / Analytics / ML]:::step
```

---

## ✅ O que esta documentado

- **Arquitetura** e fluxo do Lakehouse
- **Camadas Bronze, Silver e Gold** com regras aplicadas
- **Orquestracao do pipeline** no Databricks Jobs
- **Tecnologias** utilizadas e seus beneficios

---

## ⚙️ Tecnologias utilizadas

| Tecnologia | Finalidade |
|---|---|
| Databricks | Processamento distribuido e orquestracao |
| Apache Spark | ETL escalavel |
| Delta Lake | Armazenamento transacional e ACID |
| MongoDB Atlas | Fonte operacional |
| Python / PySpark | Transformacoes e modelagem |
| MkDocs | Documentacao |