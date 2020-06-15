---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: MLInances
topic: Developer guide
translation-type: tm+mt
source-git-commit: 0197c2f5e304f2fc194289b064cc37c91bb658c8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 4%

---


# MLInances

Un&#39;istanza MLI è un accoppiamento di un [motore](./engines.md) esistente con un set appropriato di configurazioni che definisce eventuali parametri di formazione, parametri di punteggio o configurazioni di risorse hardware.

## Creare un&#39;istanza MLI {#create-an-mlinstance}

Potete creare un&#39;istanza MLI eseguendo una richiesta POST fornendo al contempo un payload di richiesta costituito da un ID motore (`{ENGINE_ID}`) valido e da un set appropriato di configurazioni predefinite.

Se l’ID del motore fa riferimento a un motore PySpark o Spark Engine, potete configurare la quantità di risorse di calcolo, ad esempio il numero di core o la quantità di memoria. Se viene fatto riferimento a un Motore Python, potete scegliere se utilizzare una CPU o una GPU a scopo di formazione e valutazione. Per ulteriori informazioni, consulta le sezioni di appendice sulle configurazioni [delle risorse](./appendix.md#resource-config) PySpark e Spark e sulle configurazioni [della CPU e della GPU](./appendix.md#cpu-gpu-config) Python.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Il nome desiderato per l&#39;istanza MLIn. Il modello che corrisponde a questa istanza MLI erediterà questo valore per essere visualizzato nell&#39;interfaccia utente come nome del modello. |
| `description` | Una descrizione facoltativa per l&#39;istanza MLI. Il modello che corrisponde a questa istanza MLI erediterà questo valore per essere visualizzato nell&#39;interfaccia utente come descrizione del modello. Questa proprietà è obbligatoria. Se non si desidera fornire una descrizione, impostare il relativo valore su una stringa vuota. |
| `engineId` | ID di un motore esistente. |
| `tasks` | Set di configurazioni per la formazione, il punteggio o le tubazioni di feature. |

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

## Recuperare un elenco di istanze MLI

Potete recuperare un elenco di istanze MLI eseguendo una singola richiesta GET. Per facilitare il filtraggio dei risultati, potete specificare i parametri di query nel percorso di richiesta. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.

**Formato API**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno dei parametri [di query](./appendix.md#query) disponibili utilizzati per filtrare i risultati. |
| `{VALUE}` | Il valore del parametro di query precedente. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di istanze MLI e i relativi dettagli.

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

## Recuperare un&#39;istanza MLI specifica {#retrieve-specific}

Potete recuperare i dettagli di una specifica istanza MLIneseguendo una richiesta GET che include l&#39;ID dell&#39;istanza MLI desiderata nel percorso della richiesta.

**Formato API**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | L’ID dell’istanza MLI desiderata. |

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli dell&#39;istanza MLIninstance.

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

## Aggiornare un&#39;istanza MLI

Potete aggiornare un&#39;istanza MLI esistente sovrascrivendone le proprietà tramite una richiesta PUT che include l&#39;ID dell&#39;istanza MLI di destinazione nel percorso di richiesta e fornisce un payload JSON contenente le proprietà aggiornate.

>[!TIP] Per garantire il successo di questa richiesta PUT, si consiglia innanzitutto di eseguire una richiesta GET per [recuperare l&#39;istanza MLI per ID](#retrieve-specific). Quindi, modificate e aggiornate l&#39;oggetto JSON restituito e applicate l&#39;intero oggetto JSON modificato come payload per la richiesta PUT.

La seguente chiamata API di esempio aggiornerà i parametri di formazione e punteggio di un&#39;istanza MLInpur disponendo inizialmente di queste proprietà:

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
| `{MLINSTANCE_ID}` | Un ID istanza MLI valido. |

**Richiesta**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una risposta corretta restituisce un payload contenente i dettagli aggiornati dell&#39;istanza MLI.

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

Potete eliminare tutte le istanze MLI che condividono lo stesso motore eseguendo una richiesta di DELETE che include l’ID del motore come parametro di query.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

È possibile eliminare una singola istanza MLI eseguendo una richiesta DELETE che include l&#39;ID MLInance di destinazione nel percorso della richiesta.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
