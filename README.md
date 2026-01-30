# Título: Modelo de Previsão de Risco Cardiovascular - Equipe 16

## Especificações

- **Eixo**: Saúde e Bem-Estar (A).

- **Tema**: Previsão de Risco Cardiovascular.

- **Dataset**: ["Sleep Health and Lifestyle Dataset"](https://www.kaggle.com/datasets/uom190346a/sleep-health-and-lifestyle-dataset).


## 📌 Descrição

Este projeto desenvolve um sistema de suporte à decisão clínica para identificar o estágio de risco cardiovascular (baseado na pressão arterial) utilizando dados não invasivos de hábitos de sono e estilo de vida.

O modelo classifica o risco em 5 categorias: **Normal, Elevada, Estágio 1, Estágio 2 e Estágio 3**, seguindo critérios clínicos de pressão sistólica e diastólica.

---

## 🧾 Objetivo

- 📊 **Explorar o dataset** para entender padrões relacionados a fatores de risco cardiovascular.  
- 🧪 **Utilizar modelos de ML** para identificar riscos cardiovasculares.
- 📉 Documentar métricas de desempenho e interpretação do modelo.

---

## 📁 Estrutura do Repositório

```
CardiopatiaModel/
├── Colab/                  # Notebooks otimizados para execução no Google Colab
├── Data/
├──Local/             # Pipeline numerado para execução local
│   ├── 01_EDA/             # Análise Exploratória de Dados
│   ├── 02_Experimentos/    # Testes com KNN, LogReg, RF, SVM, XGBoost
│   ├── 03_Treinamento/     # Modelagem final de todos os modelos para comparação
│   └── 04_Inferência/      # Notebook para demonstração funcional (MVP)
├── Models/                 # Pesos do modelos treinados (XGBoost, KNN, Regressão...) e métricas
│   └── XGBoost/            # Artefatos: Metrics e Plots (Matriz de Confusão, etc)
├── README.md               # Documentação principal
└── .gitignore
```

---

## 📦 Dataset

O projeto utiliza, até o momento, o **Sleep Health and Lifestyle Dataset**, que contém informações relacionadas a:

- Hábitos de sono  
- Estilo de vida  
- Indicadores de saúde  
- Variáveis potencialmente associadas a doenças cardiovasculares

O dataset é utilizado inicialmente para **exploração, visualização e entendimento dos dados**, sem aplicação direta de modelos preditivos nesta fase.

> Detalhes adicionais sobre variáveis, tamanho do dataset e tratamentos realizados podem ser encontrados diretamente no notebook de EDA.

---

## 📊 Análise Exploratória de Dados (EDA)

A análise exploratória está concentrada no notebook:

📄 [`EDA_SleepHealth.ipynb`](Local/01_EDA/EDA_SleepHealth.ipynb)

Nele são abordados, entre outros pontos:

- Estatísticas descritivas
- Análise de valores ausentes
- Distribuição das variáveis
- Visualizações gráficas
- Exploração de possíveis correlações relevantes

Essa etapa é essencial para embasar as próximas decisões do projeto.

---

## 🧠 Modelagem de Machine Learning

- **Algoritmo Final**: XGBoost e SVM (Melhores desempenhos).
- **Métrica Principal**: F2-Score Macro (Priorizando Recall para evitar falsos negativos em saúde).
- **Feature Engineering**: Criação de Sleep Efficiency e Cardiac Stress Index.
- **Tratamento de Dados**: Balanceamento com SMOTE e Padronização com StandardSc.

---

## 🛠️ Como Executar o Projeto

> Pré-requisitos: Python 3.12 (Versão obrigatória para compatibilidade de dependências).

1. Clone o repositório:
   ```bash
   git clone https://github.com/gabrielbelo2007/CardiopatiaModel.git
   cd CardiopatiaModel

2. Criar e ativar ambiente virtual:
   ```bash
   python -m venv venv
   # No Windows:
   .\venv\Scripts\activate
   # No Linux/Mac:
   source venv/bin/activate

3. Instalar as dependências:
   ```bash
   pip install -r requirements.txt

#### 🚀 Execução no Google Colab

Caso prefira não configurar o ambiente localmente, utilize os arquivos dentro da pasta /Colab. Eles já contêm as células de instalação de dependências necessárias para o ambiente de nuvem.

#### 🚀 Executando Inferência (Teste do Modelo)

- Navegue até Local/04_Inferência/.
- Abra o notebook [Inferência.ipynb](Local/04_Inferência/Inferência.ipynb).
- Este notebook carrega o modelo salvo em /Models/XGBoost/ e permite a entrada de novos dados de pacientes para prever o risco cardiovascular.

---

## Integrantes do grupo:
- @AllanF-0101
- @arthursean
- @CaduFalcaoT
- @dantteroberto-draaf
- @gabrielbelo2007
- @nuneslg
- @renatomsa 

   
