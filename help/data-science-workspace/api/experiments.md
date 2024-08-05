---
keywords: Experience Platform; guida per sviluppatori; Endpoint; Data Science Area di lavoro; argomenti popolari; Esperimenti; API di Machine Learning di Sensei
solution: Experience Platform
title: Endpoint API esperimenti
description: Lo sviluppo e la training del modello avvengono a livello di esperimento, dove un esperimento è costituito da MLInstance, esecuzioni di training ed esecuzioni di punteggio.
role: Developer
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 4%

---

# Punto finale degli esperimenti

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

Lo sviluppo e la training del modello avvengono a livello di esperimento, dove un esperimento è costituito da MLInstance, esecuzioni di training ed esecuzioni di punteggio.

## Crea un esperimento {#create-an-experiment}

Puoi creare un esperimento eseguendo una richiesta POST fornendo un nome e un ID MLInstance valido nel payload richiesta.

>[!NOTE]
>
>A differenza dei training modello nell&#39;interfaccia, la creazione di un esperimento tramite una chiamata API esplicita non crea ed esegue automaticamente un&#39;esecuzione training.

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
| `mlInstanceId` | Un ID MLInstance valido. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli dell&#39;esperimento appena creato, incluso il relativo identificatore univoco (`id`).

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

## Crea ed eseguire una training o un&#39;esecuzione di punteggio {#experiment-training-scoring}

Puoi creare esecuzioni di training o di assegnazione di punteggi eseguendo un richiesta POST e fornendo un ID esperimento valido e specificando l&#39;attività di esecuzione. Le esecuzioni dei punteggi possono essere create solo se l&#39;esperimento dispone di un&#39;esecuzione training esistente e riuscita. La corretta creazione di un&#39;esecuzione di training inizializzerà la procedura di training del modello e il suo corretto completamento genererà un modello sottoposto a training. La generazione di modelli addestrati sostituirà quelli precedentemente esistenti in modo tale che un esperimento possa utilizzare solo un singolo modello addestrato in un dato momento.

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
| `{TASK}` | Specifica l&#39;attività di esecuzione. Imposta questo valore come per `train` training, `score` per il punteggio o `featurePipeline` per la pipeline di funzionalità. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli dell&#39;esecuzione appena creata, inclusi i parametri di training o punteggio predefiniti ereditati e l&#39;ID univoco dell&#39;esecuzione (`{RUN_ID}`).

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

Per recuperare un elenco di esperimenti appartenenti a una particolare istanza MLInstance, esegui una singola richiesta GET e fornisci un ID istanza MLInstance valido come parametro query. Per un elenco delle query disponibili, consulta la sezione dell&#39;appendice sui [parametri di query per il recupero delle risorse](./appendix.md#query).


**Formato API**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Fornisci un ID MLInstance valido per recuperare un elenco di esperimenti appartenenti a quella particolare MLInstance. |

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

Una risposta corretta restituisce un elenco di esperimenti che condividono lo stesso ID MLInstance (`{MLINSTANCE_ID}`).

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

Puoi recuperare i dettagli di un esperimento specifico eseguendo una richiesta GET che include l&#39;ID dell&#39;esperimento desiderato nel percorso richiesta.

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

Per recuperare un elenco di esecuzioni di formazione o punteggio appartenenti a un particolare esperimento, devi eseguire una singola richiesta di GET e fornire un ID esperimento valido. Per filtrare i risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco completo dei parametri di query disponibili, consulta la sezione dell&#39;appendice sui [parametri di query per il recupero delle risorse](./appendix.md#query).

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
| `{EXPERIMENT_ID}` | Un ID esperimento valido. |
| `{QUERY_PARAMETER}` | Uno dei parametri](./appendix.md#query) di query disponibili utilizzati per filtrare i [risultati. |
| `{VALUE}` | Valore del parametro di query precedente. |

**Richiesta**

Il seguente richiesta contiene una query e recupera un elenco di training esecuzioni appartenenti ad alcuni esperimenti.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un elenco di esecuzioni e ciascuno dei relativi dettagli, incluso l&#39;ID esecuzione dell&#39;esperimento (`{RUN_ID}`).

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

Puoi aggiornare un esperimento esistente sovrascrivendone le proprietà tramite un richiesta PUT che include l&#39;ID dell&#39;esperimento destinazione nel percorso richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questo richiesta PUT, si consiglia innanzitutto di eseguire una richiesta GET per [recuperare l&#39;esperimento per ID](#retrieve-specific). Quindi, modificare e aggiornare l&#39;oggetto JSON restituito e applicare l&#39;intero oggetto JSON modificato come payload per il richiesta PUT.

La seguente chiamata API di esempio aggiorna il nome di un esperimento pur avendo inizialmente queste proprietà:

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

## Elimina un esperimento

Puoi eliminare un singolo esperimento eseguendo una richiesta DELETE che includa l&#39;ID dell&#39;esperimento destinazione nel percorso richiesta.

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

## Elimina Esperimenti di MLInstance ID

È possibile eliminare tutti gli esperimenti appartenenti a una particolare MLInstance eseguendo una richiesta DELETE che include l&#39;ID MLInstance come parametro di query.

**Formato API**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | ---|
| `{MLINSTANCE_ID}` | Un ID MLInstance valido. |

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
