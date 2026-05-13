# 🔄 Pipeline ETL

O pipeline segue as etapas modernas de engenharia de dados.

---

## Fluxo Completo

```mermaid
flowchart TD

A[Extração] --> B[Bronze]
B --> C[Transformação]
C --> D[Silver]
D --> E[Agregações]
E --> F[Gold]
```

---

## Etapas

### Extração
Coleta dos dados brutos.

### Transformação
Padronização e limpeza.

### Carga
Persistência em Delta Lake.

---

## Benefícios

- Escalabilidade
- Reprocessamento
- Confiabilidade