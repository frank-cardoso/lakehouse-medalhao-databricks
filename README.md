# 🚀 Lakehouse Medallion (Databricks)

Projeto completo de **Data Lakehouse** para aula de engenharia de dados, construído no **Databricks** com a **Arquitetura Medallion**. O fluxo cobre desde a extração de dados no MongoDB Atlas até a modelagem dimensional no Gold, garantindo governança, qualidade e performance em cada camada.

---

## 🧩 Badges de Tecnologias

![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?style=for-the-badge&logo=apache-spark&logoColor=white)
![PySpark](https://img.shields.io/badge/PySpark-1F6FEB?style=for-the-badge&logo=python&logoColor=white)
![Spark SQL](https://img.shields.io/badge/Spark%20SQL-4B8BBE?style=for-the-badge&logo=databricks&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![MongoDB Atlas](https://img.shields.io/badge/MongoDB%20Atlas-00ED64?style=for-the-badge&logo=mongodb&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-0A2A43?style=for-the-badge&logo=delta&logoColor=white)

---

## 🎯 Objetivo do Projeto

Construir um **Lakehouse corporativo** para aula de engenharia de dados, consolidando dados operacionais em um pipeline robusto e escalável, com:

- **Ingestão segura** (credenciais via widget).
- **Persistência confiável** em Delta Lake.
- **Curadoria de dados** por camadas.
- **Modelo dimensional** pronto para BI e análises avançadas.

---

## 🏗️ Arquitetura Medallion (Resumo)

A Arquitetura Medallion separa a jornada do dado em três camadas de maturidade:

- **Bronze:** dados crus, com rastreabilidade e metadados.
- **Silver:** dados tratados, com tipagem correta e padronização.
- **Gold:** dados prontos para consumo analítico (fato e dimensões).

Neste projeto, a camada **Landing** é usada para armazenar os arquivos de extração em CSV, organizando a ingestão inicial antes da escrita no Bronze.

---

## 🧱 Estrutura e Fluxo do Projeto

### 00_Setup (Infraestrutura)
- Script SQL que cria os schemas `landing`, `bronze`, `silver`, `gold` e o Volume `landing.dados` usando `IF NOT EXISTS`.

### 01_Extracao_Mongo
- Conecta ao MongoDB Atlas com `pymongo`.
- Converte documentos em **Pandas DataFrames** para simplificar a gravação sequencial.
- Salva **um CSV por coleção** no Volume da Landing Zone.
- Usa `dbutils.widgets` para receber a URI do banco (sem credenciais hardcoded).

### 02_Camada_Bronze
- Lê os CSVs da Landing.
- Adiciona metadados: `data_hora_bronze` e `nome_arquivo`.
- Salva tabelas no formato **Delta**.

### 03_Camada_Silver
- Limpeza de dados, tratamento de nulos e tipagem de colunas.
- Padronização dos campos.
- Persistência em **Delta**.

### 04_Camada_Gold
- Modelagem dimensional (Tabelas Fato e Dimensão).
- Uso de **CTEs** e **MERGE INTO**.
- Implementa **SCD Tipo 1** para evitar duplicações e manter atualização dos registros.

---

## ▶️ Como Executar (Passo a Passo)

1. **Importar o repositório no Databricks**
	- Vá para **Repos** → **Git Folders / Repos** → Clone o repositório.

2. **Executar o notebook de setup**
	- Rode o notebook `00_Setup` para criar schemas e volumes.

3. **Configurar a extração do MongoDB**
	- No notebook `01_Extracao_Mongo`, preencha o **widget no topo** com a string de conexão do MongoDB Atlas antes de executar.

4. **Orquestrar o pipeline completo**
	- Use a aba **Workflows** para criar um **Job sequencial** com dependências (DAG):
	  `00_Setup` → `01_Extracao_Mongo` → `02_Camada_Bronze` → `03_Camada_Silver` → `04_Camada_Gold`.

---

## 🗂️ Estrutura do Projeto

```text
├── docs/
│   ├── index.md
│   ├── arquitetura.md
│   ├── bronze.md
│   ├── silver.md
│   ├── gold.md
│   ├── execucao-pipeline.md
│   ├── databricks.md
│   ├── delta-lake.md
│   └── stylesheets/
│       └── extra.css
└── notebooks/
    ├── 000_-_Atividade_Pratica_-_Lakehouse_-_Preparando_ambiente-69fa4f0f2d7b1.ipynb
    ├── 001 - Atividade Pratica - Lakehouse - Extracao.ipynb
    ├── 002_-_Atividade_Pratica_-_Lakehouse_-_Bronze-69fa4f0f35b55.ipynb
    ├── 003_-_Atividade_Pratica_-_Lakehouse_-_Silver-69fa4f0f39c3c.ipynb
    ├── 004_-_Atividade_Pratica_-_Lakehouse_-_Gold-69fa4f0f6afff.ipynb
    └── 005_-_Atifidade_Pratica_-_Lakehouse_-_Destruindo_ambiente-69fa4f0f1bc85.ipynb
├── mkdocs.yml
├── README.md
```

## 📌 Observacoes Importantes

- O uso de `dbutils.widgets` evita credenciais hardcoded no codigo.
- A camada Gold esta preparada para atualizacoes com SCD Tipo 1.
- Todos os dados persistem em **Delta Lake** para confiabilidade e performance.

---

# 📚 Documentação Interativa com MkDocs

Este projeto possui uma documentação profissional desenvolvida com **MkDocs Material**, oferecendo uma navegação moderna, organizada e responsiva para explorar toda a arquitetura do pipeline Lakehouse.

## 🚀 Tecnologias da Documentação

- MkDocs
- Material for MkDocs
- Mermaid Diagrams
- GitHub Pages

---

## 📖 Acesse a Documentação

👉 https://github.com/frank-cardoso/lakehouse-medalhao-databricks

---

## 🏗 Conteúdo da Documentação

A documentação inclui:

- Visão geral da arquitetura Medalhão
- Explicação das camadas Bronze, Silver e Gold
- Pipeline ETL completo
- Diagramas Mermaid
- Tecnologias utilizadas
- Fluxo de processamento dos dados
- Estrutura do projeto

---

## ▶️ Executar Localmente

### Pré-requisitos
Certifique-se de ter o [Python](https://www.python.org/downloads/) e o gerenciador de pacotes `pip` instalados em sua máquina. Recomenda-se o uso de um ambiente virtual (venv).

### Instalar dependências

Crie e ative um ambiente virtual (opcional, mas recomendado):
```bash
# Linux/macOS
python3 -m venv .venv
source .venv/bin/activate

# Windows (PowerShell)
python -m venv .venv
.\.venv\Scripts\Activate
```

Instale as dependências:
```bash
pip install mkdocs-material mkdocs-mermaid2-plugin pymdown-extensions
```

### Iniciar servidor local

```bash
mkdocs serve
```

Acesse:

```txt
http://127.0.0.1:8000
```

---

## 🌐 Deploy GitHub Pages

Para publicar a documentação:

```bash
mkdocs gh-deploy
```
