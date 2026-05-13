# 🥉 Bronze Layer

A camada Bronze é responsável pela ingestão dos dados brutos.

## Objetivos

- Preservar dados originais
- Garantir rastreabilidade
- Permitir reprocessamento

---

## Fluxo

```mermaid
flowchart TD

A[Fonte de Dados] --> B[Landing Zone]
B --> C[Bronze Delta Table]
```

---

## Características

- Dados sem transformação
- Estrutura original mantida
- Particionamento inicial