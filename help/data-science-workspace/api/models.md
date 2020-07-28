---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modelli
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 4%

---


# Modelli

Un modello è un&#39;istanza di una ricetta di machine learning che viene formata utilizzando dati storici e configurazioni per risolvere un caso d&#39;uso aziendale.

## Recupera un elenco di Modelli

È possibile recuperare un elenco di dettagli modello appartenenti a tutti i modelli eseguendo una singola richiesta di GET a /models. Per impostazione predefinita, questo elenco si ordina dal modello meno recente creato e limita i risultati a 25. Potete scegliere di filtrare i risultati specificando alcuni parametri di query. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.

**Formato API**

```http
GET /models
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli dei modelli, incluso ciascun identificatore univoco (`id`) dei modelli.

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | L&#39;ID corrispondente al modello. |
| `modelArtifactUri` | URI che indica la posizione di memorizzazione del modello. L&#39;URI termina con il `name` valore del modello. |
| `experimentId` | Un ID di esperimento valido. |
| `experimentRunId` | Un ID di esecuzione dell&#39;esperimento valido. |

## Recuperare un modello specifico

È possibile recuperare un elenco di dettagli modello appartenenti a un particolare modello eseguendo una singola richiesta di GET e fornendo un ID modello valido nel percorso della richiesta. Per facilitare il filtraggio dei risultati, potete specificare i parametri di query nel percorso di richiesta. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.

**Formato API**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello addestrato o pubblicato. |
| `{EXPERIMENT_RUN_ID}` | Identificatore dell&#39;esecuzione dell&#39;esperimento. |

**Richiesta**

La richiesta seguente contiene una query e recupera un elenco di Modelli qualificati che condividono lo stesso identificatore ExperienceRunID ({EXPERIMENT_RUN_ID}).

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del modello, incluso l&#39;identificatore univoco Modelli (`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
        "count": 1
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | L&#39;ID corrispondente al modello. |
| `modelArtifactUri` | URI che indica la posizione di memorizzazione del modello. L&#39;URI termina con il `name` valore del modello. |
| `experimentId` | Un ID di esperimento valido. |
| `experimentRunId` | Un ID di esecuzione dell&#39;esperimento valido. |

## Registrazione di un modello pregenerato {#register-a-model}

È possibile registrare un modello pregenerato effettuando una richiesta di POST all&#39; `/models` endpoint. Per registrare il modello, è necessario includere nel corpo della richiesta i valori del `modelArtifact` file e `model` delle proprietà.

**Formato API**

```http
POST /models
```

**Richiesta**

L&#39;POST seguente contiene i valori `modelArtifact` di file e `model` proprietà necessari. Per ulteriori informazioni su questi valori, vedere la tabella seguente.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| Parametro | Descrizione |
| --- | --- |
| `modelArtifact` | Posizione dell&#39;artifact del modello completo che si desidera includere. |
| `model` | I dati del modulo dell&#39;oggetto Model da creare. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del modello, incluso l&#39;identificatore univoco Modelli (`id`).

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | L&#39;ID corrispondente al modello. |
| `modelArtifactUri` | URI che indica la posizione di memorizzazione del modello. L&#39;URI termina con il `id` valore del modello. |

## Aggiornare un modello in base all&#39;ID

È possibile aggiornare un modello esistente sovrascrivendone le proprietà tramite una richiesta di PUT che include l&#39;ID del modello di destinazione nel percorso della richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta di PUT, si consiglia innanzitutto di eseguire una richiesta di GET per recuperare il modello per ID. Quindi, modificate e aggiornate l&#39;oggetto JSON restituito e applicate l&#39;intero oggetto JSON modificato come payload per la richiesta di PUT.

**Formato API**

```http
PUT /models/{MODEL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello addestrato o pubblicato. |

**Richiesta**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli aggiornati dell&#39;esperimento.

```json
{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## Eliminazione di un modello per ID

È possibile eliminare un singolo modello eseguendo una richiesta di DELETE che include l&#39;ID del modello di destinazione nel percorso della richiesta.

**Formato API**

```http
DELETE /models/{MODEL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello addestrato o pubblicato. |

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente uno stato di 200 che conferma l&#39;eliminazione del modello.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## Creare una nuova transcodifica per un modello {#create-transcoded-model}

La transcodifica è la conversione diretta da digitale a digitale di una codifica a un’altra. È possibile creare una nuova transcodifica per un modello fornendo l&#39;output `{MODEL_ID}` e l&#39; `targetFormat` output desiderato.

**Formato API**

```http
POST /models/{MODEL_ID}/transcodings
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello addestrato o pubblicato. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId" : "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto JSON con le informazioni della transcodifica. Ciò include l&#39;identificatore univoco (`id`) di transcodifica utilizzato per [recuperare uno specifico modello](#retrieve-transcoded-model)transcodificato.

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## Recuperare un elenco di transcodifiche per un modello {#retrieve-transcoded-model-list}

È possibile recuperare un elenco delle transcodifiche eseguite su un modello eseguendo una richiesta di GET con il `{MODEL_ID}`.

**Formato API**

```http
GET /models/{MODEL_ID}/transcodings
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello addestrato o pubblicato. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto json con un elenco di ciascuna transcodifica eseguita sul modello. Ogni modello transcodificato riceve un identificatore univoco (`id`).

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## Recuperare un modello transcodificato specifico {#retrieve-transcoded-model}

È possibile recuperare uno specifico modello transcodificato eseguendo una richiesta di GET con il proprio `{MODEL_ID}` e l&#39;ID di un modello transcodificato.

**Formato API**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore univoco di un modello addestrato o pubblicato. |
| `{TRANSCODING_ID}` | Identificatore univoco di un modello transcodificato. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto JSON con i dati del modello transcodificato.

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```


