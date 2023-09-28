# Criação de um modelo de Machine Learning para prever fraudes nas transações de cartão de crédito utilizando Python
#### Autor: Guilherme Oliveira da Rocha Cunha

## 1. Conjunto de dados
O conjunto de dados utilizado foi o [**Credit Card Fraud Detection**](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) disponibilizado no Kaggle pelo seu proprietário MACHINE LEARNING GROUP - ULB e possui licença Database Contents License (DbCL). O conjunto de dados contém aproximadamente 144 MB, disposto em 1 planilha nomeada "creditcard.csv".

Conforme sua descrição no Kaggle, o conjunto de dados contém transações efetuadas com cartões de crédito em setembro de 2013 por titulares de cartões europeus. Ele apresenta transações ocorridas em dois dias, onde apresentam-se 492 fraudes em 284.807 transações. O conjunto de dados é altamente desbalanceado, a classe positiva (fraudes) representa 0,172% de todas as transações.

O conjunto de dados contém apenas variáveis de entrada numéricas que são o resultado de uma transformação PCA. Infelizmente, devido a questões de confidencialidade, não são fornecidos os atributos originais e mais informações básicas sobre os dados. Os atributos V1, V2,… V28 são os principais componentes obtidos com PCA, os únicos atributos que não foram transformados com PCA são 'Time' e 'Amount'. O atributo 'Time' representa os segundos decorridos entre cada transação e a primeira transação no conjunto de dados. O atributo 'Amount' é o valor da transação e o atributo 'Class' é a variável de resposta e assume valor 1 em caso de fraude e 0 caso contrário.

## 2. Limpeza e Pré-processamento dos dados
Foi verificado o seguinte: 
- O conjunto de dados (dataset) presente em creditcard.csv possui 284807 observações e 31 atributos, **todos numéricos**.
- Esse dataset não possui valores nulos.
- A variável alvo (rótulo) é definida pelo atributo 'Class', que assume valor 1 em caso de fraude e 0 caso contrário.
- O dataset está bastante desbalanceado: são 284315 observações do tipo não fraude e apenas 492 do tipo fraude.

Foram criados dois dataframes, um para acomodar apenas as observações de fraude e um para as observações de não fraude, mas, como visto anteriormente, o dataset está desbalanceado. Para deixá-lo balanceado foi utilizada a técnica de undersampling (subamostragem). Essa é uma técnica utilizada para equilibrar conjuntos de dados desiguais, mantendo todos os dados na classe minoritária e diminuindo o tamanho da classe majoritária, ou seja, ambos os dataframes agora possuem 492 observações.

Os dois dataframes foram unidos (concatenados) os índices das observações foram corrigidos, gerando um dataframe geral com 984 observações e 32 atributos.

## 3. Divisão dos dados
Foram escolhidas 10 observações para compor o conjunto de dados de validação: 5 observações fraude e 5 observações não fraude. Como o conjunto de validação é um conjunto de dados separado, distinto do conjunto de treinamento e do conjunto de teste, essas 10 observações foram retiradas do dataframe geral. Agora o dataframe geral ("df") conta com 974 observações (487 fraude e 487 não fraude) e 32 atributos; e o dataframe de validação concatenado e com índices corrigidos ("df_val_total") com 10 observações e 33 atributos.

Desses atributos do dataframe de validação, quatro ('level_0', 'index', 'Time' e 'Class') não serão utilizados e foram removidos, gerando um dataframe de validação com 10 observações e 29 atributos.

Para a separação em labels (características) e features (rótulos), as labels ficaram definidas como sendo o dataframe geral sem os atributos 'index', 'Time' e 'Class' que não serão utilizados; e as features definidas como sendo o atributo 'Class' do dataframe geral:
```
#separando labels e features
X = df.drop(['index','Time','Class'], axis=1)
y = df['Class']
```
Foi definido que 80% dos dados serão utilizados para o treinamento e 20% para teste:
```
#separando em dados de treino e de teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=Y)
```

## 4. Seleção do algoritmo e Treinamento do modelo
O algoritmo de aprendizado de máquina escolhido foi a Regressão Logística (Logistic Regression) por ser uma técnica estatística que estima a probabilidade de uma variável pertencer a uma determinada classe ou categoria. 
```
#treinamento
lr = LogisticRegression(max_iter=1000)
lr.fit(X_train, y_train)
pred = lr.predict(X_test)
```

## 5. Avaliação de desempenho
Para a avaliação do desempenho foram utilizadas duas métricas:
- Acurácia do treinamento
```
#acurácia do treinamento
acc = accuracy_score(y_test, pred)
f'Acurácia do treinamento: {acc*100:.2f}%'
```

- Acurácia da validação
```
#acurácia da validação
pred = lr.predict(df_val_total)
df = pd.DataFrame({'real':df_val_total_real, 'previsao':pred})
acc = accuracy_score(df_val_total_real, pred)

print(df)

f'Acurácia da validação: {acc*100:.2f}%'
```
