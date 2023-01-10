---
keywords: Experience Platform;home;argomenti popolari;accesso ai dati;python sdk;api di accesso ai dati;read python;write python
solution: Experience Platform
title: Accesso ai dati tramite Python in Data Science Workspace
type: Tutorial
description: Il seguente documento contiene esempi su come accedere ai dati in Python da utilizzare in Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Accesso ai dati tramite Python in Data Science Workspace

Il seguente documento contiene esempi su come accedere ai dati utilizzando Python per l’utilizzo in Data Science Workspace. Per informazioni sull&#39;accesso ai dati tramite i notebook JupyterLab, visita [Accesso ai dati dei notebook JupyterLab](../jupyterlab/access-notebook-data.md) documentazione.

## Lettura di un set di dati

Dopo aver impostato le variabili di ambiente e aver completato l&#39;installazione, il set di dati può ora essere letto nel dataframe di panda.

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

### Ottieni informazioni sul partizionamento:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### clausola DISTINCT

La clausola DISTINCT consente di recuperare tutti i valori distinti a livello di riga/colonna, rimuovendo tutti i valori duplicati dalla risposta.

Un esempio di utilizzo del `distinct()` funzionalità di seguito:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### clausola WHERE

Puoi utilizzare alcuni operatori in Python per filtrare il set di dati.

>[!NOTE]
>
>Le funzioni utilizzate per il filtraggio sono sensibili all’uso di maiuscole e minuscole.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

Di seguito è riportato un esempio di utilizzo di queste funzioni di filtro:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### Clausola ORDER BY

La clausola ORDER BY consente di ordinare i risultati ricevuti in base a una colonna specifica in un ordine specifico (crescente o decrescente). A tale scopo, utilizza le `sort()` funzione .

Un esempio di utilizzo del `sort()` funzionalità di seguito:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Clausola LIMIT

La clausola LIMIT ti consente di limitare il numero di record ricevuti dal set di dati.

Un esempio di utilizzo del `limit()` funzionalità di seguito:

```python
df = dataset_reader.limit(100).read()
```

### Clausola OFFSET

La clausola OFFSET consente di saltare le righe dall&#39;inizio per iniziare a restituire le righe da un punto successivo. In combinazione con LIMIT, può essere utilizzato per iterare le righe nei blocchi.

Un esempio di utilizzo del `offset()` funzionalità di seguito:

```python
df = dataset_reader.offset(100).read()
```

## Scrittura di un set di dati

Per scrivere in un set di dati, è necessario fornire il dataframe panda al set di dati.

### Scrittura del dataframe dei panda

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Directory degli spazi utente (Checkpoint)

Per i lavori più lunghi, potrebbe essere necessario memorizzare i passaggi intermedi. In casi come questo, è possibile leggere e scrivere in uno spazio utente.

>[!NOTE]
>
>I percorsi dei dati sono **not** memorizzato. È necessario memorizzare il percorso corrispondente ai relativi dati.

### Scrivi nello spazio utente

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Leggi da userspace

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Passaggi successivi

Adobe Experience Platform Data Science Workspace fornisce un esempio di ricetta che utilizza gli esempi di codice riportati sopra per leggere e scrivere i dati. Per ulteriori informazioni su come utilizzare Python per accedere ai dati, consulta la [Archivio GitHub Python di Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
