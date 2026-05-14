# 🏗 Arquitetura Medalhão

Esta arquitetura organiza os dados em camadas para **garantir qualidade, governanca e performance**. O pipeline e orquestrado pelo Databricks Jobs, executando notebooks em sequencia e promovendo os dados da Landing ate o consumo analitico.

---

## 🎯 Entradas e saidas

**Entradas**

- Fonte operacional: **MongoDB Atlas**
- Entidades: **clientes, carros, apolices, sinistros, enderecos**
- Extracao via Pandas e salvamento em **CSV na Landing Zone**

**Saidas**

- Tabelas **Delta** em Bronze, Silver e Gold
- **Gold** preparado para consumo por BI, analytics e ML

---

## 🔁 Fluxo detalhado

1. **Setup** cria schemas e volumes
2. **Extracao** conecta no Mongo, remove `_id` e grava CSVs na Landing
3. **Bronze** adiciona metadados tecnicos e salva em Delta
4. **Silver** faz limpeza, tipagem e tratamento de nulos
5. **Gold** aplica modelagem dimensional com SCD Tipo 1 (upsert)

---

## 🧭 Diagrama avancado da arquitetura

```mermaid
%%{init: {"theme": "dark", "themeVariables": {"edgeLabelBackground": "transparent"}}}%%
flowchart TD
    classDef landing fill:#37474f,stroke:#fff,stroke-width:1px,color:#fff
    classDef bronze fill:#cd7f32,stroke:#fff,stroke-width:1px,color:#fff
    classDef silver fill:#757575,stroke:#fff,stroke-width:1px,color:#fff
    classDef gold fill:#b7791f,stroke:#fff,stroke-width:1px,color:#fff
    classDef step fill:#2d3748,stroke:#4a5568,color:#fff

    subgraph Orquestracao [Databricks Workflows Jobs]
        J0[00_Setup]:::step
        J1[01_Extracao_Mongo]:::step
        J2[02_Bronze]:::step
        J3[03_Silver]:::step
        J4[04_Gold]:::step
        J0 --> J1 --> J2 --> J3 --> J4
    end

    M[MongoDB Atlas]:::step -->|Leitura via<br>Pandas| L[Landing Zone<br>CSV em /Volumes/workspace/landing/dados]:::landing
    L -->|Ingestao| B[Bronze<br>Delta + metadados]:::bronze
    B -->|Qualidade e<br>padronizacao| S[Silver<br>Delta limpo e tipado]:::silver
    S -->|Modelagem<br>dimensional| G[Gold<br>Fato + Dimensoes - SCD Tipo 1]:::gold
    G -->|Consumo| C[BI / Analytics / ML]:::step

    J1 -.-> L
    J2 -.-> B
    J3 -.-> S
    J4 -.-> G

    style Orquestracao fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
```

---

## 🧱 Camadas e responsabilidades

### 🥉 Bronze

- Ingestao fiel ao dado bruto
- Metadados tecnicos adicionados
- Historico completo preservado

### 🥈 Silver

- Limpeza e padronizacao
- Tipagem de dados e regras de negocio
- Tratamento de nulos e duplicidades

### 🥇 Gold

- Modelo dimensional (fato e dimensoes)
- Upsert com SCD Tipo 1
- Dados prontos para consumo analitico