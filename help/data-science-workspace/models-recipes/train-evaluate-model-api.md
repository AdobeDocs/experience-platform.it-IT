---
keywords: Experience Platform;addestrare e valutare;Data Science Workspace;argomenti popolari;Sensei Machine Learning API
solution: Experience Platform
title: Formazione e valutazione di un modello tramite l’API di apprendimento automatico di Sensei
type: Tutorial
description: Questo tutorial illustra come creare, addestrare e valutare un modello utilizzando le chiamate API di apprendimento automatico di Sensei.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 1%

---

# Addestrare e valutare un modello utilizzando l&#39;API [!DNL Sensei Machine Learning]

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

In questo esercitazione viene illustrato come creare, addestrare e valutare un modello utilizzando le chiamate API. Fare riferimento a [questo documento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) per un elenco dettagliato della documentazione API.

## Prerequisiti

Segui [Importa una ricetta in pacchetti utilizzando l&#39;API](./import-packaged-recipe-api.md) per creare un motore, necessario per addestrare e valutare un modello utilizzando l&#39;API.

Segui l&#39;[esercitazione sull&#39;autenticazione API Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) per iniziare ad effettuare chiamate API.

Dall’esercitazione ora dovrebbero essere presenti i seguenti valori:

- `{ACCESS_TOKEN}`: il valore del token Bearer specifico fornito dopo l&#39;autenticazione.
- `{ORG_ID}`: credenziali organizzazione trovate nell&#39;integrazione univoca di Adobe Experience Platform.
- `{API_KEY}`: valore chiave API specifico trovato nell&#39;integrazione univoca di Adobe Experience Platform.

- Collegamento a un’immagine Docker di un servizio intelligente

## Flusso di lavoro API

Utilizzeremo le API per creare un’esecuzione di esperimento per la formazione. Per questo tutorial, ci concentreremo sugli endpoint &quot;Engines&quot;, &quot;MLInstance&quot; ed &quot;Experiments&quot;. Il grafico seguente illustra la relazione tra i tre e introduce anche l&#39;idea di un modello e di un&#39;esecuzione.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>I termini &quot;Engine&quot;, &quot;MLInstance&quot;, &quot;MLService&quot;, &quot;Experiment&quot; e &quot;Model&quot; vengono indicati come termini diversi nell’interfaccia utente. Se utilizzi un’interfaccia utente, la tabella che segue mappa le differenze.

| Termine interfaccia utente | Termine API |
| --- | --- |
| Ricetta | Motore |
| Modello | MLInstance |
| Addestramenti | Esperimento |
| Servizio | MLService |

### Creare un&#39;istanza MLI

La creazione di un’istanza MLI può essere eseguita utilizzando la seguente richiesta. Si utilizzerà `{ENGINE_ID}` restituito durante la creazione di un motore da [Importare una composizione in pacchetti utilizzando l&#39;esercitazione API](./import-packaged-recipe-ui.md).

**Richiesta**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: il valore specifico del token portatore fornito dopo l&#39;autenticazione.\
`{ORG_ID}`: credenziali dell&#39;organizzazione trovate nell&#39;integrazione univoca del Adobe Experience Platform.\
`{API_KEY}`: valore chiave API specifico trovato nell&#39;integrazione univoca di Adobe Experience Platform.\
`{JSON_PAYLOAD}`: configurazione dell&#39;istanza MLI. L’esempio utilizzato nel nostro tutorial è mostrato qui:

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
>In `{JSON_PAYLOAD}` vengono definiti i parametri utilizzati per l&#39;apprendimento e il punteggio nell&#39;array `tasks`. `{ENGINE_ID}` è l&#39;ID del motore che si desidera utilizzare e il campo `tag` è un parametro facoltativo utilizzato per identificare l&#39;istanza.

La risposta contiene `{INSTANCE_ID}` che rappresenta l&#39;istanza MLI creata. È possibile creare più istanze del modello MLI con configurazioni diverse.

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

`{ENGINE_ID}`: questo ID rappresenta il motore in cui viene creata l&#39;istanza MLI.\
`{INSTANCE_ID}`: ID che rappresenta l&#39;istanza MLI.

### Creare un esperimento

Un esperimento viene utilizzato da uno scienziato dei dati per arrivare a un modello ad alte prestazioni durante la formazione. Gli esperimenti multipli includono la modifica di set di dati, funzioni, parametri di apprendimento e hardware. L’esempio seguente illustra come creare un esperimento.

**Richiesta**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}`: credenziali organizzazione trovate nell&#39;integrazione univoca di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: il valore del token Bearer specifico fornito dopo l&#39;autenticazione.\
`{API_KEY}`: il valore specifico della chiave API trovato nell&#39;integrazione Adobe Experience Platform univoca.\
`{JSON_PAYLOAD}`: oggetto esperimento creato. L&#39;esempio che usiamo nel nostro esercitazione è mostrato qui:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: ID che rappresenta l&#39;istanza MLI.

La risposta dalla creazione dell’esperimento è simile alla seguente.

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

`{EXPERIMENT_ID}`: ID che rappresenta l&#39;esperimento appena creato.
`{INSTANCE_ID}`: ID che rappresenta l&#39;istanza MLI.

### Creare un esperimento pianificato per la formazione

Gli esperimenti pianificati vengono utilizzati in modo da non dover creare ogni singola esecuzione di esperimenti tramite una chiamata API. Invece, forniamo tutti i parametri necessari durante la creazione dell&#39;esperimento e ogni esecuzione verrà creata periodicamente.

Per indicare la creazione di un esperimento pianificato, è necessario aggiungere una sezione `template` nel corpo della richiesta. In `template` sono inclusi tutti i parametri necessari per la pianificazione delle esecuzioni, ad esempio `tasks`, che indica l&#39;azione, e `schedule`, che indica la tempistica delle esecuzioni pianificate.

**Richiesta**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}`: credenziali organizzazione trovate nell&#39;integrazione univoca di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: il valore specifico del token portatore fornito dopo l&#39;autenticazione.\
`{API_KEY}`: il valore specifico della chiave API trovato nell&#39;integrazione Adobe Experience Platform univoca.\
`{JSON_PAYLOAD}`: Set di dati da inviare. L&#39;esempio che usiamo nel nostro esercitazione è mostrato qui:

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

Quando creiamo un esperimento, il corpo, `{JSON_PAYLOAD}`, dovrebbe contenere il `mlInstanceId` parametro o il `mlInstanceQuery` parametro. In questo esempio, un esperimento pianificato richiamerà un&#39;esecuzione `cron` ogni 20 minuti, impostata nel parametro, a partire da fino a `startTime` .`endTime`

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

`{EXPERIMENT_ID}`: ID che rappresenta l&#39;esperimento.\
`{INSTANCE_ID}`: ID che rappresenta l&#39;istanza MLI.


### Creare un’esecuzione di esperimento per l’apprendimento

Una volta creata un’entità esperimento, è possibile creare ed eseguire un’esecuzione di addestramento utilizzando la chiamata seguente. Sarà necessario `{EXPERIMENT_ID}` e specificare lo stato di `mode` che si desidera attivare nel corpo della richiesta.

**Richiesta**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: ID corrispondente all&#39;esperimento di cui desideri eseguire il targeting. Questo si trova nella risposta durante la creazione dell’esperimento.\
`{ORG_ID}`: credenziali organizzazione trovate nell&#39;integrazione univoca di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: il valore del token Bearer specifico fornito dopo l&#39;autenticazione.\
`{API_KEY}`: valore chiave API specifico trovato nell&#39;integrazione univoca di Adobe Experience Platform.\
`{JSON_PAYLOAD}`: per creare un&#39;esecuzione di addestramento, è necessario includere nel corpo quanto segue:

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

Riceverai la seguente risposta che ti farà sapere `{EXPERIMENT_RUN_ID}` e la configurazione in `tasks`.

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

`{EXPERIMENT_RUN_ID}`: ID che rappresenta l&#39;esecuzione dell&#39;esperimento.\
`{EXPERIMENT_ID}`: ID che rappresenta l&#39;esperimento in cui si trova l&#39;esecuzione dell&#39;esperimento.

### Recuperare lo stato di esecuzione di un esperimento

È possibile eseguire una query sullo stato dell&#39;esecuzione dell&#39;esperimento con `{EXPERIMENT_RUN_ID}`.

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: ID che rappresenta l&#39;esperimento.\
`{EXPERIMENT_RUN_ID}`: ID che rappresenta l&#39;esecuzione dell&#39;esperimento.\
`{ACCESS_TOKEN}`: il valore del token Bearer specifico fornito dopo l&#39;autenticazione.\
`{ORG_ID}`: credenziali organizzazione trovate nell&#39;integrazione univoca di Adobe Experience Platform.\
`{API_KEY}`: il valore specifico della chiave API trovato nell&#39;integrazione Adobe Experience Platform univoca.

**Risposta**

La chiamata GET fornirà lo stato nel `state` parametro, come mostrato di seguito:

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

`{EXPERIMENT_RUN_ID}`: l&#39;ID che rappresenta l&#39;esecuzione dell&#39;esperimento.\
`{EXPERIMENT_ID}`: ID che rappresenta l&#39;esperimento in cui si trova l&#39;esecuzione dell&#39;esperimento.

Oltre allo stato `DONE`, gli altri stati includono:
- `PENDING`
- `RUNNING`
- `FAILED`

Per ulteriori informazioni, i registri dettagliati si trovano sotto il parametro `tasklogs`.

### Recupera il modello addestrato

Per ottenere il modello addestrato creato in precedenza durante la formazione, effettuiamo la seguente richiesta:

**Richiesta**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`: ID corrispondente all&#39;esecuzione dell&#39;esperimento di cui si desidera eseguire il targeting. Questo si trova nella risposta durante la creazione dell’esecuzione dell’esperimento.\
`{ACCESS_TOKEN}`: il valore del token Bearer specifico fornito dopo l&#39;autenticazione.\
`{ORG_ID}`: credenziali organizzazione trovate nell&#39;integrazione univoca di Adobe Experience Platform.

La risposta rappresenta il modello addestrato che è stato creato.

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

`{MODEL_ID}`: ID corrispondente al modello.\
`{EXPERIMENT_ID}`: l&#39;ID corrispondente all&#39;esperimento eseguito.\
`{EXPERIMENT_RUN_ID}`: ID corrispondente all&#39;esecuzione dell&#39;esperimento.

### Interruzione ed eliminare un esperimento pianificato

Se si desidera interrompere l&#39;esecuzione di un esperimento pianificato prima della sua `endTime`, è possibile eseguire questa operazione interrogando un richiesta DELETE al `{EXPERIMENT_ID}`

**Richiesta**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: ID corrispondente all&#39;esperimento.\
`{ACCESS_TOKEN}`: il valore del token Bearer specifico fornito dopo l&#39;autenticazione.\
`{ORG_ID}`: credenziali organizzazione trovate nell&#39;integrazione univoca di Adobe Experience Platform.

>[!NOTE]
>
>La chiamata API disabiliterà la creazione di nuove esecuzioni dell’esperimento. Tuttavia, non interrompe l’esecuzione di esecuzioni di esperimenti già in esecuzione.

Di seguito è riportata la risposta che notifica che l&#39;esperimento è stato eliminato correttamente.

**Risposta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Passaggi successivi

Questo tutorial illustra come utilizzare le API per creare un motore, un esperimento, esecuzioni di esperimenti pianificate e modelli addestrati. Nell&#39;[esercizio successivo](./score-model-api.md), effettuerai delle previsioni assegnando un punteggio a un nuovo set di dati utilizzando il modello addestrato con le prestazioni migliori.
