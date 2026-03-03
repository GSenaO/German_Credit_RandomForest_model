# 🏦 Risco de Crédito: Otimização de Threshold e Explicabilidade

## 📌 O Problema de Negócio
Em operações de crédito, um falso negativo (aprovar um mau pagador) gera prejuízo direto, enquanto um falso positivo (negar um bom pagador) gera perda de receita e atrito comercial. O objetivo deste projeto foi construir um modelo preditivo utilizando o dataset German Credit Data que equilibrasse essa balança, focando na métrica de negócio, não apenas em Acurácia matemática.

## 🛠️ Tecnologias e Ferramentas
* **Linguagem:** Python
* **Bibliotecas:** Pandas, Scikit-Learn, XGBoost, Matplotlib, Seaborn, SHAP
* **Algoritmos Testados:** Random Forest Classifier, XGBoost

## 📊 A Solução Abordada (O Trade-off Risco vs. Retorno)
A maioria dos modelos assume um limite de decisão (Threshold) de 50%. Através de uma análise da curva de Precisão vs. Recall, o ponto de corte foi calibrado para **47%**. 

**Impacto Simulado:**
* **Recall de Calotes (Classe 1): 67%** - Protege o caixa do banco.
* **Recall de Bons Pagadores (Classe 0): 72%** - Mantém a aprovação saudável para a área comercial.
* O modelo escolhido para produção foi o **Random Forest** tunado, que apresentou maior robustez e melhor adaptação ao ponto de corte do que o XGBoost neste contexto específico.

## 🔍 Explicabilidade do Modelo (SHAP)
Para garantir a transparência exigida por órgãos reguladores e comitês de risco, o modelo foi dissecado utilizando a teoria dos jogos (SHAP Values).

![Summary Plot SHAP](SHAPValue.png)

**Principais Insights:**
1. **Prazo (`num_duration_log`):** Empréstimos mais longos aumentam drasticamente o risco de default.
2. **Status da Conta (`cat_checking_3_negativo`):** Clientes com contas já negativadas são os perfis de maior risco.
3. **Sem Histórico (`cat_checking_1_sem_conta`):** Paradoxalmente, a ausência de uma conta corrente registrada demonstrou reduzir o risco de inadimplência, indicando possível ausência de alavancagem financeira anterior.
   
![ResultadoFinal](ResultadoModeloFinal.png)

## 🚀 Como Executar o Projeto
1. Clone este repositório: `git clone [URL_DO_SEU_REPO]`
2. Instale as dependências: `pip install -r requirements.txt`
3. Execute o notebook `[nome_do_seu_notebook].ipynb`
