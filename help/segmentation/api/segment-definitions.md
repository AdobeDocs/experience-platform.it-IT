---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;definizione del segmento;definizioni del segmento;API;API;
solution: Experience Platform
title: Endpoint API per le definizioni dei segmenti
topic-legacy: developer guide
description: L’endpoint per le definizioni dei segmenti nell’API del servizio di segmentazione di Adobe Experience Platform consente di gestire in modo programmatico le definizioni dei segmenti per la tua organizzazione.
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 3%

---

# Endpoint per le definizioni dei segmenti

Adobe Experience Platform consente di creare segmenti che definiscono un gruppo di attributi o comportamenti specifici da un gruppo di profili. Una definizione di segmento è un oggetto che incapsula una query scritta in [!DNL Profile Query Language] (PQL). Questo oggetto è anche denominato predicato PQL. I predicati PQL definiscono le regole per il segmento in base alle condizioni relative a qualsiasi record o dato della serie temporale fornito a [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla scrittura di query PQL, consulta la [Guida PQL](../pql/overview.md) .

Questa guida fornisce informazioni utili per comprendere meglio le definizioni dei segmenti e include chiamate API di esempio per l’esecuzione di azioni di base tramite l’API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell’ API [!DNL Adobe Experience Platform Segmentation Service] . Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recupera un elenco di definizioni di segmenti {#list}

Puoi recuperare un elenco di tutte le definizioni di segmenti per la tua organizzazione IMS effettuando una richiesta di GET all’ endpoint `/segment/definitions` .

**Formato API**

L’endpoint `/segment/definitions` supporta diversi parametri di query per filtrare i risultati. Sebbene questi parametri siano opzionali, si consiglia vivamente di utilizzarli per ridurre i costi di overhead. Effettuare una chiamata a questo endpoint senza parametri recupererà tutte le definizioni di segmenti disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciali (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Parametri query**

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `start` | Specifica l’offset iniziale per le definizioni dei segmenti restituite. | `start=4` |
| `limit` | Specifica il numero di definizioni di segmento restituite per pagina. | `limit=20` |
| `page` | Specifica da quale pagina partiranno i risultati delle definizioni dei segmenti. | `page=5` |
| `sort` | Specifica il campo in cui ordinare i risultati. È scritto nel seguente formato: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Specifica se la definizione del segmento è abilitata per lo streaming. | `evaluationInfo.continuous.enabled=true` |

**Richiesta**

Nella richiesta seguente vengono recuperate le ultime due definizioni di segmenti pubblicate nell’organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di definizioni di segmenti per l’organizzazione IMS specificata come JSON.

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

Puoi creare una nuova definizione di segmento effettuando una richiesta POST all’endpoint `/segment/definitions` .

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
| `schema` | **Obbligatorio.** Lo schema associato alle entità nel segmento. È costituito da un campo `id` o `name`. |
| `expression` | **Obbligatorio.** Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione nel valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |
| `description` | Una descrizione della definizione leggibile dall&#39;uomo. |

>[!NOTE]
>
>Un&#39;espressione di definizione del segmento può fare riferimento anche a un attributo calcolato. Per ulteriori informazioni, consulta la [guida all’endpoint API calcolato](../../profile/computed-attributes/ca-api.md)
>
>La funzionalità dell&#39;attributo calcolato è in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

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
| `evaluationInfo` | Un oggetto generato dal sistema che indica a quale tipo di valutazione verrà sottoposta la definizione del segmento. Può essere batch, continuo (noto anche come streaming) o segmentazione sincrona. |

## Recupera una definizione di segmento specifica {#get}

Puoi recuperare informazioni dettagliate su una definizione di segmento specifica effettuando una richiesta di GET all’ endpoint `/segment/definitions` e fornendo l’ID della definizione di segmento che desideri recuperare nel percorso della richiesta.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | Il valore `id` della definizione del segmento da recuperare. |

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
| `id` | ID di sola lettura generato dal sistema della definizione del segmento. |
| `name` | Un nome univoco con cui fare riferimento al segmento. |
| `schema` | Lo schema associato alle entità nel segmento. È costituito da un campo `id` o `name`. |
| `expression` | Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione nel valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |
| `description` | Descrizione umana leggibile della definizione. |
| `evaluationInfo` | Un oggetto generato dal sistema che indica il tipo di valutazione, batch, continuo (noto anche come streaming) o sincrono, cui verrà sottoposta la definizione del segmento. |

## Recupera in blocco le definizioni dei segmenti {#bulk-get}

È possibile recuperare informazioni dettagliate su più definizioni di segmenti specificate effettuando una richiesta POST all&#39;endpoint `/segment/definitions/bulk-get` e fornendo i valori `id` delle definizioni di segmenti nel corpo della richiesta.

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
| `id` | ID di sola lettura generato dal sistema della definizione del segmento. |
| `name` | Un nome univoco con cui fare riferimento al segmento. |
| `schema` | Lo schema associato alle entità nel segmento. È costituito da un campo `id` o `name`. |
| `expression` | Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione nel valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |
| `description` | Descrizione umana leggibile della definizione. |
| `evaluationInfo` | Un oggetto generato dal sistema che indica il tipo di valutazione, batch, continuo (noto anche come streaming) o sincrono, cui verrà sottoposta la definizione del segmento. |

## Eliminare una definizione di segmento specifica {#delete}

Puoi richiedere di eliminare una definizione di segmento specifica effettuando una richiesta di DELETE all’ endpoint `/segment/definitions` e fornendo l’ID della definizione di segmento da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | Il valore `id` della definizione del segmento da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 senza alcun messaggio.

## Aggiornare una definizione di segmento specifica

Puoi aggiornare una definizione di segmento specifica effettuando una richiesta di PATCH all’ endpoint `/segment/definitions` e fornendo l’ID della definizione di segmento che desideri aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | Il valore `id` della definizione del segmento da aggiornare. |

**Richiesta**

La seguente richiesta aggiornerà il paese dell&#39;indirizzo di lavoro dagli USA al Canada.

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

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della nuova definizione di segmento aggiornata. Si noti che il paese dell&#39;indirizzo di lavoro è stato aggiornato dagli Stati Uniti (USA) al Canada (CA).

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

## Convertire la definizione del segmento

Puoi convertire una definizione di segmento tra `pql/text` e `pql/json` o `pql/json` in `pql/text` effettuando una richiesta POST all’endpoint `/segment/conversion`.

**Formato API**

```http
POST /segment/conversion
```

**Richiesta**

Nella richiesta seguente viene modificato il formato della definizione del segmento da `pql/text` a `pql/json`.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
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

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della nuova definizione del segmento convertito.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Passaggi successivi

Dopo aver letto questa guida hai ora una migliore comprensione del funzionamento delle definizioni dei segmenti. Per ulteriori informazioni sulla creazione di un segmento, consulta l’ esercitazione [creazione di un segmento](../tutorials/create-a-segment.md) .
