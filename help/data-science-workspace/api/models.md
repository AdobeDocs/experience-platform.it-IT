---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti popolari;modelli;sensei machine learning api
solution: Experience Platform
title: Endpoint Models API
description: Un modello è un’istanza di una ricetta di apprendimento automatico che viene addestrata utilizzando dati e configurazioni storici per risolvere un caso d’uso aziendale.
role: Developer
exl-id: e66119a9-9552-497c-9b3a-b64eb3b51fcf
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# Endpoint &quot;model&quot;

Un modello è un’istanza di una ricetta di apprendimento automatico che viene addestrata utilizzando dati e configurazioni storici per risolvere un caso d’uso aziendale.

## Recuperare un elenco di modelli

Per recuperare un elenco di dettagli del modello appartenenti a tutti i modelli, esegui una singola richiesta GET a /models. Per impostazione predefinita, questo elenco si ordina dal modello creato più vecchio e limita i risultati a 25. Puoi scegliere di filtrare i risultati specificando alcuni parametri di query. Per un elenco delle query disponibili, consulta la sezione dell’appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli dei modelli, incluso ogni identificatore univoco dei modelli (`id`).

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
| `id` | L’ID corrispondente al modello. |
| `modelArtifactUri` | URI che indica dove è memorizzato il modello. L’URI termina con `name` per il modello. |
| `experimentId` | Un ID esperimento valido. |
| `experimentRunId` | Un ID di esecuzione esperimento valido. |

## Recuperare un modello specifico

GET Per recuperare un elenco di dettagli modello appartenenti a un particolare modello, esegui una singola richiesta e fornisci un ID modello valido nel percorso della richiesta. Per filtrare i risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco delle query disponibili, consulta la sezione dell’appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).

**Formato API**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | L’identificatore del modello addestrato o pubblicato. |
| `{EXPERIMENT_RUN_ID}` | Identificatore dell’esecuzione dell’esperimento. |

**Richiesta**

La richiesta seguente contiene una query e recupera un elenco di modelli addestrati che condividono lo stesso experimentRunID ({EXPERIMENT_RUN_ID}).

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli del modello, incluso l’identificatore univoco dei modelli (`id`).

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
| `id` | L’ID corrispondente al modello. |
| `modelArtifactUri` | URI che indica dove è memorizzato il modello. L’URI termina con `name` per il modello. |
| `experimentId` | Un ID esperimento valido. |
| `experimentRunId` | Un ID di esecuzione esperimento valido. |

## Registra un modello pregenerato {#register-a-model}

Per registrare un modello pregenerato, invia una richiesta POST al `/models` endpoint. Per registrare il modello, è necessario `modelArtifact` file e `model` I valori delle proprietà devono essere inclusi nel corpo della richiesta.

**Formato API**

```http
POST /models
```

**Richiesta**

Il seguente POST contiene `modelArtifact` file e `model` valori delle proprietà necessari. Per ulteriori informazioni su questi valori, consulta la tabella seguente.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| Parametro | Descrizione |
| --- | --- |
| `modelArtifact` | Posizione dell&#39;artefatto modello completo che si desidera includere. |
| `model` | Dati del modulo dell&#39;oggetto Model da creare. |

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli del modello, incluso l’identificatore univoco dei modelli (`id`).

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
| `id` | L’ID corrispondente al modello. |
| `modelArtifactUri` | URI che indica dove è memorizzato il modello. L’URI termina con `id` valore per il modello. |

## Aggiornare un modello per ID

Puoi aggiornare un modello esistente sovrascrivendo le relative proprietà tramite una richiesta PUT che include l’ID del modello di destinazione nel percorso della richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta PUT, si consiglia di eseguire prima una richiesta GET per recuperare il modello per ID. Quindi, modifica e aggiorna l’oggetto JSON restituito e applica l’intero oggetto JSON modificato come payload per la richiesta PUT.

**Formato API**

```http
PUT /models/{MODEL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | L’identificatore del modello addestrato o pubblicato. |

**Richiesta**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli aggiornati dell’esperimenti.

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

## Eliminare un modello per ID

Per eliminare un singolo modello, devi eseguire una richiesta DELETE che includa l’ID del modello di destinazione nel percorso della richiesta.

**Formato API**

```http
DELETE /models/{MODEL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | L’identificatore del modello addestrato o pubblicato. |

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente lo stato 200 che conferma l’eliminazione del modello.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## Creare una nuova transcodifica per un modello {#create-transcoded-model}

La trascodifica è la conversione digitale-digitale diretta di una codifica in un’altra. Per creare una nuova transcodifica per un modello, devi fornire `{MODEL_ID}` e un `targetFormat` desideri che il nuovo output sia in.

**Formato API**

```http
POST /models/{MODEL_ID}/transcodings
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | L’identificatore del modello addestrato o pubblicato. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
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

In caso di esito positivo, la risposta restituisce un payload contenente un oggetto JSON con le informazioni della transcodifica. Questo include l’identificatore univoco delle trascodifiche (`id`) utilizzato in [recupero di un modello transcodificato specifico](#retrieve-transcoded-model).

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

## Recuperare un elenco di trascodifiche per un modello {#retrieve-transcoded-model-list}

Per recuperare un elenco delle trascodifiche eseguite su un modello, devi eseguire una richiesta GET con `{MODEL_ID}`.

**Formato API**

```http
GET /models/{MODEL_ID}/transcodings
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | L’identificatore del modello addestrato o pubblicato. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente un oggetto json con un elenco di ogni transcodifica eseguita sul modello. Ogni modello transcodificato riceve un identificatore univoco (`id`).

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

Per recuperare un modello transcodificato specifico, devi eseguire una richiesta GET con il `{MODEL_ID}` e l’id di un modello transcodificato.

**Formato API**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | L’identificatore univoco di un modello addestrato o pubblicato. |
| `{TRANSCODING_ID}` | L’identificatore univoco di un modello transcodificato. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente un oggetto JSON con i dati del modello transcodificato.

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
