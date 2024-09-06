---
solution: Experience Platform
title: Endpoint API per le definizioni dei segmenti
description: L’endpoint per le definizioni dei segmenti nell’API del servizio di segmentazione di Adobe Experience Platform consente di gestire in modo programmatico le definizioni dei segmenti per la tua organizzazione.
role: Developer
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: f35fb6aae6aceb75391b1b615ca067a72918f4cf
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 3%

---

# Endpoint di definizioni segmento

Adobe Experience Platform consente di creare definizioni di segmenti che definiscono un gruppo di attributi o comportamenti specifici da un gruppo di profili. Una definizione di segmento è un oggetto che incapsula una query scritta in [!DNL Profile Query Language] (PQL). Le definizioni dei segmenti vengono applicate ai profili per creare tipi di pubblico. Questo oggetto (definizione del segmento) è anche denominato predicato PQL. I predicati PQL definiscono le regole per la definizione del segmento in base alle condizioni relative a qualsiasi record o dati di serie temporali forniti a [!DNL Real-Time Customer Profile]. Per ulteriori informazioni sulla scrittura di query PQL, consulta la [guida di PQL](../pql/overview.md).

Questa guida fornisce informazioni utili per comprendere meglio le definizioni dei segmenti e include esempi di chiamate API per eseguire azioni di base utilizzando l’API.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura delle chiamate API di esempio.

## Recuperare un elenco di definizioni di segmenti {#list}

Per recuperare un elenco di tutte le definizioni di segmenti per l&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/segment/definitions`.

**Formato API**

L&#39;endpoint `/segment/definitions` supporta diversi parametri di query per filtrare i risultati. Anche se questi parametri sono facoltativi, si consiglia vivamente di utilizzarli per ridurre i costi generali. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperate tutte le definizioni di segmento disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciali (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Parametri query**

+++ Elenco dei parametri di query disponibili.

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `start` | Specifica l&#39;offset iniziale per le definizioni dei segmenti restituite. | `start=4` |
| `limit` | Specifica il numero di definizioni di segmenti restituite per pagina. | `limit=20` |
| `page` | Specifica da quale pagina inizieranno i risultati delle definizioni dei segmenti. | `page=5` |
| `sort` | Specifica il campo in base al quale ordinare i risultati. È scritto nel seguente formato: `[attributeName]:[desc/asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Specifica se la definizione del segmento è abilitata per lo streaming. | `evaluationInfo.continuous.enabled=true` |

+++

**Richiesta**

La richiesta seguente recupererà le ultime due definizioni di segmenti pubblicate all’interno della tua organizzazione.

+++ Una richiesta di esempio per recuperare un elenco di definizioni di segmenti.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di definizioni di segmenti per l’organizzazione specificata come JSON.

+++ Una risposta di esempio durante il recupero di un elenco di definizioni di segmenti.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

+++

## Creare una nuova definizione di segmento {#create}

Per creare una nuova definizione di segmento, devi eseguire una richiesta POST all&#39;endpoint `/segment/definitions`.

>[!IMPORTANT]
>
>Le definizioni dei segmenti create tramite l&#39;API **non possono** essere modificate con Segment Builder.

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

Quando crei una nuova definizione di segmento, puoi crearla nel formato `pql/text` o `pql/json`.

>[!BEGINTABS]

>[!TAB Utilizzo di pql/text]

+++ Una richiesta di esempio per creare una definizione di segmento.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
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
        "schema": {
            "name": "_xdm.context.profile"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome univoco in base al quale fare riferimento alla definizione del segmento. |
| `description` | (Facoltativo) Una descrizione della definizione del segmento che stai creando. |
| `expression` | Un’entità che contiene informazioni sui campi relative alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell’espressione in valore. I valori supportati includono `pql/text` e `pql/json`. |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |
| `evaluationInfo` | (Facoltativo) Il tipo di definizione del segmento che stai creando. Se si desidera creare un segmento batch, impostare `evaluationInfo.batch.enabled` su true. Se si desidera creare un segmento di streaming, impostare `evaluationInfo.continuous.enabled` su true. Se si desidera creare un segmento perimetrale, impostare `evaluationInfo.synchronous.enabled` su true. Se non specificato, la definizione del segmento verrà creata come segmento **batch**. |
| `schema` | Lo schema associato alle entità nel segmento. È costituito da un campo `id` o `name`. |

+++

>[!TAB Utilizzo di pql/json]

+++ Una richiesta di esempio per creare una definizione di segmento.

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
            "format": "pql/json",
            "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"a\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}},{\"nodeType\":\"fieldLookup\",\"fieldName\":\"b\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}]}"
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
        "payloadSchema": "string"
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome univoco in base al quale fare riferimento alla definizione del segmento. |
| `description` | (Facoltativo) Una descrizione della definizione del segmento che stai creando. |
| `evaluationInfo` | (Facoltativo) Il tipo di definizione del segmento che stai creando. Se si desidera creare un segmento batch, impostare `evaluationInfo.batch.enabled` su true. Se si desidera creare un segmento di streaming, impostare `evaluationInfo.continuous.enabled` su true. Se si desidera creare un segmento perimetrale, impostare `evaluationInfo.synchronous.enabled` su true. Se non specificato, la definizione del segmento verrà creata come segmento **batch**. |
| `schema` | Lo schema associato alle entità nel segmento. È costituito da un campo `id` o `name`. |
| `expression` | Un’entità che contiene informazioni sui campi relative alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell’espressione in valore. |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |

+++

>[!ENDTABS]

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della definizione del segmento appena creata.

+++ Una risposta di esempio durante la creazione di una definizione di segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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
| `id` | ID generato dal sistema della definizione del segmento appena creata. |
| `evaluationInfo` | Oggetto che indica il tipo di valutazione a cui verrà sottoposta la definizione del segmento. Può essere in batch, in streaming (o continua) o in segmentazione Edge (o sincrona). |

+++

## Recuperare una definizione di segmento specifica {#get}

Per recuperare informazioni dettagliate su una definizione di segmento specifica, effettua una richiesta di GET all&#39;endpoint `/segment/definitions` e fornisci l&#39;ID della definizione di segmento da recuperare nel percorso della richiesta.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | Il valore `id` della definizione del segmento che si desidera recuperare. |

**Richiesta**

+++ Una richiesta di esempio per recuperare una definizione di segmento.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sulla definizione del segmento specificata.

+++ Una risposta di esempio durante il recupero di una definizione di segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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
| `name` | Un nome univoco in base al quale fare riferimento alla definizione del segmento. |
| `schema` | Lo schema associato alle entità nel segmento. È costituito da un campo `id` o `name`. |
| `expression` | Un’entità che contiene informazioni sui campi relative alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell’espressione in valore. Attualmente, è supportato il seguente formato: <ul><li>`pql/text`: rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |
| `description` | Una descrizione leggibile della definizione. |
| `evaluationInfo` | Oggetto che indica il tipo di valutazione, batch, streaming (noto anche come continuo) o edge (noto anche come sincrono) a cui verrà sottoposta la definizione del segmento. |

+++

## Definizioni di segmenti di recupero in blocco {#bulk-get}

È possibile recuperare informazioni dettagliate su più definizioni di segmenti specificate effettuando una richiesta POST all&#39;endpoint `/segment/definitions/bulk-get` e fornendo i valori `id` delle definizioni di segmenti nel corpo della richiesta.

**Formato API**

```http
POST /segment/definitions/bulk-get
```

**Richiesta**

+++ Una richiesta di esempio quando si utilizza l’endpoint bulk-get.

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

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 207 con le definizioni dei segmenti richieste.

+++ Risposta di esempio quando si utilizza l’endpoint bulk-get.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
| `name` | Un nome univoco in base al quale fare riferimento alla definizione del segmento. |
| `schema` | Lo schema associato alle entità nel segmento. È costituito da un campo `id` o `name`. |
| `expression` | Un’entità che contiene informazioni sui campi relative alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell’espressione in valore. Attualmente, è supportato il seguente formato: <ul><li>`pql/text`: rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Espressione conforme al tipo indicato in `expression.format`. |
| `description` | Una descrizione leggibile della definizione. |
| `evaluationInfo` | Oggetto che indica il tipo di valutazione, batch, streaming (noto anche come continuo) o edge (noto anche come sincrono) a cui verrà sottoposta la definizione del segmento. |

+++

## Eliminare una definizione di segmento specifica {#delete}

È possibile richiedere l&#39;eliminazione di una definizione di segmento specifica effettuando una richiesta DELETE all&#39;endpoint `/segment/definitions` e fornendo l&#39;ID della definizione di segmento che si desidera eliminare nel percorso della richiesta.

>[!NOTE]
>
> Una definizione di segmento utilizzata in un&#39;attivazione di destinazione **non può** essere eliminata.

**Formato API**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | Il valore `id` della definizione del segmento che si desidera eliminare. |

**Richiesta**

+++ Una richiesta di esempio per eliminare una definizione di segmento.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 senza messaggio.

## Aggiornare una definizione di segmento specifica

Per aggiornare una definizione di segmento specifica, devi eseguire una richiesta PATCH all&#39;endpoint `/segment/definitions` e fornire l&#39;ID della definizione di segmento da aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_ID}` | Il valore `id` della definizione del segmento da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna il paese dell’indirizzo di lavoro dagli Stati Uniti al Canada.

+++ Richiesta di esempio per aggiornare la definizione di un segmento.

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
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della definizione del segmento appena aggiornata.

+++ Una risposta di esempio durante l’aggiornamento della definizione di un segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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

+++

## Converti definizione segmento

È possibile convertire una definizione di segmento tra `pql/text` e `pql/json` o `pql/json` in `pql/text` effettuando una richiesta POST all&#39;endpoint `/segment/conversion`.

**Formato API**

```http
POST /segment/conversion
```

**Richiesta**

La richiesta seguente modificherà il formato della definizione del segmento da `pql/text` a `pql/json`.

+++ Una richiesta di esempio per convertire la definizione del segmento.

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
        "payloadSchema": "string"
    }'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della definizione del segmento appena convertito.

+++ Una risposta di esempio durante la conversione della definizione del segmento.

```json
{
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

+++

## Passaggi successivi

Dopo aver letto questa guida hai acquisito una migliore comprensione del funzionamento delle definizioni dei segmenti. Per ulteriori informazioni sulla creazione di un segmento, consulta l&#39;esercitazione [creazione di un segmento](../tutorials/create-a-segment.md).
