---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti comuni;esperimenti;api di apprendimento macchina sensei
solution: Experience Platform
title: Endpoint API per gli esperimenti
description: Lo sviluppo e la formazione dei modelli avviene a livello di Esperimento, dove un Esperimento è costituito da un’istanza MLI, da percorsi di formazione e da percorsi di valutazione.
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# Endpoint esperimento

Lo sviluppo e la formazione dei modelli avviene a livello di Esperimento, dove un Esperimento è costituito da un’istanza MLI, da percorsi di formazione e da percorsi di valutazione.

## Creare un esperimento {#create-an-experiment}

Puoi creare un esperimento eseguendo una richiesta di POST fornendo un nome e un ID istanza MLI valido nel payload della richiesta.

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
| `name` | Nome desiderato per l’esperimento. L’esecuzione di formazione corrispondente a questo esperimento erediterà questo valore da visualizzare nell’interfaccia utente come nome dell’esecuzione di formazione. |
| `mlInstanceId` | Un ID istanza valido. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli dell’esperimento appena creato, incluso l’identificatore univoco (`id`).

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

## Creazione ed esecuzione di un&#39;esecuzione di formazione o valutazione {#experiment-training-scoring}

Puoi creare esecuzioni di formazione o di punteggio eseguendo una richiesta di POST e fornendo un ID di esperimento valido e specificando l’attività di esecuzione. Le esecuzioni di valutazione possono essere create solo se l’esperimento dispone di un’esecuzione di formazione esistente e di successo. La creazione corretta di un&#39;esecuzione di formazione inizializzerà la procedura di formazione del modello e il suo completamento con successo genererà un modello addestrato. La generazione di modelli addestrati sostituirà quelli esistenti in precedenza, in modo tale che un esperimento possa utilizzare un solo modello addestrato in un dato momento.

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
| `{TASK}` | Specifica l&#39;attività dell&#39;esecuzione. Imposta questo valore come `train` per la formazione, `score` per il punteggio, oppure `featurePipeline` per la pipeline delle funzioni. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli della nuova esecuzione creata, inclusi i parametri di formazione o punteggio predefiniti ereditati, e l’ID univoco dell’esecuzione (`{RUN_ID}`).

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

## Recupera un elenco di esperimenti

È possibile recuperare un elenco di Esperimenti appartenenti a una particolare istanza MLI eseguendo una singola richiesta di GET e fornendo un ID istanza MLI valido come parametro di query. Per un elenco delle query disponibili, fare riferimento alla sezione dell&#39;appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).


**Formato API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Specifica un ID istanza valido per recuperare un elenco di esperimenti appartenenti a tale istanza MLI. |

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

## Recupera un esperimento specifico {#retrieve-specific}

Puoi recuperare i dettagli di un esperimento specifico eseguendo una richiesta di GET che include l’ID dell’esperimento desiderato nel percorso della richiesta.

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

## Recupera un elenco di esecuzioni di esperimenti

Puoi recuperare un elenco di esecuzioni di formazione o di punteggio appartenenti a un particolare esperimento eseguendo una singola richiesta di GET e fornendo un ID di esperimento valido. Per facilitare il filtro dei risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco completo dei parametri di query disponibili, consulta la sezione dell’appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).

>[!NOTE]
>
>Quando si combinano più parametri di query, devono essere separati da e commerciale (&amp;).

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
| `{VALUE}` | Il valore del parametro di query precedente. |

**Richiesta**

La richiesta seguente contiene una query e recupera un elenco di esecuzioni di formazione appartenenti ad alcuni Esperimenti.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un elenco di esecuzioni e ciascuno dei loro dettagli, compreso l’ID di esecuzione dell’esperimento (`{RUN_ID}`).

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

Puoi aggiornare un esperimento esistente sovrascrivendo le sue proprietà tramite una richiesta PUT che include l’ID dell’esperimento di destinazione nel percorso della richiesta e fornendo un payload JSON contenente proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta PUT, si consiglia innanzitutto di eseguire una richiesta GET a [recuperare l’esperimento per ID](#retrieve-specific). Quindi, modifica e aggiorna l’oggetto JSON restituito e applica l’intero oggetto JSON modificato come payload per la richiesta PUT.

La seguente chiamata API di esempio aggiorna il nome di un esperimento quando queste proprietà sono inizialmente disponibili:

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

Una risposta corretta restituisce un payload contenente i dettagli aggiornati dell’esperimento.

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

Puoi eliminare un singolo esperimento eseguendo una richiesta DELETE che include l’ID dell’esperimento di destinazione nel percorso della richiesta.

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

## Elimina esperimenti per ID istanza

Puoi eliminare tutti gli esperimenti appartenenti a una particolare istanza MLI eseguendo una richiesta DELETE che include l’ID istanza MLI come parametro di query.

**Formato API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | ---|
| `{MLINSTANCE_ID}` | Un ID istanza valido. |

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
