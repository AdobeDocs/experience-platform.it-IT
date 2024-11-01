---
title: Estensione SQL per Feature Engineering
description: Scopri l’estensione SQL per la progettazione delle funzioni di Data Distiller, che consente di pre-elaborare i dati per la modellazione statistica avanzata. Vengono descritte le tecniche di estrazione, trasformazione e selezione delle feature disponibili.
role: Developer
source-git-commit: 1fcfb5c41750e853daaf036ceaae3527b805391c
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Estensione SQL per ingegneria delle funzioni

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che hanno acquistato il componente aggiuntivo Data Distiller. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.

Per soddisfare le esigenze tecniche, utilizza l’estensione SQL Transformer per semplificare e automatizzare la preelaborazione dei dati. Utilizza questa estensione per creare funzionalità e usufruire di una sperimentazione perfetta con diverse tecniche di ingegneria delle funzionalità, inclusa l’associazione con i modelli. Progettato per l&#39;elaborazione distribuita, è possibile eseguire la progettazione di funzionalità su set di dati di grandi dimensioni in modo parallelo e scalabile, riducendo in modo significativo il tempo necessario per la preelaborazione dei dati con l&#39;estensione SQL per la progettazione di funzionalità di Data Distiller.

## Panoramica tecnica {#technique-overview}

Le funzionalità di ingegneria delle feature coprono tre aree principali: Estrazione feature (Feature Extraction), Trasformazione feature (Feature Transformation) e Selezione feature (Feature Selection). Ogni area include funzioni specifiche progettate per estrarre, convertire, mettere a fuoco e migliorare la preelaborazione dei dati.

### Estrazione delle funzioni {#feature-extraction}

Estrai informazioni rilevanti dai dati, in particolare dati di testo, e convertili in un formato numerico che i modelli supportati possono utilizzare o trasformare e derivare set di dati. Utilizzate le seguenti funzioni per eseguire l&#39;estrazione delle feature:

- **[Trasformatore testuale](./feature-transformation.md#textual-transformations)**: converte i dati testuali in funzioni numeriche.
- **[Vectorizer conteggio](./feature-transformation.md#countvectorizer)**: trasforma una raccolta di documenti di testo in vettori di conteggi di token.
- **[N-grammi](./feature-transformation.md#ngram)**: genera sequenze di n-grammi dai dati di testo.
- **[Rimozione parole non consentite](./feature-transformation.md#stopwordsremover)**: escludere le parole comuni che non hanno un significato significativo.
- **[TF-IDF](./feature-transformation.md#tf-idf)**: misura l&#39;importanza delle parole in un documento rispetto a un corpus.
- **[Tokenizer](./feature-transformation.md#tokenizer)**: suddividi il testo in singoli termini (parole).
- **[Word2Vec](./feature-transformation.md#word2vec)**: mappa le parole su vettori a dimensione fissa e crea incorporamenti di parole.

### Trasformazione delle feature {#feature-transformation}

Oltre alle feature di estrazione, utilizzate i trasformatori generali riportati di seguito per preparare le feature per modelli statistici avanzati e set di dati derivati. Applica il ridimensionamento, la normalizzazione o la codifica per garantire che le funzioni abbiano la stessa scala e una distribuzione simile.

#### Trasformatori generici

Di seguito è riportato un elenco di strumenti per l’elaborazione di un’ampia gamma di tipi di dati al fine di migliorare il flusso di lavoro di preelaborazione dei dati.

- **[Imputer numerico](./feature-transformation.md#numeric-imputer)**: riempie i valori mancanti nelle colonne numeriche con un
- **[Input stringa](./feature-transformation.md#string-imputer)**: sostituire i valori stringa mancanti con un valore specificato
- **[Assemblatore vettoriale](./feature-transformation.md#vector-assembler)**: combina più colonne in un&#39;unica colonna vettoriale.

#### Trasformatori numerici

Applicate queste tecniche per elaborare e scalare in modo efficace i dati numerici per migliorare le prestazioni del modello.

- **[Binarizer](./feature-transformation.md#binarizer)**: converte le funzionalità continue in valori binari basati su una soglia.
- **[Bucketizer](./feature-transformation.md#bucketizer)**: mappa le funzioni continue in bucket discreti.
- **[Scaler min-max](./feature-transformation.md#minmaxscaler)**: ridimensionare le funzionalità a un intervallo specificato, in genere [0, 1].
- **[Max Abs Scaler](./feature-transformation.md#maxabsscaler)**: ridimensiona le funzioni all&#39;intervallo [-1, 1] senza modificare la sparsità.
- **[Normalizer](./feature-transformation.md#normalizer)**: normalizza i vettori in modo che abbiano una norma unitaria.
- **[Discretizzatore quantile](./feature-transformation.md#quantilediscretizer)**: converte le funzionalità continue in funzionalità categoriche associandole a quantili.
- **[Scala standard](./feature-transformation.md#standardscaler)**: normalizza le funzionalità in modo che abbiano una deviazione standard unitaria e/o una media pari a zero.

#### Trasformatori categorici

Utilizza questi trasformatori per convertire e codificare i dati delle categorie in formati adatti ai modelli di apprendimento automatico.

- **[Indicizzatore stringa](./feature-transformation.md#stringindexer)**: converte dati stringa categorici in indici numerici.
- **[Un Hot Encoder](./feature-transformation.md#onehotencoder)**: mappa dati categorici in vettori binari.

### Selezione di funzioni {#feature-selection}

Quindi, focalizzate la selezione di un sottoinsieme delle feature più importanti dal set originale. Questo processo consente di ridurre la dimensionalità dei dati, semplificando l’elaborazione dei modelli e migliorando le prestazioni complessive del modello.

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## Implementare la clausola OPTIONS {#options-clause}

Quando si definisce il modello, utilizzare la clausola `OPTIONS` per specificare l&#39;algoritmo e i relativi parametri. Iniziare impostando il parametro `type` per indicare l&#39;algoritmo in uso, ad esempio `K-Means`. Definire quindi i parametri rilevanti nella clausola `OPTIONS` come coppie chiave-valore per ottimizzare il modello. Alcuni parametri possono essere posizionati e richiedere che tutti i parametri precedenti siano specificati se vengono forniti valori personalizzati. Se si sceglie di non personalizzare determinati parametri, il sistema applica le impostazioni predefinite. Consulta la documentazione pertinente per informazioni sulla funzione di ciascun parametro e sui valori predefiniti.

### Passaggi successivi

Dopo aver appreso le tecniche di ingegneria delle funzionalità descritte in questo documento, passare al documento [Modelli](./models.md). Ti guida attraverso il processo di creazione, formazione e gestione di modelli affidabili utilizzando le funzioni che hai progettato. Una volta generati i modelli, passare al documento [Implementare modelli statistici avanzati.](./implement-models/implement-models.md). Questo documento offre una panoramica e collegamenti a guide approfondite per diverse tecniche di modellazione, tra cui clustering, classificazione e regressione. Seguendo questi documenti, imparerai a configurare e implementare vari modelli affidabili all’interno dei flussi di lavoro SQL e a ottimizzare i modelli per l’analisi avanzata dei dati.
