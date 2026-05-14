# ⚡ Databricks

O Databricks foi utilizado como plataforma principal de processamento.

---

## Funcionalidades Utilizadas

- Apache Spark
- Delta Lake
- Notebooks
- Jobs
- Cluster Computing

---

## Benefícios

- Processamento distribuído
- Alta performance
- Integração com Delta Lake

---

## Arquitetura

```mermaid
%%{init: {"theme": "dark", "themeVariables": {"edgeLabelBackground": "transparent"}}}%%
flowchart TD
    classDef step fill:#2d3748,stroke:#4a5568,color:#fff

    subgraph ORQ [Databricks Workflows - Jobs DAG]
        J0[00_Setup]:::step
        J1[01_Extracao_Mongo]:::step
        J2[02_Camada_Bronze]:::step
        J3[03_Camada_Silver]:::step
        J4[04_Camada_Gold]:::step
    end

    subgraph EXEC [Execucao]
        N1[Job Cluster<br>execucoes isoladas]:::step
        N2[Serverless<br>autoscaling gerenciado]:::step
    end

    J0 -->|task<br>dependency| J1
    J1 -->|task<br>dependency| J2
    J2 -->|task<br>dependency| J3
    J3 -->|task<br>dependency| J4

    J1 -->|run<br>on| N1
    J2 -->|run<br>on| N1
    J3 -->|run<br>on| N1
    J4 -->|run<br>on| N2

    style ORQ fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
    style EXEC fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
```
