### Arquitetura

O termo "XGBoost" é *eXtreme Gradient Boosting*, sendo um modelo baseado em árvores de decisão, com aplicação do "Gradient Boosting", onde cada etapa da sequência, gera uma nova árvore que tenta corrigir os erros (residuais) cometidos pelas árvores anteriores.

- O modelo de *Decision Tree* é interessante para investigação médica pois permite que o médico consiga visualizar as variáveis que foram cruciais para a decisão do modelo (Feature Importance), o que é perfeito para explicabilidade.

- Outro benefício é pela pequena quantidade da dados, esse modelo tem como característica uma maior resistência ao overfitting, visto que:

	- O modelo de *Decision Tree* utilizado no **XGBoost** não possui essa tendência, por serem propositalmente árvores pequenas (*weak learners*). Visto que, a capacidade de aprendizado depende da profundidade e números de folhas, quanto maior a profundidade e mais ramificações mais específico será a classificação.
	
	- A função de perda desse algoritmo também é construída de forma a evitar a construção de árvores "desnecessárias" para o aprendizado do modelo.
	
	- Esse algoritmo também possui a aplicação da técnica de *prunning* (Poda Reversa), no qual o modelo cresce até a profundidade definida, porém depois faz a remoção das divisões que não contribuem significativamente no aprendizado.

> Em resumo, é um modelo que ignora grandes outliers.

---

### Dataset

Por se tratar de um dataset "pequeno", com poucas features, analisando a correlação entre essas features, foi observado que existiam muitas variáveis altamente correlacionadas. Dessa forma, buscando evitar a influência que essa multicolinearidade poderia causar, foi utilizado:

- **PCA (Principal Component Analysis)**: De forma resumida, é uma ferramenta que busca encontrar um "ângulo" para enxergar os dados de uma forma que eles estejam totalmente independentes entre si, além de aplicar uma redução de de dimensionalidade baseado na variância dos dados.

> Foi feito uma normalização dos dados com o *StandardScaler* pois o PCA exige os dados normalizados para controle da variância.

- Essa redução de dimensionalidade é também colabora para dificultar o overfitting do modelo, visto que definindo uma quantidade menor de features porém mais significativas, o modelo aprende melhor.

> A aplicação dessa ferramenta gera variáveis sintéticas, mas menos ruidosas, porém isso mistura as variáveis e reduz a explicabilidade do resultado.

Por isso, que é utilizado a ferramenta "SHAP" que calcula a contribuição de cada feature para a predição final, como se fosse um Raio-X em cima do resultado embaralhado gerado pelo PCA.

> O uso do *stratify* no split dos conjuntos de treino e teste, serve para garantir que a proporção das 3 classes do **Target** esteja mantida no treino e no teste, com foco de não ignorar a classe minoritária.

---

### Métricas

Por se tratar de um modelo médico, tendo a noção de que o erro tem um valor muito significativo, temos que as principais métricas são:

- **Sensibilidade (Recall)**: Evitar uma previsão "Normal" para um paciente que tenha "Hipertensão".

- **F1 e F2 Score:** O F1 demonstra o equilíbrio entre a precisão e a sensibilidade do modelo, e o F2 faz o mesmo porém com um peso dobrado para a sensibilidade, evidenciando ainda mais o quão seguro é o modelo para o contexto de saúde.

- **AUC-ROC**: Avalia o quão bem o modelo consegue distinguir dentre as classes possíveis de previsão.

---

### Pipeline

Essa ferramenta permite a estruturação correta entre os dados e o treinamento do modelo, para evitar problemas de *Data Leakage*.

Por exemplo, garantindo que a normalização dos dados e o PCA sejam aplicados somente no conjunto de treino, impedindo que o modelo seja viciado e entregue resultados excepcionais porém falsos.

Dessa maneira, a pipeline do modelo, é definida pela aplicação da normalização do conjunto de treino, depois o PCA também no conjunto de treino e por fim ao chamar a saída do modelo, todas essas transformações são aplicadas isoladamente ao conjunto de teste, sem influenciar o treinamento.

---

### GridSearchCV

Pela grande quantidade de hiperparâmetros existentes no algoritmo do XGBoost, adivinhar a combinação que resulta na melhor predição do modelo de forma manual é impossível. 

Dessa maneira, essa ferramenta faz essa busca, construindo todas as combinações possíveis, fazendo a aplicação do Cross-Validation em cada combinação, calculando a métrica de sucesso definida (a utilizada para comparação da melhor combinação de hiperparâmetros) e assim entrega o modelo com a melhor performance.

É evidente, que esse processo é bem custoso computacionalmente e no tempo, contudo como esse dataset não é muito grande, e ainda tem suas features otimizadas pelo processo de PCA, essa questão não será muito relevante, favorecendo muito o seu uso em busca do melhor modelo possível.

> O pipeline colabora muito nessa etapa, pois garante a aplicação de todas as transformações nos conjuntos de dados gerado pelo Cross-Validation a cada iteração de combinação de hiperparâmetros.

