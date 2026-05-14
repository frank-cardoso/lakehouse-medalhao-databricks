# ▶️ Execucao do Pipeline no Databricks

Esta secao descreve a orquestracao completa do Lakehouse no Databricks Jobs, com **execucao sequencial** dos notebooks e protecao de credenciais via `dbutils.widgets`.

---

## 🧭 Ordem de execucao (Databricks Workflows)

1. **00_Setup**
   - Cria schemas `landing`, `bronze`, `silver`, `gold`
   - Cria o Volume para a Landing Zone

2. **01_Extracao_Mongo**
   - Conecta no MongoDB Atlas
   - Usa `dbutils.widgets` para receber a senha com seguranca
   - Extrai colecoes com Pandas
   - Remove a coluna `_id`
   - Salva arquivos **CSV** em `/Volumes/workspace/landing/dados`

3. **02_Bronze**
   - Le os CSVs da Landing
   - Adiciona metadados tecnicos: `data_hora_bronze`, `nome_arquivo`
   - Persiste em **Delta** na camada Bronze

4. **03_Silver**
   - Limpeza e padronizacao
   - Tipagem de dados
   - Tratamento de nulos
   - Persiste em **Delta** na camada Silver

5. **04_Gold**
   - Modelagem dimensional (fato e dimensoes)
   - Upsert com **MERGE INTO** (SCD Tipo 1)
   - Persiste em **Delta** na camada Gold

---

## 🔐 Uso de Widgets para credenciais

O acesso ao MongoDB Atlas e feito com `dbutils.widgets`, evitando expor a senha no codigo. Exemplo simplificado:

```python
# Recebe a senha em tempo de execucao
# dbutils.widgets.text("mongo_pwd", "", "Senha do Mongo")
# mongo_pwd = dbutils.widgets.get("mongo_pwd")
```

Boas praticas:

- Nao versionar senhas no repositorio
- Usar variaveis de ambiente ou Secret Scopes quando disponivel
- Restringir permissao de execucao dos Jobs

---

## ✅ Garantias do pipeline

- **Reprocessamento seguro**: Bronze preserva o historico
- **Qualidade crescente**: Silver padroniza e valida
- **Consumo confiavel**: Gold entrega dados prontos para BI e analytics
