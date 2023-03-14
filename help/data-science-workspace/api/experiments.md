---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti popolari;esperimenti;sensei machine learning api
solution: Experience Platform
title: Endpoint API per esperimenti
description: Lo sviluppo e l’addestramento dei modelli si verificano a livello di esperimento, dove un esperimento è costituito da un’istanza MLI, esecuzioni di addestramento e esecuzioni di punteggio.
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# Endpoint &quot;experiment&quot;

Lo sviluppo e l’addestramento dei modelli si verificano a livello di esperimento, dove un esperimento è costituito da un’istanza MLI, esecuzioni di addestramento e esecuzioni di punteggio.

## Creare un esperimento {#create-an-experiment}

Per creare un esperimento, esegui una richiesta POST e fornisci un nome e un ID MLInstance valido nel payload della richiesta.

>[!NOTE]
>
>A differenza dell’apprendimento dei modelli nell’interfaccia utente, la creazione di un esperimento tramite una chiamata API esplicita non crea ed esegue automaticamente un’esecuzione di apprendimento.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Il nome desiderato per l’esperimento. L’esecuzione dell’addestramento corrispondente a questo esperimento erediterà questo valore per essere visualizzato nell’interfaccia utente come nome dell’esecuzione dell’addestramento. |
| `mlInstanceId` | Un ID istanza MLI valido. |

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli dell’esperimento appena creato, compreso il relativo identificatore univoco (`id`).

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

## Creare ed eseguire un’esecuzione di apprendimento o punteggio {#experiment-training-scoring}

Per creare esecuzioni di formazione o punteggio, esegui una richiesta POST e fornisci un ID esperimento valido, specificando l’attività di esecuzione. È possibile creare esecuzioni di punteggio solo se l’esperimento dispone di un’esecuzione di apprendimento esistente e corretta. La creazione di un&#39;esecuzione di apprendimento comporta l&#39;inizializzazione della procedura di apprendimento del modello e il suo completamento genera un modello addestrato. La generazione di modelli addestrati sostituirà quelli esistenti in precedenza, in modo che un Esperimento possa utilizzare un solo modello addestrato in un dato momento.

**Formato API**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID esperimento valido. |

**Richiesta**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `{TASK}` | Specifica l&#39;attività dell&#39;esecuzione. Imposta questo valore come `train` per la formazione, `score` per il punteggio, oppure `featurePipeline` per la tubazione di feature. |

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli della nuova esecuzione creata, inclusi i parametri predefiniti di formazione o punteggio ereditati e l’ID univoco dell’esecuzione (`{RUN_ID}`).

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

Per recuperare un elenco di esperimenti appartenenti a una particolare istanza MLInstance, esegui una singola richiesta GET e fornisci un ID istanza MLInstance valido come parametro query. Per un elenco delle query disponibili, consulta la sezione dell’appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).


**Formato API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Fornisci un ID istanza MLI valido per recuperare un elenco di esperimenti appartenenti a quella particolare istanza MLI. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di esperimenti che condividono lo stesso ID istanza MLI (`{MLINSTANCE_ID}`).

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

Per recuperare i dettagli di un esperimento specifico, esegui una richiesta di GET che include l’ID dell’esperimento desiderato nel percorso della richiesta.

**Formato API**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID esperimento valido. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Recuperare un elenco di esecuzioni di esperimenti

Per recuperare un elenco di esecuzioni di formazione o punteggio appartenenti a un particolare esperimento, devi eseguire una singola richiesta di GET e fornire un ID esperimento valido. Per filtrare i risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco completo dei parametri di query disponibili, consulta la sezione dell’appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).

>[!NOTE]
>
>Quando si combinano più parametri di query, questi devono essere separati da un simbolo &amp;.

**Formato API**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID esperimento valido. |
| `{QUERY_PARAMETER}` | Uno dei [parametri di query disponibili](./appendix.md#query) utilizzato per filtrare i risultati. |
| `{VALUE}` | Valore per il parametro di query precedente. |

**Richiesta**

La richiesta seguente contiene una query e recupera un elenco di esecuzioni di addestramento appartenenti a un esperimento.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente un elenco di esecuzioni e ciascuno dei relativi dettagli, incluso l’ID esecuzione dell’esperimento (`{RUN_ID}`).

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

Puoi aggiornare un esperimento esistente sovrascrivendo le relative proprietà tramite una richiesta PUT che include l’ID dell’esperimento target nel percorso della richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta PUT, si consiglia di eseguire prima una richiesta GET a [recupera l’esperimento per ID](#retrieve-specific). Quindi, modifica e aggiorna l’oggetto JSON restituito e applica l’intero oggetto JSON modificato come payload per la richiesta PUT.

La chiamata API di esempio seguente aggiorna il nome di un esperimento quando si hanno inizialmente queste proprietà:

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
| `{EXPERIMENT_ID}` | Un ID esperimento valido. |

**Richiesta**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli aggiornati dell’esperimenti.

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

Puoi eliminare un singolo esperimento eseguendo una richiesta DELETE che include l’ID dell’esperimento target nel percorso della richiesta.

**Formato API**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{EXPERIMENT_ID}` | Un ID esperimento valido. |

**Richiesta**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Elimina esperimenti per ID istanza MLI

Puoi eliminare tutti gli esperimenti appartenenti a una particolare istanza MLI eseguendo una richiesta DELETE che includa l’ID istanza MLI come parametro di query.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
