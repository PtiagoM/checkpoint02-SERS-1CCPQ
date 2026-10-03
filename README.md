```markdown
# Avaliação — APIs de Energia Renovável e Aprendizado de Máquina

Este projeto consiste na coleta de dados de duas APIs públicas (ANEEL e Open-Meteo), organização de conjuntos de dados locais em formato CSV e a resolução de duas tarefas de aprendizado de máquina utilizando modelos de classificação e regressão.

## 📋 Estrutura do Repositório

- `projeto.ipynb`: Notebook executável contendo as consultas às APIs, análise exploratória, tratamento de dados e modelagem.
- `aneel_classificacao_orange.csv`: Dados extraídos do SIGA (ANEEL) para a tarefa de classificação.
- `meteo_regressao_orange.csv`: Dados meteorológicos históricos de Petrolina (PE) para a tarefa de regressão.
- `README.md`: Este arquivo com a documentação do projeto.

---

## 🛠️ Instalação e Execução

1. Clone este repositório:
   ```bash
   git clone <LINK_DO_SEU_REPOSITORIO>
   cd <NOME_DO_REPOSITORIO>
   ```

2. Instale as dependências necessárias utilizando pip:
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn
   ```

3. Abra o Jupyter Notebook ou envie o arquivo `.ipynb` para o Google Colab e execute todas as células em ordem cronológica.

---

## ⚡ Tarefa 1 — Classificação de Fontes de Energia (ANEEL)

### **Objetivo**
Classificar a fonte de geração de energia de um empreendimento cadastrado na ANEEL como **Solar, Eólica ou Hidráulica** com base em sua **potência (kW), latitude e longitude**.

### **Metodologia**
- **Divisão dos Dados**: Divisão estratificada com 80% para treino e 20% para teste, garantindo a mesma proporção de classes.
- **Algoritmos Testados**:
  1. Regressão Logística (com dados padronizados)
  2. K-Nearest Neighbors (KNN com `n_neighbors=7` e dados padronizados)
  3. Random Forest Classifier (`n_estimators=300` e dados originais)
- **Métricas de Avaliação**: Accuracy, Precision (Macro), Recall (Macro) e F1-Score (Macro).

### **Resultados Obtidos**

| Modelo | Accuracy | Precision (Macro) | Recall (Macro) | F1-Score (Macro) |
| :--- | :---: | :---: | :---: | :---: |
| **Random Forest** | **97.55%** | **97.69%** | **97.41%** | **97.53%** |
| KNN | 96.52% | 96.68% | 96.33% | 96.47% |
| Regressão Logística | 82.47% | 82.82% | 82.14% | 81.97% |

* **Modelo Escolhido**: O **Random Forest** obteve o melhor desempenho em todas as métricas, atingindo um F1-Score macro de **97.53%**.
* **Maior Confusão**: O modelo confundiu levemente a classe **Solar sendo classificada como Hidráulica** em alguns casos pontuais (7 ocorrências).

---

## ☀️ Tarefa 2 — Regressão de Radiação Solar (Open-Meteo)

### **Objetivo**
Estimar a radiação solar horizontal global média ($W/m^2$) em Petrolina (PE) com base em condições meteorológicas locais (temperatura, umidade, cobertura de nuvens, velocidade do vento e a hora local).

### **Metodologia**
- **Divisão dos Dados**: Divisão estritamente temporal (80% primeiros registros para treino, 20% finais para teste) preservando o histórico temporal sem embaralhar.
- **Algoritmos Testados**:
  1. Regressão Linear
  2. Árvore de Decisão (Decision Tree Regressor)
  3. Random Forest Regressor
- **Métricas de Avaliação**: Erro Médio Absoluto (MAE), Erro Quadrático Médio (MSE) e Coeficiente de Determinação ($R^2$).

### **Discussão & Conclusões**
1. **Peso da Hora**: A hora do dia se mostrou a variável mais impactante por representar a curva parabólica solar natural (limite teórico de irradiação ao longo do dia).
2. **Radiação vs Energia Efetiva**: Estimar a radiação em $W/m^2$ não se traduz diretamente em geração elétrica real. Fatores práticos do sistema fotovoltaico físico — como eficiência das placas, perdas por calor, eficiência dos inversores, perdas na fiação e sujeira — influenciam a energia final produzida.
```
