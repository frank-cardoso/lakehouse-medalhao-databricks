# 🏗 Arquitetura Medalhão

A arquitetura Medalhão organiza os dados em múltiplas camadas para melhorar:

- Governança
- Qualidade
- Escalabilidade
- Performance

---

## Fluxo da Arquitetura

```mermaid
    A[Landing Zone] 
    A --> B[Bronze Layer]
    B --> C[Silver Layer]
    C --> D[Gold Layer]
```

---

## 🥉 Bronze Layer

Camada responsável pela ingestão dos dados brutos.

Características:

- Dados sem tratamento
- Histórico completo
- Alta volumetria

---

## 🥈 Silver Layer

Camada responsável pela limpeza e transformação.

Características:

- Padronização
- Tratamento de nulos
- Regras de negócio

---

## 🥇 Gold Layer

Camada analítica final.

Características:

- KPIs
- Agregações
- Dados prontos para BI