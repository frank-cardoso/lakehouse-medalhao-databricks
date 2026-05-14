# 🥇 Gold Layer

A camada Gold entrega o **modelo dimensional** para consumo, com Fato e Dimensoes geradas via **MERGE INTO (SCD Tipo 1)**.

---

## 🎯 Objetivos

- Criar metricas confiaveis
- Gerar KPIs
- Disponibilizar dados para BI e analytics

---

## 🔁 Fluxo analitico

```mermaid
%%{init: {"theme": "dark", "themeVariables": {"edgeLabelBackground": "transparent"}}}%%
flowchart TD
    classDef silver fill:#757575,stroke:#fff,stroke-width:1px,color:#fff
    classDef gold fill:#b7791f,stroke:#fff,stroke-width:1px,color:#fff
    classDef step fill:#2d3748,stroke:#4a5568,color:#fff

    subgraph SV [Camada Silver]
        A[Tabelas Delta<br>Silver]:::silver
    end

    subgraph PROC [Modelagem Dimensional - NB 04]
        B[Dimensoes<br>dim_cliente, dim_apolice]:::step
        C[Fatos<br>fato_sinistros, fato_premios]:::step
    end

    subgraph GL [Camada Gold]
        D[Tabelas Delta<br>Gold prontas para BI]:::gold
    end

    A -->|read format<br>delta| B
    A -->|read format<br>delta| C
    B -->|merge into -<br>scd1 upsert| D
    C -->|merge into -<br>scd1 upsert| D

    style SV fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
    style PROC fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
    style GL fill:none,stroke:#718096,stroke-width:2px,stroke-dasharray:5
```

---

## ✅ Regras principais

- Modelagem dimensional (Fato e Dimensoes)
- SCD Tipo 1 com **MERGE INTO** (upsert)
- Chaves substitutas quando necessario

### 💻 Exemplo de Código (PySpark)

```python
spark.sql(
        """
        MERGE INTO gold.dim_cliente AS tgt
        USING silver.clientes AS src
        ON tgt.cliente_id = src.cliente_id
        WHEN MATCHED THEN UPDATE SET
            tgt.nome = src.nome,
            tgt.cpf = src.cpf,
            tgt.data_nascimento = src.data_nascimento
        WHEN NOT MATCHED THEN INSERT (cliente_id, nome, cpf, data_nascimento)
        VALUES (src.cliente_id, src.nome, src.cpf, src.data_nascimento)
        """
)
```

---

## 🧩 Exemplo simplificado de schema

```text
fato_sinistros
    - sinistro_id (string)
    - cliente_sk (int)
    - apolice_sk (int)
    - data_sinistro (date)
    - valor_sinistro (decimal)

dim_cliente
    - cliente_sk (int)
    - cliente_id (string)
    - nome (string)
    - cpf (string)
```