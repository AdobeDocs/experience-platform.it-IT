---
keywords: Experience Platform;Punteggio di un modello;Data Science Workspace;argomenti popolari;api di apprendimento automatico sensei
solution: Experience Platform
title: Punteggio di un modello utilizzando l’API di apprendimento automatico di Sensei
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione ti mostrerà come sfruttare le API di apprendimento automatico di Sensei per creare un esperimento e un’esecuzione di un esperimento.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 6ae6bbb5af0f007e483145dca5d4d505c388cc2c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# Punteggio di un modello utilizzando [!DNL Sensei Machine Learning API]

Questa esercitazione ti mostrerà come sfruttare le API per creare un esperimento e un’esecuzione di un esperimento. Per un elenco di tutti gli endpoint nell&#39;API di apprendimento automatico di Sensei, fai riferimento a [presente documento](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Creare un esperimento pianificato per il punteggio

Simile agli esperimenti pianificati per la formazione, la creazione di un esperimento pianificato per il punteggio viene eseguita anche includendo un `template` al parametro body. Inoltre, la `name` campo sotto `tasks` nel corpo è impostato come `score`.

Di seguito è riportato un esempio di creazione di un esperimento che verrà eseguito ogni 20 minuti a partire da `startTime` e funzionerà fino a `endTime`.

**Richiesta**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{API_KEY}`: Il valore chiave API specifico si trova nell’integrazione Adobe Experience Platform univoca.\
`{JSON_PAYLOAD}`: Oggetto Experience Run da inviare. L’esempio che utilizziamo nel nostro tutorial è mostrato qui:

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

`{INSTANCE_ID}`: L&#39;ID che rappresenta l&#39;istanza MLI.\
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

`{EXPERIMENT_ID}`: L&#39;ID che rappresenta l&#39;esperimento.\
`{INSTANCE_ID}`: L&#39;ID che rappresenta l&#39;istanza MLI.


### Creare un’esecuzione di un esperimento per il punteggio

Ora, con il modello addestrato, possiamo creare un Experience Run per il punteggio. Il valore del `modelId` è il parametro `id` parametro restituito nella richiesta del modello di GET precedente.

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

`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{API_KEY}`: Il valore chiave API specifico si trova nell’integrazione Adobe Experience Platform univoca.\
`{EXPERIMENT_ID}`: L’ID corrispondente all’esperimento di cui desideri eseguire il targeting. Questo si trova nella risposta durante la creazione del tuo esperimento.\
`{JSON_PAYLOAD}`: Dati da registrare. L’esempio che utilizziamo nel nostro tutorial è il seguente:

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

`{MODEL_ID}`: L&#39;ID corrispondente al modello.

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

`{EXPERIMENT_ID}`: L&#39;ID corrispondente all&#39;esperimento in cui si trova l&#39;esecuzione.\
`{EXPERIMENT_RUN_ID}`: L&#39;ID corrispondente all&#39;esecuzione dell&#39;esperimento appena creato.


### Recupera lo stato di esecuzione di un esperimento per l&#39;esecuzione programmata di un esperimento

Per ottenere le esecuzioni di esperimenti per gli esperimenti pianificati, la query è mostrata di seguito:

**Richiesta**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: L&#39;ID corrispondente all&#39;esperimento in cui si trova l&#39;esecuzione.\
`{ACCESS_TOKEN}`: Il valore specifico del token portatore fornito dopo l’autenticazione.\
`{IMS_ORG}`: Le credenziali dell’organizzazione IMS sono state trovate nell’integrazione unica di Adobe Experience Platform.

Poiché sono presenti più esecuzioni di esperimenti per un esperimento specifico, la risposta restituita avrà una matrice di ID di esecuzione.

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

`{EXPERIMENT_RUN_ID}`: L&#39;ID corrispondente all&#39;esecuzione dell&#39;esperimento.\
`{EXPERIMENT_ID}`: L&#39;ID corrispondente all&#39;esperimento in cui si trova l&#39;esecuzione.

### Arrestare ed eliminare un esperimento pianificato

Se desideri interrompere l’esecuzione di un esperimento pianificato prima del relativo `endTime`, può essere eseguito eseguendo una query su una richiesta di DELETE al `{EXPERIMENT_ID}`

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
