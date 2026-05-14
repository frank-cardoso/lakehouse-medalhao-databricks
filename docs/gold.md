# 🥇 Gold Layer

Camada analítica final para consumo.

## Objetivos

- Criar métricas
- Gerar KPIs
- Disponibilizar dashboards

---

## Fluxo Analítico

```mermaid
flowchart TB
    A[Silver]     -->|Agregação de métricas|  B[Agregações]
    B[Agregações] -->|Cálculo de indicadores| C[KPIs]
    C[KPIs]       -->|Visualização|           D[Dashboards]
```

---

## Casos de Uso

- Power BI
- Analytics
- Machine Learning