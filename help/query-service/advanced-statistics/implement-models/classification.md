---
title: Algoritmi di classificazione
description: Scopri come configurare e ottimizzare vari algoritmi di classificazione con parametri chiave, descrizioni e codice di esempio per implementare modelli statistici avanzati.
role: Developer
exl-id: 9105ab04-b480-48a0-b8f7-cf0ed5e5399d
source-git-commit: 489063fcd003e20f233a9c9d85d8cb6c22708d88
workflow-type: tm+mt
source-wordcount: '2449'
ht-degree: 4%

---

# Algoritmi di classificazione {#classification-algorithms}

Questo documento fornisce una panoramica dei vari algoritmi di classificazione, concentrandosi sulla loro configurazione, sui parametri chiave e sull’utilizzo pratico in modelli statistici avanzati. Gli algoritmi di classificazione vengono utilizzati per assegnare categorie ai punti dati in base alle funzioni di input. Ogni sezione include descrizioni dei parametri e codice di esempio per implementare e ottimizzare questi algoritmi per attività quali alberi delle decisioni, foresta casuale e classificazione Bayes naive.

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier] è un approccio di apprendimento supervisionato utilizzato in statistica, data mining e machine learning. In questo approccio, un albero decisionale viene utilizzato come modello predittivo per le attività di classificazione, traendo conclusioni da una serie di osservazioni.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni di [!DNL Decision Tree Classifier].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | Il numero massimo di raccoglitori determina il modo in cui le feature continue vengono suddivise in intervalli discreti. Questo influisce sul modo in cui le funzioni vengono suddivise in ciascun nodo della struttura decisionale. Più contenitori forniscono maggiore granularità. | 32 | Deve essere almeno pari a 2 e almeno uguale al numero di categorie in qualsiasi funzione categoriale. |
| `CACHE_NODE_IDS` | Se `false`, l&#39;algoritmo passa gli alberi agli esecutori per far corrispondere le istanze con i nodi. Se `true`, l&#39;algoritmo memorizza nella cache gli ID dei nodi per ogni istanza, velocizzando l&#39;addestramento di strutture più profonde. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Specifica la frequenza di checkpoint per gli ID dei nodi memorizzati in cache. `10`, ad esempio, indica che la cache viene sottoposta a checkpoint ogni 10 iterazioni. | 10 | (>= 1) |
| `IMPURITY` | Il criterio utilizzato per il calcolo dell’acquisizione di informazioni (senza distinzione tra maiuscole e minuscole). | gini | `entropy`, `gini` |
| `MAX_DEPTH` | Profondità massima dell&#39;albero (non negativa). Ad esempio, profondità `0` significa 1 nodo foglia e profondità `1` significa 1 nodo interno e 2 nodi foglia. | 5 | (>= 0) (intervallo: [0,30]) |
| `MIN_INFO_GAIN` | Il guadagno minimo di informazioni necessario affinché una suddivisione possa essere considerata in un nodo della struttura. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Frazione minima del numero di campioni ponderati che ogni bambino deve avere dopo una divisione. Se una suddivisione fa sì che la frazione del peso totale in uno dei figli sia inferiore a questo valore, viene eliminata. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Il numero minimo di istanze che ogni figlio deve avere dopo una suddivisione. Se una suddivisione genera un numero di istanze inferiore a questo valore, la suddivisione viene eliminata. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria massima, in MB, allocata all&#39;aggregazione dell&#39;istogramma. Se questo valore è troppo piccolo, viene diviso solo 1 nodo per iterazione e i relativi aggregati possono superare queste dimensioni. | 256 | (>= 0) |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `SEED` | Il seme casuale. | N/D | Qualsiasi numero a 64 bit |
| `WEIGHT_COL` | Il nome della colonna, ad esempio pesi. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | NON IMPOSTATO | Qualsiasi stringa |
| `ONE_VS_REST` | Abilita o disabilita il wrapping di questo algoritmo con One-vs-Rest, utilizzato per problemi di classificazione in più classi. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Esempio**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

[!DNL Factorization Machine Classifier] è un algoritmo di classificazione che supporta la normale discesa con gradiente e il risolutore AdamW. Il modello di classificazione della macchina di fattorizzazione utilizza la perdita logistica, che può essere ottimizzata tramite una discesa con gradiente, e spesso include termini di regolarizzazione come L2 per evitare l&#39;eccesso di adattamento.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni di [!DNL Factorization Machine Classifier].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | La tolleranza di convergenza, che controlla la precisione dell&#39;ottimizzazione. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | La dimensionalità dei fattori. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Specifica se adattare un termine di intercettazione. | `true` | `true`, `false` |
| `FIT_LINEAR` | Specifica se adattarsi al termine lineare (noto anche come termine a una via). | `true` | `true`, `false` |
| `INIT_STD` | Deviazione standard per l&#39;inizializzazione dei coefficienti. | 0,01 | (>= 0) |
| `MAX_ITER` | Il numero massimo di iterazioni per l’algoritmo da eseguire. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Frazione di dati da utilizzare in mini-batch durante l’apprendimento. Deve essere compreso nell&#39;intervallo `(0, 1]`. | 1,0 | 0 &lt; valore &lt;= 1 |
| `REG_PARAM` | Il parametro di regolarizzazione, che consente di controllare la complessità del modello e di evitare l&#39;adattamento eccessivo. | 0,0 | (>= 0) |
| `SEED` | Valore di inizializzazione casuale per il controllo dei processi casuali nell&#39;algoritmo. | N/D | Qualsiasi numero a 64 bit |
| `SOLVER` | L’algoritmo del risolutore utilizzato per l’ottimizzazione. Le opzioni supportate sono `gd` (discendenza sfumata) e `adamW`. | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | Dimensione del passaggio iniziale per l’ottimizzazione, spesso interpretata come tasso di apprendimento. | 1,0 | > 0 |
| `PROBABILITY_COL` | Nome di colonna per le probabilità condizionali di classe previste. Nota: non tutti i modelli generano probabilità ben calibrate; queste dovrebbero essere trattate come punteggi di affidabilità piuttosto che come probabilità esatte. | &quot;probabilità&quot; | Qualsiasi stringa |
| `PREDICTION_COL` | Nome di colonna per le etichette di classe previste. | &quot;previsione&quot; | Qualsiasi stringa |
| `RAW_PREDICTION_COL` | Nome della colonna per i valori di previsione non elaborati (noti anche come affidabilità). | &quot;rawPrediction&quot; | Qualsiasi stringa |
| `ONE_VS_REST` | Specifica se abilitare One-vs-Rest per la classificazione in più classi. | FALSE | `true`, `false` |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

[!DNL Gradient Boosted Tree Classifier] utilizza un insieme di strutture decisionali per migliorare la precisione delle attività di classificazione, combinando più strutture per migliorare le prestazioni del modello.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni di [!DNL Gradient Boosted Tree Classifier].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Il numero massimo di raccoglitori determina il modo in cui le feature continue vengono suddivise in intervalli discreti. Questo influisce sul modo in cui le funzioni vengono suddivise in ciascun nodo della struttura decisionale. Più contenitori forniscono maggiore granularità. | 32 | Deve essere almeno 2 e uguale o maggiore del numero di categorie in qualsiasi caratteristica categoriale. |
| `CACHE_NODE_IDS` | Se `false`, l&#39;algoritmo passa gli alberi agli esecutori per far corrispondere le istanze con i nodi. Se `true`, l&#39;algoritmo memorizza nella cache gli ID dei nodi per ogni istanza, velocizzando l&#39;addestramento di strutture più profonde. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Specifica la frequenza di checkpoint per gli ID dei nodi memorizzati in cache. `10`, ad esempio, indica che la cache viene sottoposta a checkpoint ogni 10 iterazioni. | 10 | (>= 1) |
| `MAX_DEPTH` | Profondità massima dell&#39;albero (non negativa). Ad esempio, profondità `0` significa 1 nodo foglia e profondità `1` significa 1 nodo interno e 2 nodi foglia. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Il guadagno minimo di informazioni necessario affinché una suddivisione possa essere considerata in un nodo della struttura. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Frazione minima del numero di campioni ponderati che ogni bambino deve avere dopo una divisione. Se una suddivisione fa sì che la frazione del peso totale in uno dei figli sia inferiore a questo valore, viene eliminata. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Il numero minimo di istanze che ogni figlio deve avere dopo una suddivisione. Se una suddivisione genera un numero di istanze inferiore a questo valore, la suddivisione viene eliminata. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria massima, in MB, allocata all&#39;aggregazione dell&#39;istogramma. Se questo valore è troppo piccolo, viene diviso solo 1 nodo per iterazione e i relativi aggregati possono superare queste dimensioni. | 256 | (>= 0) |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `VALIDATION_INDICATOR_COL` | Il nome della colonna indica se ogni riga viene utilizzata per l’apprendimento o la convalida. Il valore `false` indica l&#39;addestramento, mentre `true` indica la convalida. Se non viene impostato alcun valore, il valore predefinito è `None`. | “Nessuno” | Qualsiasi stringa |
| `RAW_PREDICTION_COL` | Nome della colonna per i valori di previsione non elaborati (noti anche come affidabilità). | &quot;rawPrediction&quot; | Qualsiasi stringa |
| `LEAF_COL` | Il nome della colonna per gli indici foglia, che è l&#39;indice foglia previsto di ogni istanza in ogni albero, generato dall&#39;attraversamento del preordine. | &quot;&quot; | Qualsiasi stringa |
| `FEATURE_SUBSET_STRATEGY` | Il numero di feature considerate per la suddivisione in ciascun nodo della struttura. Opzioni supportate: `auto` (determinata automaticamente in base all&#39;attività), `all` (utilizza tutte le funzionalità), `onethird` (utilizza un terzo delle funzionalità), `sqrt` (utilizza la radice quadrata del numero di funzionalità), `log2` (utilizza il logaritmo base 2 del numero di funzionalità) e `n` (dove n è una frazione delle funzionalità se nell&#39;intervallo `(0, 1]` o un numero specifico di funzionalità se nell&#39;intervallo `[1, total number of features]`). | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` |
| `WEIGHT_COL` | Il nome della colonna, ad esempio pesi. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | NON IMPOSTATO | Qualsiasi stringa |
| `LOSS_TYPE` | Funzione di perdita che il modello [!DNL Gradient Boosted Tree] tenta di ridurre a icona. | &quot;logistico&quot; | `logistic` (senza distinzione maiuscole/minuscole) |
| `STEP_SIZE` | Dimensione del passaggio (nota anche come tasso di apprendimento) nell&#39;intervallo `(0, 1]`, utilizzata per ridurre il contributo di ogni stimatore. | 0,1 | (>= 0,0, &lt;= 1) |
| `MAX_ITER` | Il numero massimo di iterazioni per l’algoritmo. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Frazione di dati di addestramento utilizzata per addestrare ogni albero decisionale. Il valore deve essere compreso nell&#39;intervallo 0 &lt; valore &lt;= 1. | 1,0 | `(0, 1]` |
| `PROBABILITY_COL` | Nome di colonna per le probabilità condizionali di classe previste. Nota: non tutti i modelli generano probabilità ben calibrate; queste dovrebbero essere trattate come punteggi di affidabilità piuttosto che come probabilità esatte. | &quot;probabilità&quot; | Qualsiasi stringa |
| `ONE_VS_REST` | Abilita o disabilita il wrapping di questo algoritmo con One-vs-Rest per la classificazione in più classi. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Esempio**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (SVC lineare) {#linear-support-vector-classifier}

[!DNL Linear Support Vector Classifier] (LinearSVC) costruisce un iperpiano per classificare i dati in uno spazio ad alta dimensione. Puoi utilizzarlo per massimizzare il margine tra le classi al fine di ridurre al minimo gli errori di classificazione.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni di [!DNL Linear Support Vector Classifier (LinearSVC)].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | Il numero massimo di iterazioni per l’algoritmo da eseguire. | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | Profondità dell&#39;aggregazione ad albero. Questo parametro viene utilizzato per ridurre il sovraccarico delle comunicazioni di rete. | 2 | Qualsiasi numero intero positivo |
| `FIT_INTERCEPT` | Se adattare un termine di intercettazione. | `true` | `true`, `false` |
| `TOL` | Questo parametro determina la soglia per l’interruzione delle iterazioni. | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | Memoria massima in MB per lo stacking dei dati di input in blocchi. Se il parametro è impostato su `0`, il valore ottimale viene scelto automaticamente (in genere circa 1 MB). | 0,0 | (>= 0) |
| `REG_PARAM` | Il parametro di regolarizzazione, che consente di controllare la complessità del modello e di evitare l&#39;adattamento eccessivo. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Questo parametro indica se standardizzare le feature di addestramento prima di adattare il modello. | `true` | `true`, `false` |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `RAW_PREDICTION_COL` | Nome della colonna per i valori di previsione non elaborati (noti anche come affidabilità). | &quot;rawPrediction&quot; | Qualsiasi stringa |
| `ONE_VS_REST` | Abilita o disabilita il wrapping di questo algoritmo con One-vs-Rest per la classificazione in più classi. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Esempio**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression] è un algoritmo supervisionato utilizzato per le attività di classificazione binaria. Modella la probabilità che un’istanza appartenga a una classe utilizzando la funzione logistica e assegna l’istanza alla classe con la probabilità più elevata. Questo lo rende adatto a problemi in cui l’obiettivo è quello di separare i dati in una di due categorie.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni di [!DNL Logistic Regression].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | Numero massimo di iterazioni eseguite dall&#39;algoritmo. | 100 | (>= 0) |
| `REGPARAM` | Il parametro di regolarizzazione viene utilizzato per controllare la complessità del modello. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Il parametro di combinazione `ElasticNet` controlla il saldo tra le penalità L1 (Lazo) e L2 (Ridge). Un valore pari a 0 applica una penalità L2 (Ridge, che riduce la dimensione dei coefficienti), mentre un valore pari a 1 applica una penalità L1 (Lasso, che incoraggia la sparsità impostando alcuni coefficienti a zero). | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Esempio**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

[!DNL Multilayer Perceptron Classifier] (MLPC) è un classificatore di rete neurale artificiale di avanzamento. È costituito da più livelli completamente connessi di nodi, dove ogni nodo applica una combinazione lineare ponderata di input, seguita da una funzione di attivazione. MLPC viene utilizzato per attività di classificazione complesse che richiedono limiti di decisione non lineari.

**Parametri**

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Il numero massimo di iterazioni per l’algoritmo da eseguire. | 100 | (>= 0) |
| `BLOCK_SIZE` | Dimensione del blocco per lo stacking dei dati di input nelle matrici all&#39;interno delle partizioni. Se la dimensione del blocco supera i dati rimanenti in una partizione, viene regolata di conseguenza. | 128 | (>= 0) |
| `STEP_SIZE` | Dimensione del passaggio utilizzata per ogni iterazione di ottimizzazione (applicabile solo per il risolutore `gd`). | 0,03 | (> 0) |
| `TOL` | La tolleranza di convergenza per l&#39;ottimizzazione. | `1E-6` | (>= 0) |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `SEED` | Valore di inizializzazione casuale per il controllo dei processi casuali nell&#39;algoritmo. | NON IMPOSTATO | Qualsiasi numero a 64 bit |
| `PROBABILITY_COL` | Nome di colonna per le probabilità condizionali di classe previste. Questi devono essere trattati come punteggi di affidabilità piuttosto che come probabilità esatte. | &quot;probabilità&quot; | Qualsiasi stringa |
| `RAW_PREDICTION_COL` | Nome della colonna per i valori di previsione non elaborati (noti anche come affidabilità). | &quot;rawPrediction&quot; | Qualsiasi stringa |
| `ONE_VS_REST` | Abilita o disabilita il wrapping di questo algoritmo con One-vs-Rest per la classificazione in più classi. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier] è un semplice classificatore probabilistico e multiclasse basato sul teorema di Bayes con ipotesi di indipendenza forte (naive) tra le feature. Si addestra in modo efficiente calcolando le probabilità condizionali in un singolo passaggio sui dati di addestramento per calcolare la distribuzione delle probabilità condizionali di ogni funzione data ogni etichetta. Per le previsioni, usa il teorema di Bayes per calcolare la distribuzione di probabilità condizionale di ogni etichetta data un&#39;osservazione.

**Parametri**

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Specifica il tipo di modello. Le opzioni supportate sono `"multinomial"`, `"complement"`, `"bernoulli"` e `"gaussian"`. Il tipo di modello distingue tra maiuscole e minuscole. | &quot;multinomiale&quot; | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | Il parametro di uniformità viene utilizzato per gestire i problemi di frequenza zero nei dati categorici. | 1,0 | (>= 0) |
| `PROBABILITY_COL` | Questo parametro specifica il nome della colonna per le probabilità condizionali di classe previste. Nota: non tutti i modelli forniscono stime di probabilità ben calibrate; questi valori vengono considerati come attendibilità anziché come probabilità precise. | &quot;probabilità&quot; | Qualsiasi stringa |
| `WEIGHT_COL` | Nome della colonna per i pesi dell’istanza. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | NON IMPOSTATO | Qualsiasi stringa |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `RAW_PREDICTION_COL` | Nome della colonna per i valori di previsione non elaborati (noti anche come affidabilità). | &quot;rawPrediction&quot; | Qualsiasi stringa |
| `ONE_VS_REST` | Specifica se abilitare One-vs-Rest per la classificazione in più classi. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier] è un algoritmo di apprendimento di gruppo che crea più strutture decisionali durante l&#39;apprendimento. Attenua l’eccesso di adattamento calcolando la media delle previsioni e selezionando la classe scelta dalla maggior parte degli alberi per le attività di classificazione.

**Parametri**

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Il numero massimo di raccoglitori determina il modo in cui le feature continue vengono suddivise in intervalli discreti. Questo influisce sul modo in cui le funzioni vengono suddivise in ciascun nodo della struttura decisionale. Più contenitori forniscono maggiore granularità. | 32 | Deve essere almeno 2 e uguale o maggiore del numero di categorie in qualsiasi caratteristica categoriale. |
| `CACHE_NODE_IDS` | Se `false`, l&#39;algoritmo passa gli alberi agli esecutori per far corrispondere le istanze con i nodi. Se `true`, l&#39;algoritmo memorizza nella cache gli ID nodo per ogni istanza, velocizzando l&#39;apprendimento. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Specifica la frequenza di checkpoint per gli ID dei nodi memorizzati in cache. `10`, ad esempio, indica che la cache viene sottoposta a checkpoint ogni 10 iterazioni. | 10 | (>= 1) |
| `IMPURITY` | Il criterio utilizzato per il calcolo dell’acquisizione di informazioni (senza distinzione tra maiuscole e minuscole). | gini | `entropy`, `gini` |
| `MAX_DEPTH` | Profondità massima dell&#39;albero (non negativa). Ad esempio, profondità `0` significa 1 nodo foglia e profondità `1` significa 1 nodo interno e 2 nodi foglia. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Il guadagno minimo di informazioni necessario affinché una suddivisione possa essere considerata in un nodo della struttura. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Frazione minima del numero di campioni ponderati che ogni bambino deve avere dopo una divisione. Se una suddivisione fa sì che la frazione del peso totale in uno dei figli sia inferiore a questo valore, viene eliminata. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Il numero minimo di istanze che ogni figlio deve avere dopo una suddivisione. Se una suddivisione genera un numero di istanze inferiore a questo valore, la suddivisione viene eliminata. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria massima, in MB, allocata all&#39;aggregazione dell&#39;istogramma. Se questo valore è troppo piccolo, viene diviso solo 1 nodo per iterazione e i relativi aggregati possono superare queste dimensioni. | 256 | (>= 1) |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `WEIGHT_COL` | Il nome della colonna, ad esempio pesi. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | NON IMPOSTATO | Qualsiasi nome di colonna valido o vuoto |
| `SEED` | Valore di inizializzazione casuale utilizzato per controllare i processi casuali nell&#39;algoritmo. | -1689246527 | Qualsiasi numero a 64 bit |
| `BOOTSTRAP` | Se i campioni di bootstrap vengono utilizzati durante la creazione di alberi. | `true` | `true`, `false` |
| `NUM_TREES` | Il numero di alberi da addestrare. Se `1`, non viene utilizzato alcun bootstrapping. Se maggiore di `1`, viene applicato il bootstrapping. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | La frazione dei dati di formazione utilizzati per imparare ogni albero decisionale. | 1,0 | (> 0, &lt;= 1) |
| `LEAF_COL` | Il nome della colonna per gli indici foglia, che contiene l&#39;indice foglia previsto di ogni istanza in ogni albero per preordine. | &quot;&quot; | Qualsiasi stringa |
| `PROBABILITY_COL` | Nome di colonna per le probabilità condizionali di classe previste. Questi devono essere trattati come punteggi di affidabilità piuttosto che come probabilità esatte. | NON IMPOSTATO | Qualsiasi stringa |
| `RAW_PREDICTION_COL` | Nome della colonna per i valori di previsione non elaborati (noti anche come affidabilità). | &quot;rawPrediction&quot; | Qualsiasi stringa |
| `ONE_VS_REST` | Specifica se abilitare One-vs-Rest per la classificazione in più classi. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Esempio**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## Passaggi successivi

Dopo aver letto questo documento, ora sai come configurare e utilizzare vari algoritmi di classificazione. Quindi, consulta i documenti su [regressione](./regression.md) e [clustering](./clustering.md) per ulteriori informazioni su altri tipi di modelli statistici avanzati.
