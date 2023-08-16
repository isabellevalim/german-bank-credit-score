# german-bank-credit-score
Desenvolvimento de um modelo de concessão de crédito utilizando regressão logística.

## Data Source
A base de dados utilizada para modelagem do problema está disponibilizada na pasta 'data'.

## Explicação conceitual sobre as técnicas e recursos utilizados no projeto
Você vai encontrar uma explicação mais aprofundada no módulo Machine Learning 

## Entendimento do problema
Vamos supor que Maria precisa de um empréstimo. Ela entra no aplicativo do banco, fornece alguns dados e faz uma solicitação de empréstimo.
Para saber se deve ou não emprestar dinheiro para Maria, o banco faz uma análise de crédito e, com base nas informações dessa análise, o banco toma a decisão.

Vamos ver no detalhe como isso funciona. Algumas informações importantes:
- O banco possui uma base de clientes enriquecida com uma série de informações cadastrais e financeiras compradas em provedores de dados.
- Esses clientes do banco são marcados. Existem indicadores que sinalizam se eles estão com fatura em atraso, a quanto tempo está em atraso e qual valor esses clientes devem ao banco.
- O banco utiliza um modelo desenvolvido com base nas características dos clientes antigos para tentar prever se um novo cliente seria um bom ou mau pagador, afim de minimizar as chances de emprestar dinheiro e não receber.

Que modelo é esse? É o chamado Credit Score (ou score de crédito).
O score de crédito tem por objetivo estimar a probabilidade de um evento acontecer e, por isso, se trata de um valor entre 0 e 1.

Pensando na concessão de crédito, o evento que estamos buscando saber é se o cliente que solicitou empréstimo no banco vai ser um mau pagador.
Por isso nós queremos classificar os solicitantes de crédito em adimplentes ou inadimplentes. É um evento binário.

Toda operação de crédito tem um risco associado. Nós podemos entender o risco como sendo a probabilidade do cliente não pagar o valor devido em determinado período de tempo.

## Entendendo a base de dados
A primeira etapa de qualquer processo de modelagem é o entendimento da base de dados.
Neste caso, vemos que a base de dados possui 21 variáveis, sendo uma delas a variável binária 'default'que indica se o cliente é bom (1) ou mau (0) pagador.
Nesta etapa é importante verificar se a base possui dados duplicados ou dados nulos.

Na vida real, a alta incidência de dados duplicados ou nulos deve ser reportada para a área de negócios, onde a decisão do que fazer será tomada em conjunto.
Substituir esses dados por médias ou excluí-los do dataset só é uma boa estratégia no caso de projetos de estudo, como esse aqui.

## Exploração dos dados
Logo de cara é possível notar que existem várias colunas com valores do tipo string. Isso é um problema porque a regressão logística é um algoritmo capaz de receber apenas inputs numéricos.
Pensando nisso, precisamos fazer uma transformação em todas essas variáveis do tipo string.
Vamos transformar todos os valores em categorias utilizando o método .map()

Com essas transformações prontas, podemos continuar explorando os dados.
De início, selecionei algumas variáveis para analisar utilizando o método .describe() e fazer uma análise descritiva.
É uma ótima opção para variáveis numéricas. No caso de 'idade' e 'valor_emprestimo', por exemplo, consigo extrair informações que fazem sentido como mínimo, máximo e média.
Mas no caso das variáveis categóricas como 'sexo_est_civil' e binárias como 'default', aqueles valores não nos dizem nada.

Não faz sentido avaliar variáveis categóricas e binárias dessa forma. Para variáveis deste tipo, a análise descritiva deve ser realizada utilizando o método .value_counts()

  #### Para praticar:
- Faça uma análise descritiva com o restante das variáveis do dataset (numéricas e categóricas)

Uma informação MUITO IMPORTANTE que conseguimos extrair com a análise descritiva dos dados é que o dataset é desbalanceado.
Existe uma incidência muito maior de clientes mau pagadores do que clientes bom pagadores.
Isso nos indica que a acurácia não é uma boa métrica para avaliar a qualidade do modelo. Análises complementares precisarão serem realizadas.

Depois de analisar estatisticamente a base de dados, o próximo passo para desenvolver um bom modelo é entender como funciona a distribuição das variáveis.
Para isso, contamos com o auxílio dos gráficos. Os mais comuns a serem analisados são histograma, bloxplot e gráfico de barras.

  #### Para praticar:
- Analise a distribuição do restante das variáveis do dataset utilizando histogramas, bloxplot e gráficos de barra

## Desenvolvimento do modelo
Aqui começamos, de fato, a desenvolver o modelo de regressão logística para identificação de bons e maus pagadores do banco.

1. A base de dados é dividida, randomicamente, em base de treino e base de teste.
2. O modelo de regressão logística é aplicado na base de treino.
3. Com o modelo treinado, são geradas as previsões utilizando a base de teste.
4. As métricas estatísticas são calculadas.
5. Os resultados são avaliados.

## Considerações finais
Este projeto é um modelo básico do que você precisa saber para se jogar no mercado!
Eu dei o pontapé inicial, mas você precisa fazer a sua parte. Posso contar contigo?

Vou listar aqui o que você precisa desenvolver para que esse seja um projeto de Credit Score completo, tecnicamente falando:
- separe a variável 'sexo_est_civil' nas variáveis 'sexo' e 'estado_civil' e analise o impacto disso no resultado
- ao invés de utilizar o 'train_test_split' para dividir a base de dados em base de treino e base de teste, utilize o método de validação cruzada
- utilize outro algoritmo mais aderente ao problema de dados desbalanceados (como o DecisionTreeClassifier) e compare os resultados
- otimize os hiperparâmetros do algoritmo para tentar melhorar os resultados. Para isso, use o GridSearchCV.

Falando pela ótica do negócio, 
- no sistema financeiro, um indivíduo dificilmente é analisado sozinho. A ideia é analisar o comportamento de um grupo e ajustar esse indivíduo dentro de um grupo. Por isso, é muito comum trabalhar com faixas de classificação para esses indivíduos solicitantes de crédito.
- Remodele o problema utilizando, ao invés da variável 'idade', uma variável 'faixa_idade' onde indivíduos de 18 a 30 anos pertencem à faixa 1, de 31 a 40 anos pertencem à faixa 2, de 41 à 50 anos pertencem à faixa 3 e daí por diante.

