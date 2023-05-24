---
keywords: Experience Platform;valutare un modello;Data Science Workspace;argomenti popolari;sensei machine learning api
solution: Experience Platform
title: Punteggio di un modello utilizzando l’API di apprendimento automatico di Sensei
type: Tutorial
description: Questa esercitazione ti mostrerà come sfruttare le API di apprendimento automatico di Sensei per creare un’esecuzione di un esperimento e di un esperimento.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# Punteggio di un modello utilizzando [!DNL Sensei Machine Learning API]

Questa esercitazione ti mostrerà come sfruttare le API per creare un’esecuzione di un esperimento e di un esperimento. Per un elenco di tutti gli endpoint nell’API di apprendimento automatico di Sensei, consulta [questo documento](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Creare un esperimento pianificato per il punteggio

Analogamente agli esperimenti pianificati per la formazione, la creazione di un esperimento pianificato per il punteggio viene eseguita anche includendo una `template` al parametro body. Inoltre, il `name` campo in `tasks` nel corpo è impostato come `score`.

Di seguito è riportato un esempio di creazione di un esperimento che verrà eseguito ogni 20 minuti a partire da `startTime` e verrà eseguito fino al `endTime`.

**Richiesta**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`: le credenziali della tua organizzazione sono state trovate nell’integrazione univoca di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: valore del token Bearer specifico fornito dopo l’autenticazione.\
`{API_KEY}`: valore chiave API specifico trovato nell’integrazione univoca di Adobe Experience Platform.\
`{JSON_PAYLOAD}`: oggetto esecuzione esperimento da inviare. L’esempio utilizzato nel nostro tutorial è mostrato qui:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
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
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`: ID che rappresenta l’istanza MLI.\
`{MODEL_ID}`: ID che rappresenta il modello addestrato.

Di seguito è riportata la risposta dopo la creazione dell’esperimento pianificato.

**Risposta**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`: ID che rappresenta l’esperimento.\
`{INSTANCE_ID}`: ID che rappresenta l’istanza MLI.


### Creare un’esecuzione dell’esperimento per il punteggio

Ora con il modello addestrato, possiamo creare un’esecuzione di esperimento per il punteggio. Il valore della proprietà `modelId` il parametro è il `id` parametro restituito nella richiesta del modello di GET precedente.

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

`{ORG_ID}`: le credenziali della tua organizzazione sono state trovate nell’integrazione univoca di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: valore del token Bearer specifico fornito dopo l’autenticazione.\
`{API_KEY}`: valore chiave API specifico trovato nell’integrazione univoca di Adobe Experience Platform.\
`{EXPERIMENT_ID}`: ID corrispondente all’esperimento di cui desideri eseguire il targeting. Questo si trova nella risposta durante la creazione dell’esperimento.\
`{JSON_PAYLOAD}`: dati da pubblicare. L’esempio utilizzato nel nostro tutorial è il seguente:

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`: ID corrispondente al modello.

La risposta dalla creazione dell’esecuzione dell’esperimento è mostrata di seguito:

**Risposta**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`: ID corrispondente all’esperimento in cui si trova l’esecuzione.\
`{EXPERIMENT_RUN_ID}`: ID corrispondente all’esecuzione dell’esperimento appena creata.


### Recuperare lo stato di esecuzione di un esperimento per l’esecuzione pianificata dell’esperimento

Per eseguire un esperimento per gli esperimenti pianificati, la query è mostrata di seguito:

**Richiesta**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: ID corrispondente all’esperimento in cui si trova l’esecuzione.\
`{ACCESS_TOKEN}`: valore del token Bearer specifico fornito dopo l’autenticazione.\
`{ORG_ID}`: le credenziali della tua organizzazione sono state trovate nell’integrazione univoca di Adobe Experience Platform.

Poiché esistono più esecuzioni di esperimenti per un esperimento specifico, la risposta restituita avrà una matrice di ID di esecuzione.

**Risposta**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: ID corrispondente all’esecuzione dell’esperimento.\
`{EXPERIMENT_ID}`: ID corrispondente all’esperimento in cui si trova l’esecuzione.

### Interrompere ed eliminare un esperimento pianificato

Se desideri interrompere l’esecuzione di un esperimento pianificato prima del relativo `endTime`, è possibile eseguire una query su una richiesta DELETE al `{EXPERIMENT_ID}`

**Richiesta**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: ID corrispondente all’esperimento.\
`{ACCESS_TOKEN}`: valore del token Bearer specifico fornito dopo l’autenticazione.\
`{ORG_ID}`: le credenziali della tua organizzazione sono state trovate nell’integrazione univoca di Adobe Experience Platform.

>[!NOTE]
>
>La chiamata API disabiliterà la creazione di nuove esecuzioni dell’esperimento. Tuttavia, non interrompe l’esecuzione di esecuzioni di esperimenti già in esecuzione.

Di seguito è riportata la risposta con la quale si notifica che l’esperimento è stato eliminato correttamente.

**Risposta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```
