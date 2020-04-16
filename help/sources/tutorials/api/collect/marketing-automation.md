---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Raccolta di dati di automazione marketing tramite connettori di origine e API
topic: overview
translation-type: tm+mt
source-git-commit: 2f7961a4ca0bc0fec2ed1f50f5101e4dd734a282

---


# Raccolta di dati di automazione marketing tramite connettori di origine e API

Questa esercitazione descrive i passaggi necessari per recuperare i dati da un sistema di automazione di marketing e inserirli nella piattaforma tramite connettori sorgente e API.

## Introduzione

Questa esercitazione richiede informazioni sul file da inserire nella piattaforma, incluso il percorso e la struttura del file. Se non disponi di queste informazioni, consulta l’esercitazione sull’ [esplorazione di un’applicazione di automazione di marketing tramite l’API](../../api/create/marketing-automation/hubspot.md) del servizio di flusso prima di provare a seguire questa esercitazione.

Questa esercitazione richiede anche di avere una conoscenza approfondita dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Schema Guida](../../../../xdm/api/getting-started.md)per lo sviluppatore del Registro di sistema: Include informazioni importanti che è necessario conoscere per eseguire correttamente le chiamate all&#39;API del Registro di sistema dello schema. Ciò include il vostro `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all’intestazione Accetta e ai suoi possibili valori).
* [Servizio](../../../../catalog/home.md)catalogo: Catalog è il sistema di record per la posizione dei dati e la linea di collegamento all’interno di Experience Platform.
* [Caricamento](../../../../ingestion/batch-ingestion/overview.md)batch: L’API Batch Ingestion consente di trasferire i dati in Experience Platform come file batch.
* [Sandbox](../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un sistema di automazione di marketing tramite l&#39;API del servizio di flusso.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform, incluse quelle appartenenti a Flow Service, sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Creare una classe e uno schema XDM ad hoc

Per inserire dati esterni in Platform tramite connettori di origine, è necessario creare una classe e uno schema XDM ad hoc per i dati di origine non elaborati.

Per creare una classe e uno schema ad hoc, segui i passaggi descritti nell&#39;esercitazione [sullo schema](../../../../xdm/tutorials/ad-hoc.md)ad hoc. Quando create una classe ad hoc, tutti i campi trovati nei dati di origine devono essere descritti all&#39;interno del corpo della richiesta.

Continuate a seguire i passaggi descritti nella guida per gli sviluppatori fino a quando non avete creato uno schema ad hoc. Ottenete e archiviate l&#39;identificatore univoco (`$id`) dello schema ad hoc, quindi passate alla fase successiva dell&#39;esercitazione.

## Creazione di una connessione di origine {#source}

Con la creazione di uno schema XDM ad hoc, ora è possibile creare una connessione di origine utilizzando una richiesta POST all&#39;API del servizio di flusso. Una connessione di origine è costituita da una connessione di base, un file di dati di origine e un riferimento allo schema che descrive i dati di origine.

**Formato API**

```https
POST /sourceConnections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Marketing automation source connection",
        "baseConnectionId": "2fce94c1-9a93-4971-8e94-c19a93097129",
        "description": "Marketing automation source connection",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/80a6e931bd5e00190b72daafb4e1e4f7913a114808be9ac0",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "Hubspot.Contacts"
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `baseConnectionId` | ID connessione dell’applicazione di automazione di marketing |
| `data.schema.id` | Indica `$id` lo schema XDM ad hoc. |
| `params.path` | Percorso del file di origine. |
| `connectionSpec.id` | ID specifica di connessione dell’applicazione di automazione di marketing. |

**Risposta**

Una risposta corretta restituisce l’identificatore univoco (`id`) della connessione di origine appena creata. Archiviate questo valore come richiesto nei passaggi successivi per la creazione di una connessione di destinazione.

```json
{
    "id": "c315c0ae-a339-44c4-95c0-aea33964c420",
    "etag": "\"67010af9-0000-0200-0000-5e9795c40000\""
}
```

## Creare uno schema XDM di destinazione {#target}

Nei passaggi precedenti, era stato creato uno schema XDM ad hoc per strutturare i dati di origine. Affinché i dati di origine siano utilizzati in Piattaforma, è necessario creare anche uno schema di destinazione per strutturare i dati di origine in base alle esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati della piattaforma in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST all&#39;API [del Registro di](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)schema. Se si preferisce utilizzare l&#39;interfaccia utente in Experience Platform, l&#39;esercitazione [Editor di](../../../../xdm/tutorials/create-schema-ui.md) schema fornisce istruzioni dettagliate per eseguire azioni simili nell&#39;Editor di schema.

**Formato API**

```https
POST /schemaregistry/tenant/schemas
```

**Richiesta**

La seguente richiesta di esempio crea uno schema XDM che estende la classe di profilo singolo XDM.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Target schema for marketing automation",
        "description": "Target schema for marketing automation",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            },
                    {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**Risposta**

Una risposta corretta restituisce i dettagli dello schema appena creato, incluso il relativo identificatore univoco (`$id`). Archivia l’ID così come è richiesto nei passaggi successivi per creare un set di dati di destinazione, una mappatura e un flusso di dati.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
    "meta:altId": "_{TENANT_ID}.schemas.63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for marketing automation",
    "type": "object",
    "description": "Target schema for marketing automation",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1586992941717,
        "repo:lastModifiedDate": 1586992941717,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CREATED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{CREATED_USER_ID}",
        "eTag": "d11e63a422b84a843cdd58d0ba8a16ce0a2068eda49ab380c1605ddd10efdf23",
        "meta:globalLibVersion": "1.9.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creare un dataset di destinazione

Un set di dati di destinazione può essere creato eseguendo una richiesta POST all&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog Service, fornendo l&#39;ID dello schema di destinazione all&#39;interno del payload.

**Formato API**

```https
POST /catalog/dataSets
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target dataset for marketing automation",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/14d89c5bb88e2ff488f23db896be469e7e30bb166bda8722",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `schemaRef.id` | Il valore `$id` dello schema XDM di destinazione. |

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L&#39;ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API. Archiviate l&#39;ID del set di dati di destinazione come richiesto nei passaggi successivi per creare una connessione di destinazione e un flusso di dati.

```json
[
    "@/dataSets/5e9797ac6d771118ad8356db"
]
```

## Creazione di una connessione di base di dataset

Per creare una connessione di destinazione e assimilare dati esterni in Platform, è necessario innanzitutto acquisire una connessione di base di dataset.

Per creare una connessione alla base di dati, seguire i passaggi descritti nell&#39;esercitazione [sulla connessione alla base di](../create-dataset-base-connection.md)dati.

Continuate a seguire i passaggi descritti nella guida per gli sviluppatori fino a quando non avete creato una connessione di base per i dataset. Ottenete e archiviate l&#39;identificatore univoco (`$id`) della connessione di base, quindi passate alla fase successiva dell&#39;esercitazione.

## Creare una connessione di destinazione

Ora sono disponibili identificatori univoci per una connessione di base di set di dati, uno schema di destinazione e un set di dati di destinazione. Utilizzando questi identificatori, potete creare una connessione di destinazione utilizzando l&#39;API del servizio di flusso per specificare il set di dati che conterrà i dati di origine in entrata.

**Formato API**

```https
POST /targetConnections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "44b1c1e43-a5ee-4d86-9c1e-43a5eebd8601",
        "name": "Target Connection for marketing automation",
        "description": "Target Connection for marketing automation",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e9797ac6d771118ad8356db
        },
            "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `baseConnectionId` | ID della connessione di base del set di dati. |
| `data.schema.id` | Il valore `$id` dello schema XDM di destinazione. |
| `params.dataSetId` | ID del set di dati di destinazione. |
| `connectionSpec.id` | ID specifica di connessione per l&#39;automazione di marketing. |

>[!IMPORTANT] Quando create una connessione di destinazione, accertatevi di utilizzare il valore della connessione di base del dataset per la connessione di base, `id` anziché l&#39;ID di connessione del connettore di origine di terze parti.

```json
{
    "id": "fd82157f-0eea-4c81-8215-7f0eeaec8139",
    "etag": "\"5301d5ac-0000-0200-0000-5e97981a0000\""
}
```

## Creare una mappatura {#mapping}

Affinché i dati di origine siano assimilati in un set di dati di destinazione, devono essere mappati sullo schema di destinazione a cui aderisce il set di dati di destinazione. Questo si ottiene eseguendo una richiesta POST all&#39;API del servizio di conversione con mappature dati definite all&#39;interno del payload della richiesta.

**Formato API**

```https
POST /conversion/mappingSets
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/63f2c82fcdcb606c536a62d7716e34acbf63cd4582a1c16b",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "Properties_Firstname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "Properties_Lastname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "repositoryCreatedBy",
                "sourceAttribute": "Added_At",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Portal_Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `xdmSchema` | ID dello schema XDM di destinazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Archiviate questo valore come richiesto nel passaggio successivo per la creazione di un flusso di dati.

```json
{
    "id": "280a3cc950894945bf815c5fc60f3803",
    "version": 0,
    "createdDate": 1586993661034,
    "modifiedDate": 1586993661034,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Ricerca delle specifiche del flusso di dati {#specs}

Un flusso di dati è responsabile della raccolta di dati da origini e del loro inserimento in Piattaforma. Per creare un flusso di dati, è innanzitutto necessario ottenere le specifiche del flusso di dati responsabili della raccolta dei dati di automazione del marketing.

**Formato API**

```https
GET /flowSpecs?property=name=="CRMToAEP"
```

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CRMToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta di successo restituisce i dettagli della specifica del flusso di dati che è responsabile dell&#39;inserimento dei dati dal sistema di automazione di marketing in Piattaforma. Memorizzare il valore del `id` campo come richiesto nel passaggio successivo per creare un nuovo flusso di dati.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            }
        }
    ]
}
```

## Creare un flusso di dati

L&#39;ultimo passo verso la raccolta dei dati di automazione del marketing è creare un flusso di dati. A questo punto sono stati preparati i seguenti valori obbligatori:

* [ID connessione di origine](#source)
* [ID connessione di destinazione](#target)
* [ID mappatura](#mapping)
* [ID specifica Dataflow](#specs)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un&#39;origine. È possibile creare un flusso di dati eseguendo una richiesta POST fornendo al contempo i valori indicati in precedenza all&#39;interno del payload.

**Formato API**

```https
POST /flows
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataflow for marketing automation",
        "description": "Dataflow for marketing automation",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "c315c0ae-a339-44c4-95c0-aea33964c420"
        ],
        "targetConnectionIds": [
            "fd82157f-0eea-4c81-8215-7f0eeaec8139"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "280a3cc950894945bf815c5fc60f3803",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "<START TIME>",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `flowSpec.id` | ID specifica di Flusso di dati. |
| `sourceConnectionIds` | ID connessione di origine. |
| `targetConnectionIds` | ID connessione di destinazione. |
| `transformations.params.mappingId` | ID mappatura. |

**Risposta**

Una risposta corretta restituisce l’ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore di origine per raccogliere i dati da un sistema di automazione di marketing su base programmata. I dati in entrata possono ora essere utilizzati dai servizi della piattaforma a valle, come Profilo cliente in tempo reale e Data Science Workspace. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
* [Panoramica di Analysis Workspace](../../../../data-science-workspace/home.md)