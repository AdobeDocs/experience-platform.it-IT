---
title: Algoritmi di clustering
description: Scopri come configurare e ottimizzare vari algoritmi di clustering con parametri chiave, descrizioni e codice di esempio per implementare modelli statistici avanzati.
role: Developer
exl-id: 273853c6-85d2-43e5-b51a-aa9d20b313ae
source-git-commit: 69c08f688d355e689e78426dd4b0ed1f4934965c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 4%

---

# Algoritmi di clustering {#clustering-algorithms}

Gli algoritmi di clustering raggruppano i punti dati in cluster distinti in base alle loro somiglianze, consentendo all’apprendimento non supervisionato di individuare pattern all’interno dei dati. Per creare un algoritmo di clustering, utilizzare il parametro `type` nella clausola `OPTIONS` per specificare l&#39;algoritmo da utilizzare per l&#39;apprendimento del modello. Quindi, definisci i parametri rilevanti come coppie chiave-valore per ottimizzare il modello.

>[!NOTE]
>
>Assicurati di conoscere i requisiti dei parametri per l’algoritmo scelto. Se si sceglie di non personalizzare determinati parametri, il sistema applica le impostazioni predefinite. Consulta la documentazione pertinente per comprendere la funzione di ciascun parametro e i valori predefiniti.

## [!DNL K-Means] {#kmeans}

`K-Means` è un algoritmo di clustering che suddivide i dati in un numero predefinito di cluster (k). È uno degli algoritmi più comunemente utilizzati per il clustering per la sua semplicità ed efficienza.

**Parametri**

Quando si utilizza `K-Means`, è possibile impostare i seguenti parametri nella clausola `OPTIONS`:

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITER` | Il numero di iterazioni che l’algoritmo deve eseguire. | `20` | (>= 0) |
| `TOL` | Livello di tolleranza della convergenza. | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | Numero di cluster da creare (`k`). | `2` | (>1) |
| `DISTANCE_TYPE` | Algoritmo utilizzato per calcolare la distanza tra due punti. Il valore distingue tra maiuscole e minuscole. | `euclidean` | `euclidean`, `cosine` |
| `KMEANS_INIT_METHOD` | Algoritmo di inizializzazione per i centri cluster. | `k-means\|\|` | `random`, `k-means\|\|` (versione parallela di k-mean++) |
| `INIT_STEPS` | Numero di passaggi per la modalità di inizializzazione `k-means\|\|` (applicabile solo quando `KMEANS_INIT_METHOD` è `k-means\|\|`). | `2` | (>0) |
| `PREDICTION_COL` | Nome della colonna in cui verranno memorizzate le previsioni. | `prediction` | Qualsiasi stringa |
| `SEED` | Un seme casuale per la riproducibilità. | `-1689246527` | Qualsiasi numero a 64 bit |
| `WEIGHT_COL` | Nome della colonna utilizzata per i pesi dell’istanza. Se non viene impostato, tutte le varianti vengono ponderate in modo uniforme. | `not set` | N/D |

{style="table-layout:auto"}

**Esempio**

```sql
CREATE MODEL modelname 
OPTIONS(
  type = 'kmeans',
  MAX_ITERATIONS = 30,
  NUM_CLUSTERS = 4
) 
AS SELECT col1, col2, col3 FROM training-dataset;
```

## [!DNL Bisecting K-means] {#bisecting-kmeans}

[!DNL Bisecting K-means] è un algoritmo di clustering gerarchico che utilizza un approccio divisivo (o top-down). Tutte le osservazioni iniziano in un singolo cluster e le divisioni vengono eseguite in modo ricorsivo durante la creazione della gerarchia. [!DNL Bisecting K-means] può essere spesso più veloce delle normali medie K, ma in genere produce risultati cluster diversi.

**Parametri**

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | Numero massimo di iterazioni eseguite dall&#39;algoritmo. | 20 | (>= 0) |
| `WEIGHT_COL` | Nome della colonna per i pesi dell’istanza. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | NON IMPOSTATO | Qualsiasi stringa |
| `NUM_CLUSTERS` | Il numero desiderato di cluster foglia. Se non rimangono cluster divisibili, il numero effettivo potrebbe essere inferiore. | 4 | (> 1) |
| `SEED` | Valore di inizializzazione casuale utilizzato per controllare i processi casuali nell&#39;algoritmo. | NON IMPOSTATO | Qualsiasi numero a 64 bit |
| `DISTANCE_MEASURE` | La misura della distanza utilizzata per calcolare la somiglianza tra i punti. | &quot;euclideo&quot; | `euclidean`, `cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | Il numero minimo di punti (se >= 1,0) o la proporzione minima di punti (se &lt; 1,0) necessaria per la divisibile di un cluster. | 1,0 | (>= 0) |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |

{style="table-layout:auto"}

**Esempio**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model] rappresenta una distribuzione composita in cui i punti dati vengono ricavati da una delle sottodistribuzioni di k Gaussian, ciascuna con la propria probabilità. Viene utilizzato per modellare set di dati che si presume siano generati da una miscela di diverse distribuzioni gaussiane.

**Parametri**

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Il numero massimo di iterazioni per l’algoritmo da eseguire. | 100 | (>= 0) |
| `WEIGHT_COL` | Il nome della colonna, ad esempio pesi. Se non è impostato o vuoto, tutti i pesi delle istanze vengono trattati come `1.0`. | NON IMPOSTATO | Qualsiasi nome di colonna valido o vuoto |
| `NUM_CLUSTERS` | Il numero di distribuzioni gaussiane indipendenti nel modello di miscela. | 2 | (> 1) |
| `SEED` | Valore di inizializzazione casuale utilizzato per controllare i processi casuali nell&#39;algoritmo. | NON IMPOSTATO | Qualsiasi numero a 64 bit |
| `AGGREGATION_DEPTH` | Questo parametro controlla la profondità degli alberi di aggregazione utilizzati durante il calcolo. | 2 | (>= 1) |
| `PROBABILITY_COL` | Nome di colonna per le probabilità condizionali di classe previste. Questi devono essere trattati come punteggi di affidabilità piuttosto che come probabilità esatte. | &quot;probabilità&quot; | Qualsiasi stringa |
| `TOL` | La tolleranza di convergenza per gli algoritmi iterativi. | 0,01 | (>= 0) |
| `PREDICTION_COL` | Nome della colonna per l’output di previsione. | &quot;previsione&quot; | Qualsiasi stringa |

{style="table-layout:auto"}

**Esempio**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA) è un modello probabilistico che acquisisce la struttura argomento sottostante da una raccolta di documenti. Si tratta di un modello bayesiano gerarchico a tre livelli con livelli di parola, argomento e documento. LDA utilizza questi livelli, insieme ai documenti osservati, per creare una struttura di argomenti latente.

**Parametri**

| Parametro | Descrizione | Valore predefinito | Valori possibili |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Numero massimo di iterazioni eseguite dall&#39;algoritmo. | 20 | (>= 0) |
| `OPTIMIZER` | Algoritmo di ottimizzazione o di inferenza utilizzato per stimare il modello LDA. Le opzioni supportate sono `"online"` (Online Variational Bayes) e `"em"` (Expectation-Maximization). | &quot;online&quot; | `online`, `em` (senza distinzione maiuscole/minuscole) |
| `NUM_CLUSTERS` | Numero di cluster da creare (k). | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | Specifica la frequenza di checkpoint per gli ID dei nodi memorizzati in cache. | 10 | (>= 1) |
| `DOC_CONCENTRATION` | Il parametro di concentrazione (&quot;alpha&quot;) determina le ipotesi precedenti relative alla distribuzione degli argomenti tra i documenti. Il comportamento predefinito è determinato dall&#39;ottimizzatore. Per l&#39;ottimizzatore `EM`, i valori alfa devono essere maggiori di 1,0 (impostazione predefinita: distribuiti uniformemente come (50/k) + 1), garantendo distribuzioni dell&#39;argomento simmetriche. Per l&#39;ottimizzatore `online`, i valori alfa possono essere uguali o superiori a 0 (impostazione predefinita: distribuiti uniformemente come 1,0/k), consentendo un&#39;inizializzazione più flessibile degli argomenti. | Automatico | Qualsiasi singolo valore o vettore di lunghezza k dove valori > 1 per EM |
| `KEEP_LAST_CHECKPOINT` | Indica se mantenere l&#39;ultimo punto di controllo quando si utilizza l&#39;ottimizzatore `em`. L’eliminazione del punto di controllo può causare errori in caso di perdita di una partizione di dati. I punti di controllo vengono rimossi automaticamente dall&#39;archivio quando non sono più necessari, come determinato dal conteggio dei riferimenti. | `true` | `true`, `false` |
| `LEARNING_DECAY` | Tasso di apprendimento per l&#39;ottimizzatore `online`, impostato come tasso di decadimento esponenziale tra `(0.5, 1.0]`. | 0,51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | Parametro di apprendimento per l&#39;ottimizzatore `online` che sottopone a downweight le iterazioni iniziali per ridurre il conteggio delle iterazioni iniziali. | 1024 | (> 0) |
| `SEED` | Valore di inizializzazione casuale per il controllo dei processi casuali nell’algoritmo. | NON IMPOSTATO | Qualsiasi numero a 64 bit |
| `OPTIMIZE_DOC_CONCENTRATION` | Per l&#39;ottimizzatore `online`: se ottimizzare `docConcentration` (parametro Dirichlet per la distribuzione di argomenti dei documenti) durante l&#39;apprendimento. | `false` | `true`, `false` |
| `SUBSAMPLING_RATE` | Per l&#39;ottimizzatore `online`: la frazione del corpo campionata e utilizzata in ogni iterazione di discendenza sfumata mini-batch, nell&#39;intervallo `(0, 1]`. | 0,05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | Il parametro di concentrazione (&quot;beta&quot; o &quot;eta&quot;) definisce le ipotesi precedenti poste sulla distribuzione degli argomenti nei termini. Il valore predefinito è determinato dall&#39;ottimizzatore: Per `EM`, valori > 1,0 (valore predefinito = 0,1 + 1). Per `online`, i valori ≥ 0 (valore predefinito = 1,0/k). | Automatico | Qualsiasi valore singolo o vettore di lunghezza k, dove valori > 1 per EM |
| `TOPIC_DISTRIBUTION_COL` | Questo parametro produce la distribuzione stimata della miscela di argomenti per ciascun documento, spesso indicata come &quot;theta&quot; in letteratura. Per i documenti vuoti, restituisce un vettore di zeri. Le stime sono derivate utilizzando un&#39;approssimazione variazionale (&quot;gamma&quot;). | NON IMPOSTATO | Qualsiasi stringa |

{style="table-layout:auto"}

**Esempio**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## Passaggi successivi

Dopo aver letto questo documento, saprai come configurare e utilizzare vari algoritmi di clustering. Quindi, consulta i documenti su [classificazione](./classification.md) e [regressione](./regression.md) per ulteriori informazioni su altri tipi di modelli statistici avanzati.
