
# Ficha Técnica: Projeto de Implementação de Sistema ETL

Este projeto aborda um desafio clássico de engenharia de dados: transformar uma base de dados de vendas bruta e desestruturada em um modelo de dados relacional e otimizado. O resultado é um **Esquema em Estrela (Star Schema)** implementado no Google BigQuery, pronto para suportar análises de Business Intelligence e a tomada de decisão estratégica na Super Store.

## 🎯 Objetivo do Projeto
- **Estruturar dados brutos** em um modelo de dados dimensional (Star Schema) para otimizar análises.
- **Melhorar a Tomada de Decisões** ao permitir a análise de dados de forma integrada e eficiente.
- **Aumentar a Eficiência Operacional** ao definir um processo de ETL claro e replicável.

## 👥 Equipe
- O projeto foi desenvolvido por: Gabriela Albuquerque.

## 🛠️ Ferramentas e Tecnologias
- **Google BigQuery**: Utilizado como Data Warehouse para todo o processo de limpeza, transformação (SQL) e armazenamento do modelo dimensional final.
- **LucidApp**: Ferramenta para o desenho e visualização da arquitetura do banco de dados (Esquema em Estrela).
- **Python (via Google Colab)**: Usado para a etapa de web scraping (com Beautiful Soup) e para a análise e limpeza inicial dos dados (com Pandas).
- **Google Sheets**: Utilizado para a tradução inicial e exploração dos dados.

## 📊 Processamento e Análises

### 1. Fonte de Dados e Preparação Inicial
As análises e transformações foram realizadas com base no arquivo `superstore.csv`, contendo **51.288 registros** e **27 atributos**. O trabalho inicial de tratamento foi feito em um notebook do Google Colab.

### 2. Limpeza e Transformação dos Dados
- **Problemas Resolvidos:**
  - **Tipos de Dados Inconsistentes:** A coluna `lucro` foi identificada como `object` e convertida para o tipo numérico `float64`.
  - **Normalização de Strings:** Foi aplicada uma função para padronizar todas as colunas de texto, removendo espaços extras e ajustando a capitalização.
  - **Valores Duplicados:** A base de dados não apresentou registros duplicados.

### 3. Extração de Dados Externos
- Foi utilizado **Beautiful Soup** em Python para extrair dados de uma tabela da Wikipedia sobre as maiores empresas do mundo para enriquecer o contexto da análise.

### 4. Carga e Validação no BigQuery
- Os dados tratados foram carregados no BigQuery na tabela `superstore-table`.
- Uma segunda rodada de validação no BigQuery identificou e corrigiu **1.154 linhas** com espaços ou caracteres especiais, resultando na tabela `superstore_cleaned`.

### 5. Modelagem de Dados (Star Schema)
- A arquitetura do banco de dados foi desenhada no **LucidApp**, e a metodologia escolhida foi o **Esquema em Estrela**.

### 6. Criação das Tabelas de Dimensão e Fato
- **Tabelas de Dimensão:** Foram criadas 5 dimensões (`dim_cliente`, `dim_produto`, `dim_localizacao`, `dim_data`, `dim_prioridade`). Para dimensões sem um ID pré-existente, foram geradas chaves primárias (surrogate keys).
- **Tabela de Fatos:** A tabela `fato_vendas` foi criada e conectada a todas as dimensões através de `JOINs`.

### 7. Planejamento do Pipeline de Atualização
- Foi desenhado o fluxo lógico para a atualização contínua dos dados, estabelecendo a regra de **"Dimensões primeiro, Fatos depois"** para garantir a integridade do modelo.

## 📈 Resultados e Conclusões
- **Resultado Principal:** O projeto transformou com sucesso um conjunto de dados bruto em um modelo dimensional funcional e otimizado no BigQuery.
- **Conclusão:** A implementação do sistema ETL capacita a Super Store a gerenciar seus dados de forma mais eficiente, permitindo análises mais rápidas e apoiando diretamente a tomada de decisões.
- **Recomendações:**
  1. Utilizar o novo modelo estrela como fonte padrão para todas as análises e dashboards de BI.
  2. Avançar com a automação do pipeline de atualização desenhado.

## 🚧 Limitações e Próximos Passos
### Limitações da Análise:
- **Foco na Estruturação:** O projeto concentrou-se no processo de ETL, não na análise exploratória.
- **Pipeline Não Automatizado:** O fluxo de atualização foi desenhado, mas não implementado com ferramentas de automação.

### Próximos Passos:
- **Desenvolver Análises e Dashboards:** Conectar o modelo a ferramentas como Looker Studio ou Power BI.
- **Implementar e Automatizar o Pipeline de ETL:** Usar serviços de nuvem para automatizar o processo.
- **Enriquecer o Modelo:** Integrar novas fontes de dados para criar uma visão 360º do negócio.

## 🔗 Links de Interesse
- **[Google Colab projeto ETL](https://colab.research.google.com/drive/13I5wEU6Lqv9AtcZH8YL5mSVDMpOmQsqu?usp=sharing)**
- **[Diagrama do Esquema Estrela no LucidApp](https://lucid.app/lucidchart/053ebb0e-73d2-46d7-91f5-606b7558672c/edit?invitationId=inv_72f6740c-0cd9-4e28-a5e2-d6a3ce43d24f)**
