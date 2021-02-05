---
keywords: ' Experience Platform;JupyterLab;blocchi appunti;Data Science Workspace;argomenti più comuni;%dataset;modalità interattiva;modalità batch;Spark sdk;python sdk;accesso ai dati;notebook data access'
solution: Experience Platform
title: Accesso ai dati nei notebook Jupyterlab
topic: Developer Guide
description: Questa guida è incentrata su come utilizzare i notebook Jupyter, creati all'interno di Data Science Workspace per accedere ai dati.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 9%

---


# Accesso ai dati nei notebook [!DNL Jupyterlab]

Ogni kernel supportato fornisce funzionalità integrate che consentono di leggere i dati della piattaforma da un dataset all&#39;interno di un blocco appunti. Attualmente JupyterLab in Adobe Experience Platform Data Science Workspace supporta i notebook per [!DNL Python], R, PySpark e Scala. Tuttavia, il supporto per l&#39;impaginazione dei dati è limitato ai notebook [!DNL Python] e R. Questa guida è incentrata su come utilizzare i notebook JupyterLab per accedere ai dati.

## Introduzione

Prima di leggere questa guida, consultare la [[!DNL JupyterLab] guida utente](./overview.md) per un&#39;introduzione di alto livello a [!DNL JupyterLab] e il relativo ruolo all&#39;interno di Data Science Workspace.

## Limiti dei dati del notebook {#notebook-data-limits}

>[!IMPORTANT]
>
>Per i notebook PySpark e Scala se viene visualizzato un errore con il motivo &quot;Client RPC remoto non associato&quot;. In genere significa che il driver o l&#39;esecutore non dispongono di memoria sufficiente. Per risolvere l&#39;errore, provare a passare alla modalità [&quot;batch&quot;](#mode).

Le informazioni seguenti definiscono la quantità massima di dati leggibili, il tipo di dati utilizzato e il periodo di tempo stimato necessario per la lettura dei dati.

Per [!DNL Python] e R, per i benchmark è stato utilizzato un server notebook configurato a 40 GB di RAM. Per PySpark e Scala, un cluster di database configurato a 64 GB di RAM, 8 core, 2 DBU con un massimo di 4 dipendenti è stato utilizzato per i benchmark indicati di seguito.

I dati dello schema ExperienceEvent utilizzati variavano nelle dimensioni a partire da mille (1K) righe fino a un miliardo di righe (1B). Per le metriche PySpark e [!DNL Spark] è stato utilizzato un intervallo di date di 10 giorni per i dati XDM.

I dati dello schema ad hoc sono stati pre-elaborati utilizzando [!DNL Query Service] Crea tabella come Seleziona (CTAS). Questi dati sono anche variati in dimensioni a partire da mille (1K) righe che vanno fino a un miliardo (1B) righe.

### Quando utilizzare la modalità batch e la modalità interattiva {#mode}

Quando si leggono i set di dati con i notebook PySpark e Scala, è possibile utilizzare la modalità interattiva o la modalità batch per leggere il set di dati. Interattivo è fatto per risultati veloci, mentre la modalità batch è per set di dati di grandi dimensioni.

- Per i notebook PySpark e Scala, la modalità batch deve essere utilizzata per la lettura di almeno 5 milioni di righe di dati. Per ulteriori informazioni sull&#39;efficienza di ciascuna modalità, vedere le tabelle dei limiti di dati [PySpark](#pyspark-data-limits) o [Scala](#scala-data-limits) riportate di seguito.

### [!DNL Python] limiti dei dati del notebook

**Schema ExperienceEvent XDM:** è necessario essere in grado di leggere un massimo di 2 milioni di righe (circa 6,1 GB di dati su disco) di dati XDM in meno di 22 minuti. L&#39;aggiunta di righe aggiuntive potrebbe causare errori.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Dimensioni su disco (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (in secondi) | 20,3 | 86,8 | 63 | 659 | 1315 |

**schema ad hoc:** dovreste essere in grado di leggere un massimo di 5 milioni di righe (circa 5,6 GB di dati su disco) di dati non XDM (ad hoc) in meno di 14 minuti. L&#39;aggiunta di righe aggiuntive potrebbe causare errori.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Dimensioni su disco (in MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in secondi) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### Limiti dei dati del notebook R

**schema XDM ExperienceEvent:** dovresti essere in grado di leggere un massimo di 1 milione di righe di dati XDM (3 GB di dati su disco) in meno di 13 minuti.

| Numero di righe | 1K | 10.000 | 100.000 | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Dimensioni su disco (MB) | 18,73 | 187,5 | 308 | 3000 |
| R Kernel (in secondi) | 14,03 | 69,6 | 86,8 | 775 |

**schema ad hoc:** dovreste essere in grado di leggere un massimo di 3 milioni di righe di dati ad hoc (293 MB di dati su disco) in circa 10 minuti.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Dimensioni su disco (in MB) | 0,082 | 0,612 | 9,0 | 91 | 188 | 293 |
| SDK R (in sec) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### Limiti dei dati del notebook PySpark ([!DNL Python] kernel): {#pyspark-data-limits}

**Schema ExperienceEvent XDM:** in modalità interattiva è possibile leggere fino a 5 milioni di righe (circa 5 milioni di dati da 13,42 GB su disco) di dati XDM in circa 20 minuti. La modalità interattiva supporta solo fino a 5 milioni di righe. Se si desidera leggere set di dati più grandi, è consigliabile passare alla modalità batch. In modalità batch è necessario essere in grado di leggere un massimo di 500 milioni di righe (circa 1,31 TB di dati su disco) di dati XDM in circa 14 ore.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M | 10 M | 50 M | 100 M | 500 M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Dimensioni su disco | 2,93 MB | 4,38 MB | 29,02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1,31 TB |
| SDK (modalità interattiva) | 33 sec | 32,4 s | 55,1 s | 253,5 s | 489,2 s | 729,6 s | 1206,8 s | - | - | - | - |
| SDK (modalità batch) | 815,8 sec | 492,8 s | 379,1 s | 637,4 s | 624,5 s | 869,2 s | 1104,1 s | 1786 s | 5387,2 s | 10624,6s | 50547 s |

**schema ad hoc:** in modalità interattiva è possibile leggere un massimo di 5 milioni di righe (circa 5,36 GB di dati su disco) di dati non XDM in meno di 3 minuti. In modalità Batch dovreste essere in grado di leggere un massimo di 1 miliardo di righe (circa 1,05 TB di dati su disco) di dati non XDM in circa 18 minuti.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M | 10 M | 50 M | 100 M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Dimensioni su disco | 1,12 MB | 11,24 MB | 109,48 MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1,05 TB |
| Modalità interattiva SDK (in secondi) | 28,2 s | 18,6 sec | 20,8 sec | 20,9 s | 23,8 sec | 21,7 sec | 24,7 sec | - | - | - | - | - |
| Modalità batch SDK (in secondi) | 428,8 sec | 578,8 sec | 641,4 s | 538,5 s | 630,9 s | 467,3 s | 411 s | 675 s | 702 s | 719,2 s | 1022,1 s | 1122,3 s |

### [!DNL Spark] Limiti dei dati del notebook (kernel Scala):  {#scala-data-limits}

**Schema ExperienceEvent XDM:** in modalità interattiva è possibile leggere fino a 5 milioni di righe (circa 13,42 GB di dati su disco) di dati XDM in circa 18 minuti. La modalità interattiva supporta solo fino a 5 milioni di righe. Se si desidera leggere set di dati più grandi, è consigliabile passare alla modalità batch. In modalità batch è necessario essere in grado di leggere un massimo di 500 milioni di righe (circa 1,31 TB di dati su disco) di dati XDM in circa 14 ore.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M | 10 M | 50 M | 100 M | 500 M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Dimensioni su disco | 2,93 MB | 4,38 MB | 29,02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1,31 TB |
| Modalità interattiva SDK (in secondi) | 37,9 s | 22,7 sec | 45,6 s | 231,7 sec | 444,7 s | 660,6 s | 1100 sec. | - | - | - | - |
| Modalità batch SDK (in secondi) | 374,4 s | 398,5 s | 527 s | 487,9 s | 588,9 s | 829 s | 939,1 s | 1441 s | 5473,2 s | 10118,8 | 49207,6 |

**schema ad hoc:** in modalità interattiva è possibile leggere un massimo di 5 milioni di righe (circa 5,36 GB di dati su disco) di dati non XDM in meno di 3 minuti. In modalità batch è necessario essere in grado di leggere un massimo di 1 miliardo di righe (circa 1,05 TB di dati su disco) di dati non XDM in circa 16 minuti.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M | 10 M | 50 M | 100 M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Dimensioni su disco | 1,12 MB | 11,24 MB | 109,48 MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1,05 TB |
| Modalità interattiva SDK (in secondi) | 35,7 sec | 31 s | 19,5 s | 25,3 s | 23 sec | 33,2 s | 25,5 sec | - | - | - | - | - |
| Modalità batch SDK (in secondi) | 448,8 s | 459,7 s | 519 s | 475,8 sec | 599,9 s | 347,6 s | 407,8 s | 397 s | 518,8 sec | 487,9 s | 760,2 s | 975,4 s |

## Notebook Python {#python-notebook}

[!DNL Python] i notebook consentono di impaginare i dati quando si accede ai set di dati. Di seguito è illustrato il codice di esempio per leggere i dati con e senza impaginazione. Per ulteriori informazioni sui notebook Python di avvio disponibili, visitare la sezione [[!DNL JupyterLab] Launcher](./overview.md#launcher) nella guida utente di JupyterLab.

La documentazione Python riportata di seguito illustra i seguenti concetti:

- [Lettura da un set di dati](#python-read-dataset)
- [Scrivere in un dataset](#write-python)
- [Dati query](#query-data-python)
- [Filtrare i dati ExperienceEvent](#python-filter)

### Leggi da un set di dati in Python {#python-read-dataset}

**Senza impaginazione:**

L&#39;esecuzione del codice seguente consente di leggere l&#39;intero set di dati. Se l&#39;esecuzione ha esito positivo, i dati verranno salvati come fotogramma dati Pandas a cui fa riferimento la variabile `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Con impaginazione:**

L&#39;esecuzione del codice seguente consente di leggere i dati dal set di dati specificato. La paginazione si ottiene limitando e compensando i dati attraverso le funzioni `limit()` e `offset()` rispettivamente. I dati limitati si riferiscono al numero massimo di punti dati da leggere, mentre l&#39;offset fa riferimento al numero di punti dati da ignorare prima della lettura dei dati. Se l&#39;operazione di lettura viene eseguita correttamente, i dati verranno salvati come fotogramma dati Pandas a cui fa riferimento la variabile `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Scrivere in un set di dati in Python {#write-python}

Per scrivere in un set di dati nel notebook JupyterLab, seleziona la scheda Icona dati (evidenziata di seguito) nella barra di navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]**. Selezionare **[!UICONTROL Datasets]** e fare clic con il pulsante destro del mouse, quindi selezionare l&#39;opzione **[!UICONTROL Write Data in Notebook]** dal menu a discesa del set di dati che si desidera utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.

![](../images/jupyterlab/data-access/write-dataset.png)

- Utilizzare **[!UICONTROL Write Data in Notebook]** per generare una cella di scrittura con il set di dati selezionato.
- Utilizzare **[!UICONTROL Explore Data in Notebook]** per generare una cella di lettura con il set di dati selezionato.
- Utilizzare **[!UICONTROL Query Data in Notebook]** per generare una cella di query di base con il set di dati selezionato.

In alternativa, è possibile copiare e incollare la seguente cella di codice. Sostituire sia il `{DATASET_ID}` che il `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Dati query che utilizzano [!DNL Query Service] in [!DNL Python] {#query-data-python}

[!DNL JupyterLab] on  [!DNL Platform] consente di utilizzare SQL in un  [!DNL Python] blocco appunti per accedere ai dati tramite  [Adobe Experience Platform Query Service](https://www.adobe.com/go/query-service-home-en). L&#39;accesso ai dati tramite [!DNL Query Service] può essere utile per gestire i set di dati di grandi dimensioni a causa dei suoi tempi di esecuzione superiori. Tenere presente che l&#39;esecuzione di query sui dati utilizzando [!DNL Query Service] ha un limite di tempo di elaborazione di dieci minuti.

Prima di utilizzare [!DNL Query Service] in [!DNL JupyterLab], verificare di disporre di una conoscenza approfondita della [[!DNL Query Service] sintassi SQL](https://www.adobe.com/go/query-service-sql-syntax-en).

Per eseguire la query dei dati utilizzando [!DNL Query Service] è necessario fornire il nome del set di dati di destinazione. È possibile generare le celle di codice necessarie individuando il set di dati desiderato utilizzando **[!UICONTROL Data explorer]**. Fare clic con il pulsante destro del mouse sull&#39;elenco dei set di dati e fare clic su **[!UICONTROL Query Data in Notebook]** per generare due celle di codice nel blocco appunti. Queste due celle sono descritte più dettagliatamente di seguito.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Per utilizzare [!DNL Query Service] in [!DNL JupyterLab], è innanzitutto necessario creare una connessione tra il notebook [!DNL Python] in uso e [!DNL Query Service]. Questo può essere ottenuto eseguendo la prima cella generata.

```python
qs_connect()
```

Nella seconda cella generata, la prima riga deve essere definita prima della query SQL. Per impostazione predefinita, la cella generata definisce una variabile opzionale (`df0`) che salva i risultati della query come fotogramma dati Pandas. <br>L&#39; `-c QS_CONNECTION` argomento è obbligatorio e indica al kernel di eseguire la query SQL con  [!DNL Query Service]. Per un elenco degli argomenti aggiuntivi, vedere l&#39; [appendice](#optional-sql-flags-for-query-service).

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Alle variabili Python è possibile fare riferimento direttamente all&#39;interno di una query SQL utilizzando la sintassi in formato stringa e racchiudendo le variabili tra parentesi graffe (`{}`), come illustrato nell&#39;esempio seguente:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrare i dati [!DNL ExperienceEvent] {#python-filter}

Per accedere e filtrare un dataset [!DNL ExperienceEvent] in un blocco appunti [!DNL Python], è necessario fornire l&#39;ID del dataset (`{DATASET_ID}`) insieme alle regole del filtro che definiscono un intervallo di tempo specifico utilizzando operatori logici. Quando viene definito un intervallo di tempo, qualsiasi impaginazione specificata viene ignorata e viene considerato l&#39;intero set di dati.

Di seguito è riportato un elenco di operatori di filtraggio:

- `eq()`: Uguale a
- `gt()`: Maggiore di
- `ge()`: Maggiore o uguale a
- `lt()`: Minore di
- `le()`: Minore o uguale a
- `And()`: Operatore logico AND
- `Or()`: Operatore OR logico

La cella seguente filtra un set di dati [!DNL ExperienceEvent] a dati esistenti esclusivamente tra il 1 gennaio 2019 e la fine del 31 dicembre 2019.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## Notebook R {#r-notebooks}

I notebook R consentono di impaginare i dati quando si accede ai set di dati. Di seguito è illustrato il codice di esempio per leggere i dati con e senza impaginazione. Per ulteriori informazioni sui notebook R disponibili, consultare la sezione [[!DNL JupyterLab] Launcher](./overview.md#launcher) nella guida utente di JupyterLab.

La documentazione R seguente delinea i seguenti concetti:

- [Lettura da un set di dati](#r-read-dataset)
- [Scrivere in un dataset](#write-r)
- [Filtrare i dati ExperienceEvent](#r-filter)

### Leggi da un set di dati in R {#r-read-dataset}

**Senza impaginazione:**

L&#39;esecuzione del codice seguente consente di leggere l&#39;intero set di dati. Se l&#39;esecuzione ha esito positivo, i dati verranno salvati come fotogramma dati Pandas a cui fa riferimento la variabile `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**Con impaginazione:**

L&#39;esecuzione del codice seguente consente di leggere i dati dal set di dati specificato. La paginazione si ottiene limitando e compensando i dati attraverso le funzioni `limit()` e `offset()` rispettivamente. I dati limitati si riferiscono al numero massimo di punti dati da leggere, mentre l&#39;offset fa riferimento al numero di punti dati da ignorare prima della lettura dei dati. Se l&#39;operazione di lettura viene eseguita correttamente, i dati verranno salvati come fotogramma dati Pandas a cui fa riferimento la variabile `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### Scrivere in un set di dati in R {#write-r}

Per scrivere in un set di dati nel notebook JupyterLab, seleziona la scheda Icona dati (evidenziata di seguito) nella barra di navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]**. Selezionare **[!UICONTROL Datasets]** e fare clic con il pulsante destro del mouse, quindi selezionare l&#39;opzione **[!UICONTROL Write Data in Notebook]** dal menu a discesa del set di dati che si desidera utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Utilizzare **[!UICONTROL Write Data in Notebook]** per generare una cella di scrittura con il set di dati selezionato.
- Utilizzare **[!UICONTROL Explore Data in Notebook]** per generare una cella di lettura con il set di dati selezionato.

In alternativa, potete copiare e incollare la seguente cella di codice:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtrare i dati [!DNL ExperienceEvent] {#r-filter}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti R, è necessario fornire l&#39;ID del set di dati (`{DATASET_ID}`) insieme alle regole del filtro che definiscono un intervallo di tempo specifico utilizzando operatori logici. Quando viene definito un intervallo di tempo, qualsiasi impaginazione specificata viene ignorata e viene considerato l&#39;intero set di dati.

Di seguito è riportato un elenco di operatori di filtraggio:

- `eq()`: Uguale a
- `gt()`: Maggiore di
- `ge()`: Maggiore o uguale a
- `lt()`: Minore di
- `le()`: Minore o uguale a
- `And()`: Operatore logico AND
- `Or()`: Operatore OR logico

La cella seguente filtra un set di dati [!DNL ExperienceEvent] a dati esistenti esclusivamente tra il 1 gennaio 2019 e la fine del 31 dicembre 2019.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## Notebook PySpark 3 {#pyspark-notebook}

La documentazione di PySpark riportata di seguito descrive i seguenti concetti:

- [Inizializza sparkSession](#spark-initialize)
- [Lettura e scrittura dei dati](#magic)
- [Creare un dataframe locale](#pyspark-create-dataframe)
- [Filtrare i dati ExperienceEvent](#pyspark-filter-experienceevent)

### Inizializzazione di sparkSession {#spark-initialize}

Tutti i notebook [!DNL Spark] 2.4 richiedono l&#39;inizializzazione della sessione con il seguente codice standard.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Utilizzo di %dataset per la lettura e la scrittura con un blocco appunti PySpark 3 {#magic}

Con l&#39;introduzione di [!DNL Spark] 2.4, `%dataset` la magia personalizzata viene fornita per l&#39;utilizzo nei notebook PySpark 3 ([!DNL Spark] 2.4). Per ulteriori dettagli sui comandi magici disponibili nel kernel IPython, visitare la [Documentazione magica IPython](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Utilizzo**

```scala
%dataset {action} --datasetId {id} --dataFrame {df}`
```

**Descrizione**

Comando [!DNL Data Science Workspace] personalizzato per la lettura o la scrittura di un dataset da un blocco appunti [!DNL PySpark] ([!DNL Python] 3 kernel).

| Nome | Descrizione | Obbligatorio |
| --- | --- | --- |
| `{action}` | Tipo di azione da eseguire sul set di dati. Sono disponibili due azioni: &quot;read&quot; o &quot;write&quot;. | Sì |
| `--datasetId {id}` | Utilizzato per fornire l&#39;ID del set di dati da leggere o scrivere. | Sì |
| `--dataFrame {df}` | Il dataframe panda. <ul><li> Quando l&#39;azione è &quot;read&quot;, {df} è la variabile in cui sono disponibili i risultati dell&#39;operazione di lettura del dataset. </li><li> Quando l&#39;azione è &quot;scrivi&quot;, il dataframe {df} viene scritto nel dataset. </li></ul> | Sì |
| `--mode` | Un parametro aggiuntivo che modifica il modo in cui i dati vengono letti. I parametri consentiti sono &quot;batch&quot; e &quot;interattivo&quot;. Per impostazione predefinita, la modalità è impostata su &quot;interattivo&quot;. Si consiglia di utilizzare la modalità &quot;batch&quot; durante la lettura di grandi quantità di dati. | No |

>[!TIP]
>
>Esaminare le tabelle PySpark all&#39;interno della sezione [limiti dei dati del notebook](#notebook-data-limits) per determinare se `mode` deve essere impostato su `interactive` o `batch`.

**Esempi**

- **Leggi l&#39;esempio**:  `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **Esempio** di scrittura:  `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

Potete generare automaticamente gli esempi di cui sopra in JupyterLab buy utilizzando il seguente metodo:

Selezionate la scheda Icona dati (evidenziata di seguito) nella navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]**. Selezionare **[!UICONTROL Datasets]** e fare clic con il pulsante destro del mouse, quindi selezionare l&#39;opzione **[!UICONTROL Write Data in Notebook]** dal menu a discesa del set di dati che si desidera utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.

- Utilizzare **[!UICONTROL Explore Data in Notebook]** per generare una cella di lettura.
- Utilizzare **[!UICONTROL Write Data in Notebook]** per generare una cella di scrittura.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Creare un dataframe locale {#pyspark-create-dataframe}

Per creare un dataframe locale utilizzando PySpark 3, utilizzate le query SQL. Esempio:

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>È inoltre possibile specificare un campione di sementi facoltativo, ad esempio un valore booleano conSostituzione, una doppia frazione o un valore seed lungo.

### Filtrare i dati [!DNL ExperienceEvent] {#pyspark-filter-experienceevent}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti PySpark è necessario fornire l&#39;identità del set di dati (`{DATASET_ID}`), l&#39;identità IMS dell&#39;azienda e le regole del filtro che definiscono un intervallo di tempo specifico. Un intervallo di tempo di filtraggio è definito utilizzando la funzione `spark.sql()`, dove il parametro della funzione è una stringa di query SQL.

Le celle seguenti filtrano un [!DNL ExperienceEvent] set di dati su dati esistenti esclusivamente tra il 1° gennaio 2019 e la fine del 31 dicembre 2019.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Notebook Scala {#scala-notebook}

La documentazione seguente contiene esempi per i seguenti concetti:

- [Inizializza sparkSession](#scala-initialize)
- [Lettura di un dataset](#read-scala-dataset)
- [Scrivere in un dataset](#scala-write-dataset)
- [Creare un dataframe locale](#scala-create-dataframe)
- [Filtrare i dati ExperienceEvent](#scala-experienceevent)

### Inizializzazione di SparkSession {#scala-initialize}

Tutti i notebook Scala richiedono l’inizializzazione della sessione con il seguente codice standard:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Leggi un set di dati {#read-scala-dataset}

In Scala, è possibile importare `clientContext` per ottenere e restituire i valori della piattaforma, eliminando la necessità di definire variabili come `var userToken`. Nell&#39;esempio di Scala seguente, `clientContext` viene utilizzato per ottenere e restituire tutti i valori richiesti necessari per la lettura di un dataset.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Elemento | Descrizione |
| ------- | ----------- |
| df1 | Variabile che rappresenta il fotogramma dati Pandas utilizzato per leggere e scrivere i dati. |
| token utente | Token utente recuperato automaticamente con `clientContext.getUserToken()`. |
| service-token | Token di servizio recuperato automaticamente con `clientContext.getServiceToken()`. |
| ims-org | L&#39;ID organizzazione IMS che viene recuperato automaticamente utilizzando `clientContext.getOrgId()`. |
| api-key | La chiave API recuperata automaticamente utilizzando `clientContext.getApiKey()`. |

>[!TIP]
>
>Esaminare le tabelle Scala all&#39;interno della sezione [limiti dei dati del notebook](#notebook-data-limits) per determinare se `mode` deve essere impostato su `interactive` o `batch`.

È possibile generare automaticamente l&#39;esempio di cui sopra in JupyterLab buy utilizzando il seguente metodo:

Selezionate la scheda Icona dati (evidenziata di seguito) nella navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]**. Selezionare **[!UICONTROL Datasets]** e fare clic con il pulsante destro del mouse, quindi selezionare l&#39;opzione **[!UICONTROL Explore Data in Notebook]** dal menu a discesa del set di dati che si desidera utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.
And
- Utilizzare **[!UICONTROL Explore Data in Notebook]** per generare una cella di lettura.
- Utilizzare **[!UICONTROL Write Data in Notebook]** per generare una cella di scrittura.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Scrivere in un set di dati {#scala-write-dataset}

In Scala, è possibile importare `clientContext` per ottenere e restituire i valori della piattaforma, eliminando la necessità di definire variabili come `var userToken`. Nell&#39;esempio di Scala seguente, `clientContext` viene utilizzato per definire e restituire tutti i valori necessari per la scrittura in un dataset.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| elemento | description |
| ------- | ----------- |
| df1 | Variabile che rappresenta il fotogramma dati Pandas utilizzato per leggere e scrivere i dati. |
| token utente | Token utente recuperato automaticamente con `clientContext.getUserToken()`. |
| service-token | Token di servizio recuperato automaticamente con `clientContext.getServiceToken()`. |
| ims-org | L&#39;ID organizzazione IMS che viene recuperato automaticamente utilizzando `clientContext.getOrgId()`. |
| api-key | La chiave API recuperata automaticamente utilizzando `clientContext.getApiKey()`. |

>[!TIP]
>
>Esaminare le tabelle Scala all&#39;interno della sezione [limiti dei dati del notebook](#notebook-data-limits) per determinare se `mode` deve essere impostato su `interactive` o `batch`.

### creare un dataframe locale {#scala-create-dataframe}

Per creare un dataframe locale utilizzando Scala, sono necessarie query SQL. Esempio:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtrare i dati [!DNL ExperienceEvent] {#scala-experienceevent}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti Scala è necessario fornire l&#39;identità del set di dati (`{DATASET_ID}`), l&#39;identità IMS dell&#39;azienda e le regole del filtro che definiscono un intervallo di tempo specifico. Un intervallo di tempo di filtro è definito utilizzando la funzione `spark.sql()`, dove il parametro della funzione è una stringa di query SQL.

Le celle seguenti filtrano un [!DNL ExperienceEvent] set di dati su dati esistenti esclusivamente tra il 1° gennaio 2019 e la fine del 31 dicembre 2019.

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## Passaggi successivi

Questo documento ha trattato le linee guida generali per l&#39;accesso ai dataset utilizzando i notebook JupyterLab. Per esempi dettagliati sull&#39;esecuzione di query sui set di dati, consultare la documentazione [Query Service in JupyterLab Notebook](./query-service.md). Per ulteriori informazioni su come esplorare e visualizzare i set di dati, consultare il documento relativo all&#39; [analisi dei dati utilizzando i blocchi appunti](./analyze-your-data.md).

## Flag SQL facoltativi per [!DNL Query Service] {#optional-sql-flags-for-query-service}

La tabella riportata di seguito illustra i flag SQL facoltativi utilizzabili per [!DNL Query Service].

| **Flag** | **Descrizione** |
| --- | --- |
| `-h`, `--help` | Visualizza il messaggio della Guida e esci. |
| `-n`,  `--notify` | Attiva/disattiva l&#39;opzione per la notifica dei risultati della query. |
| `-a`,  `--async` | L&#39;utilizzo di questo flag consente di eseguire la query in modo asincrono e di liberare il kernel durante l&#39;esecuzione della query. Prestate attenzione quando assegnate i risultati della query alle variabili, in quanto potrebbe essere undefined se la query non è completa. |
| `-d`,  `--display` | L&#39;utilizzo di questo flag impedisce la visualizzazione dei risultati. |

