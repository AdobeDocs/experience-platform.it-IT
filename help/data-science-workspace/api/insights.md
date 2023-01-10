---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti comuni;informazioni;api di apprendimento automatico sensei
solution: Experience Platform
title: Endpoint API Insights
description: Gli approfondimenti contengono metriche utilizzate per consentire a uno scienziato dei dati di valutare e scegliere modelli ML ottimali visualizzando le metriche di valutazione pertinenti.
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# Endpoint Insights

Gli approfondimenti contengono metriche utilizzate per consentire a uno scienziato dei dati di valutare e scegliere modelli ML ottimali visualizzando le metriche di valutazione pertinenti.

## Recupera un elenco di informazioni approfondite

Puoi recuperare un elenco di informazioni approfondite eseguendo una singola richiesta di GET all’endpoint di insights.  Per facilitare il filtro dei risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco delle query disponibili, fare riferimento alla sezione dell&#39;appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload che include un elenco di approfondimenti e ogni insight ha un identificatore univoco ( `id` ). Inoltre riceverai `context` che contiene gli identificatori univoci associati a tali informazioni specifiche a seguito dei dati relativi agli eventi e alle metriche Approfondimenti .

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `experimentId` | Un ID esperimento valido. |
| `experimentRunId` | Un ID esecuzione esperimento valido. |
| `modelId` | Un ID modello valido. |

## Recuperare un Insight specifico

Per cercare una particolare informazione, effettuare una richiesta GET e fornire una valida `{INSIGHT_ID}` nel percorso della richiesta. Per facilitare il filtro dei risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco delle query disponibili, fare riferimento alla sezione dell&#39;appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).

**Formato API**

```http
GET /insights/{INSIGHT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{INSIGHT_ID}` | Identificatore univoco di un insight Sensei. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload che include l’identificatore univoco delle informazioni (`id`). Inoltre riceverai `context` che contiene gli identificatori univoci associati alle informazioni specifiche che seguono i dati relativi agli eventi e alle metriche Approfondimenti .

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `experimentId` | Un ID esperimento valido. |
| `experimentRunId` | Un ID esecuzione esperimento valido. |
| `modelId` | Un ID modello valido. |

## Aggiungere una nuova intuizione del modello

È possibile creare una nuova intuizione del modello eseguendo una richiesta di POST e un payload che forniscono contesto, eventi e metriche per la nuova intuizione del modello. Il campo di contesto utilizzato per creare una nuova intuizione modello non è necessario che vi siano servizi esistenti collegati, ma puoi scegliere di creare la nuova intuizione modello con i servizi esistenti fornendo uno o più ID corrispondenti:

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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

Una risposta corretta restituirà un payload con un `{INSIGHT_ID}` e tutti i parametri forniti nella richiesta iniziale.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `insightId` | L’ID univoco creato per questa informazione quando viene effettuata una richiesta POST corretta. |

## Recupera un elenco di metriche predefinite per gli algoritmi

Puoi recuperare un elenco di tutte le metriche dell’algoritmo e predefinite eseguendo una singola richiesta di GET all’endpoint delle metriche. Per eseguire una query su una particolare metrica, effettuare una richiesta di GET e fornire una valida `{ALGORITHM}` nel percorso della richiesta.

**Formato API**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parametro | Descrizione |
| --- | --- |
| `{ALGORITHM}` | Identificatore del tipo di algoritmo. |

**Richiesta**

La richiesta seguente contiene una query e recupera una metrica specifica utilizzando l’identificatore dell’algoritmo `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload che include `algorithm` identificatore univoco e array di metriche predefinite.

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
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
