---
title: Algoritmi di regressione
description: Scopri come configurare e ottimizzare vari algoritmi di regressione con parametri chiave, descrizioni e codice di esempio per implementare modelli statistici avanzati.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 4%

---

# Algoritmi di regressione {#regression-algorithms}

Questo documento fornisce una panoramica di vari algoritmi di regressione, concentrandosi sulla loro configurazione, sui parametri chiave e sull’utilizzo pratico in modelli statistici avanzati. Gli algoritmi di regressione sono utilizzati per modellare la relazione tra variabili dipendenti e indipendenti, predicendo risultati continui sulla base dei dati osservati. Ogni sezione include descrizioni dei parametri e codice di esempio per implementare e ottimizzare questi algoritmi per attività quali la regressione lineare, casuale e di sopravvivenza.

## Regressione di [!DNL Decision Tree] {#decision-tree-regression}

L&#39;apprendimento di [!DNL Decision Tree] è un metodo di apprendimento supervisionato utilizzato in statistica, data mining e machine learning. In questo approccio, un albero decisionale di classificazione o regressione è utilizzato come modello predittivo per trarre conclusioni su una serie di osservazioni.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l’ottimizzazione delle prestazioni dei modelli dell’albero decisionale.

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Il numero massimo di raccoglitori determina il modo in cui le feature continue vengono suddivise in intervalli discreti. Questo influisce sul modo in cui le funzioni vengono suddivise in ciascun nodo della struttura decisionale. Più contenitori forniscono maggiore granularità. | 32 | Deve essere almeno 2 e il numero di categorie in qualsiasi funzione categorica. |
| `CACHE_NODE_IDS` | Se `false`, l&#39;algoritmo passa gli alberi agli esecutori per far corrispondere le istanze con i nodi. Se `true`, l&#39;algoritmo memorizza nella cache gli ID nodo per ogni istanza. La memorizzazione nella cache può accelerare la formazione degli alberi più profondi. | false | `true` o `false` |
| `CHECKPOINT_INTERVAL` | Specifica la frequenza di checkpoint per gli ID dei nodi memorizzati in cache. `10`, ad esempio, indica che la cache verrà sottoposta a checkpoint ogni 10 iterazioni. | 10 | (>=1) |
| `IMPURITY` | Il criterio utilizzato per il calcolo dell’acquisizione di informazioni (senza distinzione tra maiuscole e minuscole). | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | Profondità massima dell&#39;albero (non negativa). Ad esempio, profondità `0` significa 1 nodo foglia e profondità `1` significa 1 nodo interno e 2 nodi foglia. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Il guadagno minimo di informazioni necessario affinché una suddivisione possa essere considerata in un nodo della struttura. | 0,0 | (>=0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Frazione minima del numero di campioni ponderati che ogni bambino deve avere dopo una divisione. Se una suddivisione fa sì che la frazione del peso totale in uno dei figli sia inferiore a questo valore, viene eliminata. | 0,0 | (>=0,0; 0,5) |
| `MIN_INSTANCES_PER_NODE` | Il numero minimo di istanze che ogni figlio deve avere dopo una suddivisione. Se una suddivisione genera un numero di istanze inferiore a questo valore, la suddivisione viene eliminata. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Memoria massima, in MB, allocata all&#39;aggregazione dell&#39;istogramma. Se la memoria è troppo piccola, viene diviso solo 1 nodo per iterazione, il che può causare il superamento delle dimensioni degli aggregati. | 256 |                                                                                                        |
| `PREDICTION_COL` | Il parametro per il nome della colonna di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `SEED` | Il parametro per il valore di inizializzazione casuale. | N/D | Qualsiasi numero a 64 bit |
| `WEIGHT_COL` | Parametro per il nome della colonna di rilevanza. Se non è impostato o è vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | non impostato |                                                                                                        |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressione di [!DNL Factorization Machines] {#factorization-machines-regression}

[!DNL Factorization Machines] è un algoritmo di apprendimento della regressione che supporta la normale discesa con gradiente e il risolutore AdamW. L&#39;algoritmo si basa sul documento di S. Rendle (2010), &quot;[!DNL Factorization Machines]&quot;.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni della regressione di [!DNL Factorization Machines].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|------------------------|--------------------------------------------------------------------------------------|---------------|----------------|
| `TOL` | La tolleranza di convergenza. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | La dimensionalità dei fattori. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Se adattare un termine di intercettazione. | `true` | `true`, `false` |
| `FIT_LINEAR` | Se adattarsi al termine lineare (noto anche come termine a una via). | `true` | `true`, `false` |
| `INIT_STD` | Deviazione standard dei coefficienti iniziali. | 0,01 | (>= 0) |
| `MAX_ITER` | Il numero di iterazioni che l’algoritmo deve eseguire. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Frazione mini-batch, che deve essere compresa nell&#39;intervallo `(0, 1]`. | 1,0 | `(0, 1]` |
| `REG_PARAM` | Il parametro di regolarizzazione. | 0,0 | (>= 0) |
| `SEED` | Il seme casuale. | NON IMPOSTATO | Qualsiasi numero a 64 bit |
| `SOLVER` | L’algoritmo del risolutore utilizzato per l’ottimizzazione. | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | Dimensione del passaggio iniziale per il primo passaggio (simile al tasso di apprendimento). | 1,0 |                   |
| `PREDICTION_COL` | Nome della colonna di previsione. | &quot;previsione&quot; | Qualsiasi stringa |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressione di [!DNL Generalized Linear] {#generalized-linear-regression}

A differenza della regressione lineare, che presuppone che il risultato segua una distribuzione normale (gaussiana), i modelli [!DNL Generalized Linear] (GLM) consentono al risultato di seguire diversi tipi di distribuzioni, come [!DNL Poisson] o binomiale, a seconda della natura dei dati.

**Parametri**

La tabella seguente descrive i parametri chiave per configurare e ottimizzare le prestazioni della regressione di [!DNL Generalized Linear].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | Imposta il numero massimo di iterazioni (applicabile quando si utilizza il risolutore `irls`). | 25 | (>= 0) |
| `REG_PARAM` | Il parametro di regolarizzazione. | NON IMPOSTATO | (>= 0) |
| `TOL` | La tolleranza di convergenza. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Profondità suggerita per `treeAggregate`. | 2 | (>= 2) |
| `FAMILY` | Parametro family che descrive la distribuzione degli errori utilizzata nel modello. Le opzioni supportate sono `gaussian`, `binomial`, `poisson`, `gamma` e `tweedie`. | &quot;gaussian&quot; | `gaussian`, `binomial`, `poisson`, `gamma`, `tweedie` |
| `FIT_INTERCEPT` | Se adattare un termine di intercettazione. | `true` | `true`, `false` |
| `LINK` | La funzione di collegamento, che definisce la relazione tra il predittore lineare e la media della funzione di distribuzione. Le opzioni supportate sono `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog` e `sqrt`. | NON IMPOSTATO | `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog`, `sqrt` |
| `LINK_POWER` | L&#39;indice nella funzione di collegamento di alimentazione, applicabile alla famiglia [!DNL Tweedie]. Se non viene impostato, il valore predefinito è `1 - variancePower`, seguendo il pacchetto R `statmod`. Le potenze di collegamento di 0, 1, -1 e 0,5 corrispondono rispettivamente ai collegamenti Log, Identity, Inverse e Sqrt. | 1 |
| `SOLVER` | L’algoritmo del risolutore utilizzato per l’ottimizzazione. Opzione supportata: `irls` (riponderazione iterativa dei minimi quadrati). | &quot;irls&quot; | `irls` |
| `VARIANCE_POWER` | La potenza della funzione di varianza della distribuzione [!DNL Tweedie], che definisce la relazione tra varianza e media. I valori supportati sono 0 e `[1, inf)`. | 0,0 | 0, `[1, inf)` |
| `LINK_PREDICTION_COL` | Nome della colonna di previsione del collegamento (predicatore lineare). | NON IMPOSTATO | Qualsiasi stringa |
| `OFFSET_COL` | Nome della colonna di offset. Se non è impostato, tutti gli offset di istanza vengono trattati come 0,0. La feature di offset ha un coefficiente costante di 1,0. | NON IMPOSTATO |                                                                        |
| `WEIGHT_COL` | Nome della colonna di rilevanza. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. Nella famiglia Binomial, i pesi corrispondono al numero di prove e i pesi non interi sono arrotondati nel calcolo dell’AIC. | NON IMPOSTATO |                                                                        |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressione di [!DNL Gradient Boosted Tree] {#gradient-boosted-tree-regression}

Gli alberi potenziati dal gradiente (Gradient Boosted Tree, GBT) sono un metodo efficace per la classificazione e la regressione che combina le previsioni di più alberi decisionali per migliorare l&#39;accuratezza predittiva e le prestazioni del modello.

**Parametri**

La tabella seguente descrive i parametri chiave per configurare e ottimizzare le prestazioni della regressione di [!DNL Gradient Boosted Tree].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Il numero massimo di raccoglitori utilizzati per dividere le feature continue in intervalli discreti, che consente di determinare il modo in cui le feature vengono divise in ciascun nodo dell&#39;albero decisionale. Più contenitori forniscono maggiore granularità. | 32 | Deve essere almeno 2 e uguale o maggiore del numero di categorie in qualsiasi caratteristica categoriale. |
| `CACHE_NODE_IDS` | Se `false`, l&#39;algoritmo passa gli alberi agli esecutori per far corrispondere le istanze con i nodi. Se `true`, l&#39;algoritmo memorizza nella cache gli ID nodo per ogni istanza. La memorizzazione nella cache può accelerare l&#39;apprendimento degli alberi più profondi. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Specifica la frequenza di checkpoint per gli ID dei nodi memorizzati in cache. Ad esempio, `10` significa che la cache viene sottoposta a checkpoint ogni 10 iterazioni. | 10 | (>= 1) |
| `MAX_DEPTH` | Profondità massima dell&#39;albero (non negativa). Ad esempio, profondità `0` significa 1 nodo foglia e profondità `1` significa 1 nodo interno con 2 nodi foglia. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Il guadagno minimo di informazioni necessario affinché una suddivisione possa essere considerata in un nodo della struttura. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Frazione minima del numero di campioni ponderati che ogni bambino deve avere dopo una divisione. Se una suddivisione fa sì che la frazione del peso totale in uno dei figli sia inferiore a questo valore, viene eliminata. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Il numero minimo di istanze che ogni figlio deve avere dopo una suddivisione. Se una suddivisione genera un numero di istanze inferiore a questo valore, la suddivisione viene eliminata. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria massima, in MB, allocata all&#39;aggregazione dell&#39;istogramma. Se questo valore è troppo piccolo, viene diviso solo 1 nodo per iterazione e i relativi aggregati possono superare queste dimensioni. | 256 |                                                                                                      |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `VALIDATION_INDICATOR_COL` | Il nome della colonna che indica se ogni riga è utilizzata per l’apprendimento o la convalida. `false` per la formazione e `true` per la convalida. | NON IMPOSTATO | Qualsiasi stringa |
| `LEAF_COL` | Nome della colonna per gli indici foglia. L&#39;indice foglia previsto di ogni istanza in ogni albero, generato dall&#39;attraversamento del preordine. | &quot;&quot; | Qualsiasi stringa |
| `FEATURE_SUBSET_STRATEGY` | Il numero di feature considerate per la suddivisione in ciascun nodo della struttura. | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` (dove `n` è una frazione compresa tra 0 e 1,0) |
| `SEED` | Il seme casuale. | NON IMPOSTATO | Qualsiasi numero a 64 bit |
| `WEIGHT_COL` | Il nome della colonna, ad esempio pesi. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | NON IMPOSTATO |                                                                                                      |
| `LOSS_TYPE` | Funzione di perdita che il modello [!DNL Gradient Boosted Tree] tenta di ridurre a icona. | &quot;al quadrato&quot; | `squared` (L2) e `absolute` (L1). Nota: i valori non fanno distinzione tra maiuscole e minuscole. |
| `STEP_SIZE` | Dimensione del passaggio (nota anche come tasso di apprendimento) nell&#39;intervallo `(0, 1]`, utilizzata per ridurre il contributo di ogni stimatore. | 0,1 | `(0, 1]` |
| `MAX_ITER` | Il numero massimo di iterazioni per l’algoritmo. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Frazione dei dati di formazione utilizzati per apprendere ogni albero decisionale, nell&#39;intervallo `(0, 1]`. | 1,0 | `(0, 1]` |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressione di [!DNL Isotonic] {#isotonic-regression}

[!DNL Isotonic Regression] è un algoritmo utilizzato per regolare iterativamente le distanze mantenendo l&#39;ordine relativo delle differenze nei dati.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni di [!DNL Isotonic Regression].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | Specifica se la sequenza di output deve essere isotonica (crescente) quando `true` o antitonica (decrescente) quando `false`. | `true` | `true`, `false` |
| `WEIGHT_COL` | Il nome della colonna, ad esempio pesi. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | NON IMPOSTATO | Qualsiasi stringa |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `FEATURE_INDEX` | L&#39;indice della funzionalità, applicabile quando `featuresCol` è una colonna vettoriale. Se non viene impostato, il valore predefinito è `0`. In caso contrario, non ha alcun effetto. | 0 |                 |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Regressione di [!DNL Linear] {#linear-regression}

[!DNL Linear Regression] è un algoritmo di machine learning supervisionato che inserisce un&#39;equazione lineare ai dati per modellare la relazione tra una variabile dipendente e funzionalità indipendenti.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni di [!DNL Linear Regression].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Numero massimo di iterazioni. | 100 | (>= 0) |
| `REGPARAM` | Parametro di regolarizzazione utilizzato per controllare la complessità del modello. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Il parametro di mixaggio ElasticNet, che controlla l&#39;equilibrio tra penalità L1 (Lazo) e L2 (Ridge). Un valore pari a 0 applica una penalità L2, mentre un valore pari a 1 applica una penalità L1. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression] è un algoritmo di insieme che crea più alberi decisionali durante l&#39;addestramento e restituisce la previsione media di tali alberi per le attività di regressione, contribuendo a evitare l&#39;adattamento eccessivo.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni di [!DNL Random Forest Regression].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Il numero massimo di raccoglitori utilizzati per determinare le feature continue e il modo in cui vengono suddivise in ciascun nodo. Più contenitori forniscono maggiore granularità. | 32 | Deve essere almeno pari a 2 e almeno uguale al numero di categorie in qualsiasi funzione categoriale. |
| `CACHE_NODE_IDS` | Se `false`, l&#39;algoritmo passa gli alberi agli esecutori per far corrispondere le istanze con i nodi. Se `true`, l&#39;algoritmo memorizza nella cache gli ID dei nodi per ogni istanza, velocizzando l&#39;addestramento di strutture più profonde. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Specifica la frequenza di checkpoint per gli ID dei nodi memorizzati in cache. Ad esempio, `10` significa che la cache viene sottoposta a checkpoint ogni 10 iterazioni. | 10 | (>= 1) |
| `IMPURITY` | Il criterio utilizzato per il calcolo dell’acquisizione di informazioni (senza distinzione tra maiuscole e minuscole). | entropia | `entropy`, `gini` |
| `MAX_DEPTH` | Profondità massima dell&#39;albero (non negativa). Ad esempio, profondità `0` significa 1 nodo foglia e profondità `1` significa 1 nodo interno e 2 nodi foglia. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Il guadagno minimo di informazioni necessario affinché una suddivisione possa essere considerata in un nodo della struttura. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Frazione minima del numero di campioni ponderati che ogni bambino deve avere dopo una divisione. Se una suddivisione fa sì che la frazione del peso totale in uno dei figli sia inferiore a questo valore, viene eliminata. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Il numero minimo di istanze che ogni figlio deve avere dopo una suddivisione. Se una suddivisione genera un numero di istanze inferiore a questo valore, la suddivisione viene eliminata. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Memoria massima, in MB, allocata all&#39;aggregazione dell&#39;istogramma. Se questo valore è troppo piccolo, viene diviso solo 1 nodo per iterazione e i relativi aggregati possono superare queste dimensioni. | 256 |                                                                                                      |
| `BOOTSTRAP` | Se utilizzare i campioni di bootstrap durante la creazione di alberi. | TRUE | `true`, `false` |
| `NUM_TREES` | Numero di alberi da addestrare (almeno 1). Se `1`, non viene utilizzato alcun bootstrapping. Se maggiore di `1`, viene applicato il bootstrapping. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Frazione di dati di addestramento utilizzata per addestrare ogni albero decisionale, nell&#39;intervallo `(0, 1]`. | 1,0 | `(0, 1]` |
| `LEAF_COL` | Il nome della colonna per gli indici foglia, che è l&#39;indice foglia previsto di ogni istanza in ogni albero, generato dall&#39;attraversamento del preordine. | &quot;&quot; | Qualsiasi stringa |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `SEED` | Il seme casuale. | NON IMPOSTATO | Qualsiasi numero a 64 bit |
| `WEIGHT_COL` | Il nome della colonna, ad esempio pesi. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | NON IMPOSTATO | Qualsiasi nome di colonna valido o lascia vuoto. |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression] viene utilizzato per adattarsi a un modello di regressione di sopravvivenza parametrica, noto come modello [!DNL Accelerated Failure Time] (AFT), basato su [!DNL Weibull distribution]. Può impilare le istanze in blocchi per migliorare le prestazioni.

**Parametri**

La tabella seguente illustra i parametri chiave per la configurazione e l&#39;ottimizzazione delle prestazioni di [!DNL Survival Regression].

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Il numero massimo di iterazioni che l’algoritmo deve eseguire. | 100 | (>= 0) |
| `TOL` | La tolleranza di convergenza. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Profondità suggerita per `treeAggregate`. Se le quote della feature o il numero di partizioni sono elevati, questo parametro può essere impostato su un valore maggiore. | 2 | (>= 2) |
| `FIT_INTERCEPT` | Se adattare un termine di intercettazione. | TRUE | `true`, `false` |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |
| `CENSOR_COL` | Nome della colonna per la censura. Un valore di `1` indica che l&#39;evento si è verificato (non censurato), mentre `0` indica che l&#39;evento è censurato. | &quot;censore&quot; | 0, 1 |
| `MAX_BLOCK_SIZE_IN_MB` | Memoria massima in MB per lo stacking dei dati di input in blocchi. Se la dimensione dei dati rimanenti in una partizione è inferiore, questo valore viene regolato di conseguenza. Il valore `0` consente la regolazione automatica. | 0,0 | (>= 0) |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Passaggi successivi

Dopo aver letto questo documento, ora sai come configurare e utilizzare vari algoritmi di regressione. Quindi, consulta i documenti su [classificazione](./classification.md) e [clustering](./clustering.md) per ulteriori informazioni su altri tipi di modelli statistici avanzati.
