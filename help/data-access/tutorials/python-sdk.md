---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Secure Python Data Access SDK
topic: tutorial
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Secure [!DNL Python][!DNL Data Access] SDK

Secure [!DNL Python][!DNL Data Access] SDK è un kit di sviluppo software che consente di leggere e scrivere set di dati da  Adobe Experience Platform.

## Introduzione

Per poter accedere ai valori per effettuare chiamate all’SDK di protezione, devi completare l’esercitazione [di autenticazione](../../tutorials/authentication.md) [!DNL Python][!DNL Data Access] :

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. L’utilizzo dell’ [!DNL Python] SDK richiede il nome e l’ID della sandbox in cui avrà luogo l’operazione:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

## Configurazione dell&#39;ambiente

Per impostazione predefinita, gli endpoint del servizio sono impostati sugli endpoint dell&#39;ambiente di integrazione. Di conseguenza, per puntare alla produzione, impostate le seguenti variabili di ambiente sui seguenti valori:

| Variable | Endpoint |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

Inoltre, le credenziali possono essere aggiunte come variabili di ambiente.

| Variable | Valore |
| -------- | ----- |
| `ORG_ID` | Your `{IMS_ORG}` ID. |
| `SERVICE_API_KEY` | Il vostro `{API_KEY}` valore. |
| `USER_TOKEN` | Il vostro `{ACCESS_TOKEN}` valore. |
| `SERVICE_TOKEN` | Utente `{SERVICE_TOKEN}`, che potrebbe essere necessario autorizzare richieste per canali back-channel tra i servizi. |
| `SANDBOX_ID` | Il `{SANDBOX_ID}` valore della sandbox. |
| `SANDBOX_NAME` | Il `{SANDBOX_NAME}` valore della sandbox. |

## Installazione

Tutti i pacchetti vengono inviati `./dist` dopo la creazione.

### Ruota

```python
python3 setup.py bdist_wheel --universal
```

Dalla directory del progetto, caricate la ruota nell’ambiente [!DNL Python] 3.

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### Egg, file

```python
python3 setup.py bdist_egg
```

## Lettura di un dataset

Dopo aver impostato le variabili di ambiente e aver completato l&#39;installazione, il dataset ora può essere letto nel dataframe di panda.

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### SELEZIONARE le colonne dal dataset

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Ottieni informazioni sul partizionamento:

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Clausola DISTINCT

La clausola DISTINCT consente di recuperare tutti i valori distinti a livello di riga/colonna, rimuovendo tutti i valori duplicati dalla risposta.

Di seguito è riportato un esempio di utilizzo della `distinct()` funzione:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### Clausola WHERE

L&#39; [!DNL Python] SDK supporta alcuni operatori per filtrare il set di dati.

>[!NOTE] Le funzioni utilizzate per il filtraggio sono con distinzione tra maiuscole e minuscole.

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

La clausola ORDER BY consente di ordinare i risultati ricevuti in base a una colonna specificata in un ordine specifico (crescente o decrescente). Nell’ [!DNL Python] SDK, questa operazione viene eseguita utilizzando la `sort()` funzione.

Di seguito è riportato un esempio di utilizzo della `sort()` funzione:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Clausola LIMIT

La clausola LIMIT consente agli utenti di limitare il numero di record ricevuti dall&#39;insieme di dati.

Di seguito è riportato un esempio di utilizzo della `limit()` funzione:

```python
df = dataset_reader.limit(100).read()
```

### Clausola OFFSET

La clausola OFFSET consente agli utenti di saltare le righe dall&#39;inizio per iniziare a restituire le righe da un punto successivo. In combinazione con LIMIT, può essere utilizzato per iterare le righe nei blocchi.

Di seguito è riportato un esempio di utilizzo della `offset()` funzione:

```python
df = dataset_reader.offset(100).read()
```

## Scrittura di un dataset

L&#39; [!DNL Python] SDK supporta la scrittura di set di dati. Gli utenti dovranno fornire il fotogramma dati panda che deve essere scritto nel dataset.

### Creazione di un fotogramma dati panda

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## Directory di Userspace (Checkpoint)

Per i processi più lunghi, gli utenti potrebbero dover memorizzare i passaggi intermedi. In casi come questo, l&#39; [!DNL Python] SDK fornisce all&#39;utente la possibilità di leggere e scrivere in un userspace.

>!![NOTE] I percorsi dei dati **non** sono memorizzati dall’SDK. Gli utenti dovranno memorizzare il percorso corrispondente ai rispettivi dati.

### Scrivi in userspace

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Lettura da userspace

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
