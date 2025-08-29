---
title: Endpoint API di Audiences
description: Utilizza l’endpoint "audiences" nell’API del servizio di segmentazione di Adobe Experience Platform per creare, gestire e aggiornare in modo programmatico i tipi di pubblico per la tua organizzazione.
role: Developer
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: 63fa87ac9777b3ac66d990dd4bfbd202f07b0eba
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 3%

---

# Endpoint &quot;audience&quot;

Un pubblico è una raccolta di persone che condividono comportamenti e/o caratteristiche simili. Queste raccolte di persone possono essere generate utilizzando Adobe Experience Platform o da origini esterne. È possibile utilizzare l&#39;endpoint `/audiences` nell&#39;API di segmentazione, che consente di recuperare, creare, aggiornare ed eliminare in modo programmatico i tipi di pubblico.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura delle chiamate API di esempio.

## Recuperare un elenco di tipi di pubblico {#list}

Per recuperare un elenco di tutti i tipi di pubblico per l&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/audiences`.

**Formato API**

L&#39;endpoint `/audiences` supporta diversi parametri di query per filtrare i risultati. Anche se questi parametri sono facoltativi, si consiglia vivamente di utilizzarli per ridurre i costi comuni quando si elencano le risorse. Se effettui una chiamata a questo endpoint senza parametri, verranno recuperati tutti i tipi di pubblico disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciali (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

>[!NOTE]
>
>Se utilizzi questo endpoint senza parametri di query, i tipi di pubblico inattivi **non** verranno restituiti. Tuttavia, se utilizzi questo endpoint insieme al parametro di query `property=audienceId`, verranno restituiti i tipi di pubblico inattivi **will**.

Durante il recupero di un elenco di tipi di pubblico è possibile utilizzare i seguenti parametri di query:

| Parametri query | Descrizione | Esempio |
| --------------- | ----------- | ------- |
| `start` | Specifica l&#39;offset iniziale per i tipi di pubblico restituiti. | `start=5` |
| `limit` | Specifica il numero massimo di pubblici restituiti per pagina. | `limit=10` |
| `sort` | Specifica l&#39;ordine di ordinamento dei risultati. Scritto nel formato `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Filtro che consente di specificare tipi di pubblico che **corrispondono esattamente** al valore di un attributo. Scritto nel formato `property=` | `property=audienceId==test-audience-id` |
| `name` | Filtro che consente di specificare tipi di pubblico i cui nomi **contengono** il valore specificato. Questo valore non distingue tra maiuscole e minuscole. | `name=Sample` |
| `description` | Un filtro che consente di specificare tipi di pubblico le cui descrizioni **contengono** il valore specificato. Questo valore non distingue tra maiuscole e minuscole. | `description=Test Description` |
| `entityType` | Un filtro che ti consente di specificare il tipo di pubblico che stai cercando. | `entityType=_xdm.context.account` |

**Richiesta**

La richiesta seguente recupera gli ultimi due tipi di pubblico creati nell’organizzazione.

+++Una richiesta di esempio per recuperare un elenco di tipi di pubblico.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di tipi di pubblico creati nell’organizzazione come JSON.

+++Una risposta di esempio contenente gli ultimi due tipi di pubblico creati che appartengono alla tua organizzazione

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
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
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "totalPages": 21,
      "sortField": "name",
      "sort": "asc", 
      "pageSize": 5,
      "limit": 5,
      "start": "0",
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| Proprietà | Tipo di pubblico | Descrizione |
| -------- | ------------- | ----------- | 
| `id` | Entrambi | Identificatore di sola lettura generato dal sistema per il pubblico. |
| `audienceId` | Entrambi | Se il pubblico è generato da Platform, è lo stesso valore di `id`. Se il pubblico è generato esternamente, questo valore viene fornito dal client. |
| `schema` | Entrambi | Lo schema Experience Data Model (XDM) del pubblico. |
| `imsOrgId` | Entrambi | ID dell’organizzazione a cui appartiene il pubblico. |
| `sandbox` | Entrambi | Informazioni sulla sandbox a cui appartiene il pubblico. Ulteriori informazioni sulle sandbox sono disponibili nella [panoramica sulle sandbox](../../sandboxes/home.md). |
| `name` | Entrambi | Il nome del pubblico. |
| `description` | Entrambi | Una descrizione del pubblico. |
| `expression` | Generato da piattaforma | L’espressione Profile Query Language (PQL) del pubblico. Ulteriori informazioni sulle espressioni di PQL sono disponibili nella [guida delle espressioni di PQL](../pql/overview.md). |
| `mergePolicyId` | Generato da piattaforma | ID del criterio di unione a cui è associato il pubblico. Ulteriori informazioni sui criteri di unione sono disponibili nella [guida dei criteri di unione](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Generato da piattaforma | Mostra come verrà valutato il pubblico. I possibili metodi di valutazione includono batch, sincrono (streaming) o continuo (edge). Ulteriori informazioni sui metodi di valutazione sono disponibili nella [panoramica sulla segmentazione](../home.md) |
| `dependents` | Entrambi | Un array di ID di pubblico che dipendono dal pubblico corrente. Questa opzione è utile per creare un pubblico che è un segmento di un segmento. |
| `dependencies` | Entrambi | Un array di ID di pubblico da cui dipende il pubblico. Questa opzione è utile per creare un pubblico che è un segmento di un segmento. |
| `type` | Entrambi | Campo generato dal sistema che indica se il pubblico è generato da Platform o da un pubblico generato esternamente. I valori possibili includono `SegmentDefinition` e `ExternalSegment`. Un `SegmentDefinition` fa riferimento a un pubblico generato in Platform, mentre un `ExternalSegment` fa riferimento a un pubblico non generato in Platform. |
| `originName` | Entrambi | Campo che fa riferimento al nome dell’origine del pubblico. Per il pubblico generato da Platform, questo valore sarà `REAL_TIME_CUSTOMER_PROFILE`. Per il pubblico generato in Audience Orchestration, questo valore sarà `AUDIENCE_ORCHESTRATION`. Per il pubblico generato in Adobe Audience Manager, questo valore sarà `AUDIENCE_MANAGER`. Per altri tipi di pubblico generati esternamente, questo valore sarà `CUSTOM_UPLOAD`. |
| `createdBy` | Entrambi | ID dell’utente che ha creato il pubblico. |
| `labels` | Entrambi | Etichette di controllo dell’accesso basate su attributi e utilizzo dati a livello di oggetto rilevanti per il pubblico. |
| `namespace` | Entrambi | Lo spazio dei nomi a cui appartiene il pubblico. I valori possibili sono `AAM`, `AAMSegments`, `AAMTraits` e `AEPSegments`. |
| `linkedAudienceRef` | Entrambi | Oggetto che contiene identificatori di altri sistemi relativi al pubblico. |

+++

## Creare un nuovo pubblico {#create}

Per creare un nuovo pubblico, devi eseguire una richiesta POST all&#39;endpoint `/audiences`.

**Formato API**

```http
POST /audiences
```

**Richiesta**

+++ Richiesta di esempio per la creazione di un pubblico generato da Platform

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "AEPSegments",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `name` | Il nome del pubblico. |
| `description` | Una descrizione del pubblico. |
| `type` | Campo che indica se il pubblico è generato da Platform o da un pubblico generato esternamente. I valori possibili includono `SegmentDefinition` e `ExternalSegment`. Un `SegmentDefinition` fa riferimento a un pubblico generato in Platform, mentre un `ExternalSegment` fa riferimento a un pubblico non generato in Platform. |
| `expression` | L’espressione Profile Query Language (PQL) del pubblico. Ulteriori informazioni sulle espressioni di PQL sono disponibili nella [guida delle espressioni di PQL](../pql/overview.md). |
| `schema` | Lo schema Experience Data Model (XDM) del pubblico. |
| `labels` | Etichette di controllo dell’accesso basate su attributi e utilizzo dati a livello di oggetto rilevanti per il pubblico. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sul pubblico appena creato.

+++Una risposta di esempio durante la creazione di un pubblico generato da Platform.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Cercare un pubblico specificato {#get}

Per cercare informazioni dettagliate su un pubblico specifico, effettua una richiesta GET all&#39;endpoint `/audiences` e specifica l&#39;ID del pubblico da recuperare nel percorso della richiesta.

**Formato API**

```http
GET /audiences/{AUDIENCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | ID del pubblico che stai tentando di recuperare. Tieni presente che si tratta del campo `id` e che **non** è il campo `audienceId`. |

**Richiesta**

+++Una richiesta di esempio per recuperare un pubblico

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sul pubblico specificato.

+++Una risposta di esempio durante il recupero di un pubblico generato da Platform.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Sovrascrivere un pubblico {#put}

È possibile aggiornare (sovrascrivere) un pubblico specifico effettuando una richiesta PUT all&#39;endpoint `/audiences` e fornendo l&#39;ID del pubblico che si desidera aggiornare nel percorso della richiesta.

**Formato API**

```http
PUT /audiences/{AUDIENCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID del pubblico che desideri aggiornare. Tieni presente che si tratta del campo `id` e che **non** è il campo `audienceId`. |

**Richiesta**

+++Una richiesta di esempio per aggiornare un intero pubblico.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-platform-audience-id",
    "name": "New Platform audience",
    "namespace": "AEPSegments",
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country=\"US\""
    }
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `audienceId` | ID del pubblico. Per i tipi di pubblico generati esternamente, questo valore può essere fornito dall’utente. |
| `name` | Il nome del pubblico. |
| `namespace` | Lo spazio dei nomi per il pubblico. |
| `description` | Una descrizione del pubblico. |
| `type` | Campo generato dal sistema che indica se il pubblico è generato da Platform o da un pubblico generato esternamente. I valori possibili includono `SegmentDefinition` e `ExternalSegment`. `SegmentDefinition` fa riferimento a un pubblico generato in Experience Platform, mentre `ExternalSegment` fa riferimento a un pubblico non generato in Experience Platform. |
| `expression` | Oggetto che contiene l’espressione PQL del pubblico. |
| `lifecycleState` | Stato del pubblico. I valori possibili sono `draft`, `published` e `inactive`. `draft` rappresenta quando viene creato il pubblico, `published` quando il pubblico viene pubblicato e `inactive` quando il pubblico non è più attivo. |
| `datasetId` | ID del set di dati in cui è possibile trovare i dati sul pubblico. |
| `labels` | Etichette di controllo dell’accesso basate su attributi e utilizzo dati a livello di oggetto rilevanti per il pubblico. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del pubblico appena aggiornato. Tieni presente che i dettagli del pubblico variano a seconda che si tratti di un pubblico generato da Experience Platform o da un pubblico generato esternamente.

+++Una risposta di esempio durante l’aggiornamento di un intero pubblico.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Aggiornare un pubblico {#patch}

Per aggiornare un pubblico specifico, devi eseguire una richiesta PATCH all&#39;endpoint `/audiences` e fornire l&#39;ID del pubblico da aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID del pubblico che desideri aggiornare. Tieni presente che si tratta del campo `id` e che **non** è il campo `audienceId`. |

**Richiesta**

+++ Una richiesta di esempio per aggiornare un pubblico.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "op": "add",
        "path": "/lifecycleState",
        "value": "inactive"
    }
 ]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `op` | Tipo di operazione PATCH eseguita. Per questo endpoint, il valore è **always** `/add`. |
| `path` | Percorso del campo da aggiornare. Impossibile modificare i campi generati dal sistema, ad esempio `id`, `audienceId` e `namespace` **4}.** |
| `value` | Il nuovo valore assegnato alla proprietà specificata in `path`. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con il pubblico aggiornato.

+++Una risposta di esempio durante l’applicazione della patch a un campo in un pubblico.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab5",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "inactive",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Eliminare un pubblico {#delete}

Per eliminare un pubblico specifico, devi eseguire una richiesta DELETE all&#39;endpoint `/audiences` e fornire l&#39;ID del pubblico da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID del pubblico da eliminare. Tieni presente che si tratta del campo `id` e che **non** è il campo `audienceId`. |

**Richiesta**

+++ Una richiesta di esempio per eliminare un pubblico.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 senza messaggio.

## Recuperare più tipi di pubblico {#bulk-get}

Per recuperare più tipi di pubblico, devi eseguire una richiesta POST all&#39;endpoint `/audiences/bulk-get` e fornire gli ID dei tipi di pubblico da recuperare.

**Formato API**

```http
POST /audiences/bulk-get
```

**Richiesta**

+++ Una richiesta di esempio per recuperare più tipi di pubblico.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 207 con le informazioni relative ai tipi di pubblico richiesti.

+++ Una risposta di esempio durante il recupero di più tipi di pubblico.

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
         "evaluationInfo": {
            "batch": {
               "enabled": false
            },
            "continuous": {
               "enabled": true
            },
            "synchronous": {
               "enabled": false
            }
         },
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
         "dependents": [],
         "definedOn": [
            {
               "meta:resourceType": "unions",
               "meta:containerId": "tenant",
               "$ref": "https://ns.adobe.com/xdm/context/profile__union"
            }
         ],
         "dependencies": [],
         "type": "SegmentDefinition",
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++


## Passaggi successivi

Dopo aver letto questa guida, ora hai una migliore comprensione di come creare, gestire ed eliminare i tipi di pubblico utilizzando l’API di Adobe Experience Platform. Per ulteriori informazioni sulla gestione dell&#39;audience tramite l&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente di segmentazione](../ui/overview.md).
