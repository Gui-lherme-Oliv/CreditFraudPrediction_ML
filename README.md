# Criação de um modelo de Machine Learning para prever fraudes nas transações de cartão de crédito utilizando Python
#### Autor: Guilherme Oliveira da Rocha Cunha

## 1. Conjunto de dados
O conjunto de dados utilizado foi o [**Credit Card Fraud Detection**](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) disponibilizado no Kaggle pelo seu proprietário MACHINE LEARNING GROUP - ULB e possui licença Database Contents License (DbCL). O conjunto de dados contém aproximadamente 144 MB, disposto em 1 planilha nomeada "creditcard.csv".

Conforme sua descrição no Kaggle, o conjunto de dados contém transações efetuadas com cartões de crédito em setembro de 2013 por titulares de cartões europeus. Ele apresenta transações ocorridas em dois dias, onde apresentam-se 492 fraudes em 284.807 transações. O conjunto de dados é altamente desbalanceado, a classe positiva (fraudes) representa 0,172% de todas as transações.

O conjunto de dados contém apenas variáveis de entrada numéricas que são o resultado de uma transformação PCA. Infelizmente, devido a questões de confidencialidade, não são fornecidos os atributos originais e mais informações básicas sobre os dados. Os atributos V1, V2,… V28 são os principais componentes obtidos com PCA, os únicos atributos que não foram transformados com PCA são 'Time' e 'Amount'. O atributo 'Time' representa os segundos decorridos entre cada transação e a primeira transação no conjunto de dados. O atributo 'Amount' é o valor da transação e o atributo 'Class' é a variável de resposta e assume valor 1 em caso de fraude e 0 caso contrário.
