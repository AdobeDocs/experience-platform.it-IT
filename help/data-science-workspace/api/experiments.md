---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Esperimenti
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 4%

---


# Esperimenti

Lo sviluppo di modelli e la formazione si svolgono a livello di Esperimento, dove un Esperimento consiste in un&#39;istanza MLI, in esecuzioni di formazione e in esecuzioni di punteggio.

## Creare un esperimento {#create-an-experiment}

Potete creare un esperimento eseguendo una richiesta POST fornendo al contempo un nome e un ID MLInvalido nel payload della richiesta.

>[!NOTE]
>
>A differenza della formazione sui modelli nell’interfaccia utente, la creazione di un esperimento tramite una chiamata API esplicita non crea ed esegue automaticamente un’esecuzione di formazione.

**Formato API**

```http
POST /experiments
```

**Richiesta**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Il nome desiderato per l&#39;esperimento. L’esecuzione della formazione corrispondente a questo esperimento erediterà questo valore per essere visualizzato nell’interfaccia utente come nome dell’esecuzione della formazione. |
| `mlInstanceId` | Un ID istanza MLI valido. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli dell’esperimento appena creato, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Creazione ed esecuzione di un&#39;esecuzione di formazione o punteggio {#experiment-training-scoring}

Potete creare le esecuzioni di formazione o punteggio eseguendo una richiesta POST e fornendo un ID di esperimento valido e specificando l&#39;attività di esecuzione. Le esecuzioni di punteggio possono essere create solo se l’esperimento dispone di un’esecuzione di formazione esistente e di successo. La creazione di un&#39;esecuzione di formazione corretta inizializzerà la procedura di formazione del modello e il suo completamento genererà un modello qualificato. La generazione di modelli formati sostituirà quelli esistenti in precedenza, in modo che un esperimento possa utilizzare un solo modello addestrato in qualsiasi momento.

**Formato API**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID di esperimento valido. |

**Richiesta**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `{TASK}` | Specifica l&#39;attività dell&#39;esecuzione. Impostate questo valore come `train` per la formazione, `score` per il punteggio o `featurePipeline` per la pipeline delle funzioni. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli della nuova esecuzione creata, inclusi i parametri di formazione o punteggio predefiniti ereditati, e l&#39;ID univoco dell&#39;esecuzione (`{RUN_ID}`).

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Recuperare un elenco di esperimenti

Potete recuperare un elenco di Esperimenti appartenenti a una particolare istanza MLIneseguendo una singola richiesta GET e fornendo un ID MLInvalido come parametro di query. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.


**Formato API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Fornire un ID MLInvalido per recuperare un elenco di Esperimenti appartenenti a tale istanza MLI. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di Esperimenti che condividono lo stesso ID istanza (`{MLINSTANCE_ID}`).

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## Recuperare un esperimento specifico {#retrieve-specific}

Potete recuperare i dettagli di un esperimento specifico eseguendo una richiesta GET che include l&#39;ID dell&#39;esperimento desiderato nel percorso della richiesta.

**Formato API**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID di esperimento valido. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli dell’esperimento richiesto.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Recuperare un elenco di esecuzioni sperimentali

Potete recuperare un elenco di sessioni di formazione o di valutazione appartenenti a un particolare esperimento eseguendo una singola richiesta GET e fornendo un ID di esperimento valido. Per facilitare il filtraggio dei risultati, potete specificare i parametri di query nel percorso di richiesta. Per un elenco completo dei parametri di query disponibili, consultate la sezione appendice sui parametri di [query per il recupero](./appendix.md#query)delle risorse.

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da e commerciale (&amp;).

**Formato API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID di esperimento valido. |
| `{QUERY_PARAMETER}` | Uno dei parametri [di query](./appendix.md#query) disponibili utilizzati per filtrare i risultati. |
| `{VALUE}` | Il valore del parametro di query precedente. |

**Richiesta**

La richiesta seguente contiene una query e recupera un elenco di esecuzioni di formazione appartenenti ad alcuni Esperimenti.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un elenco di esecuzioni e ciascuno dei relativi dettagli, incluso il relativo ID di esecuzione degli esperimenti (`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Aggiornare un esperimento

Potete aggiornare un esperimento esistente sovrascrivendone le proprietà tramite una richiesta PUT che include l&#39;ID dell&#39;esperimento di destinazione nel percorso della richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta PUT, si consiglia di eseguire prima una richiesta GET per [recuperare l&#39;esperimento con ID](#retrieve-specific). Quindi, modificate e aggiornate l&#39;oggetto JSON restituito e applicate l&#39;intero oggetto JSON modificato come payload per la richiesta PUT.

La seguente chiamata API di esempio aggiorna il nome di un Esperimento pur avendo inizialmente queste proprietà:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**Formato API**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID di esperimento valido. |

**Richiesta**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli aggiornati dell&#39;esperimento.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Eliminare un esperimento

Potete eliminare un singolo esperimento eseguendo una richiesta DELETE che include l&#39;ID dell&#39;esperimento di destinazione nel percorso della richiesta.

**Formato API**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID di esperimento valido. |

**Richiesta**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Elimina esperimenti per ID istanza

Potete eliminare tutti gli Esperimenti appartenenti a una particolare istanza MLI eseguendo una richiesta DELETE che include l’ID di istanza MLI come parametro di query.

**Formato API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | ---|
| `{MLINSTANCE_ID}` | Un ID istanza MLI valido. |

**Richiesta**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiments successfully deleted"
}
```
