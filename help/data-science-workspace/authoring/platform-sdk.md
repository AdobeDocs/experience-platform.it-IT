---
keywords: Experience Platform;guida per sviluppatori;SDK;Data Access SDK;Data Science Workspace;argomenti comuni
solution: Experience Platform
title: Authoring dei modelli con l’SDK della piattaforma Adobe Experience Platform
description: Questa esercitazione fornisce informazioni sulla conversione di data_access_sdk_python nel nuovo Python platform_sdk sia in Python che in R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Authoring di modelli con Adobe Experience Platform [!DNL Platform] SDK

Questa esercitazione fornisce informazioni sulla conversione `data_access_sdk_python` al nuovo Python `platform_sdk` in Python e R. Questa esercitazione fornisce informazioni sulle seguenti operazioni:

- [Creare l’autenticazione](#build-authentication)
- [Lettura di base dei dati](#basic-reading-of-data)
- [Scrittura dei dati di base](#basic-writing-of-data)

## Creare l’autenticazione {#build-authentication}

È necessaria l’autenticazione per effettuare chiamate a [!DNL Adobe Experience Platform]ed è composto da chiave API, ID organizzazione IMS, un token utente e un token di servizio.

### Pitone

Se utilizzi Jupyter Notebook, utilizza il codice seguente per creare il `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Se non utilizzi Jupyter Notebook o hai bisogno di modificare l&#39;organizzazione IMS, utilizza il seguente codice di esempio:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Se utilizzi Jupyter Notebook, utilizza il codice seguente per creare il `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Se non utilizzi Jupyter Notebook o hai bisogno di modificare l&#39;organizzazione IMS, utilizza il seguente codice di esempio:

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

Con il nuovo [!DNL Platform] SDK, la dimensione massima di lettura è di 32 GB, con un tempo massimo di lettura di 10 minuti.

Se il tempo di lettura è troppo lungo, puoi provare a utilizzare una delle seguenti opzioni di filtro:

- [Filtrare i dati per offset e limite](#filter-by-offset-and-limit)
- [Filtrare i dati per data](#filter-by-date)
- [Filtrare i dati per colonna](#filter-by-selected-columns)
- [Risultati ordinati](#get-sorted-results)

>[!NOTE]
>
>L’organizzazione IMS è impostata all’interno della `client_context`.

### Pitone

Per leggere i dati in Python, si prega di utilizzare il codice di esempio qui sotto:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Per leggere i dati in R, utilizza il codice di esempio qui sotto:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtra per offset e limite {#filter-by-offset-and-limit}

Poiché il filtro per ID batch non è più supportato, per poter estendere la lettura dei dati è necessario utilizzare `offset` e `limit`.

### Pitone

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

La granularità del filtro data è ora definita dalla marca temporale, anziché essere impostata dal giorno.

### Pitone

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

Il nuovo [!DNL Platform] L&#39;SDK supporta le seguenti operazioni:

| Funzionamento | Funzione |
| --------- | -------- |
| È uguale a (`=`) | `eq()` |
| Maggiore di (`>`) | `gt()` |
| Maggiore o uguale a (`>=`) | `ge()` |
| Minore di (`<`) | `lt()` |
| Minore o uguale a (`<=`) | `le()` |
| E (`&`) | `And()` |
| Oppure (`|`) | `Or()` |

## Filtra per colonne selezionate {#filter-by-selected-columns}

Per perfezionare ulteriormente la lettura dei dati, puoi anche filtrare per nome della colonna.

### Pitone

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Ottieni risultati ordinati {#get-sorted-results}

I risultati ricevuti possono essere ordinati in base a colonne specifiche del set di dati di destinazione e nell’ordine corrispondente (rispettivamente asc/desc).

Nell&#39;esempio seguente, il dataframe viene ordinato per &quot;column-a&quot; prima in ordine crescente. Le righe con gli stessi valori per &quot;colonna-a&quot; vengono quindi ordinate per &quot;colonna-b&quot; in ordine decrescente.

### Pitone

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Scrittura dei dati di base {#basic-writing-of-data}

>[!NOTE]
>
>L’organizzazione IMS è impostata all’interno della `client_context`.

Per scrivere dati in Python e R, utilizza uno dei seguenti esempi:

### Pitone

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

Una volta configurato il `platform_sdk` data loader, i dati vengono preparati e quindi suddivisi in `train` e `val` set di dati. Per informazioni sulla preparazione dei dati e sull&#39;ingegneria delle funzioni, visita la sezione su [preparazione dei dati e ingegneria delle funzioni](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) nell’esercitazione per creare una ricetta utilizzando [!DNL JupyterLab] quaderni.
