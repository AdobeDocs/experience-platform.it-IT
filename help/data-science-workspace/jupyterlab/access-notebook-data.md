---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti comuni;%set di dati;modalità interattiva;modalità batch;Spark sdk;python sdk;accesso ai dati;accesso ai dati del blocco appunti
solution: Experience Platform
title: Accesso ai dati nei notebook Jupyterlab
topic-legacy: Developer Guide
description: Questa guida si concentra su come utilizzare i notebook Jupyter, creati all’interno di Data Science Workspace per accedere ai tuoi dati.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 9%

---

# Accesso ai dati nei notebook [!DNL Jupyterlab]

Ogni kernel supportato fornisce funzionalità integrate che consentono di leggere i dati di Platform da un set di dati all’interno di un blocco appunti. Al momento JupyterLab in Adobe Experience Platform Data Science Workspace supporta i notebook per [!DNL Python], R, PySpark e Scala. Tuttavia, il supporto per i dati di impaginazione è limitato ai notebook [!DNL Python] e R. Questa guida si concentra su come utilizzare i notebook JupyterLab per accedere ai dati.

## Introduzione

Prima di leggere questa guida, consulta la [[!DNL JupyterLab] guida utente](./overview.md) per un’introduzione di alto livello a [!DNL JupyterLab] e il suo ruolo all’interno di Data Science Workspace.

## Limiti dei dati del blocco appunti {#notebook-data-limits}

>[!IMPORTANT]
>
>Per i notebook PySpark e Scala se si riceve un errore con il motivo &quot;Client RPC remoto disassociato&quot;. In genere significa che la memoria del driver o dell&#39;esecutore è esaurita. Prova a passare alla modalità [&quot;batch&quot;](#mode) per risolvere questo errore.

Le informazioni seguenti definiscono la quantità massima di dati leggibili, il tipo di dati utilizzato e il periodo di tempo stimato necessario per la lettura dei dati.

Per [!DNL Python] e R, per i benchmark è stato utilizzato un server notebook configurato a 40 GB di RAM. Per PySpark e Scala, è stato utilizzato un cluster di database configurato a 64 GB di RAM, 8 core, 2 DBU con un massimo di 4 dipendenti per i benchmark descritti di seguito.

I dati dello schema ExperienceEvent utilizzati variano a partire da mille (1K) righe che variano fino a un miliardo di righe (1B). Per le metriche PySpark e [!DNL Spark] è stato utilizzato un intervallo di date di 10 giorni per i dati XDM.

I dati dello schema ad-hoc sono stati preelaborati utilizzando [!DNL Query Service] Crea tabella come selezione (CTAS). Questi dati sono anche variati in dimensioni a partire da mille (1K) righe che vanno fino a un miliardo (1B) righe.

### Quando utilizzare la modalità batch rispetto alla modalità interattiva {#mode}

Quando si leggono i set di dati con i blocchi appunti PySpark e Scala, è possibile utilizzare la modalità interattiva o la modalità batch per leggere il set di dati. La modalità interattiva viene eseguita per risultati rapidi, mentre la modalità batch è per set di dati di grandi dimensioni.

- Per i notebook PySpark e Scala, utilizzare la modalità batch quando si leggono almeno 5 milioni di righe di dati. Per ulteriori informazioni sull&#39;efficienza di ciascuna modalità, vedere le tabelle dei limiti di dati [PySpark](#pyspark-data-limits) o [Scala](#scala-data-limits) riportate di seguito.

### [!DNL Python] limiti dei dati del blocco appunti

**Schema ExperienceEvent XDM:** dovresti essere in grado di leggere un massimo di 2 milioni di righe (~6,1 GB di dati su disco) di dati XDM in meno di 22 minuti. L’aggiunta di righe aggiuntive potrebbe causare errori.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Dimensioni su disco (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (in secondi) | 20,3 | 86,8 | 63 | 659 | 1315 |

**schema ad-hoc:** dovresti essere in grado di leggere un massimo di 5 milioni di righe (~5,6 GB di dati su disco) di dati non XDM (ad-hoc) in meno di 14 minuti. L’aggiunta di righe aggiuntive potrebbe causare errori.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Dimensioni su disco (in MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in secondi) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### Limiti dei dati del notebook R

**Schema XDM ExperienceEvent:** dovresti essere in grado di leggere un massimo di 1 milione di righe di dati XDM (dati da 3 GB sul disco) in meno di 13 minuti.

| Numero di righe | 1K | 10.000 | 100.000 | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Dimensioni su disco (MB) | 18,73 | 187,5 | 308 | 3000 |
| R Kernel (in secondi) | 14,03 | 69,6 | 86,8 | 775 |

**schema ad-hoc:** dovresti essere in grado di leggere un massimo di 3 milioni di righe di dati ad-hoc (293 MB di dati su disco) in circa 10 minuti.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Dimensioni su disco (in MB) | 0,082 | 0,612 | 9,0 | 91 | 188 | 293 |
| SDK R (in secondi) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### Limiti dei dati del notebook PySpark ([!DNL Python] kernel): {#pyspark-data-limits}

**Schema XDM ExperienceEvent:** in modalità interattiva dovresti essere in grado di leggere un massimo di 5 milioni di righe (circa 13,42 GB di dati su disco) di dati XDM in circa 20 minuti. La modalità interattiva supporta solo fino a 5 milioni di righe. Se desideri leggere set di dati più grandi, ti consigliamo di passare alla modalità batch. In modalità batch è necessario essere in grado di leggere un massimo di 500 milioni di righe (~1,31 TB di dati su disco) di dati XDM in circa 14 ore.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M | 10 M | 50 M | 100 M | 500 M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Dimensioni su disco | 2,93 MB | 4,38 MB | 29,02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1,31 TB |
| SDK (modalità interattiva) | 33 s | 32,4 s | 55,1 s | 253,5 s | 489,2 s | 729,6 s | 1206,8 s | - | - | - | - |
| SDK (modalità Batch) | 815,8 s | 492,8 s | 379,1 s | 637,4 s | 624,5 s | 869,2 s | 1104.1s | 1786 s | 5387,2s | 10624.6s | 50547 s |

**schema ad-hoc:** in modalità interattiva dovresti essere in grado di leggere un massimo di 5 milioni di righe (~5,36 GB di dati su disco) di dati non XDM in meno di 3 minuti. In modalità Batch dovresti essere in grado di leggere un massimo di 1 miliardo di righe (~1,05 TB di dati su disco) di dati non XDM in circa 18 minuti.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M | 10 M | 50 M | 100 M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Dimensioni su disco | 1,12 MB | 11,24 MB | 109,48 MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1,05 TB |
| Modalità interattiva SDK (in secondi) | 28,2 s | 18,6 s | 20,8 s | 20,9 s | 23,8 s | 21,7 s | 24,7 s | - | - | - | - | - |
| Modalità batch SDK (in secondi) | 428,8 s | 578,8 s | 641,4 s | 538,5 s | 630,9 s | 467,3s | 411 s | 675 s | 702 s | 719,2 s | 1022.1s | 1122.3s |

### [!DNL Spark] Limiti dei dati del notebook (kernel Scala):  {#scala-data-limits}

**Schema XDM ExperienceEvent:** in modalità interattiva dovresti essere in grado di leggere un massimo di 5 milioni di righe (circa 13,42 GB di dati su disco) di dati XDM in circa 18 minuti. La modalità interattiva supporta solo fino a 5 milioni di righe. Se desideri leggere set di dati più grandi, ti consigliamo di passare alla modalità batch. In modalità batch è necessario essere in grado di leggere un massimo di 500 milioni di righe (~1,31 TB di dati su disco) di dati XDM in circa 14 ore.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M | 10 M | 50 M | 100 M | 500 M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Dimensioni su disco | 2,93 MB | 4,38 MB | 29,02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1,31 TB |
| Modalità interattiva SDK (in secondi) | 37,9 s | 22,7 s | 45,6 s | 231,7 s | 444,7 s | 660,6 s | 1100 | - | - | - | - |
| Modalità batch SDK (in secondi) | 374,4 s | 398,5 s | 527 s | 487,9 s | 588,9 s | 829 s | 939,1 s | 1441 s | 5473,2s | 10118,8 | 49207,6 |

**schema ad-hoc:** in modalità interattiva dovresti essere in grado di leggere un massimo di 5 milioni di righe (~5,36 GB di dati su disco) di dati non XDM in meno di 3 minuti. In modalità batch dovresti essere in grado di leggere un massimo di 1 miliardo di righe (~1.05 TB di dati su disco) di dati non XDM in circa 16 minuti.

| Numero di righe | 1K | 10.000 | 100.000 | 1M | 2M | 3M | 5M | 10 M | 50 M | 100 M | 500 M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Dimensioni su disco | 1,12 MB | 11,24 MB | 109,48 MB | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1,05 TB |
| Modalità interattiva SDK (in secondi) | 35,7 s | 31 s | 19,5 s | 25,3 s | 23 s | 33,2 s | 25,5 s | - | - | - | - | - |
| Modalità batch SDK (in secondi) | 448,8 s | 459,7 s | 519 | 475,8 s | 599,9 s | 347,6 s | 407,8 s | 397 s | 518,8 s | 487,9 s | 760,2 s | 975,4 s |

## Notebook Python {#python-notebook}

[!DNL Python] i notebook consentono di impaginare i dati quando si accede ai set di dati. Di seguito è illustrato un codice di esempio per leggere i dati con e senza impaginazione. Per ulteriori informazioni sui notebook Python disponibili, visita la sezione [[!DNL JupyterLab] Launcher](./overview.md#launcher) nella guida utente di JupyterLab .

La documentazione di Python riportata di seguito delinea i seguenti concetti:

- [Lettura da un set di dati](#python-read-dataset)
- [Scrivere in un set di dati](#write-python)
- [Dati query](#query-data-python)
- [Filtrare i dati ExperienceEvent](#python-filter)

### Leggi da un set di dati in Python {#python-read-dataset}

**Senza impaginazione:**

L&#39;esecuzione del codice seguente leggerà l&#39;intero set di dati. Se l’esecuzione ha esito positivo, i dati verranno salvati come dataframe panda a cui fa riferimento la variabile `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Con impaginazione:**

L&#39;esecuzione del codice seguente leggerà i dati dal set di dati specificato. La paginazione si ottiene limitando e compensando i dati attraverso le funzioni `limit()` e `offset()` rispettivamente. I dati limitanti si riferiscono al numero massimo di punti di dati da leggere, mentre l’offset si riferisce al numero di punti di dati da ignorare prima di leggere i dati. Se l’operazione di lettura viene eseguita correttamente, i dati verranno salvati come dataframe di dati Pandas a cui fa riferimento la variabile `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Scrivi in un set di dati in Python {#write-python}

Per scrivere in un set di dati nel notebook JupyterLab, seleziona la scheda Icona Dati (evidenziata di seguito) nella navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** . Seleziona **[!UICONTROL Datasets]** e fai clic con il pulsante destro del mouse, quindi seleziona l’opzione **[!UICONTROL Write Data in Notebook]** dal menu a discesa del set di dati che desideri utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.

![](../images/jupyterlab/data-access/write-dataset.png)

- Utilizza **[!UICONTROL Write Data in Notebook]** per generare una cella di scrittura con il set di dati selezionato.
- Utilizza **[!UICONTROL Explore Data in Notebook]** per generare una cella di lettura con il set di dati selezionato.
- Utilizza **[!UICONTROL Query Data in Notebook]** per generare una cella di query di base con il set di dati selezionato.

In alternativa, puoi copiare e incollare la seguente cella di codice. Sostituisci sia `{DATASET_ID}` che `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Dati query utilizzando [!DNL Query Service] in [!DNL Python] {#query-data-python}

[!DNL JupyterLab] su  [!DNL Platform] consente di utilizzare SQL in un  [!DNL Python] blocco appunti per accedere ai dati tramite il servizio Query  [Adobe Experience Platform](https://www.adobe.com/go/query-service-home-en). L’accesso ai dati tramite [!DNL Query Service] può essere utile per gestire set di dati di grandi dimensioni a causa dei suoi tempi di esecuzione superiori. È consigliabile che l’esecuzione di query sui dati utilizzando [!DNL Query Service] abbia un limite di tempo di elaborazione di dieci minuti.

Prima di utilizzare [!DNL Query Service] in [!DNL JupyterLab], assicurati di avere familiarità con la [[!DNL Query Service] sintassi SQL](https://www.adobe.com/go/query-service-sql-syntax-en).

Per eseguire la query dei dati utilizzando [!DNL Query Service] è necessario fornire il nome del set di dati di destinazione. Puoi generare le celle di codice necessarie trovando il set di dati desiderato utilizzando **[!UICONTROL Data explorer]**. Fai clic con il pulsante destro del mouse sull’elenco dei set di dati e fai clic su **[!UICONTROL Query Data in Notebook]** per generare due celle di codice nel blocco appunti. Queste due celle sono descritte più dettagliatamente di seguito.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Per utilizzare [!DNL Query Service] in [!DNL JupyterLab], è innanzitutto necessario creare una connessione tra il blocco appunti in uso [!DNL Python] e [!DNL Query Service]. Questo può essere ottenuto eseguendo la prima cella generata.

```python
qs_connect()
```

Nella seconda cella generata, la prima riga deve essere definita prima della query SQL. Per impostazione predefinita, la cella generata definisce una variabile opzionale (`df0`) che salva i risultati della query come dataframe panda. <br>L&#39; `-c QS_CONNECTION` argomento è obbligatorio e indica al kernel di eseguire la query SQL su  [!DNL Query Service]. Per un elenco di argomenti aggiuntivi, vedere l&#39; [appendice](#optional-sql-flags-for-query-service) .

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

È possibile fare riferimento direttamente alle variabili Python all&#39;interno di una query SQL utilizzando la sintassi in formato stringa e racchiudendo le variabili tra parentesi graffe (`{}`), come illustrato nell&#39;esempio seguente:

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

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti [!DNL Python], è necessario fornire l&#39;ID del set di dati (`{DATASET_ID}`) insieme alle regole di filtro che definiscono un intervallo di tempo specifico utilizzando gli operatori logici. Quando viene definito un intervallo di tempo, qualsiasi impaginazione specifica viene ignorata e viene considerato l’intero set di dati.

Di seguito è descritto un elenco di operatori di filtro:

- `eq()`: Uguale a
- `gt()`: Maggiore di
- `ge()`: Maggiore o uguale a
- `lt()`: Minore di
- `le()`: Minore o uguale a
- `And()`: Operatore AND logico
- `Or()`: Operatore OR logico

La cella seguente filtra un set di dati [!DNL ExperienceEvent] in base ai dati esistenti esclusivamente tra il 1° gennaio 2019 e la fine del 31 dicembre 2019.

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

I notebook R consentono di impaginare i dati quando si accede ai set di dati. Di seguito è illustrato un codice di esempio per leggere i dati con e senza impaginazione. Per ulteriori informazioni sui notebook R disponibili, visita la sezione [[!DNL JupyterLab] Launcher](./overview.md#launcher) nella guida utente di JupyterLab .

La documentazione R riportata di seguito delinea i seguenti concetti:

- [Lettura da un set di dati](#r-read-dataset)
- [Scrivere in un set di dati](#write-r)
- [Filtrare i dati ExperienceEvent](#r-filter)

### Leggi da un set di dati in R {#r-read-dataset}

**Senza impaginazione:**

L&#39;esecuzione del codice seguente leggerà l&#39;intero set di dati. Se l’esecuzione ha esito positivo, i dati verranno salvati come dataframe panda a cui fa riferimento la variabile `df0`.

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

L&#39;esecuzione del codice seguente leggerà i dati dal set di dati specificato. La paginazione si ottiene limitando e compensando i dati attraverso le funzioni `limit()` e `offset()` rispettivamente. I dati limitanti si riferiscono al numero massimo di punti di dati da leggere, mentre l’offset si riferisce al numero di punti di dati da ignorare prima di leggere i dati. Se l’operazione di lettura viene eseguita correttamente, i dati verranno salvati come dataframe di dati Pandas a cui fa riferimento la variabile `df0`.

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

### Scrivi in un set di dati in R {#write-r}

Per scrivere in un set di dati nel notebook JupyterLab, seleziona la scheda Icona Dati (evidenziata di seguito) nella navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** . Seleziona **[!UICONTROL Datasets]** e fai clic con il pulsante destro del mouse, quindi seleziona l’opzione **[!UICONTROL Write Data in Notebook]** dal menu a discesa del set di dati che desideri utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Utilizza **[!UICONTROL Write Data in Notebook]** per generare una cella di scrittura con il set di dati selezionato.
- Utilizza **[!UICONTROL Explore Data in Notebook]** per generare una cella di lettura con il set di dati selezionato.

In alternativa, puoi copiare e incollare la seguente cella di codice:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtrare i dati [!DNL ExperienceEvent] {#r-filter}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti R, è necessario fornire l&#39;ID del set di dati (`{DATASET_ID}`) insieme alle regole di filtro che definiscono un intervallo di tempo specifico utilizzando gli operatori logici. Quando viene definito un intervallo di tempo, qualsiasi impaginazione specifica viene ignorata e viene considerato l’intero set di dati.

Di seguito è descritto un elenco di operatori di filtro:

- `eq()`: Uguale a
- `gt()`: Maggiore di
- `ge()`: Maggiore o uguale a
- `lt()`: Minore di
- `le()`: Minore o uguale a
- `And()`: Operatore AND logico
- `Or()`: Operatore OR logico

La cella seguente filtra un set di dati [!DNL ExperienceEvent] in base ai dati esistenti esclusivamente tra il 1° gennaio 2019 e la fine del 31 dicembre 2019.

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

La documentazione di PySpark riportata di seguito delinea i seguenti concetti:

- [Inizializza sparkSession](#spark-initialize)
- [Lettura e scrittura di dati](#magic)
- [Creare un dataframe locale](#pyspark-create-dataframe)
- [Filtrare i dati ExperienceEvent](#pyspark-filter-experienceevent)

### Inizializzazione di sparkSession {#spark-initialize}

Tutti i notebook [!DNL Spark] 2.4 richiedono l’inizializzazione della sessione con il seguente codice standard.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Utilizzo di %dataset per leggere e scrivere con un blocco appunti PySpark 3 {#magic}

Con l&#39;introduzione di [!DNL Spark] 2.4, `%dataset` la magia personalizzata viene fornita per l&#39;uso nei notebook PySpark 3 ([!DNL Spark] 2.4). Per maggiori dettagli sui comandi magici disponibili nel kernel IPython, visita la [documentazione magica IPython](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Utilizzo**

```scala
%dataset {action} --datasetId {id} --dataFrame {df}`
```

**Descrizione**

Comando [!DNL Data Science Workspace] magico personalizzato per la lettura o la scrittura di un set di dati da un blocco appunti [!DNL PySpark] ([!DNL Python] 3 kernel).

| Nome | Descrizione | Obbligatorio |
| --- | --- | --- |
| `{action}` | Tipo di azione da eseguire sul set di dati. Sono disponibili due azioni: &quot;read&quot; o &quot;write&quot;. | Sì |
| `--datasetId {id}` | Utilizzato per fornire l&#39;ID del set di dati da leggere o scrivere. | Sì |
| `--dataFrame {df}` | Il dataframe panda. <ul><li> Quando l&#39;azione è &quot;read&quot;, {df} è la variabile in cui sono disponibili i risultati dell&#39;operazione di lettura del set di dati. </li><li> Quando l&#39;azione è &quot;write&quot;, il dataframe {df} viene scritto nel set di dati. </li></ul> | Sì |
| `--mode` | Un parametro aggiuntivo che modifica la modalità di lettura dei dati. I parametri consentiti sono &quot;batch&quot; e &quot;interattivo&quot;. Per impostazione predefinita, la modalità è impostata su &quot;interattivo&quot;. Si consiglia di utilizzare la modalità &quot;batch&quot; durante la lettura di grandi quantità di dati. | No |

>[!TIP]
>
>Controlla le tabelle PySpark all&#39;interno della sezione [limiti dei dati del notebook](#notebook-data-limits) per determinare se `mode` deve essere impostato su `interactive` o `batch`.

**Esempi**

- **Esempio** di lettura:  `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **Esempio** di scrittura:  `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

Puoi generare automaticamente gli esempi di cui sopra in JupyterLab buy utilizzando il seguente metodo:

Seleziona la scheda Icona Dati (evidenziata di seguito) nella navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** . Seleziona **[!UICONTROL Datasets]** e fai clic con il pulsante destro del mouse, quindi seleziona l’opzione **[!UICONTROL Write Data in Notebook]** dal menu a discesa del set di dati che desideri utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.

- Utilizzare **[!UICONTROL Explore Data in Notebook]** per generare una cella di lettura.
- Utilizza **[!UICONTROL Write Data in Notebook]** per generare una cella di scrittura.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Creare un dataframe locale {#pyspark-create-dataframe}

Per creare un dataframe locale utilizzando PySpark 3, utilizzare le query SQL. Esempio:

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
>Puoi anche specificare un campione di seed facoltativo, ad esempio un valore booleano con sostituzione, doppia frazione o un valore di seed lungo.

### Filtrare i dati [!DNL ExperienceEvent] {#pyspark-filter-experienceevent}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti PySpark è necessario fornire l&#39;identità del set di dati (`{DATASET_ID}`), l&#39;identità IMS della propria organizzazione e le regole del filtro che definiscono un intervallo di tempo specifico. Un intervallo di tempo di filtro viene definito utilizzando la funzione `spark.sql()`, dove il parametro della funzione è una stringa di query SQL.

Le celle seguenti filtrano un set di dati [!DNL ExperienceEvent] in base ai dati esistenti esclusivamente tra il 1° gennaio 2019 e la fine del 31 dicembre 2019.

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
- [Leggere un set di dati](#read-scala-dataset)
- [Scrivere in un set di dati](#scala-write-dataset)
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

In Scala, puoi importare `clientContext` per ottenere e restituire i valori di Platform, eliminando la necessità di definire variabili quali `var userToken`. Nell’esempio di Scala seguente, `clientContext` viene utilizzato per ottenere e restituire tutti i valori richiesti necessari per la lettura di un set di dati.

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
| df1 | Variabile che rappresenta il dataframe panda utilizzato per leggere e scrivere i dati. |
| user-token | Il token utente viene recuperato automaticamente utilizzando `clientContext.getUserToken()`. |
| service-token | Il token di servizio viene recuperato automaticamente utilizzando `clientContext.getServiceToken()`. |
| ims-org | L’ID organizzazione IMS viene recuperato automaticamente utilizzando `clientContext.getOrgId()`. |
| api-key | Chiave API recuperata automaticamente utilizzando `clientContext.getApiKey()`. |

>[!TIP]
>
>Rivedere le tabelle Scala all&#39;interno della sezione [limiti dei dati del blocco appunti](#notebook-data-limits) per determinare se `mode` deve essere impostato su `interactive` o `batch`.

Puoi generare automaticamente l&#39;esempio precedente in JupyterLab buy utilizzando il seguente metodo:

Seleziona la scheda Icona Dati (evidenziata di seguito) nella navigazione a sinistra di JupyterLab. Vengono visualizzate le directory **[!UICONTROL Datasets]** e **[!UICONTROL Schemas]** . Seleziona **[!UICONTROL Datasets]** e fai clic con il pulsante destro del mouse, quindi seleziona l’opzione **[!UICONTROL Explore Data in Notebook]** dal menu a discesa del set di dati che desideri utilizzare. Nella parte inferiore del blocco appunti viene visualizzata una voce di codice eseguibile.
E
- Utilizzare **[!UICONTROL Explore Data in Notebook]** per generare una cella di lettura.
- Utilizza **[!UICONTROL Write Data in Notebook]** per generare una cella di scrittura.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Scrivere in un set di dati {#scala-write-dataset}

In Scala, puoi importare `clientContext` per ottenere e restituire i valori di Platform, eliminando la necessità di definire variabili quali `var userToken`. Nell’esempio di Scala seguente, `clientContext` viene utilizzato per definire e restituire tutti i valori richiesti necessari per la scrittura in un set di dati.

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

| elemento | descrizione |
| ------- | ----------- |
| df1 | Variabile che rappresenta il dataframe panda utilizzato per leggere e scrivere i dati. |
| user-token | Il token utente viene recuperato automaticamente utilizzando `clientContext.getUserToken()`. |
| service-token | Il token di servizio viene recuperato automaticamente utilizzando `clientContext.getServiceToken()`. |
| ims-org | L’ID organizzazione IMS viene recuperato automaticamente utilizzando `clientContext.getOrgId()`. |
| api-key | Chiave API recuperata automaticamente utilizzando `clientContext.getApiKey()`. |

>[!TIP]
>
>Rivedere le tabelle Scala all&#39;interno della sezione [limiti dei dati del blocco appunti](#notebook-data-limits) per determinare se `mode` deve essere impostato su `interactive` o `batch`.

### creare un dataframe locale {#scala-create-dataframe}

Per creare un dataframe locale utilizzando Scala, sono necessarie query SQL. Esempio:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtrare i dati [!DNL ExperienceEvent] {#scala-experienceevent}

Per accedere e filtrare un set di dati [!DNL ExperienceEvent] in un blocco appunti Scala è necessario fornire l&#39;identità del set di dati (`{DATASET_ID}`), l&#39;identità IMS della propria organizzazione e le regole del filtro che definiscono un intervallo di tempo specifico. Un intervallo di tempo di filtro viene definito utilizzando la funzione `spark.sql()`, dove il parametro della funzione è una stringa di query SQL.

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

Questo documento illustra le linee guida generali per l’accesso ai set di dati utilizzando i notebook JupyterLab. Per esempi più approfonditi sulla query dei set di dati, visita la documentazione [Query Service in JupyterLab Notebook](./query-service.md) . Per ulteriori informazioni su come esplorare e visualizzare i set di dati, visita il documento relativo all’ [analisi dei dati tramite blocchi appunti](./analyze-your-data.md).

## Flag SQL facoltativi per [!DNL Query Service] {#optional-sql-flags-for-query-service}

Questa tabella delinea i flag SQL facoltativi che possono essere utilizzati per [!DNL Query Service].

| **Flag** | **Descrizione** |
| --- | --- |
| `-h`, `--help` | Visualizza il messaggio della guida e esci. |
| `-n`,  `--notify` | Attiva/disattiva l&#39;opzione per la notifica dei risultati della query. |
| `-a`,  `--async` | L’utilizzo di questo flag esegue la query in modo asincrono e può liberare il kernel durante l’esecuzione della query. Presta attenzione quando assegni i risultati della query alle variabili, in quanto potrebbe non essere definita se la query non è completa. |
| `-d`,  `--display` | L’utilizzo di questo flag impedisce la visualizzazione dei risultati. |
