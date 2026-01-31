Artigo completo: https://drive.google.com/file/d/11r0oSXG1MW1504ukh8XqqVnM9g6cPCNQ/view?usp=sharing

# Geração de Curva de Colina para Turbina Hidrelétrica Usando Rede Neural Artificial

#### Autores
FELIPE L. LAVRADOR, CLARIMAR J. COELHO AND DIOGO F. COSTA SILVA

## RESUMO 
Dentro de uma usina hidroelétrica, a curva de colina é um gráfico importante para realizar predições de valores em circunstâncias específicas. Asism, é proposto três modelos de regressão sendo Feedforward, Regressão Linear e XGBoost. Os dados utilzados para treinar as redes, foram obtidos através de um modelo em escala reduzida, totalizam 1243 dados. Assim notando que dentre os três modelos, o modelo Feedforward demonstrou uma maior capacidade de generalização. Sendo assim uma melhor alternativa dentre as três redes propostas.


## Introdução
A curva de colina é uma ferramenta fundamental para o estudo de desempenho da turbina, gestão e controle de uma usina hidrelétrica. Dixon [1], em seu livro “Fluid Mechanics and Thermodynamics of Turbomachinery” diz que existe uma altura ideal para a maior eficiência de uma turbina hidrelétrica. A curva de colina é um diagrama que proporciona visualizar a relação entre múltiplos parâmetros, como a eficiência, altura de queda, vazão turbinada, potência gerada, ângulo da pá, e outros. A curva de colina é construída por medições feitas manualmente, e experimentalmente, em um modelo reduzido da turbina. Os dados obtidos ainda sofrem normatizações e interpolações para torná-los mais representativos possíveis. Caso a turbina sofra alguma alteração, os dados da curva apresentarão erros, e a construção de um novo modelo reduzido ou medições na planta real é extremamente oneroso. Para a redução deste custo, as redes neurais artificiais (ANN’s) podem ser utilizadas para a predição dos parâmetros da turbina e geração de uma curva de colina baseada nos pontos de medição do modelo reduzido. Diversos trabalhos propõe o uso de ANN’s para soluções em reconhecimento de padrões e predições aplicados à problemas de geração de energia elétrica. "Shaw, et al.” [5] exemplifica e demonstra em “Hydropower Optimization Using Artificial Neural Network Surrogate Models of a High Fidelity Hydrodynamics and Water Quality Model” um método baseado em redes neurais para determinar as operações ideais do reservatório multiuso, em Nashville cidade de Tennessee nos EUA, que segundo suas palavras “O modelo reproduziu com sucesso informações de reservatórios de alta fidelidade, permitindo aumentos de 6,8% e 6,6% no valor da produção de energia hidrelétrica em relação às operações reais para limites de oxigênio dissolvido”. “Old Hickory. Hammid, et al.” [6] e colaboradores apresentam um método baseado em ANN que, após vários testes, em uma pequena usina hidrelétrica no lago Himreen localizada em Diyala previu o desempenho da planta com um coeficiente de correlação, além de modelar o desempenho da planta. Já “Iraq. Bouzic e Jovanovic” [7] pela interpolação espacial de pontos medidos apresentam um método baseado em ANN para predição das características de turbinas considerando um conjunto de dados do modelo reduzido da turbina. Neste contexto, foi demonstrado por Galvão Filho [4] a possibilidade de gerar a curva de colina a partir de um modelo de regressão. Assim será proposto outros modelos de regressão com intuito de minimizar os custos computacionais para se gerar a própria curva de colina.

## Caso de Estudo
Os dados foram cedidos pela Usina Hidrelétrica Jirau, instalada no rio Madeira, no estado de Rondônia - Brasil, é composta por cinquenta unidades geradoras de bulbo horizontal tipo Kaplan. Dentre as 50, 28 estão localizadas na margem direita e 22 na margem esquerda. Assim, a partir das medições de um modelo em escala reduzida, foi retirado os dados que totalizavam 1243. De acordo com Galvão Filho [4], a curva de colina é um gráfico que expressa a complexa dependência da eficiência com vários outros parâmetros. Podendo ter uma demonstração simplificada sendo: η = F(h, ρ, μ, α, β) (1) A eficiência (η) é obtida pela relação entre a queda d’água (h), vazão (ρ) e os parâmetros de saída da turbina sendo, potência da turbina (μ), ângulo da porta wicket (α) e ângulo da pá do rotor(β).

## Linha de Base
Os três modelos selecionados para comparação e avaliação são Regressão Linear, Regressão XGBoost e Feedforward Neural Network. Utilizando de artifícios como grid search para a definição de hiperparâmetros [9] e k-fold para separação de variáveis entre treino e teste [10]. Por fim foi aplicado uma normalização na amplitude de [0,1].
<ul>
  <li>Regressão Linear</li>
  Como dito por H. Roopa e T. Asha em [2], a regressão prevê o valor y com base em um conjunto de variáveis independentes de entrada. Como a regressão linear expresso pela equação:<br>
  y = b0 + b1x0 + b2x2 + b3x3 + ... + bnxn + ε (2)<br>
  Cada regressão consegue prever uma única variável, como o modelo necessita de quatro saídas, se aplica uma regressão por variável de saída, permitindo um modelo de rede predizer todos os resultados. Assim, ao se notar a equação, a mesma é ajustada de acordo com cada ponto, portanto não apresentando hiperparâmetros apenas a própria equação.
  
  <li>Regressão XGBoost</li>
  Como explicado por [8], regressão XGBoost é um algorítmo de árvore com aumento de gradiente, permitindo através de uma árvore de decisões convergir até o melhor valor de uma dada entrada. Assim para tal modelo, utilizou-se os hiperparâmetros learning-rate, n-estimators, max-depth, min-child-weight, seed, subsample, colsamplebytree, gamma, reg-alpha e reg-lambda com os repectivos valores 0.116, 1000, 15, 0, 0, 0.8, 0.8, 0, 0 e 1.
  
  <li>FeedForward Neural Network</li>
  Feedforward Neural Network(FFNN) são modelos inspirados no cérebro humano com capacidade de generalização [3]. Para tal problemática, foi estabelecido uma rede com dois perceptrons [11] de entrada sendo respectivamente h e ρ. Contendo duas camadas ocultas sendo a primeira com 100 perceptrons e a segunda com 80. Já a camada de saída apresenta 4 perceptrons para determinar os valores de η, μ, α e β. Vale salientar que para as camadas de entrada e oculta, foi utilizado a tangente hiperbólica como função de ativação, enquanto a camada de saída usou sigmoide. Assim, os hiperparâmetros podem ser definidos, utilizando de valores como 0.01192 para learning-rate e 1000 para as épocas. Por fim, para melhorar a capacidade de generalização de tal algoritmo se aplica uma função de otimização chamada Adam [12], assim permitindo a rede se adequar de modo devido à problemática.
  
  <li>Erros</li>
  Para avaliar o critério preditivo destes modelos, foi aplicado três critérios, <b>sendo a raiz quadrada do erro-médio (RMSE)</b>,<b>erro médio absoluto (MAE)</b> e <b>coeficiente de determinação (R2)</b>
</ul>

## Discussão
Todos os modelos de modelos apresentados, se mostraram promissores, contudo o modelo Feedforward teve uma capacidade de generalização superior ao modelo XGBoost, contudo o XGBoost ainda se mostrou superior ao modelo de regressão linear. Vale ressaltar também que o modelo de regressão linear apresentou um erro alto em eficiência, demonstrando uma incapacidade de generalizar significativamente os dados, devido à maneira de dispersão dos mesmos.

## Conclusão
Como citado anteriormente, o modelo Feedforward dentre todos os modelos propostos, apresentou uma melhor capacidade de generalização, gerando a curva de colina demonFIGURE 1. Amostragem dados treino strada na imagem 6. Outro modelo que se mostra bastante promissor em questão de geração de dados, é o modelo XGBoost, visto que todos seus erros foram próximos ao modelo Feedforward.

## Referências
[1] Dixon, Sydney Lawrence, and Cesare Hall. Fluid mechanics and thermo-dynamics of turbomachinery. Butterworth-Heinemann, 2013.

[2] H. Roopa and T. Asha, "A linear model based on principal component analysis for disease prediction," IEEE Access, vol. 7, pp. 105314-105318, 2019.

[3] M. Hassoun, “Fundamentals of Artificial Neural Networks”, A Bradford Book, 2003.

[4] Galvão Filho, Arlindo R., et al. "Generation of Two Turbine Hill Chart Using Artificial Neural Networks." 2020 IEEE 10th International Conference on Intelligent System (IS). IEEE, 2020.

[5] A. R. Shaw and H. S. Sawyer and E. J. LeBoeuf and B. Hadjerioua, “Hydropower Optimization Using Artificial Neural Network Surrogate Models of a High-Fidelity Hydrodynamics and Water Quality Model”, Water Resources Research, vol. 53, nr. 11, pp. 9444–9461, 2017.

[6] A. T. Hammid and M. H. B. Sulaiman and A. N. Abdalla, “Prediction of small hydropower plant power production in Himreen Lake dam (HLD) using artificial neural network”, Alexandria Eng. J., http://dx.doi.org/10.1016/j.aej.2016.120.011, 2018.

[7] I. Bozic and R. Jovanovic “Prediction of Double-Regulated Hydraulic Turbine On-Cam Energy Characteristics by Artificial Neural Networks Approach”, FME Transactions, vol. 44, pp. 125-132, DOI: 10.5937/fmet1602125B, 2016.

[8] Nguyen, Lien Thi Kim, et al. "Using XGBoost and skip-gram model to predict online review popularity." SAGE Open 10.4 (2020): 2158244020983316.

[9] Alibrahim, Hussain, and Simone A. Ludwig. "Hyperparameter optimization: Comparing genetic algorithm against grid search and bayesian optimization." 2021 IEEE Congress on Evolutionary Computation (CEC). IEEE, 2021.

[10] Anguita, Davide, et al. "The ‘K’in K-fold cross validation." 20th European Symposium on Artificial Neural Networks, Computational Intelligence and Machine Learning (ESANN). i6doc. com publ, 2012.

[11] Minsky, Marvin, and Seymour A. Papert. Perceptrons: An introduction to computational geometry. MIT press, 2017.

[12] Zhang, Zijun. "Improved adam optimizer for deep neural networks." 2018 IEEE/ACM 26th International Symposium on Quality of Service (IWQoS). IEEE, 2018.
