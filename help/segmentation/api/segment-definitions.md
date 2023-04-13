---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;definizione del segmento;definizioni dei segmenti;API;API;
solution: Experience Platform
title: Endpoint API per le definizioni dei segmenti
description: L’endpoint per le definizioni dei segmenti nell’API del servizio di segmentazione di Adobe Experience Platform consente di gestire in modo programmatico le definizioni dei segmenti per la tua organizzazione.
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 4%

---

# Endpoint per le definizioni dei segmenti

Adobe Experience Platform consente di creare segmenti che definiscono un gruppo di attributi o comportamenti specifici da un gruppo di profili. Una definizione di segmento è un oggetto che incapsula una query scritta in [!DNL Profile Query Language] (PQL). Questo oggetto è anche denominato predicato PQL. I predicati PQL definiscono le regole per il segmento in base alle condizioni relative a qualsiasi record o ai dati delle serie temporali forniti [!DNL Real-Time Customer Profile]. Consulta la sezione [Guida PQL](../pql/overview.md) per ulteriori informazioni sulla scrittura di query PQL.

Questa guida fornisce informazioni utili per comprendere meglio le definizioni dei segmenti e include chiamate API di esempio per l’esecuzione di azioni di base tramite l’API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recupera un elenco di definizioni di segmenti {#list}

Puoi recuperare un elenco di tutte le definizioni di segmenti per la tua organizzazione effettuando una richiesta di GET al `/segment/definitions` punto finale.

**Formato API**

La `/segment/definitions` l’endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Sebbene questi parametri siano opzionali, si consiglia vivamente di utilizzarli per ridurre i costi di overhead. Effettuare una chiamata a questo endpoint senza parametri recupererà tutte le definizioni di segmenti disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciale (`&`).

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

Nella richiesta seguente vengono recuperate le ultime due definizioni di segmenti pubblicate all’interno dell’organizzazione.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di definizioni di segmenti per l’organizzazione specificata come JSON.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

Puoi creare una nuova definizione di segmento effettuando una richiesta di POST al `/segment/definitions` punto finale.

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `description` | Una descrizione della definizione del segmento che si sta creando. |
| `evaluationInfo` | Il tipo di segmento che si sta creando. Se desideri creare un segmento batch, imposta `evaluationInfo.batch.enabled` essere vero. Se desideri creare un segmento di streaming, imposta `evaluationInfo.continuous.enabled` essere vero. Per creare un segmento edge, impostate `evaluationInfo.synchronous.enabled` essere vero. Se lasciato vuoto, il segmento viene creato come **batch** segmento. |
| `schema` | **Obbligatorio.** Lo schema associato alle entità nel segmento. È costituito da una delle due `id` o `name` campo . |
| `expression` | **Obbligatorio.** Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione nel valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |
| `description` | Una descrizione della definizione leggibile dall&#39;uomo. |

<!-- >[!NOTE]
>
>A segment definition expression may also reference a computed attribute. To learn more, please refer to the [computed attribute API endpoint guide](../../profile/computed-attributes/ca-api.md)
>
>Computed attribute functionality is in alpha and is not available to all users. Documentation and functionality are subject to change. -->

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
    "imsOrgId": "{ORG_ID}",
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
| `evaluationInfo` | Un oggetto che indica il tipo di valutazione a cui verrà sottoposta la definizione del segmento. Può essere una segmentazione batch, in streaming (nota anche come continua) o edge (nota anche come sincrono). |

## Recupera una definizione di segmento specifica {#get}

Puoi recuperare informazioni dettagliate su una definizione di segmento specifica effettuando una richiesta di GET al `/segment/definitions` e fornisce l’ID della definizione del segmento che desideri recuperare nel percorso della richiesta.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | La `id` valore della definizione del segmento da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrgId": "{ORG_ID}",
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
| `schema` | Lo schema associato alle entità nel segmento. È costituito da una delle due `id` o `name` campo . |
| `expression` | Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione nel valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |
| `description` | Descrizione umana leggibile della definizione. |
| `evaluationInfo` | Un oggetto che indica il tipo di valutazione, batch, streaming (noto anche come continuo) o edge (noto anche come sincrono), verrà sottoposto alla definizione del segmento. |

## Recuperare in blocco le definizioni dei segmenti {#bulk-get}

È possibile recuperare informazioni dettagliate su più definizioni di segmenti specificate effettuando una richiesta di POST al `/segment/definitions/bulk-get` e fornisce `id` i valori delle definizioni dei segmenti nel corpo della richiesta.

**Formato API**

```http
POST /segment/definitions/bulk-get
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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
| `schema` | Lo schema associato alle entità nel segmento. È costituito da una delle due `id` o `name` campo . |
| `expression` | Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione nel valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |
| `description` | Descrizione umana leggibile della definizione. |
| `evaluationInfo` | Un oggetto che indica il tipo di valutazione, batch, streaming (noto anche come continuo) o edge (noto anche come sincrono), verrà sottoposto alla definizione del segmento. |

## Eliminare una definizione di segmento specifica {#delete}

Puoi richiedere di eliminare una definizione di segmento specifica effettuando una richiesta di DELETE al `/segment/definitions` e fornisce l’ID della definizione del segmento da eliminare nel percorso della richiesta.

>[!NOTE]
>
> Sarà **not** puoi eliminare un segmento utilizzato in un’attivazione di destinazione.

**Formato API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | La `id` del valore della definizione del segmento da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 senza alcun messaggio.

## Aggiornare una definizione di segmento specifica

Puoi aggiornare una definizione di segmento specifica effettuando una richiesta di PATCH al `/segment/definitions` e fornisce l’ID della definizione del segmento che desideri aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | La `id` valore della definizione del segmento da aggiornare. |

**Richiesta**

La seguente richiesta aggiornerà il paese dell&#39;indirizzo di lavoro dagli USA al Canada.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrgId": "{ORG_ID}",
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

Puoi convertire una definizione di segmento tra `pql/text` e `pql/json` o `pql/json` a `pql/text` effettuando una richiesta di POST al `/segment/conversion` punto finale.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Dopo aver letto questa guida hai ora una migliore comprensione del funzionamento delle definizioni dei segmenti. Per ulteriori informazioni sulla creazione di un segmento, consulta la sezione [creazione di un segmento](../tutorials/create-a-segment.md) esercitazione.
