---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modelli
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Modelli

Un modello è un&#39;istanza di una ricetta di machine learning che viene formata utilizzando dati storici e configurazioni per risolvere un caso d&#39;uso aziendale.

## Recupera un elenco di Modelli

È possibile recuperare un elenco di dettagli modello appartenenti a tutti i modelli eseguendo una singola richiesta GET a /models. Per impostazione predefinita, questo elenco si ordina dal modello meno recente creato e limita i risultati a 25. Potete scegliere di filtrare i risultati specificando alcuni parametri di query. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.

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
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 2",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 3",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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

È possibile recuperare un elenco di dettagli del modello appartenenti a un particolare modello eseguendo una singola richiesta GET e fornendo un ID modello valido nel percorso della richiesta. Per facilitare il filtraggio dei risultati, potete specificare i parametri di query nel percorso di richiesta. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.

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
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID} \
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
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "property": "experimentRunId=={EXPERIMENT_RUN_ID},deleted==false",
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

## Aggiornare un modello in base all&#39;ID

È possibile aggiornare un modello esistente sovrascrivendone le proprietà tramite una richiesta PUT che include l&#39;ID del modello di destinazione nel percorso di richiesta e fornisce un payload JSON contenente le proprietà aggiornate.

>[!TIP] Per garantire il successo di questa richiesta PUT, si consiglia di eseguire prima una richiesta GET per recuperare il modello per ID. Quindi, modificate e aggiornate l&#39;oggetto JSON restituito e applicate l&#39;intero oggetto JSON modificato come payload per la richiesta PUT.

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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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

È possibile eliminare un singolo modello eseguendo una richiesta DELETE che include l&#39;ID del modello di destinazione nel percorso della richiesta.

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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
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
