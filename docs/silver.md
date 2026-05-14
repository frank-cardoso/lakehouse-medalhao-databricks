# 🥈 Silver Layer

A camada Silver realiza limpeza e padronização.

## Processamentos

- Tratamento de nulos
- Remoção de duplicados
- Conversão de tipos
- Padronização

---

## Pipeline

```mermaid
    A[Bronze]        -->|Validação|     B[Validação]
    B[Validação]     -->|Transformação| C[Transformação]
    C[Transformação] -->|Cálculo|       D[Silver]
```

---

## Benefícios

- Melhor qualidade dos dados
- Consistência
- Dados confiáveis