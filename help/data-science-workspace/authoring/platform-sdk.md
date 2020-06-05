---
keywords: Experience Platform;developer guide;SDK;Data Access SDK;Data Science Workspace;popular topics
solution: Experience Platform
title: Guida all'SDK per la piattaforma
topic: SDK authoring
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 2%

---


# Guida all&#39;SDK per la piattaforma

Questa esercitazione fornisce informazioni sulla conversione `data_access_sdk_python` al nuovo Python `platform_sdk` sia in Python che in R. Questa esercitazione fornisce informazioni sulle operazioni seguenti:

- [Autenticazione build](#build-authentication)
- [Lettura di base dei dati](#basic-reading-of-data)
- [Scrittura di base dei dati](#basic-writing-of-data)

## Autenticazione build {#build-authentication}

L’autenticazione è necessaria per effettuare chiamate a [!DNL Adobe Experience Platform]e comprende chiave API, ID organizzazione IMS, token utente e token di servizio.

### Python

Se si utilizza il blocco appunti Jupyter, utilizzare il codice seguente per creare il `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Se non si utilizza il blocco appunti Jupyter o è necessario modificare l&#39;organizzazione IMS, utilizzare il seguente esempio di codice:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Se si utilizza il blocco appunti Jupyter, utilizzare il codice seguente per creare il `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Se non si utilizza il blocco appunti Jupyter o è necessario modificare l&#39;organizzazione IMS, utilizzare il seguente esempio di codice:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Lettura di base dei dati {#basic-reading-of-data}

Con il nuovo SDK della piattaforma, la dimensione massima di lettura è 32 GB, con un tempo massimo di lettura di 10 minuti.

Se il tempo di lettura è troppo lungo, è possibile provare a utilizzare una delle seguenti opzioni di filtro:

- [Filtrare i dati per offset e limite](#filter-by-offset-and-limit)
- [Filtrare i dati per data](#filter-by-date)
- [Filtrare i dati per colonna](#filter-by-selected-columns)
- [Ottenimento dei risultati ordinati](#get-sorted-results)

>[!NOTE] L’organizzazione IMS è impostata all’interno dell’ `client_context`.

### Python

Per leggere i dati in Python, si prega di utilizzare l&#39;esempio di codice seguente:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Per leggere i dati in R, utilizzare l&#39;esempio di codice seguente:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtrare per offset e limite {#filter-by-offset-and-limit}

Poiché il filtro per ID batch non è più supportato, per estendere la lettura dei dati è necessario utilizzare `offset` e `limit`.

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

## Filtrare per data {#filter-by-date}

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

Il nuovo SDK della piattaforma supporta le seguenti operazioni:

| Funzionamento | Funzione |
| --------- | -------- |
| È uguale a (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| Maggiore o uguale a (`>=`) | `ge()` |
| Less than (`<`) | `lt()` |
| Minore o uguale a (`<=`) | `le()` |
| And (`&`) | `And()` |
| Oppure (`|`) | `Or()` |

## Filtra per colonne selezionate {#filter-by-selected-columns}

Per migliorare ulteriormente la lettura dei dati, è inoltre possibile filtrare in base al nome della colonna.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Ottieni risultati ordinati {#get-sorted-results}

I risultati ricevuti possono essere ordinati in base alle colonne specificate del dataset di destinazione e nel relativo ordine (asc/desc), rispettivamente.

Nell&#39;esempio seguente, i dataframe vengono ordinati per &quot;colonna-a&quot; in ordine crescente. Le righe con gli stessi valori per &quot;colonna-a&quot; vengono quindi ordinate per &quot;colonna-b&quot; in ordine decrescente.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Scrittura di base dei dati {#basic-writing-of-data}

>[!NOTE] L’organizzazione IMS è impostata all’interno dell’ `client_context`.

Per scrivere dati in Python e R, utilizzare uno dei seguenti esempi:

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

Una volta configurato il `platform_sdk` data loader, i dati vengono preparati e quindi suddivisi nei `train` set di dati e `val` nei set di dati. Per saperne di più sulla preparazione dei dati e sulla progettazione di funzionalità, consulta la sezione sulla preparazione [dei dati e la progettazione](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering) di funzionalità nell&#39;esercitazione per la creazione di una ricetta con i notebook JupyterLab.