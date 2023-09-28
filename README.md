# Criação de um modelo de Machine Learning para prever fraudes nas transações de cartão de crédito utilizando Python
#### Autor: Guilherme Oliveira da Rocha Cunha

## 1. Conjunto de dados
O conjunto de dados utilizado foi o [**Credit Card Fraud Detection**](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) disponibilizado no Kaggle pelo seu proprietário MACHINE LEARNING GROUP - ULB e possui licença Database Contents License (DbCL). O conjunto de dados contém aproximadamente 144 MB, disposto em 1 planilha nomeada "creditcard.csv".

Conforme sua descrição no Kaggle, o conjunto de dados contém transações efetuadas com cartões de crédito em setembro de 2013 por titulares de cartões europeus. Ele apresenta transações ocorridas em dois dias, onde apresentam-se 492 fraudes em 284.807 transações. O conjunto de dados é altamente desbalanceado, a classe positiva (fraudes) representa 0,172% de todas as transações.

O conjunto de dados contém apenas variáveis de entrada numéricas que são o resultado de uma transformação PCA. Infelizmente, devido a questões de confidencialidade, não são fornecidos os atributos originais e mais informações básicas sobre os dados. Os atributos V1, V2,… V28 são os principais componentes obtidos com PCA, os únicos atributos que não foram transformados com PCA são 'Time' e 'Amount'. O atributo 'Time' representa os segundos decorridos entre cada transação e a primeira transação no conjunto de dados. O atributo 'Amount' é o valor da transação e o atributo 'Class' é a variável de resposta e assume valor 1 em caso de fraude e 0 caso contrário.

## 2. Limpeza e pré-processamento dos dados
Foi verificado o seguinte: 
- O conjunto de dados (dataset) presente em creditcard.csv possui 284807 observações e 31 atributos, todos numéricos.
- Esse dataset não possui valores nulos.
- A variável alvo (rótulo) é definida pelo atributo 'Class', que assume valor 1 em caso de fraude e 0 caso contrário.
- O dataset está bastante desbalanceado: são 284315 observações do tipo não fraude e apenas 492 do tipo fraude.

Foram criados dois dataframes, um para acomodar apenas as observações de fraude e um para as observações de não fraude, mas, como visto anteriormente, o dataset está desbalanceado. Para deixá-lo balanceado foi utilizada a técnica de undersampling (subamostragem). Essa é uma técnica utilizada para equilibrar conjuntos de dados desiguais, mantendo todos os dados na classe minoritária e diminuindo o tamanho da classe majoritária, ou seja, ambos os dataframes agora possuem 492 observações.

Os dois dataframes foram unidos (concatenados) em um só, com 984 observações e 33 atributos:

![df](https://github.com/Gui-lherme-Oliv/FraudeCredito_ML/assets/123426025/10fdb10d-4d1c-4ad9-b63c-063389e6b11a)

## 3. Divisão dos dados

