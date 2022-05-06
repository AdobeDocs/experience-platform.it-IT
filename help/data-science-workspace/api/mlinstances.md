---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti popolari;istanze multiple;api di apprendimento automatico sensei
solution: Experience Platform
title: Endpoint API per le istanze mobili
topic-legacy: Developer guide
description: Un'istanza MLI è un'associazione di un motore esistente con un set appropriato di configurazioni che definisce eventuali parametri di formazione, parametri di punteggio o configurazioni di risorse hardware.
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 4%

---

# Endpoint MLInases

Un&#39;istanza MLI è un&#39;associazione di un esistente [Motore](./engines.md) con un set appropriato di configurazioni che definisca eventuali parametri di formazione, parametri di punteggio o configurazioni di risorse hardware.

## Creare un&#39;istanza MLI {#create-an-mlinstance}

Puoi creare un’istanza MLI eseguendo una richiesta POST fornendo al contempo un payload di richiesta costituito da un ID motore valido (`{ENGINE_ID}`) e un set appropriato di configurazioni predefinite.

Se l&#39;ID del motore fa riferimento a un PySpark o a un motore Spark, puoi configurare la quantità di risorse di calcolo, ad esempio il numero di core o la quantità di memoria. Se si fa riferimento a un motore Python, è possibile scegliere se utilizzare una CPU o una GPU a scopo di formazione e valutazione. Fare riferimento alle sezioni dell&#39;appendice [Configurazioni delle risorse PySpark e Spark](./appendix.md#resource-config) e [Configurazioni CPU e GPU Python](./appendix.md#cpu-gpu-config) per ulteriori informazioni.

**Formato API**

```http
POST /mlInstances
```

**Richiesta**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "training parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "scoring parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "fp",
                "parameters": [
                    {
                        "key": "feature pipeline parameter",
                        "value": "parameter value"
                    }
                ]
            }
        ],
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome desiderato per l&#39;istanza MLI. Il modello corrispondente a questa istanza MLI erediterà questo valore da visualizzare nell&#39;interfaccia utente come nome del modello. |
| `description` | Una descrizione facoltativa per l&#39;istanza MLI. Il modello corrispondente a questa istanza MLI erediterà questo valore da visualizzare nell&#39;interfaccia utente come descrizione del modello. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostare il relativo valore su una stringa vuota. |
| `engineId` | ID di un motore esistente. |
| `tasks` | Un insieme di configurazioni per la formazione, il punteggio o le pipeline di funzioni. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli dell’istanza MLI appena creata, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "fp",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Recupera un elenco di istanze MLI

È possibile recuperare un elenco di istanze MLI eseguendo una singola richiesta di GET. Per facilitare il filtro dei risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco delle query disponibili, fare riferimento alla sezione dell&#39;appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).

**Formato API**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno dei [parametri di query disponibili](./appendix.md#query) utilizzato per filtrare i risultati. |
| `{VALUE}` | Il valore del parametro di query precedente. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di istanze MLI e relativi dettagli.

```json
{
    "children": [
        {
            "id": "46986c8f-7739-4376-8509-0178bdf32cda",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "56986c8f-7739-4376-8509-0178bdf32cda",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "32f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 2,
        "count": 2
    }
}
```

## Recupera un&#39;istanza MLI specifica {#retrieve-specific}

Puoi recuperare i dettagli di un’istanza MLI specifica eseguendo una richiesta di GET che include l’ID dell’istanza MLI desiderata nel percorso della richiesta.

**Formato API**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | ID dell&#39;istanza MLI desiderata. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli dell&#39;istanza MLI.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "featurePipeline",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Aggiornare un’istanza MLI

Puoi aggiornare un’istanza MLI esistente sovrascrivendo le sue proprietà tramite una richiesta PUT che include l’ID dell’istanza MLI di destinazione nel percorso della richiesta e fornendo un payload JSON contenente proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta PUT, si consiglia innanzitutto di eseguire una richiesta GET a [recupera l&#39;istanza MLI per ID](#retrieve-specific). Quindi, modifica e aggiorna l’oggetto JSON restituito e applica l’intero oggetto JSON modificato come payload per la richiesta PUT.

La seguente chiamata API di esempio aggiornerà i parametri di formazione e valutazione di un MLInance quando queste proprietà sono inizialmente disponibili:

```json
{
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.3"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-dataset-000"
                }
            ]
        }
    ]
}
```

**Formato API**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Un ID istanza valido. |

**Richiesta**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "00000000-0000-0000-0000-000000000000",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "displayName": "Jane Doe",
            "userId": "Jane_Doe@AdobeID"
        },
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "learning_rate",
                        "value": "0.5"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "output_dataset_id",
                        "value": "output-dataset-001"
                    }
                ]
            }
        ]
    }'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli aggiornati dell’istanza MLI.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.5"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-data-set-001"
                }
            ]
        }
    ]
}
```

## Eliminare le istanze MLI per ID motore

Puoi eliminare tutte le istanze MLI che condividono lo stesso motore eseguendo una richiesta DELETE che include l’ID del motore come parametro di query.

**Formato API**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{ENGINE_ID}` | Un ID motore valido. |

**Richiesta**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
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
    "detail": "MLInstances successfully deleted"
}
```

## Eliminare un&#39;istanza MLI

Puoi eliminare una singola istanza MLI eseguendo una richiesta DELETE che include l’ID MLInance di destinazione nel percorso della richiesta.

**Formato API**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Un ID istanza valido. |

**Richiesta**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLInstance deletion was successful"
}
```
