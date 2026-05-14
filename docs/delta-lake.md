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
flowchart TB
    A[Data Lake]  -->|Camada de armazenamento|   B[Delta Lake]
    B[Delta Lake] -->|Garantia de consistência|  C[ACID]
    B[Delta Lake] -->|Histórico e versionamento| D[Time Travel]
```

---

## Benefícios

| Funcionalidade | Benefício |
|---|---|
| ACID | Confiabilidade |
| Time Travel | Versionamento |
| Schema Enforcement | Qualidade |