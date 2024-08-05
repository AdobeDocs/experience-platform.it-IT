---
keywords: Experience Platform; guida per sviluppatori; Endpoint; Data Science Area di lavoro; argomenti popolari; modelli; API di Machine Learning di Sensei
solution: Experience Platform
title: Endpoint API dei modelli
description: Un modello è un istanza di una ricetta di Machine Learning che viene addestrata utilizzando dati e configurazioni cronologici per risolvere un caso d'uso aziendale.
role: Developer
exl-id: e66119a9-9552-497c-9b3a-b64eb3b51fcf
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 4%

---

# Endpoint dei modelli

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

Un modello è un istanza di una ricetta di Machine Learning che viene addestrata utilizzando dati e configurazioni cronologici per risolvere un caso d&#39;uso aziendale.

## Recupera un elenco di modelli

È possibile recuperare un elenco di dettagli del modello appartenenti a tutti i modelli eseguendo una singola richiesta GET a /models. Per impostazione predefinita, questo elenco si ordina dal modello creato meno recente e limita i risultati a 25. È possibile scegliere di filtrare i risultati specificando alcuni parametri di query. Per un elenco delle query disponibili, fare riferimento alla sezione dell&#39;appendice sui [parametri di query per il recupero risorsa](./appendix.md#query).

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

Una risposta corretta restituisce un payload contenente i dettagli dei modelli, incluso l&#39;identificatore univoco di ciascun modello (`id`).

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
| `id` | ID corrispondente al modello. |
| `modelArtifactUri` | Un URI che indica dove è memorizzato il modello. L&#39;URI termina con il `name` valore del modello. |
| `experimentId` | Un ID esperimento valido. |
| `experimentRunId` | Un ID di esecuzione dell&#39;esperimento valido. |

## Recupera un modello specifico

È possibile recuperare un elenco di dettagli del modello appartenenti a un particolare modello eseguendo una singola richiesta GET e fornendo un ID modello valido nel percorso richiesta. Per filtrare i risultati, è possibile specificare parametri di query nel percorso richiesta. Per un elenco delle query disponibili, fare riferimento alla sezione dell&#39;appendice sui [parametri di query per il recupero risorsa](./appendix.md#query).

**Formato API**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello sottoposto a training o pubblicato. |
| `{EXPERIMENT_RUN_ID}` | Identificatore dell&#39;esperimento eseguito. |

**Richiesta**

Il seguente richiesta contiene una query e recupera un elenco di modelli sottoposti a training che condividono lo stesso experimentRunID ({EXPERIMENT_RUN_ID}).

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del modello, incluso l&#39;identificatore univoco del modello (`id`).

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
| `id` | ID corrispondente al modello. |
| `modelArtifactUri` | Un URI che indica dove è memorizzato il modello. L&#39;URI termina con il `name` valore del modello. |
| `experimentId` | Un ID esperimento valido. |
| `experimentRunId` | Un ID di esecuzione dell&#39;esperimento valido. |

## Registrare un modello pregenerato {#register-a-model}

È possibile registrare un modello pregenerato effettuando una richiesta POST all&#39;endpoint `/models` . Per registrare il modello, i `modelArtifact` valori di file e `model` proprietà devono essere inclusi nel corpo del richiesta.

**Formato API**

```http
POST /models
```

**Richiesta**

La POST seguente contiene i valori di `modelArtifact` file e `model` proprietà necessari. Per ulteriori informazioni su questi valori, vedere la tabella seguente.

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
| `modelArtifact` | La posizione dell&#39;artefatto modello completo che si desidera includere. |
| `model` | I dati del modulo dell&#39;oggetto Model da creare. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del modello, incluso l&#39;identificatore univoco del modello (`id`).

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
| `id` | ID corrispondente al modello. |
| `modelArtifactUri` | Un URI che indica dove è memorizzato il modello. L&#39;URI termina con il `id` valore del modello. |

## Aggiornamento di un modello per ID

È possibile aggiornare un modello esistente sovrascrivendone le proprietà tramite un richiesta PUT che include l&#39;ID del modello di destinazione nel percorso richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questo richiesta PUT, si consiglia innanzitutto di eseguire una richiesta GET per recuperare il modello in base all&#39;ID. Quindi, modificare e aggiornare l&#39;oggetto JSON restituito e applicare l&#39;intero oggetto JSON modificato come payload per il richiesta PUT.

**Formato API**

```http
PUT /models/{MODEL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello sottoposto a training o pubblicato. |

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

## Elimina un modello per ID

È possibile eliminare un singolo modello eseguendo una richiesta DELETE che includa l&#39;ID del modello destinazione nel percorso richiesta.

**Formato API**

```http
DELETE /models/{MODEL_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello sottoposto a training o pubblicato. |

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

Una risposta corretta restituisce un payload contenente uno stato 200 che conferma l&#39;eliminazione del modello.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## Crea una nuova transcodifica per un modello {#create-transcoded-model}

La transcodifica è la conversione diretta da digitale a digitale di una codifica in un&#39;altra. È possibile creare una nuova transcodifica per un modello fornendo la `{MODEL_ID}` e a `targetFormat` in cui si desidera inserire il nuovo output.

**Formato API**

```http
POST /models/{MODEL_ID}/transcodings
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello sottoposto a training o pubblicato. |

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

Una risposta corretta restituisce un payload contenente un oggetto JSON con le informazioni della transcodifica. Questo include l&#39;identificatore univoco delle transcodifiche (`id`) utilizzato per [recuperare uno specifico modello](#retrieve-transcoded-model) transcodificato.

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

È possibile recuperare un elenco di transcodifiche eseguite su un modello eseguendo una richiesta GET con .`{MODEL_ID}`

**Formato API**

```http
GET /models/{MODEL_ID}/transcodings
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | Identificatore del modello sottoposto a training o pubblicato. |

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

Una risposta corretta restituisce un payload contenente un oggetto json con un elenco di ogni transcodifica eseguita sul modello. Ogni modello transcodificato riceve un identificatore univoco (`id`).

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

## Recuperare uno specifico modello transcodificato {#retrieve-transcoded-model}

È possibile recuperare un modello transcodificato specifico eseguendo un richiesta GET con il proprio `{MODEL_ID}` e l&#39;ID di un modello transcodificato.

**Formato API**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MODEL_ID}` | L&#39;identificatore univoco di un modello sottoposto a training o pubblicato. |
| `{TRANSCODING_ID}` | Identificatore univoco di un modello transcodificato. |

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
