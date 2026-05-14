# 🥉 Bronze Layer

A camada Bronze captura o dado **bruto** da Landing Zone e adiciona metadados tecnicos para rastreabilidade, mantendo historico completo.

---

## 🎯 Objetivos

- Preservar dados originais
- Garantir rastreabilidade
- Permitir reprocessamento

---

## 🔁 Fluxo

```mermaid
%%{init: {"theme": "dark", "themeVariables": {"edgeLabelBackground": "transparent"}}}%%
flowchart TD
    classDef landing fill:#37474f,stroke:#fff,stroke-width:1px,color:#fff
    classDef bronze fill:#cd7f32,stroke:#fff,stroke-width:1px,color:#fff
    classDef step fill:#2d3748,stroke:#4a5568,color:#fff

    subgraph LZ [Landing Zone]
        A[Arquivos CSV<br>Volume Landing]:::landing
    end

    subgraph PROC [Processamento Bronze - NB 02]
        B[Leitura CSV]:::step
        C[Adicionar metadados<br>data_hora_bronze<br>nome_arquivo]:::step
    end

    subgraph BR [Camada Bronze]
        D[Tabelas Delta<br>Bronze]:::bronze
    end

    A -->|spark read<br>csv| B
    B -->|withColumn +<br>input_file_name| C
    C -->|write format<br>delta| D

    style LZ fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
    style PROC fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
    style BR fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
```

---

## ✅ Regras principais

- Leitura dos CSVs da Landing
- Adicao de metadados: `data_hora_bronze`, `nome_arquivo`
- Persistencia em **Delta** sem transformacoes de negocio

### 💻 Exemplo de Código (PySpark)

```python
from pyspark.sql.functions import current_timestamp, input_file_name

landing_path = "/Volumes/workspace/landing/dados/clientes/*.csv"

df = (
    spark.read.option("header", True).csv(landing_path)
    .withColumn("data_hora_bronze", current_timestamp())
    .withColumn("nome_arquivo", input_file_name())
)

(
    df.write.format("delta")
    .mode("append")
    .saveAsTable("bronze.clientes")
)
```

---

## 🧩 Exemplo simplificado de schema

```text
cliente_id (string)
nome (string)
cpf (string)
data_nascimento (string)
data_hora_bronze (timestamp)
nome_arquivo (string)
```