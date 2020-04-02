---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definizioni dei segmenti
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Guida per lo sviluppo delle definizioni di segmento

Adobe Experience Platform consente di creare segmenti che definiscono un gruppo di attributi o comportamenti specifici da un gruppo di profili.

Questa guida per gli sviluppatori fornisce istruzioni sulle seguenti aree per le definizioni dei segmenti:

- [Recupera un elenco di definizioni di segmento](#retrieve-a-list-of-segment-definitions)
- [Creare una nuova definizione di segmento](#create-a-new-segment-definition)
- [Recupera una definizione di segmento specifica](#retrieve-a-specific-segment-definition)
- [Eliminare una definizione di segmento specifica](#delete-a-specific-segment-definition)
- [Aggiornare una definizione di segmento specifica](#update-a-specific-segment-definition)

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte dell&#39;API di segmentazione. Prima di continuare, consulta la guida [per lo sviluppatore di](./getting-started.md)segmentazione.

In particolare, la sezione [](./getting-started.md#getting-started) introduttiva della guida per gli sviluppatori di segmentazione include collegamenti a argomenti correlati, una guida alla lettura delle chiamate API di esempio nel documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API della piattaforma Experience.

## Recupera un elenco di definizioni di segmento

È possibile recuperare un elenco di tutte le definizioni di segmento per l&#39;organizzazione IMS effettuando una richiesta GET all&#39; `/segment/definitions` endpoint.

**Formato API**

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facoltativo*) Parametri aggiunti al percorso di richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e-mail (`&`). I parametri disponibili sono elencati di seguito.

**Parametri query**

Di seguito è riportato un elenco di parametri di query disponibili per elencare le definizioni dei segmenti. Tutti questi parametri sono facoltativi. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperate tutte le definizioni di segmento disponibili per l&#39;organizzazione.

| Parametro | Descrizione |
| --------- | ----------- |
| `start` | ??? |
| `limit` | Specifica il numero di definizioni di segmento restituite per pagina. |
| `page` | Specifica da quale pagina partiranno i risultati delle definizioni dei segmenti. |
| `sort` | Specificato per quale campo ordinare i risultati. |
| `evaluationInfo.continuous.enabled` | Specifica se la definizione del segmento è abilitata per lo streaming. |

**Richiesta**

```shell
cur -X GET https://platform.adobe.io/data/core/ups/segment/definitions?QUERY \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di definizioni di segmento per l’organizzazione IMS specificata come JSON.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{\"nodeType\":\"select\",\"variables\":[{\"nodeType\":\"varDecl\",\"varName\":\"_Checkouts1\",\"from\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"xEvent\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}},\"where\":{\"nodeType\":\"fnApply\",\"fnName\":\"equals\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"eventType\",\"object\":{\"nodeType\":\"varRef\",\"varName\":\"_Checkouts1\"}},{\"literalType\":\"String\",\"nodeType\":\"literal\",\"value\":\"commerce.checkouts\"},{\"nodeType\":\"literal\",\"literalType\":\"Boolean\",\"value\":true}]}}]}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        ... ,
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"and\",\"params\":[{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"points\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"_acpstardust\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"Double\",\"nodeType\":\"literal\",\"value\":2}]},{\"nodeType\":\"fnApply\",\"fnName\":\"equals\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"testLoyaltyID\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"_acpstardust\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"String\",\"nodeType\":\"literal\",\"value\":\"\"},{\"nodeType\":\"literal\",\"literalType\":\"Boolean\",\"value\":false}]}]}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 4,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 4,
        "limit": 100
    },
    "link": {}
}
```

## Creare una nuova definizione di segmento

Puoi creare una nuova definizione di segmento effettuando una richiesta POST all’ `/segment/definitions` endpoint.

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
  "name": "People who ordered in the last 30 days",
  "profileInstanceId": "ups",
  "description": "Last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "payloadSchema": "string",
  "ttlInDays": 60,
  "creationTime": 0,
  "updateTime": 0,
  "updateEpoch": 0
}
 '
```

organigramma

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della nuova definizione del segmento creata.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

illustrazione del corpo e delle intestazioni

## Recupera una definizione di segmento specifica

Potete recuperare informazioni dettagliate su una definizione di segmento specifica effettuando una richiesta GET all&#39; `/segment/definitions` endpoint e fornendo il valore della definizione del segmento `id` nel percorso di richiesta.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}`: Il `id` valore della definizione del segmento da recuperare.

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla definizione del segmento specificata.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

## Eliminare una definizione di segmento specifica

Puoi richiedere di eliminare una definizione di segmento specificata eseguendo una richiesta DELETE all&#39; `/segment/definitions` endpoint e fornendo il valore della definizione di segmento `id` nel percorso della richiesta.

**Formato API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}` Il `id` valore della definizione del segmento da eliminare.

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 senza messaggio.

## Aggiornare una definizione di segmento specifica

Puoi aggiornare la definizione di un segmento specificato eseguendo una richiesta PATCH all’ `/segment/definitions` endpoint e fornendo il valore della definizione del segmento `id` nel percorso della richiesta.

**Formato API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

- `{SEGMENT_ID}`: Il `id` valore della definizione del segmento da aggiornare.

**Richiesta**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}
'
```

organigramma

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della nuova definizione di segmento aggiornata.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

spiegare corpo e intestazione

## Passaggi successivi
