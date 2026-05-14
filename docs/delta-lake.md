# 🧊 Delta Lake

O Delta Lake adiciona confiabilidade e transações ACID ao Data Lake.

---

## Funcionalidades

- ACID Transactions
- Time Travel
- Schema Enforcement
- Schema Evolution

---

## Fluxo

```mermaid
%%{init: {"theme": "dark", "themeVariables": {"edgeLabelBackground": "transparent"}}}%%
flowchart TD
    classDef step fill:#2d3748,stroke:#4a5568,color:#fff

    A[Data Lake]:::step -->|Camada de<br>armazenamento| B[Delta Lake]:::step
    B -->|Garantia de<br>consistencia| C[ACID]:::step
    B -->|Historico e<br>versionamento| D[Time Travel]:::step
```

---

## Benefícios

| Funcionalidade | Benefício |
|---|---|
| ACID | Confiabilidade |
| Time Travel | Versionamento |
| Schema Enforcement | Qualidade |