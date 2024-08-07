---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti popolari;mlinstances;sensei machine learning api
solution: Experience Platform
title: Endpoint API MLInstance
description: Un'istanza MLInstance è un accoppiamento di un motore esistente con un set appropriato di configurazioni che definisce eventuali parametri di formazione, parametri di punteggio o configurazioni di risorse hardware.
role: Developer
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 3%

---

# Endpoint MLInstance

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Un MLInstance è un accoppiamento di un [motore](./engines.md) esistente con un set di configurazioni appropriato che definisce eventuali parametri di formazione, parametri di punteggio o configurazioni di risorse hardware.

## Creare un&#39;istanza MLI {#create-an-mlinstance}

È possibile creare un&#39;istanza MLI eseguendo una richiesta POST e fornendo un payload di richiesta costituito da un ID motore valido (`{ENGINE_ID}`) e da un set appropriato di configurazioni predefinite.

Se l’ID motore fa riferimento a un PySpark o a un motore Spark, puoi configurare la quantità di risorse di calcolo, ad esempio il numero di core o la quantità di memoria. Se si fa riferimento a un motore Python, è possibile scegliere se utilizzare una CPU o una GPU a scopo di formazione e punteggio. Per ulteriori informazioni, fare riferimento alle sezioni dell&#39;appendice sulle [configurazioni](./appendix.md#resource-config) delle risorse PySpark e Spark e [sulle configurazioni di CPU e GPU](./appendix.md#cpu-gpu-config) Python.

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
| `name` | Nome desiderato per MLInstance. Il modello corrispondente a questa MLInstance erediterà questo valore da visualizzare nella interfaccia come nome del modello. |
| `description` | Una descrizione facoltativa per MLInstance. Il modello corrispondente a questa MLInstance erediterà questo valore da visualizzare in interfaccia come descrizione del modello. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostarne il valore come stringa vuota. |
| `engineId` | ID di un motore esistente. |
| `tasks` | Set di configurazioni per pipeline di training, punteggio o feature. |

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli della nuova istanza MLInstance creata, incluso il relativo identificatore univoco (`id`).

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

## Recuperare un elenco di istanze MLI

Per recuperare un elenco di MLInstance, esegui una singola richiesta GET. Per filtrare i risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco delle query disponibili, consulta la sezione dell&#39;appendice sui [parametri di query per il recupero delle risorse](./appendix.md#query).

**Formato API**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno dei [parametri di query disponibili](./appendix.md#query) utilizzati per filtrare i risultati. |
| `{VALUE}` | Valore per il parametro di query precedente. |

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

Una risposta corretta restituisce un elenco di MLInstance e i relativi dettagli.

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

## Recupera un&#39;istanza MLInstance specifica {#retrieve-specific}

È possibile recuperare i dettagli di una MLInstance specifica eseguendo una richiesta GET che include l&#39;ID della MLInstance desiderata nel percorso richiesta.

**Formato API**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | ID della MLInstance desiderata. |

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

Una risposta corretta restituisce i dettagli della MLInstance.

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

Puoi aggiornare un’istanza MLI esistente sovrascrivendo le relative proprietà tramite una richiesta PUT che include l’ID dell’istanza MLI di destinazione nel percorso della richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta PUT, si consiglia di eseguire prima una richiesta GET per [recuperare l&#39;istanza MLInstance tramite ID](#retrieve-specific). Quindi, modifica e aggiorna l’oggetto JSON restituito e applica l’intero oggetto JSON modificato come payload per la richiesta PUT.

La seguente chiamata API di esempio aggiornerà i parametri di training e punteggio di MLInstance, pur avendo inizialmente queste proprietà:

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
| `{MLINSTANCE_ID}` | Un ID MLInstance valido. |

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

Una risposta corretta restituisce un payload contenente i dettagli aggiornati di MLInstance.

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

## Elimina MLInstances per ID motore

È possibile eliminare tutte le MLInstance che condividono lo stesso motore eseguendo una richiesta DELETE che include l&#39;ID motore come parametro di query.

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

## Eliminare un’istanza MLI

Per eliminare una singola istanza MLInstance, devi eseguire una richiesta DELETE che includa l’ID dell’istanza MLInstance di destinazione nel percorso della richiesta.

**Formato API**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Un ID istanza MLI valido. |

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
