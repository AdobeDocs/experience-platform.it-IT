---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;tipi di pubblico;pubblico;API;api;
title: Endpoint API per tipi di pubblico
topic-legacy: developer guide
description: L’endpoint audience nell’API del servizio di segmentazione di Adobe Experience Platform consente di gestire i tipi di pubblico a livello di programmazione per la tua organizzazione.
source-git-commit: 2a0c1f55115c541962f7bd3b7b11d367da50ff3b
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 4%

---


# Endpoint pubblico

Un pubblico è una raccolta di persone che condividono comportamenti e/o caratteristiche simili. Queste raccolte di persone possono essere generate utilizzando Adobe Experience Platform o da fonti esterne. È possibile utilizzare `/audiences` nell’API di segmentazione, che consente di recuperare, creare, aggiornare ed eliminare in modo programmatico i tipi di pubblico.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Recupera un elenco di tipi di pubblico {#list}

Puoi recuperare un elenco di tutti i tipi di pubblico per la tua organizzazione effettuando una richiesta di GET al `/audiences` punto finale.

**Formato API**

La `/audiences` l’endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Anche se questi parametri sono facoltativi, si consiglia vivamente di utilizzarli per ridurre i costi di overhead durante l’inserimento delle risorse nell’elenco. Se effettui una chiamata a questo endpoint senza parametri, verranno recuperati tutti i tipi di pubblico disponibili per la tua organizzazione. È possibile includere più parametri, separati da e commerciale (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

I seguenti parametri di query possono essere utilizzati per recuperare un elenco di tipi di pubblico:

| Parametro query | Descrizione | Esempio |
| --------------- | ----------- | ------- |
| `start` | Specifica l&#39;offset iniziale per i tipi di pubblico restituiti. | `start=5` |
| `limit` | Specifica il numero massimo di tipi di pubblico restituiti per pagina. | `limit=10` |
| `sort` | Specifica l&#39;ordine in cui ordinare i risultati. Viene scritto nel formato `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Filtro che consente di specificare i tipi di pubblico che **esattamente** corrisponde al valore di un attributo. Viene scritto nel formato `property=` | `property=audienceId==test-audience-id` |
| `name` | Filtro che consente di specificare i tipi di pubblico i cui nomi **contain** il valore fornito. Questo valore non distingue tra maiuscole e minuscole. | `name=Sample` |
| `description` | Filtro che consente di specificare i tipi di pubblico le cui descrizioni **contain** il valore fornito. Questo valore non distingue tra maiuscole e minuscole. | `description=Test Description` |
| `withMetrics` | Filtro che restituisce le metriche oltre ai tipi di pubblico. | `property=withMetrics==true` |

>[!IMPORTANT]
>
>Per i tipi di pubblico, le metriche vengono restituite nella sezione `metrics` e contiene informazioni sui conteggi dei profili, sulla creazione e sull’aggiornamento delle marche temporali.

**Nessuna metrica**

La seguente coppia di richieste/risposte viene utilizzata quando `withMetrics` il parametro query non è presente.

**Richiesta**

La seguente richiesta recupera gli ultimi cinque tipi di pubblico creati nella tua organizzazione.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**Risposta** {#no-metrics}

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di tipi di pubblico creati nella tua organizzazione come JSON.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio e mostra solo il primo pubblico restituito.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
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
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| Proprietà | Tipo di pubblico | Descrizione |
| -------- | ------------- | ----------- | 
| `id` | Entrambi | Identificatore di sola lettura generato dal sistema per il pubblico. |
| `audienceId` | Entrambi | Se il pubblico è un pubblico generato da Platform, lo stesso valore è `id`. Se il pubblico viene generato esternamente, questo valore viene fornito dal client. |
| `schema` | Entrambi | Lo schema Experience Data Model (XDM) del pubblico. |
| `imsOrgId` | Entrambi | ID dell&#39;organizzazione a cui appartiene il pubblico. |
| `sandbox` | Entrambi | Informazioni sulla sandbox a cui appartiene il pubblico. Ulteriori informazioni sulle sandbox sono disponibili nella sezione [panoramica sulle sandbox](../../sandboxes/home.md). |
| `name` | Entrambi | Il nome del pubblico. |
| `description` | Entrambi | Una descrizione del pubblico. |
| `expression` | Generato dalla piattaforma | L’espressione PQL (Profile Query Language) del pubblico. Ulteriori informazioni sulle espressioni PQL sono disponibili nella sezione [Guida alle espressioni PQL](../pql/overview.md). |
| `mergePolicyId` | Generato dalla piattaforma | ID del criterio di unione a cui è associato il pubblico. Ulteriori informazioni sui criteri di unione sono disponibili nella sezione [guida ai criteri di unione](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Generato dalla piattaforma | Mostra come verrà valutato il pubblico. I possibili metodi di valutazione includono batch, streaming o edge. Ulteriori informazioni sui metodi di valutazione sono disponibili nella sezione [panoramica sulla segmentazione](../home.md) |
| `dependents` | Entrambi | Array di ID di pubblico che dipendono dal pubblico corrente. Questa opzione viene utilizzata se crei un pubblico che è un segmento di un segmento. |
| `dependencies` | Entrambi | Array di ID di pubblico da cui dipende il pubblico. Questa opzione viene utilizzata se crei un pubblico che è un segmento di un segmento. |
| `type` | Entrambi | Campo generato dal sistema che indica se il pubblico è generato da Platform o è un pubblico generato esternamente. Eventuali valori includono `SegmentDefinition` e `ExternalAudience`. A `SegmentDefinition` fa riferimento a un pubblico generato in Platform, mentre un `ExternalAudience` fa riferimento a un pubblico non generato in Platform. |
| `createdBy` | Entrambi | ID dell’utente che ha creato il pubblico. |
| `labels` | Entrambi | Etichette di controllo dell’utilizzo dei dati a livello di oggetto e dell’accesso basate su attributi rilevanti per il pubblico. |
| `namespace` | Entrambi | Lo spazio dei nomi a cui appartiene il pubblico. Eventuali valori includono `AAM`, `AAMSegments`, `AAMTraits`e `AEPSegments`. |
| `audienceMeta` | Esterno | Metadati creati esternamente dal pubblico creato esternamente. |

**Con le metriche**

La seguente coppia di richieste/risposte viene utilizzata quando `withMetrics` parametro query presente.

**Richiesta**

La richiesta seguente recupera gli ultimi cinque tipi di pubblico, con metriche, creati nella tua organizzazione.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di audience, con metriche, per l’organizzazione specificata come JSON.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio e mostra solo il primo pubblico restituito.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
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
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "existing": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

Di seguito sono elencate le proprietà **esclusivo** al `withMetrics` risposta. Per conoscere le proprietà standard del pubblico, consulta la sezione [sezione precedente](#no-metrics).

| Proprietà | Descrizione |
| -------- | ----------- |
| `metrics.imsOrgId` | ID organizzazione del pubblico. |
| `metrics.sandbox` | Informazioni sulla sandbox relative al pubblico. |
| `metrics.jobId` | ID del processo del segmento che elabora il pubblico. |
| `metrics.type` | Il tipo di processo del segmento. Può essere `export` o `batch_segmentation`. |
| `metrics.id` | ID del pubblico. |
| `metrics.data` | Metriche correlate al pubblico. Ciò include informazioni quali il numero totale di profili inclusi nel pubblico, il numero totale di profili in base a uno spazio dei nomi e il numero totale di profili in base allo stato. |
| `metrics.createEpoch` | Una marca temporale che mostra quando è stato creato il pubblico. |
| `metrics.updateEpoch` | Una marca temporale che mostra l’ultimo aggiornamento del pubblico. |

## Creare un nuovo pubblico {#create}

Puoi creare un nuovo pubblico effettuando una richiesta di POST al `/audiences` punto finale.

**Formato API**

```http
POST /audiences
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
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
| `type` | Campo che indica se il pubblico è generato da Platform o se è un pubblico generato esternamente. Eventuali valori includono `SegmentDefinition` e `ExternalAudience`. A `SegmentDefinition` fa riferimento a un pubblico generato in Platform, mentre un `ExternalAudience` fa riferimento a un pubblico non generato in Platform. |
| `expression` | L’espressione PQL (Profile Query Language) del pubblico. Ulteriori informazioni sulle espressioni PQL sono disponibili nella sezione [Guida alle espressioni PQL](../pql/overview.md). |
| `schema` | Lo schema Experience Data Model (XDM) del pubblico. |
| `labels` | Etichette di controllo dell’utilizzo dei dati a livello di oggetto e dell’accesso basate su attributi rilevanti per il pubblico. |

**Risposta**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Cercare un pubblico specifico {#get}

Puoi cercare informazioni dettagliate su un pubblico specifico effettuando una richiesta GET al `/audiences` e fornisce l’ID del pubblico da recuperare nel percorso della richiesta.

**Formato API**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| Parametro | Descrizione |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | ID del pubblico da recuperare. |
| `property=withmetrics==true` | Parametro di query facoltativo che può essere utilizzato per recuperare un pubblico specificato con le metriche del pubblico. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul pubblico specificato. La risposta varia a seconda che il pubblico sia generato con Adobe Experience Platform o con sorgenti esterne.

**Generato dalla piattaforma**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**Generato esternamente**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Aggiornare un campo in un pubblico {#update-field}

Puoi aggiornare i campi di un pubblico specifico effettuando una richiesta di PATCH al `/audiences` e fornisce l’ID del pubblico da aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID del pubblico da aggiornare. |

**Richiesta**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `op` | Per aggiornare i tipi di pubblico, questo valore è sempre `add`. |
| `path` | Percorso del campo da aggiornare. |
| `value` | Il valore in cui si desidera aggiornare il campo. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul pubblico appena aggiornato.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
        "value": "workAddress.country = \"CA\""
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
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Aggiornare un pubblico {#put}

Puoi aggiornare (sovrascrivere) un pubblico specifico effettuando una richiesta di PUT al `/audiences` e fornisce l’ID del pubblico da aggiornare nel percorso della richiesta.

**Formato API**

```http
PUT /audiences/{AUDIENCE_ID}
```

**Richiesta**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `audienceId` | ID del pubblico. Viene utilizzato da tipi di pubblico esterni |
| `name` | Il nome del pubblico. |
| `namespace` |  |
| `description` | Una descrizione del pubblico. |
| `type` | Campo generato dal sistema che indica se il pubblico è generato da Platform o è un pubblico generato esternamente. Eventuali valori includono `SegmentDefinition` e `ExternalAudience`. A `SegmentDefinition` fa riferimento a un pubblico generato in Platform, mentre un `ExternalAudience` fa riferimento a un pubblico non generato in Platform. |
| `lifecycle` | Lo stato del pubblico. Eventuali valori includono `draft`, `published`, `inactive`e `archived`. `draft` rappresenta quando viene creato il pubblico, `published` quando il pubblico viene pubblicato, `inactive` quando il pubblico non è più attivo, e `archived` se il pubblico viene eliminato. |
| `datasetId` | ID del set di dati che è possibile trovare nei dati sul pubblico. |
| `labels` | Etichette di controllo dell’utilizzo dei dati a livello di oggetto e dell’accesso basate su attributi rilevanti per il pubblico. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del pubblico appena aggiornato. Tieni presente che i dettagli del pubblico variano a seconda che si tratti di un pubblico generato da Platform o di un pubblico generato esternamente.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Eliminare un pubblico {#delete}

Puoi eliminare un pubblico specifico effettuando una richiesta di DELETE al `/audiences` e fornisce l’ID del pubblico da eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID del pubblico da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 senza alcun messaggio.
