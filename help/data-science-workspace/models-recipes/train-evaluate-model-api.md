---
keywords: Experience Platform;formazione e valutazione;Data Science Workspace;argomenti popolari;Sensei Machine Learning API
solution: Experience Platform
title: Formazione e valutazione di un modello utilizzando l’API di apprendimento automatico di Sensei
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione ti mostrerà come creare, addestrare e valutare un modello utilizzando le chiamate API Sensei Machine Learning.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 1%

---

# Addestra e valuta un modello utilizzando l’ API [!DNL Sensei Machine Learning]


Questa esercitazione ti mostrerà come creare, addestrare e valutare un modello utilizzando le chiamate API. Per un elenco dettagliato della documentazione API, fai riferimento a [questo documento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) .

## Prerequisiti

Per creare un motore, è necessario addestrare e valutare un modello utilizzando l&#39;API ](./import-packaged-recipe-api.md).[

Per iniziare a effettuare chiamate API, segui l&#39; [Experience Platform tutorial di autenticazione API](https://www.adobe.com/go/platform-api-authentication-en) .

Dall’esercitazione dovresti avere i seguenti valori:

- `{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.
- `{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.
- `{API_KEY}`: Il valore chiave API specifico si trova nell’integrazione Adobe Experience Platform univoca.

- Collegamento a un&#39;immagine Docker di un servizio intelligente

## Flusso di lavoro API

Utilizzeremo le API per creare un Experience Run per la formazione. Per questa esercitazione, ci occuperemo degli endpoint Engines, MLInances ed Experiments. Il grafico seguente illustra la relazione tra i tre e introduce anche l&#39;idea di un&#39;esecuzione e un modello.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>I termini &quot;Engine&quot;, &quot;MLInance&quot;, &quot;MLService&quot;, &quot;Experiment&quot; e &quot;Model&quot; sono indicati come termini diversi nell’interfaccia utente. Se provieni dall’interfaccia utente, la tabella seguente mappa le differenze.

| Termine interfaccia utente | Termine API |
| --- | --- |
| Ricetta | Motore |
| Modello | MLInance |
| Corsi di formazione | Esperimento |
| Servizio | MLService |

### Creare un&#39;istanza MLI

La creazione di un&#39;istanza MLI può essere effettuata utilizzando la richiesta seguente. Utilizzerai il `{ENGINE_ID}` restituito durante la creazione di un motore dal tutorial [Importa una composizione in pacchetto utilizzando l&#39;API](./import-packaged-recipe-ui.md).

**Richiesta**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.\
`{API_KEY}`: Il valore chiave API specifico si trova nell’integrazione Adobe Experience Platform univoca.\
`{JSON_PAYLOAD}`: La configurazione della nostra istanza MLI. L’esempio che utilizziamo nel nostro tutorial è mostrato qui:

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE]
>
>Nell’array `{JSON_PAYLOAD}` vengono definiti i parametri utilizzati per la formazione e il punteggio nell’array `tasks`. Il `{ENGINE_ID}` è l&#39;ID del motore che si desidera utilizzare e il campo `tag` è un parametro facoltativo utilizzato per identificare l&#39;istanza.

La risposta contiene il `{INSTANCE_ID}` che rappresenta l’istanza MLI creata. È possibile creare più istanze modello MLI con diverse configurazioni.

**Risposta**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`: Questo ID rappresenta il motore in cui viene creata l&#39;istanza MLI.\
`{INSTANCE_ID}`: L&#39;ID che rappresenta l&#39;istanza MLI.

### Creare un esperimento

Un esperimento viene utilizzato da uno scienziato informatico per arrivare ad un modello ad alte prestazioni durante l&#39;addestramento. Più esperimenti includono la modifica di set di dati, funzionalità, parametri di apprendimento e hardware. Di seguito è riportato un esempio di creazione di un esperimento.

**Richiesta**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{API_KEY}`: Il valore chiave API specifico si trova nell’integrazione Adobe Experience Platform univoca.\
`{JSON_PAYLOAD}`: Oggetto di esperimento creato. L’esempio che utilizziamo nel nostro tutorial è mostrato qui:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: L&#39;ID che rappresenta l&#39;istanza MLI.

La risposta dalla creazione dell’esperimento si presenta così.

**Risposta**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`: L’ID che rappresenta l’esperimento appena creato.
`{INSTANCE_ID}`: L&#39;ID che rappresenta l&#39;istanza MLI.

### Creare un esperimento pianificato per la formazione

Vengono utilizzati gli esperimenti pianificati in modo che non sia necessario creare ogni singolo esperimento eseguito tramite una chiamata API. Forniamo invece tutti i parametri necessari durante la creazione dell’esperimento e ogni esecuzione verrà creata periodicamente.

Per indicare la creazione di un esperimento pianificato, è necessario aggiungere una sezione `template` nel corpo della richiesta. In `template` sono inclusi tutti i parametri necessari per le esecuzioni di pianificazione, ad esempio `tasks`, che indicano quale azione e `schedule`, che indica la tempistica delle esecuzioni pianificate.

**Richiesta**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{API_KEY}`: Il valore chiave API specifico si trova nell’integrazione Adobe Experience Platform univoca.\
`{JSON_PAYLOAD}`: Set di dati da registrare. L’esempio che utilizziamo nel nostro tutorial è mostrato qui:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
                    }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

Quando creiamo un esperimento, il corpo `{JSON_PAYLOAD}` deve contenere il parametro `mlInstanceId` o il parametro `mlInstanceQuery`. In questo esempio, un esperimento pianificato richiama un&#39;esecuzione ogni 20 minuti, impostata nel parametro `cron` , a partire da `startTime` fino a `endTime`.

**Risposta**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`: L&#39;ID che rappresenta l&#39;esperimento.\
`{INSTANCE_ID}`: L&#39;ID che rappresenta l&#39;istanza MLI.


### Creare un&#39;esecuzione di un esperimento per la formazione

Con la creazione di un’entità Sperimento, è possibile creare ed eseguire un’esecuzione di formazione utilizzando la chiamata di seguito. Sarà necessario il `{EXPERIMENT_ID}` e specificare il `mode` che si desidera attivare nel corpo della richiesta.

**Richiesta**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: L’ID corrispondente all’esperimento di cui desideri eseguire il targeting. Questo si trova nella risposta durante la creazione del tuo esperimento.\
`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{API_KEY}`: Il valore chiave API specifico si trova nell’integrazione Adobe Experience Platform univoca.\
`{JSON_PAYLOAD}`: Per creare un&#39;esecuzione di formazione, è necessario includere quanto segue nel corpo:

```JSON
{
    "mode":"Train"
}
```

È inoltre possibile ignorare i parametri di configurazione includendo un array `tasks`:

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

Riceverai la seguente risposta che ti informerà della `{EXPERIMENT_RUN_ID}` e della configurazione in `tasks`.

**Risposta**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: L&#39;ID che rappresenta l&#39;esecuzione dell&#39;esperimento.\
`{EXPERIMENT_ID}`: L&#39;ID che rappresenta l&#39;esperimento a cui si riferisce l&#39;esecuzione dell&#39;esperimento.

### Recuperare lo stato di Experience Run

Lo stato dell&#39;esecuzione dell&#39;esperimento può essere interrogato con `{EXPERIMENT_RUN_ID}`.

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: L&#39;ID che rappresenta l&#39;esperimento.\
`{EXPERIMENT_RUN_ID}`: L&#39;ID che rappresenta l&#39;esecuzione dell&#39;esperimento.\
`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.\
`{API_KEY}`: Il valore chiave API specifico si trova nell’integrazione Adobe Experience Platform univoca.

**Risposta**

La chiamata GET fornirà lo stato nel parametro `state` come mostrato di seguito:

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`: L&#39;ID che rappresenta l&#39;esecuzione dell&#39;esperimento.\
`{EXPERIMENT_ID}`: L&#39;ID che rappresenta l&#39;esperimento a cui si riferisce l&#39;esecuzione dell&#39;esperimento.

Oltre allo stato `DONE` , altri stati includono:
- `PENDING`
- `RUNNING`
- `FAILED`

Per ottenere ulteriori informazioni, i registri dettagliati si trovano sotto il parametro `tasklogs` .

### Recuperare il modello addestrato

Al fine di ottenere il modello addestrato creato sopra durante l&#39;addestramento, effettuiamo la seguente richiesta:

**Richiesta**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`: L&#39;ID corrispondente all&#39;esecuzione dell&#39;esperimento di cui desideri eseguire il targeting. Questo si trova nella risposta durante la creazione dell’esecuzione dell’esperimento.\
`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.

La risposta rappresenta il modello addestrato creato.

**Risposta**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`: L&#39;ID corrispondente al modello.\
`{EXPERIMENT_ID}`: L’ID corrispondente all’esperimento in cui viene eseguito l’esperimento.\
`{EXPERIMENT_RUN_ID}`: L&#39;ID corrispondente all&#39;esecuzione dell&#39;esperimento.

### Arrestare ed eliminare un esperimento pianificato

Per interrompere l’esecuzione di un esperimento pianificato prima del relativo `endTime`, è possibile eseguire questa operazione eseguendo una query su una richiesta DELETE al `{EXPERIMENT_ID}`

**Richiesta**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: L&#39;ID corrispondente all&#39;esperimento.\
`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.

>[!NOTE]
>
>La chiamata API disattiverà la creazione di nuove esecuzioni di Esperimenti. Tuttavia, non interromperà l&#39;esecuzione di esecuzioni di esperimenti già in esecuzione.

Di seguito è riportata la notifica della cancellazione dell’esperimento.

**Risposta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Passaggi successivi

Questa esercitazione spiega come utilizzare le API per creare un motore, un esperimento, esecuzioni di esperimenti pianificate e modelli addestrati. Nell&#39; [esercizio successivo](./score-model-api.md), effettuerai le previsioni assegnando un punteggio a un nuovo set di dati utilizzando il modello addestrato con le prestazioni migliori.
