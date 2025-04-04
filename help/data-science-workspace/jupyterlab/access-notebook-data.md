---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti comuni;%dataset;modalità interattiva;modalità batch;Spark sdk;python sdk;accedere ai dati;accesso ai dati dei notebook
solution: Experience Platform
title: Accesso ai dati nei notebook Jupyterlab
description: Questa guida si concentra sull’utilizzo di Jupyter Notebooks, integrati in Data Science Workspace per accedere ai tuoi dati.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3346'
ht-degree: 3%

---

# Accesso ai dati nei notebook [!DNL Jupyterlab]

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Ogni kernel supportato fornisce funzionalità integrate che consentono di leggere i dati di Experience Platform da un set di dati all’interno di un blocco appunti. Attualmente JupyterLab in Adobe Experience Platform Data Science Workspace supporta notebook per [!DNL Python], R, PySpark e Scala. Tuttavia, il supporto per l&#39;impaginazione dei dati è limitato a [!DNL Python] e R notebook. Questa guida illustra come utilizzare i notebook JupyterLab per accedere ai dati.

## Introduzione

Prima di leggere questa guida, consulta la [[!DNL JupyterLab] guida utente](./overview.md) per un&#39;introduzione di alto livello a [!DNL JupyterLab] e al suo ruolo in Data Science Workspace.

## Limiti dei dati del notebook {#notebook-data-limits}

>[!IMPORTANT]
>
>Per i notebook PySpark e Scala se si riceve un errore con il motivo &quot;Client RPC remoto disassociato&quot;. In genere, ciò significa che la memoria del driver o di un esecutore è quasi esaurita. Provare a passare alla modalità [&quot;batch&quot;](#mode) per risolvere l&#39;errore.

Le informazioni seguenti definiscono la quantità massima di dati che è possibile leggere, il tipo di dati utilizzato e il periodo di tempo stimato necessario per la lettura dei dati.

Per [!DNL Python] e R, per i benchmark è stato utilizzato un server notebook configurato a 40 GB di RAM. Per i benchmark descritti di seguito sono stati utilizzati PySpark e Scala, un cluster di database configurato a 64 GB di RAM, 8 core, 2 DBU con un massimo di 4 processi di lavoro.

Le dimensioni dei dati dello schema ExperienceEvent utilizzati variavano da mille (1K) righe fino a un miliardo (1B). Tieni presente che per le metriche PySpark e [!DNL Spark] è stato utilizzato un intervallo di date di 10 giorni per i dati XDM.

I dati dello schema ad hoc sono stati pre-elaborati utilizzando [!DNL Query Service] Crea tabella come Select (CTAS). Questi dati variavano anche nelle dimensioni a partire da mille (1K) righe fino a un miliardo (1B) di righe.

### Quando utilizzare la modalità batch rispetto alla modalità interattiva {#mode}

Quando si leggono i set di dati con i notebook PySpark e Scala, è possibile utilizzare la modalità interattiva o batch per leggere il set di dati. L’interattività viene eseguita per ottenere risultati rapidi, mentre la modalità batch viene applicata a set di dati di grandi dimensioni.

- Per i notebook PySpark e Scala, è necessario utilizzare la modalità batch quando vengono lette almeno 5 milioni di righe di dati. Per ulteriori informazioni sull&#39;efficienza di ogni modalità, vedere le tabelle dei limiti di dati [PySpark](#pyspark-data-limits) o [Scala](#scala-data-limits) di seguito.

### [!DNL Python] limiti dati blocco appunti

**Schema ExperienceEvent XDM:** dovresti essere in grado di leggere un massimo di 2 milioni di righe (circa 6,1 GB di dati su disco) di dati XDM in meno di 22 minuti. L’aggiunta di righe aggiuntive può causare errori.

| Numero di righe | 1 K | 10K | 100.000 | 1 M | 2 M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Dimensioni su disco (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (in secondi) | 20,3 | 86,8 | 63 | 659 | 1315 |

**schema ad hoc:** dovresti essere in grado di leggere un massimo di 5 milioni di righe (circa 5,6 GB di dati su disco) di dati non XDM (ad hoc) in meno di 14 minuti. L’aggiunta di righe aggiuntive può causare errori.

| Numero di righe | 1 K | 10K | 100.000 | 1 M | 2 M | 3 M | 5 M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Dimensioni su disco (in MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in secondi) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### R limiti dei dati dei notebook

**Schema ExperienceEvent XDM:** dovresti essere in grado di leggere un massimo di 1 milione di righe di dati XDM (dati da 3 GB su disco) in meno di 13 minuti.

| Numero di righe | 1 K | 10K | 100.000 | 1 M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Dimensioni su disco (MB) | 18,73 | 187,5 | 308 | 3000 |
| R Kernel (in secondi) | 14,03 | 69,6 | 86,8 | 775 |

**schema ad hoc:** dovrebbe essere possibile leggere un massimo di 3 milioni di righe di dati ad hoc (293 MB di dati su disco) in circa 10 minuti.

| Numero di righe | 1 K | 10K | 100.000 | 1 M | 2 M | 3 M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Dimensioni su disco (in MB) | 0,082 | 0,612 | 9,0 | 91 | 188 | 293 |
| R SDK (in sec) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### Limiti dati blocco appunti PySpark ([!DNL Python] kernel): {#pyspark-data-limits}

**Schema ExperienceEvent XDM:** In modalità interattiva dovresti essere in grado di leggere un massimo di 5 milioni di righe (circa 13,42 GB di dati su disco) di dati XDM in circa 20 minuti. La modalità interattiva supporta solo fino a 5 milioni di righe. Se desideri leggere set di dati più grandi, ti consigliamo di passare alla modalità batch. In modalità batch dovresti essere in grado di leggere un massimo di 500 milioni di righe (circa 1,31 TB di dati su disco) di dati XDM in circa 14 ore.

| Numero di righe | 1 K | 10K | 100.000 | 1 M | 2 M | 3 M | 5 M | 10 M | 50 milioni | 100 milioni | 500 milioni |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Dimensioni su disco | 2,93 MB | 4,38 MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| SDK (modalità interattiva) | 33s | 32,4s | 55,1 s | 253,5 s | 489,2 s | 729,6s | 1206,8s | - | - | - | - |
| SDK (modalità Batch) | 815,8s | 492,8s | 379,1s | 637,4s | 624,5 s | 869,2 s | 1104.1s | 1786 s | 5387,2 s | 10624,6s | 50547 s |

**schema ad hoc:** In modalità interattiva dovresti essere in grado di leggere un massimo di 5 milioni di righe (circa 5,36 GB di dati su disco) di dati non XDM in meno di 3 minuti. In modalità Batch dovresti essere in grado di leggere un massimo di 1 miliardo di righe (circa 1,05 TB di dati su disco) di dati non XDM in circa 18 minuti.

| Numero di righe | 1 K | 10K | 100.000 | 1 M | 2 M | 3 M | 5 M | 10 M | 50 milioni | 100 milioni | 500 milioni | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Dimensioni su disco | 1,12 MB | 11,24 MB | 109,48 MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Modalità interattiva SDK (in secondi) | 28,2 s | 18,6s | 20,8 s | 20,9 s | 23,8s | 21,7s | 24,7s | - | - | - | - | - |
| Modalità Batch SDK (in secondi) | 428,8s | 578,8s | 641,4s | 538,5 s | 630,9 s | 467,3s | 411s | 675 s | 702 s | 719,2 s | 1022.1s | 1122,3s |

### [!DNL Spark] (kernel Scala) limiti dati blocco appunti: {#scala-data-limits}

**Schema ExperienceEvent XDM:** In modalità interattiva dovresti essere in grado di leggere un massimo di 5 milioni di righe (circa 13,42 GB di dati su disco) di dati XDM in circa 18 minuti. La modalità interattiva supporta solo fino a 5 milioni di righe. Se desideri leggere set di dati più grandi, ti consigliamo di passare alla modalità batch. In modalità batch dovresti essere in grado di leggere un massimo di 500 milioni di righe (circa 1,31 TB di dati su disco) di dati XDM in circa 14 ore.

| Numero di righe | 1 K | 10K | 100.000 | 1 M | 2 M | 3 M | 5 M | 10 M | 50 milioni | 100 milioni | 500 milioni |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Dimensioni su disco | 2,93 MB | 4,38 MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| Modalità interattiva SDK (in secondi) | 37,9 s | 22,7s | 45,6s | 231,7 s | 444,7s | 660,6s | 1100 s | - | - | - | - |
| Modalità Batch SDK (in secondi) | 374,4s | 398,5 s | 527 s | 487,9 s | 588,9 s | 829 | 939,1s | 1441s | 5473,2 s | 10118,8 | 49207,6 |

**schema ad hoc:** In modalità interattiva dovresti essere in grado di leggere un massimo di 5 milioni di righe (circa 5,36 GB di dati su disco) di dati non XDM in meno di 3 minuti. In modalità batch dovresti essere in grado di leggere un massimo di 1 miliardo di righe (circa 1,05 TB di dati su disco) di dati non XDM in circa 16 minuti.

| Numero di righe | 1 K | 10K | 100.000 | 1 M | 2 M | 3 M | 5 M | 10 M | 50 milioni | 100 milioni | 500 milioni | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Dimensioni su disco | 1,12 MB | 11,24 MB | 109,48 MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Modalità interattiva SDK (in secondi) | 35,7s | 31s | 19,5 s | 25,3s | 23s | 33,2 s | 25,5 s | - | - | - | - | - |
| Modalità Batch SDK (in secondi) | 448,8s | 459,7s | 519 | 475,8s | 599,9 s | 347,6s | 407,8s | 397 s | 518,8s | 487,9 s | 760,2 s | 975,4s |

## Notebook Python {#python-notebook}

I blocchi appunti [!DNL Python] consentono di impaginare i dati quando si accede ai set di dati. Di seguito è illustrato il codice di esempio per la lettura dei dati con e senza impaginazione. Per ulteriori informazioni sui notebook Python starter disponibili, visita la sezione [[!DNL JupyterLab] Launcher](./overview.md#launcher) nella guida utente di JupyterLab.

La documentazione di Python seguente illustra i seguenti concetti:

- [Lettura da un set di dati](#python-read-dataset)
- [Scrivi in un set di dati](#write-python)
- [Dati della query](#query-data-python)
- [Filtrare i dati ExperienceEvent](#python-filter)

### Lettura da un set di dati in Python {#python-read-dataset}

**Senza paginazione:**

L’esecuzione del codice seguente leggerà l’intero set di dati. Se l&#39;esecuzione ha esito positivo, i dati verranno salvati come dataframe Pandas a cui fa riferimento la variabile `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Con paginazione:**

L’esecuzione del codice seguente leggerà i dati dal set di dati specificato. L&#39;impaginazione viene ottenuta limitando e spostando i dati tramite le funzioni `limit()` e `offset()` rispettivamente. Limitare i dati si riferisce al numero massimo di punti dati da leggere, mentre l&#39;offset si riferisce al numero di punti dati da saltare prima della lettura dei dati. Se l&#39;operazione di lettura viene eseguita correttamente, i dati verranno salvati come dataframe Pandas a cui fa riferimento la variabile `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Scrivere su un set di dati in Python {#write-python}

Per scrivere su un set di dati nel notebook JupyterLab, seleziona la scheda Icona dati (evidenziata di seguito) nell’area di navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Set di dati]** e **[!UICONTROL Schemi]**. Seleziona **[!UICONTROL Set di dati]** e fai clic con il pulsante destro del mouse, quindi seleziona l&#39;opzione **[!UICONTROL Scrivi dati nel blocco appunti]** dal menu a discesa del set di dati che desideri utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.

![](../images/jupyterlab/data-access/write-dataset.png)

- Utilizza **[!UICONTROL Scrivi dati in blocco appunti]** per generare una cella di scrittura con il set di dati selezionato.
- Utilizza **[!UICONTROL Esplora dati nel blocco appunti]** per generare una cella di lettura con il set di dati selezionato.
- Utilizza **[!UICONTROL Query Data in Notebook]** per generare una cella di query di base con il set di dati selezionato.

In alternativa, è possibile copiare e incollare la seguente cella di codice. Sostituire sia `{DATASET_ID}` che `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Eseguire query sui dati utilizzando [!DNL Query Service] in [!DNL Python] {#query-data-python}

[!DNL JupyterLab] su [!DNL Experience Platform] consente di utilizzare SQL in un blocco appunti [!DNL Python] per accedere ai dati tramite [Adobe Experience Platform Query Service](https://www.adobe.com/go/query-service-home-en). L&#39;accesso ai dati tramite [!DNL Query Service] può essere utile per gestire set di dati di grandi dimensioni a causa dei tempi di esecuzione superiori. Si noti che l&#39;esecuzione di query sui dati tramite [!DNL Query Service] ha un limite di tempo di elaborazione di dieci minuti.

Prima di utilizzare [!DNL Query Service] in [!DNL JupyterLab], verificare di avere una buona conoscenza della sintassi [[!DNL Query Service] SQL](https://www.adobe.com/go/query-service-sql-syntax-en).

Per eseguire una query sui dati tramite [!DNL Query Service] è necessario specificare il nome del set di dati di destinazione. Puoi generare le celle di codice necessarie trovando il set di dati desiderato utilizzando **[!UICONTROL Esplora dati]**. Fai clic con il pulsante destro del mouse sull&#39;elenco dei set di dati e fai clic su **[!UICONTROL Esegui query sui dati nel blocco appunti]** per generare due celle di codice nel blocco appunti. Queste due celle sono descritte più dettagliatamente di seguito.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Per utilizzare [!DNL Query Service] in [!DNL JupyterLab], è necessario innanzitutto creare una connessione tra il blocco appunti [!DNL Python] in uso e [!DNL Query Service]. Ciò può essere ottenuto eseguendo la prima cella generata.

```python
qs_connect()
```

Nella seconda cella generata, la prima riga deve essere definita prima della query SQL. Per impostazione predefinita, la cella generata definisce una variabile opzionale (`df0`) che salva i risultati della query come un dataframe Pandas. <br>L&#39;argomento `-c QS_CONNECTION` è obbligatorio e indica al kernel di eseguire la query SQL su [!DNL Query Service]. Per un elenco di argomenti aggiuntivi, vedere l&#39;[appendice](#optional-sql-flags-for-query-service).

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

È possibile fare riferimento direttamente alle variabili Python all&#39;interno di una query SQL utilizzando la sintassi in formato stringa e racchiudere le variabili tra parentesi graffe (`{}`), come illustrato nell&#39;esempio seguente:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtra dati [!DNL ExperienceEvent] {#python-filter}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti [!DNL Python], è necessario fornire l&#39;ID del set di dati (`{DATASET_ID}`) insieme alle regole di filtro che definiscono un intervallo di tempo specifico utilizzando operatori logici. Quando viene definito un intervallo di tempo, qualsiasi impaginazione specificata viene ignorata e viene considerato l’intero set di dati.

Di seguito è riportato un elenco di operatori di filtro:

- `eq()`: uguale a
- `gt()`: maggiore di
- `ge()`: maggiore o uguale a
- `lt()`: minore di
- `le()`: minore o uguale a
- `And()`: operatore AND logico
- `Or()`: operatore OR logico

La cella seguente filtra un set di dati [!DNL ExperienceEvent] ai dati esistenti esclusivamente tra il 1° gennaio 2019 e la fine del 31 dicembre 2019.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R notebook {#r-notebooks}

R consente di impaginare i dati quando si accede ai set di dati. Di seguito è illustrato il codice di esempio per la lettura dei dati con e senza impaginazione. Per ulteriori informazioni sui notebook R di avvio disponibili, visitare la sezione [[!DNL JupyterLab] Launcher](./overview.md#launcher) nella guida utente di JupyterLab.

La documentazione di R qui di seguito illustra i concetti seguenti:

- [Lettura da un set di dati](#r-read-dataset)
- [Scrivi in un set di dati](#write-r)
- [Filtrare i dati ExperienceEvent](#r-filter)

### Leggi da un set di dati in R {#r-read-dataset}

**Senza paginazione:**

L’esecuzione del codice seguente leggerà l’intero set di dati. Se l&#39;esecuzione ha esito positivo, i dati verranno salvati come dataframe Pandas a cui fa riferimento la variabile `df0`.

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

**Con paginazione:**

L’esecuzione del codice seguente leggerà i dati dal set di dati specificato. L&#39;impaginazione viene ottenuta limitando e spostando i dati tramite le funzioni `limit()` e `offset()` rispettivamente. Limitare i dati si riferisce al numero massimo di punti dati da leggere, mentre l&#39;offset si riferisce al numero di punti dati da saltare prima della lettura dei dati. Se l&#39;operazione di lettura viene eseguita correttamente, i dati verranno salvati come dataframe Pandas a cui fa riferimento la variabile `df0`.

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

### Scrittura in un set di dati in R {#write-r}

Per scrivere su un set di dati nel notebook JupyterLab, seleziona la scheda Icona dati (evidenziata di seguito) nell’area di navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Set di dati]** e **[!UICONTROL Schemi]**. Seleziona **[!UICONTROL Set di dati]** e fai clic con il pulsante destro del mouse, quindi seleziona l&#39;opzione **[!UICONTROL Scrivi dati nel blocco appunti]** dal menu a discesa del set di dati che desideri utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Utilizza **[!UICONTROL Scrivi dati in blocco appunti]** per generare una cella di scrittura con il set di dati selezionato.
- Utilizza **[!UICONTROL Esplora dati nel blocco appunti]** per generare una cella di lettura con il set di dati selezionato.

In alternativa, è possibile copiare e incollare la seguente cella di codice:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtra dati [!DNL ExperienceEvent] {#r-filter}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti R, è necessario fornire l&#39;ID del set di dati (`{DATASET_ID}`) insieme alle regole di filtro che definiscono un intervallo di tempo specifico utilizzando gli operatori logici. Quando viene definito un intervallo di tempo, qualsiasi impaginazione specificata viene ignorata e viene considerato l’intero set di dati.

Di seguito è riportato un elenco di operatori di filtro:

- `eq()`: uguale a
- `gt()`: maggiore di
- `ge()`: maggiore o uguale a
- `lt()`: minore di
- `le()`: minore o uguale a
- `And()`: operatore AND logico
- `Or()`: operatore OR logico

La cella seguente filtra un set di dati [!DNL ExperienceEvent] ai dati esistenti esclusivamente tra il 1° gennaio 2019 e la fine del 31 dicembre 2019.

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

## PySpark 3 notebook {#pyspark-notebook}

La documentazione di PySpark riportata di seguito descrive i concetti seguenti:

- [Inizializza sparkSession](#spark-initialize)
- [Lettura e scrittura di dati](#magic)
- [Creare un dataframe locale](#pyspark-create-dataframe)
- [Filtrare i dati ExperienceEvent](#pyspark-filter-experienceevent)

### Inizializzazione di sparkSession {#spark-initialize}

Tutti i notebook [!DNL Spark] 2.4 richiedono l&#39;inizializzazione della sessione con il seguente codice boilerplate.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Utilizzo di %dataset per la lettura e la scrittura con un blocco appunti di PySpark 3 {#magic}

Con l&#39;introduzione di [!DNL Spark] 2.4, viene fornita la magia personalizzata `%dataset` da utilizzare nei notebook PySpark 3 ([!DNL Spark] 2.4). Per ulteriori dettagli sui comandi magici disponibili nel kernel IPython, visita la [documentazione magica di IPython](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Utilizzo**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Descrizione**

Comando magico [!DNL Data Science Workspace] personalizzato per la lettura o la scrittura di un set di dati da un blocco appunti [!DNL PySpark] ([!DNL Python] 3 kernel).

| Nome | Descrizione | Obbligatorio |
| --- | --- | --- |
| `{action}` | Tipo di azione da eseguire sul set di dati. Sono disponibili due azioni: &quot;lettura&quot; o &quot;scrittura&quot;. | Sì |
| `--datasetId {id}` | Utilizzato per fornire l’ID del set di dati da leggere o scrivere. | Sì |
| `--dataFrame {df}` | Il dataframe panda. <ul><li> Quando l&#39;azione è &quot;read&quot;, {df} è la variabile in cui sono disponibili i risultati dell&#39;operazione di lettura del set di dati (ad esempio un dataframe). </li><li> Quando l&#39;azione è &quot;write&quot;, il dataframe {df} viene scritto nel set di dati. </li></ul> | Sì |
| `--mode` | Un parametro aggiuntivo che cambia il modo in cui i dati vengono letti. I parametri consentiti sono &quot;batch&quot; e &quot;interattivo&quot;. Per impostazione predefinita, la modalità è impostata su &quot;batch&quot;.<br> Si consiglia di utilizzare la modalità &quot;interattiva&quot; per migliorare le prestazioni delle query su set di dati più piccoli. | Sì |

>[!TIP]
>
>Esaminare le tabelle PySpark nella sezione [limiti dati blocco appunti](#notebook-data-limits) per determinare se `mode` deve essere impostato su `interactive` o `batch`.

**Esempi**

- **Esempio di lettura**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **Scrivi esempio**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> La memorizzazione nella cache dei dati tramite `df.cache()` prima della scrittura dei dati può migliorare notevolmente le prestazioni del blocco appunti. Questo può essere utile se ricevi uno dei seguenti errori:
> 
> - Processo interrotto a causa di un errore della fase... È possibile comprimere solo gli RDD con lo stesso numero di elementi in ogni partizione.
> - Client RPC remoto disassociato e altri errori di memoria.
> - Scarse prestazioni durante la lettura e la scrittura di set di dati.
> 
> Per ulteriori informazioni, consulta la [guida alla risoluzione dei problemi](../troubleshooting-guide.md).

Puoi generare automaticamente gli esempi di cui sopra in JupyterLab buy utilizzando il seguente metodo:

Seleziona la scheda Icona dati (evidenziata di seguito) nell’area di navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Set di dati]** e **[!UICONTROL Schemi]**. Seleziona **[!UICONTROL Set di dati]** e fai clic con il pulsante destro del mouse, quindi seleziona l&#39;opzione **[!UICONTROL Scrivi dati nel blocco appunti]** dal menu a discesa del set di dati che desideri utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.

- Utilizza **[!UICONTROL Esplora dati nel blocco appunti]** per generare una cella di lettura.
- Utilizza **[!UICONTROL Scrivi dati in blocco appunti]** per generare una cella di scrittura.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Creare un dataframe locale {#pyspark-create-dataframe}

Per creare un dataframe locale utilizzando PySpark 3, utilizzare le query SQL. Ad esempio:

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
>È inoltre possibile specificare un campione di seed facoltativo, ad esempio booleano conReplacement, frazione doppia o seme lungo.

### Filtra dati [!DNL ExperienceEvent] {#pyspark-filter-experienceevent}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti di PySpark è necessario fornire l&#39;identità del set di dati (`{DATASET_ID}`), l&#39;identità IMS dell&#39;organizzazione e le regole di filtro che definiscono un intervallo di tempo specifico. Un intervallo di tempo di filtraggio viene definito utilizzando la funzione `spark.sql()`, dove il parametro della funzione è una stringa di query SQL.

Le celle seguenti filtrano un set di dati [!DNL ExperienceEvent] in base ai dati esistenti esclusivamente tra il 1° gennaio 2019 e la fine del 31 dicembre 2019.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df --mode batch

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

La documentazione seguente contiene esempi dei seguenti concetti:

- [Inizializza sparkSession](#scala-initialize)
- [Leggere un set di dati](#read-scala-dataset)
- [Scrivi in un set di dati](#scala-write-dataset)
- [Creare un dataframe locale](#scala-create-dataframe)
- [Filtrare i dati ExperienceEvent](#scala-experienceevent)

### Inizializzazione di SparkSession {#scala-initialize}

Tutti i notebook Scala richiedono l&#39;inizializzazione della sessione con il seguente codice standard:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Leggere un set di dati {#read-scala-dataset}

In Scala è possibile importare `clientContext` per ottenere e restituire i valori Experience Platform, eliminando la necessità di definire variabili quali `var userToken`. Nell&#39;esempio Scala seguente, `clientContext` viene utilizzato per ottenere e restituire tutti i valori richiesti necessari per la lettura di un set di dati.

>[!IMPORTANT]
>
> La memorizzazione nella cache dei dati tramite `df.cache()` prima della scrittura dei dati può migliorare notevolmente le prestazioni del blocco appunti. Questo può essere utile se ricevi uno dei seguenti errori:
> 
> - Processo interrotto a causa di un errore della fase... È possibile comprimere solo gli RDD con lo stesso numero di elementi in ogni partizione.
> - Client RPC remoto disassociato e altri errori di memoria.
> - Scarse prestazioni durante la lettura e la scrittura di set di dati.
> 
> Per ulteriori informazioni, consulta la [guida alla risoluzione dei problemi](../troubleshooting-guide.md).

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
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Elemento | Descrizione |
| ------- | ----------- |
| df1 | Variabile che rappresenta il dataframe Pandas utilizzato per leggere e scrivere dati. |
| user-token | Il token utente che viene recuperato automaticamente con `clientContext.getUserToken()`. |
| service-token | Token di servizio recuperato automaticamente con `clientContext.getServiceToken()`. |
| ims-org | L&#39;ID organizzazione che viene recuperato automaticamente con `clientContext.getOrgId()`. |
| api-key | Chiave API recuperata automaticamente tramite `clientContext.getApiKey()`. |

>[!TIP]
>
>Rivedi le tabelle Scala nella sezione [limiti dati blocco appunti](#notebook-data-limits) per determinare se `mode` deve essere impostato su `interactive` o `batch`.

Puoi generare automaticamente l’esempio precedente in JupyterLab buy utilizzando il seguente metodo:

Seleziona la scheda Icona dati (evidenziata di seguito) nell’area di navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Set di dati]** e **[!UICONTROL Schemi]**. Seleziona **[!UICONTROL Set di dati]** e fai clic con il pulsante destro del mouse, quindi seleziona l&#39;opzione **[!UICONTROL Esplora dati nel blocco appunti]** dal menu a discesa del set di dati che desideri utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.
E
- Utilizza **[!UICONTROL Esplora dati nel blocco appunti]** per generare una cella di lettura.
- Utilizza **[!UICONTROL Scrivi dati in blocco appunti]** per generare una cella di scrittura.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Scrivi in un set di dati {#scala-write-dataset}

In Scala è possibile importare `clientContext` per ottenere e restituire i valori Experience Platform, eliminando la necessità di definire variabili quali `var userToken`. Nell&#39;esempio Scala seguente, `clientContext` viene utilizzato per definire e restituire tutti i valori richiesti necessari per la scrittura in un set di dati.

>[!IMPORTANT]
>
> La memorizzazione nella cache dei dati tramite `df.cache()` prima della scrittura dei dati può migliorare notevolmente le prestazioni del blocco appunti. Questo può essere utile se ricevi uno dei seguenti errori:
> 
> - Processo interrotto a causa di un errore della fase... È possibile comprimere solo gli RDD con lo stesso numero di elementi in ogni partizione.
> - Client RPC remoto disassociato e altri errori di memoria.
> - Scarse prestazioni durante la lettura e la scrittura di set di dati.
> 
> Per ulteriori informazioni, consulta la [guida alla risoluzione dei problemi](../troubleshooting-guide.md).

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
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| elemento | descrizione |
| ------- | ----------- |
| df1 | Variabile che rappresenta il dataframe Pandas utilizzato per leggere e scrivere dati. |
| user-token | Il token utente che viene recuperato automaticamente con `clientContext.getUserToken()`. |
| service-token | Token di servizio recuperato automaticamente con `clientContext.getServiceToken()`. |
| ims-org | L&#39;ID organizzazione che viene recuperato automaticamente con `clientContext.getOrgId()`. |
| api-key | Chiave API recuperata automaticamente tramite `clientContext.getApiKey()`. |

>[!TIP]
>
>Rivedi le tabelle Scala nella sezione [limiti dati blocco appunti](#notebook-data-limits) per determinare se `mode` deve essere impostato su `interactive` o `batch`.

### creare un dataframe locale {#scala-create-dataframe}

Per creare un dataframe locale utilizzando Scala, sono necessarie query SQL. Ad esempio:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtra dati [!DNL ExperienceEvent] {#scala-experienceevent}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti Scala è necessario specificare l&#39;identità del set di dati (`{DATASET_ID}`), l&#39;identità IMS dell&#39;organizzazione e le regole di filtro che definiscono un intervallo di tempo specifico. Un intervallo di tempo di filtraggio viene definito utilizzando la funzione `spark.sql()`, dove il parametro della funzione è una stringa di query SQL.

Le celle seguenti filtrano un set di dati [!DNL ExperienceEvent] in base ai dati esistenti esclusivamente tra il 1° gennaio 2019 e la fine del 31 dicembre 2019.

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

Questo documento illustra le linee guida generali per l’accesso ai set di dati con i notebook JupyterLab. Per ulteriori esempi approfonditi sull&#39;esecuzione di query sui set di dati, consulta la documentazione di [Query Service nei notebook JupyterLab](./query-service.md). Per ulteriori informazioni su come esplorare e visualizzare i set di dati, visita il documento su [analisi dei dati tramite blocchi appunti](./analyze-your-data.md).

## Flag SQL facoltativi per [!DNL Query Service] {#optional-sql-flags-for-query-service}

Questa tabella illustra i flag SQL facoltativi che possono essere utilizzati per [!DNL Query Service].

| **Contrassegno** | **Descrizione** |
| --- | --- |
| `-h`, `--help` | Visualizza il messaggio di aiuto ed esci. |
| `-n`, `--notify` | Attiva/disattiva l’opzione per la notifica dei risultati della query. |
| `-a`, `--async` | Questo flag esegue la query in modo asincrono e può liberare il kernel durante l&#39;esecuzione della query. Presta attenzione quando assegni i risultati della query alle variabili, in quanto potrebbero non essere definiti se la query non è completa. |
| `-d`, `--display` | L’utilizzo di questo flag impedisce la visualizzazione dei risultati. |
