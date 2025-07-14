# Previsão de Inadimplência com LightGBM

Este projeto foi desenvolvido como parte de um case técnico para uma vaga de Cientista de Dados Júnior. O objetivo principal foi construir um modelo preditivo para identificar a probabilidade de inadimplência de clientes empresariais, utilizando dados históricos e cadastrais.

---

## 📌 Objetivo

Desenvolver um modelo de Machine Learning capaz de prever a **probabilidade de inadimplência** com base em múltiplas fontes de dados, incluindo:

- Pagamentos históricos
- Informações cadastrais
- Atributos temporais (extraídos de datas)
- Indicadores de comportamento

---

## 🗃️ Dados Utilizados

As seguintes bases foram utilizadas no projeto:

- `base_pagamentos_desenvolvimento.csv`
- `base_pagamentos_teste.csv`
- `base_cadastral.csv`
- `base_info.csv`

Cada base foi tratada em camadas:
- **Raw**: Importação e padronização dos dados
- **Trusted**: Conversão de tipos, imputações, criação da variável-alvo (`INADIMPLENTE`)
- **Refined**: Feature engineering, agregações, normalizações e junções

---

## ⚙️ Principais Etapas

### 1. Construção da variável-alvo
- Definida como `INADIMPLENTE = 1` se `DATA_PAGAMENTO - DATA_VENCIMENTO >= 5 dias`, ou `DATA_PAGAMENTO` ausente.

### 2. Análise Exploratória (EDA)
- Visualizações e estatísticas descritivas
- Insights como:
  - Clientes reincidentes têm comportamento muito distinto dos adimplentes
  - Alta variabilidade no valor das faturas e na taxa de inadimplência histórica

### 3. Feature Engineering
- Agregações por cliente
- Criação de variáveis como:
  - `TAXA_INADIMPLENCIA`
  - `VALOR_MEDIO_FATURA`
  - `DIAS_ATRASO_MAXIMO`
  - Variáveis temporais (mês, ano, dia da semana do vencimento, etc.)

### 4. Modelagem com LightGBM
- Treinamento com `LGBMClassifier`
- Avaliação por **AUC-ROC** e **Precision-Recall AUC**
- Feature Importance para interpretação do modelo

### 5. Predição e Submissão
- Geração do arquivo `submissao_case.csv` com:
  - `ID_CLIENTE`
  - `SAFRA_REF`
  - `PROBABILIDADE_INADIMPLENCIA`

---

## 📈 Métricas do Modelo

- **AUC-ROC (validação):** ~0.85+
- **Precision-Recall AUC:** >0.40 (ótimo para classes desbalanceadas)
- Features mais importantes:
  - `TAXA_INADIMPLENCIA`
  - `VALOR_MEDIO_FATURA`
  - `DIAS_ATRASO_MAXIMO`

---

## 🧠 Principais Insights de Negócio

- Empresas com **histórico de reincidência** têm risco elevado mesmo com faturamento alto.
- **Perfis temporais** como o mês e o dia da semana do vencimento mostram padrões sazonais de inadimplência.
- A inclusão da **TAXA_INADIMPLENCIA** individual foi determinante para melhorar a performance do modelo.

---

## 📎 Arquivos Gerados

- `previsao_inadimplencia_lightgbm_case_datarisk.ipynb`
- `submissao_case.csv`

---

## 🚀 Tecnologias Utilizadas

- Python 3.11
- Pandas, NumPy
- Seaborn, Matplotlib
- Scikit-learn
- LightGBM

---

## ✍️ Autor

Elivélton Neves de Alcântara  
[Cientista de Dados | Engenheiro de Dados | Analista de Dados]  
[LinkedIn](https://www.linkedin.com/in/elivelton-neves-de-alc%C3%A2ntara-ab2192212/)
