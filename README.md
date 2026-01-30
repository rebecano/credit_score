# 🏦 Credit Score Classification Project

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Libraries](https://img.shields.io/badge/Library-Scikit--Learn%20%7C%20Pandas%20%7C%20Seaborn-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)

## 📄 Sobre o Projeto

Este projeto consiste no desenvolvimento de um modelo de Machine Learning para automatizar a classificação de risco de crédito de clientes. O objetivo é segmentar a base em três categorias: **Ruim (Poor)**, **Padrão (Standard)** e **Bom (Good)**.

A solução foca em resolver o problema de **desbalanceamento de classes** e dados "sujos", aplicando técnicas robustas de limpeza e preparação de dados para garantir alta performance na detecção de maus pagadores.

## 💼 Problema de Negócio

Instituições financeiras precisam equilibrar dois objetivos conflitantes:
1.  **Maximizar a aprovação de crédito** para bons clientes.
2.  **Minimizar o risco de inadimplência** (calote).

O desafio deste dataset envolvia dados extremamente inconsistentes e uma classe minoritária de "Bons pagadores", o que exigia uma estratégia de modelagem que não enviesasse o resultado para a classe majoritária.

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python
* **Manipulação de Dados:** Pandas, NumPy
* **Visualização:** Matplotlib, Seaborn
* **Machine Learning:** Scikit-Learn (Random Forest, Logistic Regression)
* **Pré-processamento:** StandardScaler, LabelEncoder, Undersampling

## 📊 Pipeline do Projeto

O desenvolvimento seguiu as seguintes etapas:

1.  **Coleta e Limpeza de Dados (Data Cleaning):**
    * Tratamento de caracteres indesejados (`_`) em colunas numéricas.
    * Correção de outliers fisicamente impossíveis (ex: Idade > 500 anos, contas bancárias negativas).
    * Imputação de valores nulos utilizando Mediana (numéricos) e Moda (categóricos).

2.  **Análise Exploratória (EDA):**
    * Identificação de correlações fortes entre dívida e score.
    * Visualização do desbalanceamento das classes.

3.  **Pré-processamento:**
    * **Padronização:** Aplicação de `StandardScaler`.
    * **Balanceamento:** Aplicação de **Undersampling** para igualar as classes em ~13k amostras cada, garantindo que o modelo aprendesse padrões reais e não apenas a frequência.

4.  **Modelagem (Baseline vs. Challenger):**
    * Comparação entre **Regressão Logística** (Baseline linear) e **Random Forest** (Modelo de árvore não-linear).

## 📈 Resultados e Métricas

O modelo **Random Forest** superou significativamente o baseline, demonstrando capacidade de capturar regras complexas de comportamento financeiro.

| Modelo | Acurácia (Balanceada) | Recall (Classe "Ruim") |
| :--- | :---: | :---: |
| Regressão Logística | 67% | 0.68 |
| **Random Forest** | **76%** | **0.81** |

> **Destaque:** O Recall de **0.81** na classe "Ruim" é a métrica mais crítica, pois indica que o modelo consegue identificar 81% dos potenciais inadimplentes, protegendo o capital do banco.

## 💡 Insights de Negócio

A análise de *Feature Importance* revelou padrões cruciais para a estratégia de crédito:

1.  **Dívida > Renda:** A variável `Outstanding_Debt` (Dívida Pendente) é o preditor mais forte. O modelo aprendeu que o *nível de endividamento* é mais determinante para o risco do que a `Annual_Income` (Renda Anual).
2.  **Comportamento é Rei:** Variáveis como `Interest_Rate` e `Delay_from_due_date` (atrasos) superam dados demográficos. O histórico de pontualidade pesa mais que o salário.
3.  **Conclusão:** A política de crédito deve focar na capacidade de pagamento livre (Dívida/Renda) e no histórico recente de atrasos, em vez de focar apenas em clientes com altos salários.
