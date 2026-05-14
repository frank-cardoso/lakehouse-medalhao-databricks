# 🥈 Silver Layer

A camada Silver aplica **limpeza, tipagem e padronizacao**, preparando os dados para consumo analitico com qualidade elevada.

---

## 🔧 Processamentos

- Tratamento de nulos
- Remocao de duplicados
- Conversao de tipos
- Padronizacao de campos

---

## 🔁 Pipeline

```mermaid
%%{init: {"theme": "dark", "themeVariables": {"edgeLabelBackground": "transparent"}}}%%
flowchart TD
    classDef bronze fill:#cd7f32,stroke:#fff,stroke-width:1px,color:#fff
    classDef silver fill:#757575,stroke:#fff,stroke-width:1px,color:#fff
    classDef step fill:#2d3748,stroke:#4a5568,color:#fff

    subgraph BR [Camada Bronze]
        B[Tabelas Delta<br>Bronze]:::bronze
    end

    subgraph PROC [Processamento Silver NB 03]
        N1[Tipagem e validacao]:::step
        N2[Tratamento de nulos<br>e vazios]:::step
        N3[Padronizacao<br>de strings]:::step
    end

    subgraph SL [Camada Silver]
        S[Tabelas Delta Silver<br>clientes carros apolices]:::silver
    end

    B -->|read format delta| N1
    N1 -->|cast to date and int| N2
    N2 -->|fillna and dropna| N3
    N3 -->|trim and upper| S

    style BR fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
    style PROC fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
    style SL fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
```

---

## ✅ Regras principais

- Tipagem correta de datas e numericos
- Padronizacao de textos (ex: upper/lower, trim)
- Remocao de registros duplicados
- Tratamento de nulos conforme regra de negocio

### 💻 Exemplo de Código (PySpark)

```python
from pyspark.sql.functions import col, trim, upper
from pyspark.sql.types import DateType, IntegerType

df = spark.read.format("delta").table("bronze.clientes")

df = df.fillna({"nome": "NA", "cpf": "NA"})
df = df.withColumn("data_nascimento", col("data_nascimento").cast(DateType()))
df = df.withColumn("idade", col("idade").cast(IntegerType()))
df = df.withColumn("nome", upper(trim(col("nome"))))

(
    df.write.format("delta")
    .mode("overwrite")
    .saveAsTable("silver.clientes")
)
```

---

## 🧩 Exemplo simplificado de schema

```text
cliente_id (string)
nome (string)
cpf (string)
data_nascimento (date)
idade (int)
```