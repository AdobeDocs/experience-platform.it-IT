---
keywords: Experience Platform;home;argomenti popolari;accesso ai dati;python sdk;api di accesso ai dati;python di lettura;python di scrittura
solution: Experience Platform
title: Accesso ai dati con Python in Data Science Workspace
type: Tutorial
description: Il seguente documento contiene esempi su come accedere ai dati in Python per l’utilizzo in Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Accesso ai dati con Python in Data Science Workspace

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

Il documento seguente contiene esempi su come accesso dati usando Python per l&#39;uso in Data Science Area di lavoro. Per informazioni sull&#39;accesso ai dati utilizzando i notebook JupyterLab, visita i dati accesso](../jupyterlab/access-notebook-data.md) la documentazione dei [notebook JupyterLab.

## Lettura di un dataset

Dopo aver impostato le variabili di ambiente e completato l&#39;installazione, il set di dati può ora essere letto nel frame di dati di pandas.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### SELEZIONA colonne dal set di dati

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Ottenere informazioni sul partizionamento:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Clausola DISTINCT

La clausola DISTINCT consente di recuperare tutti i valori distinti a livello di riga/colonna, rimuovendo tutti i valori duplicati dalla risposta.

Di seguito è riportato un esempio di utilizzo della funzione `distinct()`:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### Clausola WHERE

È possibile usare determinati operatori in Python per filtrare il set di dati.

>[!NOTE]
>
>Le funzioni utilizzate per filtrare fanno distinzione tra maiuscole e minuscole.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

Di seguito è riportato un esempio dell&#39;utilizzo di queste funzioni di filtro:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### Clausola ORDINA BY

La clausola ORDER BY consente di ordinare i risultati ricevuti in base a una colonna specifica in un ordine specifico (crescente o decrescente). Questa operazione viene eseguita utilizzando la `sort()` funzione.

Di seguito è riportato un esempio di utilizzo della funzione `sort()`:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### clausola LIMIT

La clausola LIMIT consente di limitare il numero di record ricevuti dal set di dati.

Di seguito è riportato un esempio di utilizzo della funzione `limit()`:

```python
df = dataset_reader.limit(100).read()
```

### clausola OFFSET

La clausola OFFSET consente di saltare le righe, dall&#39;inizio, per iniziare a restituire le righe da un punto successivo. In combinazione con LIMIT, può essere utilizzato per iterare le righe in blocchi.

Di seguito è riportato un esempio dell&#39;utilizzo `offset()` della funzione:

```python
df = dataset_reader.offset(100).read()
```

## Scrittura di un dataset

Per scrivere in un dataset, è necessario fornire il frame di dati pandas al dataset.

### Scrittura del frame di dati dei panda

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Directory dello spazio utente (Checkpointing)

Per i processi con tempi di esecuzione più lunghi, potrebbe essere necessario memorizzare i passaggi intermedi. In casi come questo, puoi leggere e scrivere in uno spazio utente.

>[!NOTE]
>
>I percorsi dei dati sono **non** archiviati. È necessario memorizzare il percorso corrispondente ai rispettivi dati.

### Scrivi nello spazio utenti

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Leggi dallo spazio utente

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Passaggi successivi

Adobe Experience Platform Data Science Area di lavoro fornisce un esempio di ricetta in cui vengono utilizzati gli esempi di codice precedenti per leggere e scrivere dati. Per ulteriori informazioni su come usare Python per accedere ai dati, consulta l&#39;archivio [GitHub di Data Science Area di lavoro Python](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
