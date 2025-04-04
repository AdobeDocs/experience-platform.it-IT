---
keywords: Experience Platform;guida per sviluppatori;SDK;Data Access SDK;Data Science Workspace;argomenti più comuni
solution: Experience Platform
title: Authoring di modelli con Adobe Experience Platform SDK
description: Questa esercitazione fornisce informazioni sulla conversione di data_access_sdk_python nel nuovo Python platform_sdk sia in Python che in R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 3%

---

# Creazione di modelli con Adobe [!DNL Experience Platform] SDK

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Questa esercitazione fornisce informazioni sulla conversione di `data_access_sdk_python` nel nuovo Python `platform_sdk` sia in Python che in R. Questo tutorial fornisce informazioni sulle seguenti operazioni:

- [Genera autenticazione](#build-authentication)
- [Lettura di base dei dati](#basic-reading-of-data)
- [Scrittura di base dei dati](#basic-writing-of-data)

## Genera autenticazione {#build-authentication}

Per effettuare chiamate a [!DNL Adobe Experience Platform] è necessaria l&#39;autenticazione, che comprende la chiave API, l&#39;ID organizzazione, un token utente e un token di servizio.

### Python

Se si utilizza Jupyter Notebook, utilizzare il codice seguente per generare `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Se non utilizzi Jupyter Notebook o se devi cambiare l’organizzazione, utilizza il seguente codice di esempio:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Se si utilizza Jupyter Notebook, utilizzare il codice seguente per generare `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Se non utilizzi Jupyter Notebook o se devi cambiare organizzazione, utilizza il seguente codice di esempio:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Lettura di base dei dati {#basic-reading-of-data}

Con il nuovo SDK [!DNL Experience Platform], la dimensione massima di lettura è di 32 GB, con un tempo massimo di lettura di 10 minuti.

Se il tempo di lettura richiede troppo tempo, puoi provare a utilizzare una delle seguenti opzioni di filtro:

- [Filtraggio dei dati per offset e limite](#filter-by-offset-and-limit)
- [Filtrare i dati per data](#filter-by-date)
- [Filtrare i dati per colonna](#filter-by-selected-columns)
- [Recupero risultati ordinati](#get-sorted-results)

>[!NOTE]
>
>L&#39;organizzazione è impostata in `client_context`.

### Python

Per leggere i dati in Python, usa il codice di esempio seguente:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Per leggere i dati in R, utilizza il codice di esempio seguente:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtra per offset e limite {#filter-by-offset-and-limit}

Poiché il filtro per ID batch non è più supportato, per eseguire la lettura dei dati è necessario utilizzare `offset` e `limit`.

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## Filtra per data {#filter-by-date}

La granularità del filtro delle date ora è definita dalla marca temporale, anziché essere impostata dal giorno.

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

Il nuovo SDK [!DNL Experience Platform] supporta le operazioni seguenti:

| Operazione | Funzione |
| --------- | -------- |
| È uguale a (`=`) | `eq()` |
| Maggiore di (`>`) | `gt()` |
| Maggiore o uguale a (`>=`) | `ge()` |
| Minore di (`<`) | `lt()` |
| Minore o uguale a (`<=`) | `le()` |
| E (`&`) | `And()` |
| Oppure (`|`) | `Or()` |

## Filtra per colonne selezionate {#filter-by-selected-columns}

Per perfezionare ulteriormente la lettura dei dati, puoi anche filtrare per nome di colonna.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Ottieni risultati ordinati {#get-sorted-results}

I risultati ricevuti possono essere ordinati in base a colonne specificate del set di dati di destinazione e nel loro ordine (asc/desc) rispettivamente.

Nell’esempio seguente, il dataframe è ordinato per &quot;colonna-a&quot; in ordine crescente. Le righe con gli stessi valori per &quot;column-a&quot; sono quindi ordinate per &quot;column-b&quot; in ordine decrescente.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Scrittura di base dei dati {#basic-writing-of-data}

>[!NOTE]
>
>L&#39;organizzazione è impostata in `client_context`.

Per scrivere i dati in Python e R, usate uno dei seguenti esempi:

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## Passaggi successivi

Dopo aver configurato il caricatore di dati `platform_sdk`, i dati vengono preparati e quindi suddivisi nei set di dati `train` e `val`. Per informazioni sulla preparazione dei dati e sulla progettazione delle funzionalità, visitare la sezione relativa alla [preparazione dei dati e alla progettazione delle funzionalità](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) nell&#39;esercitazione per la creazione di una ricetta utilizzando [!DNL JupyterLab] notebook.
