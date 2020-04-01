---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Approfondimenti
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Approfondimenti

Gli approfondimenti contengono metriche utilizzate per consentire a uno scienziato dei dati di valutare e scegliere modelli ML ottimali, mostrando metriche di valutazione rilevanti.

## Recupera un elenco di approfondimenti

Puoi recuperare un elenco di approfondimenti eseguendo una singola richiesta GET all&#39;endpoint di approfondimenti.  Per facilitare il filtraggio dei risultati, potete specificare i parametri di query nel percorso di richiesta. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.

**Formato API**

```http
GET /insights
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload che include un elenco di approfondimenti e ogni approfondimento ha un identificatore univoco ( `id` ). Inoltre, riceverai `context` che contiene gli identificatori univoci associati a tale approfondimento in seguito ai dati degli eventi e delle metriche Insights.

```json
{
    "children": [
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | L’ID corrispondente a Insight. |
| `experimentId` | Un ID di esperimento valido. |
| `experimentRunId` | Un ID di esecuzione dell&#39;esperimento valido. |
| `modelId` | Un ID modello valido. |

## Recuperare un&#39;interfaccia specifica

Per cercare una particolare conoscenza, effettuare una richiesta GET e fornire una valida `{INSIGHT_ID}` nel percorso della richiesta. Per facilitare il filtraggio dei risultati, potete specificare i parametri di query nel percorso di richiesta. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.

**Formato API**

```http
GET /insights/{INSIGHT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{INSIGHT_ID}` | Identificatore univoco di una visione Sensei. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/{INSIGHT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload che include l’identificatore univoco dell’analisi (`id`). Inoltre riceverai `context` che contiene gli identificatori univoci associati alle informazioni specifiche che seguono con gli eventi Insights e i dati delle metriche.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | L’ID corrispondente a Insight. |
| `experimentId` | Un ID di esperimento valido. |
| `experimentRunId` | Un ID di esecuzione dell&#39;esperimento valido. |
| `modelId` | Un ID modello valido. |

## Aggiungere una nuova conoscenza del modello

È possibile creare una nuova conoscenza del modello eseguendo una richiesta POST e un payload che fornisca contesto, eventi e metriche per la nuova visione del modello. Il campo contestuale utilizzato per creare una nuova conoscenza del modello non è necessario che vi siano servizi esistenti associati, ma potete scegliere di creare la nuova visione del modello con i servizi esistenti fornendo uno o più ID corrispondenti:

```json
"context": {
    "clientId": "{CLIENT_ID}",
    "notebookId": "{NOTEBOOK_ID}",
    "experimentId": "{EXPERIMENT_ID}",
    "engineId": "{ENGINE_ID}",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "modelId": "{MODEL_ID}",
    "dataSetId": "{DATASET_ID}"
  }
```

**Formato API**

```http
POST /insights
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**Risposta**

Una risposta corretta restituirà un payload con un `{INSIGHT_ID}` ed eventuali parametri forniti nella richiesta iniziale.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `insightId` | L’ID univoco creato per questa particolare approfondimento quando viene effettuata una richiesta POST di successo. |

## Recupera un elenco di metriche predefinite per gli algoritmi

Puoi recuperare un elenco di tutte le metriche dell&#39;algoritmo e predefinite eseguendo una singola richiesta GET all&#39;endpoint delle metriche. Per eseguire una query su una particolare metrica, effettuare una richiesta GET e fornire una valida `{ALGORITHM}` nel percorso della richiesta.

**Formato API**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parametro | Descrizione |
| --- | --- |
| `{ALGORITHM}` | Identificatore del tipo di algoritmo. |

**Richiesta**

La richiesta seguente contiene una query e recupera una metrica specifica utilizzando l&#39;identificatore dell&#39;algoritmo `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload che include l&#39;identificatore `algorithm` univoco e un array di metriche predefinite.

```json
{
    "children": [
        {
            "algorithm": "{ALGORITHM}",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```
