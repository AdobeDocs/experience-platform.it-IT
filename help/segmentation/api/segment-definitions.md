---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definizioni dei segmenti
topic: developer guide
translation-type: tm+mt
source-git-commit: b3e6a6f1671a456b2ffa61139247c5799c495d92
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 4%

---


# Endpoint definizioni segmento

 Adobe Experience Platform consente di creare segmenti che definiscono un gruppo di attributi o comportamenti specifici da un gruppo di profili. Una definizione di segmento è un oggetto che racchiude una query scritta in [!DNL Profile Query Language] (PQL). Questo oggetto è anche denominato predicato PQL. I predicati PQL definiscono le regole per il segmento in base alle condizioni relative a qualsiasi record o dati delle serie temporali forniti da [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla scrittura di query PQL, consultate la guida [](../pql/overview.md) PQL.

Questa guida fornisce informazioni utili per comprendere meglio le definizioni dei segmenti e include chiamate API di esempio per eseguire azioni di base tramite l&#39;API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39; [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controllate la guida [](./getting-started.md) introduttiva per informazioni importanti che dovete conoscere per effettuare correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recupera un elenco di definizioni di segmento {#list}

È possibile recuperare un elenco di tutte le definizioni di segmento per l&#39;organizzazione IMS effettuando una richiesta di GET all&#39; `/segment/definitions` endpoint.

**Formato API**

L&#39; `/segment/definitions` endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Anche se questi parametri sono opzionali, il loro utilizzo è fortemente consigliato per ridurre i costi di sovraccarico. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperate tutte le definizioni di segmento disponibili per l&#39;organizzazione. È possibile includere più parametri, separati da e-mail (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Parametri query**

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `start` | Specifica l&#39;offset iniziale per le definizioni di segmento restituite. | `start=4` |
| `limit` | Specifica il numero di definizioni di segmento restituite per pagina. | `limit=20` |
| `page` | Specifica da quale pagina partiranno i risultati delle definizioni dei segmenti. | `page=5` |
| `sort` | Specifica per quale campo ordinare i risultati. È scritto nel seguente formato: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Specifica se la definizione del segmento è abilitata per lo streaming. | `evaluationInfo.continuous.enabled=true` |

**Richiesta**

Nella richiesta seguente vengono recuperate le ultime due definizioni di segmento pubblicate all’interno dell’organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
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
            "imsOrgId": "{IMS_ORG}",
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
                "value": "{PQL_EXPRESSION}"
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
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
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
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Creare una nuova definizione di segmento {#create}

Puoi creare una nuova definizione di segmento effettuando una richiesta di POST all’ `/segment/definitions` endpoint.

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
 -d '{
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
        "ttlInDays": 60
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | **Obbligatorio.** Un nome univoco con cui fare riferimento al segmento. |
| `schema` | **Obbligatorio.** Schema associato alle entità nel segmento. È costituito da un campo `id` o `name` . |
| `expression` | **Obbligatorio.** Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione in valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Un&#39;espressione conforme al tipo indicato in `expression.format`. |
| `description` | Descrizione leggibile della definizione. |

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

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID generato dal sistema della nuova definizione del segmento creata. |
| `evaluationInfo` | Un oggetto generato dal sistema che indica il tipo di valutazione cui verrà sottoposta la definizione del segmento. Può essere batch, continuo (noto anche come streaming) o segmentazione sincrona. |

## Recupera una definizione di segmento specifica {#get}

Puoi recuperare informazioni dettagliate su una definizione di segmento specifica effettuando una richiesta di GET all’ `/segment/definitions` endpoint e fornendo l’ID della definizione di segmento che desideri recuperare nel percorso della richiesta.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | Il `id` valore della definizione del segmento da recuperare. |

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

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID di sola lettura generato dal sistema per la definizione del segmento. |
| `name` | Un nome univoco con cui fare riferimento al segmento. |
| `schema` | Schema associato alle entità nel segmento. È costituito da un campo `id` o `name` . |
| `expression` | Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione in valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Un&#39;espressione conforme al tipo indicato in `expression.format`. |
| `description` | Una descrizione leggibile dell&#39;espressione. |
| `evaluationInfo` | Un oggetto generato dal sistema che indica il tipo di valutazione, batch, continuo (noto anche come streaming) o sincrono cui verrà sottoposta la definizione del segmento. |

## Recupero in blocco delle definizioni dei segmenti {#bulk-get}

Puoi recuperare informazioni dettagliate su più definizioni di segmento specificate effettuando una richiesta di POST all’ `/segment/definitions/bulk-get` endpoint e fornendo i `id` valori delle definizioni di segmento nel corpo della richiesta.

**Formato API**

```http
POST /segment/definitions/bulk-get
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 207 con le definizioni dei segmenti richieste.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
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
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
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

    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID di sola lettura generato dal sistema per la definizione del segmento. |
| `name` | Un nome univoco con cui fare riferimento al segmento. |
| `schema` | Schema associato alle entità nel segmento. È costituito da un campo `id` o `name` . |
| `expression` | Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione in valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Un&#39;espressione conforme al tipo indicato in `expression.format`. |
| `description` | Una descrizione leggibile dell&#39;espressione. |
| `evaluationInfo` | Un oggetto generato dal sistema che indica il tipo di valutazione, batch, continuo (noto anche come streaming) o sincrono cui verrà sottoposta la definizione del segmento. |

## Eliminare una definizione di segmento specifica {#delete}

Puoi richiedere di eliminare una definizione di segmento specifica effettuando una richiesta di DELETE all’ `/segment/definitions` endpoint e fornendo l’ID della definizione di segmento che desideri eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | Il `id` valore della definizione del segmento da eliminare. |

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

Puoi aggiornare una definizione di segmento specifica effettuando una richiesta di PATCH all’ `/segment/definitions` endpoint e fornendo l’ID della definizione di segmento che desideri aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | Il `id` valore della definizione del segmento da aggiornare. |

**Richiesta**

La seguente richiesta aggiornerà il paese dell&#39;indirizzo di lavoro dagli Stati Uniti al Canada.

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
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della nuova definizione di segmento aggiornata. Tenere presente che il paese dell&#39;indirizzo di lavoro è stato aggiornato dagli Stati Uniti (USA) al Canada (CA).

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
        "value": "workAddress.country = \"CA\""
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

## Passaggi successivi

Dopo aver letto questa guida è ora possibile comprendere meglio il funzionamento delle definizioni dei segmenti. Per ulteriori informazioni sulla creazione di un segmento, consulta l’esercitazione sulla [creazione di un segmento](../tutorials/create-a-segment.md) .