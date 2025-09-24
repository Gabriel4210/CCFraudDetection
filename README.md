# Projeto de Detecção de Fraude em Cartões de Crédito

## 1. Visão Geral

Este projeto tem como objetivo a construção e avaliação de um modelo de Machine Learning para detecção de transações fraudulentas em cartões de crédito.

O desafio deste problema é o **grande desbalanceamento de classes** no conjunto de dados, onde as fraudes representam uma porcentagem quase nula do total de transações. A abordagem deste projeto foca em métricas de avaliação adequadas e técnicas de modelagem que contornam esse desafio.

## 2. Fonte dos Dados

O conjunto de dados utilizado é o "Credit Card Fraud Detection", disponibilizado publicamente no Kaggle. Você pode encontrá-lo [neste link](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud).

A maioria das features são compostas por componentes principais (V1, V2, ..., V28) resultantes de uma transformação de PCA, visando anonimizar os dados sensíveis. As únicas features que não foram anonimizadas são `Time` (tempo decorrido desde a primeira transação) e `Amount` (valor da transação).

## 3. Metodologia Aplicada

O projeto foi estruturado seguindo as seguintes etapas:

1.  **Análise Exploratória de Dados (EDA):** Investigação inicial para entender a distribuição das variáveis, a correlação entre elas e, principalmente, a proporção entre classes (fraudes vs. transações legítimas).
2.  **Pré-Processamento:** Padronização (scaling) da feature `Amount` e conversão da feature `Time` de segundos para horas para que tivessem a mesma escala das outras variáveis e não influenciassem o modelo indevidamente e pela interpretabilidade.
3.  **Modelagem e Treinamento:**
    * **Baseline Model:** Utilização de uma **Regressão Logística** como modelo inicial para estabelecer uma performance de referência.
    * **Advanced Model:** Implementação de um modelo **XGBoost (Extreme Gradient Boosting)**, conhecido por sua alta performance em competições e problemas complexos.
4.  **Tratamento do Desbalanceamento:** Para o modelo XGBoost, foi utilizado o hiperparâmetro `scale_pos_weight` para atribuir um peso maior aos erros cometidos na classe minoritária (fraude), forçando o modelo a prestar mais atenção a ela.
5.  **Avaliação de Performance:** Análise crítica dos modelos com foco em métricas adequadas para dados desbalanceados, como **Recall**, **Precision** e a **Área Sob a Curva Precision-Recall (AUPRC)**.

## 4. Tecnologias Utilizadas

* **Linguagem:** Python 3
* **Bibliotecas Principais:**
    * Pandas e NumPy para manipulação de dados.
    * Matplotlib e Seaborn para visualização.
    * Scikit-learn para pré-processamento e o modelo de Regressão Logística.
    * XGBoost para o modelo avançado.

## 5. Resultados

A performance dos modelos foi comparada para avaliar a eficácia da abordagem com XGBoost e `scale_pos_weight`.

| Modelo | Recall (Fraude) | Precisão (Fraude) | AUPRC |
| :--- | :---: | :---: | :---: |
| Regressão Logística | 0.94 | 0.06 | 0.78 |
| XGBoost (com `scale_pos_weight`) | **0.80** | **0.87** | **0.83** |

**Conclusão dos Resultados:**
O modelo de Regressão Logística, apesar de atingir um altíssimo Recall, o fez ao custo de uma Precisão muito baixa, gerando um número excessivo de falsos positivos.

O modelo **XGBoost** ajustado demonstrou um resultado muito superior e mais balanceado. Ele manteve um excelente Recall (pegando 80% das fraudes) ao mesmo tempo em que alcançou uma Precisão de 87%, tornando-o um modelo muito mais útil e confiável para um cenário de produção.

## 6. Como Executar o Projeto

1.  Clone este repositório:
    ```bash
    git clone [https://github.com/Gabriel4210/CCFraudDetection.git](https://github.com/Gabriel4210/CCFraudDetection.git)
    ```
2.  Navegue até o diretório do projeto:
    ```bash
    cd CCFraudDetection
    ```
3.  (Opcional, mas recomendado) Crie um ambiente virtual:
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    ```
4.  Instale as dependências:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn xgboost
    ```
5.  Abra o notebook `Credit_Card_Fraud_Detection.ipynb` em um ambiente Jupyter (Jupyter Lab, Jupyter Notebook ou VS Code).
