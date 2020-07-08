---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Punteggio di un modello (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---


# Punteggio di un modello (API)

Questa esercitazione vi mostrerà come sfruttare le API per creare un esperimento e un&#39;esecuzione di prova. Per un elenco dettagliato della documentazione API, consultate [questo documento](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html).

## Creazione di un esperimento pianificato per il punteggio

Come per gli esperimenti pianificati per la formazione, la creazione di un esperimento pianificato per il punteggio viene anche effettuata includendo una `template` sezione al parametro body. Inoltre, il `name` campo sotto `tasks` nel corpo è impostato come `score`.

Di seguito è riportato un esempio di creazione di un esperimento che verrà eseguito ogni 20 minuti a partire da `startTime` e che verrà eseguito fino a `endTime`.

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

`{IMS_ORG}`: Credenziali organizzazione IMS trovate nella vostra integrazione  Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Il valore del token del portatore specificato dopo l&#39;autenticazione.\
`{API_KEY}`: Il valore della chiave API specifico trovato nell&#39;integrazione del Adobe Experience Platform  univoco.\
`{JSON_PAYLOAD}`: Oggetto Experience Run da inviare. L’esempio che utilizziamo nell’esercitazione è riportato di seguito:

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
`{MODEL_ID}`: L&#39;ID che rappresenta il modello addestrato.

Di seguito è riportata la risposta dopo la creazione dell&#39;esperimento pianificato.

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

`{EXPERIMENT_ID}`: L’ID che rappresenta l’esperimento.\
`{INSTANCE_ID}`: L&#39;ID che rappresenta l&#39;istanza MLI.


### Creazione di un&#39;esecuzione di un esperimento per il punteggio

Ora, con il modello addestrato, possiamo creare una Prova Sperimentale per il punteggio. Il valore del `modelId` parametro è il `id` parametro restituito nella richiesta GET Model precedente.

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

`{IMS_ORG}`: Credenziali organizzazione IMS trovate nella vostra integrazione  Adobe Experience Platform.\
`{ACCESS_TOKEN}`: Il valore del token del portatore specificato dopo l&#39;autenticazione.\
`{API_KEY}`: Il valore della chiave API specifico trovato nell&#39;integrazione del Adobe Experience Platform  univoco.\
`{EXPERIMENT_ID}`: L’ID corrispondente all’esperimento di cui eseguire il targeting. Questo si trova nella risposta quando create il vostro esperimento.\
`{JSON_PAYLOAD}`: Dati da registrare. L&#39;esempio che utilizziamo per questa esercitazione è il seguente:

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

La risposta della creazione di Experience Run è mostrata di seguito:

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

`{EXPERIMENT_ID}`:  L&#39;ID corrispondente all&#39;esperimento su cui si trova l&#39;esecuzione.\
`{EXPERIMENT_RUN_ID}`: L’ID corrispondente all’esecuzione dell’esperimento appena creata.


### Recupero dello stato di esecuzione di un esperimento per l&#39;esecuzione programmata di un esperimento

Per ottenere le esecuzioni degli esperimenti per gli esperimenti pianificati, la query è mostrata di seguito:

**Richiesta**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  L&#39;ID corrispondente all&#39;esperimento su cui si trova l&#39;esecuzione.\
`{ACCESS_TOKEN}`: Il valore del token del portatore specificato dopo l&#39;autenticazione.\
`{IMS_ORG}`: Credenziali organizzazione IMS trovate nella vostra integrazione  Adobe Experience Platform.

Poiché per un esperimento specifico sono presenti più esecuzioni sperimentali, la risposta restituita avrà un array di ID di esecuzione.

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

`{EXPERIMENT_RUN_ID}`: L’ID corrispondente all’esecuzione dell’esperimento.\
`{EXPERIMENT_ID}`:  L&#39;ID corrispondente all&#39;esperimento su cui si trova l&#39;esecuzione.

### Arrestare ed eliminare un esperimento pianificato

Se si desidera interrompere l&#39;esecuzione di un esperimento pianificato prima del relativo `endTime`, è possibile eseguire questa operazione eseguendo una query su una richiesta DELETE al `{EXPERIMENT_ID}`

**Richiesta**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  L’ID corrispondente all’esperimento.\
`{ACCESS_TOKEN}`: Il valore del token del portatore specificato dopo l&#39;autenticazione.\
`{IMS_ORG}`: Credenziali organizzazione IMS trovate nella vostra integrazione  Adobe Experience Platform.

>[!NOTE]
>
>La chiamata API disattiverà la creazione di nuove esecuzioni di Esperimenti. Tuttavia, non interromperà l&#39;esecuzione di esecuzioni di esperti già in esecuzione.

Di seguito viene riportata la risposta che informa che l’eliminazione dell’esperimento è avvenuta correttamente.

**Risposta**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```
