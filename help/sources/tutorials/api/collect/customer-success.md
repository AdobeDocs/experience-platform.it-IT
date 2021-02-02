---
keywords: ' Experience Platform;home;argomenti popolari;raccogliere successo cliente;successo cliente'
solution: Experience Platform
title: Raccolta di dati da un sistema di successo cliente tramite connettori di origine e API
topic: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per recuperare i dati da un sistema di successo cliente e trasferirli in Piattaforma tramite connettori di origine e API.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 1%

---


# Raccolta di dati da un sistema di successo cliente tramite connettori di origine e API

Questa esercitazione descrive i passaggi necessari per recuperare i dati da un sistema di successo cliente di terze parti e trasferirli in [!DNL Platform] attraverso i connettori di origine e l&#39;API [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa esercitazione richiede l&#39;accesso a un sistema di successo cliente di terze parti tramite una connessione valida e informazioni sul file che si desidera inserire in [!DNL Platform], incluso il percorso e la struttura del file. Se non si dispone di queste informazioni, consultare l&#39;esercitazione su [esplorare un database o un sistema NoSQL utilizzando l&#39;API del servizio di flusso](../explore/customer-success.md) prima di provare a seguire questa esercitazione.

Questa esercitazione richiede inoltre di conoscere i seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Schema Guida](../../../../xdm/api/getting-started.md) per lo sviluppatore del Registro di sistema: Include informazioni importanti che è necessario conoscere per eseguire correttamente le chiamate all&#39;API del Registro di sistema dello schema. Ciò include il `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all&#39;intestazione Accetta e ai relativi valori possibili).
* [[!DNL Catalog Service]](../../../../catalog/home.md): Catalogo è il sistema di registrazione per la posizione dei dati e la linea all&#39;interno  [!DNL Experience Platform].
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): L&#39;API Batch Ingestion consente di assimilare i dati in  [!DNL Experience Platform] file batch.
* [Sandbox](../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un sistema di successo cliente tramite l&#39;API [!DNL Flow Service].

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Creare una connessione di origine {#source}

È possibile creare una connessione di origine effettuando una richiesta di POST all&#39;API [!DNL Flow Service]. Una connessione di origine è costituita da un ID connessione, un percorso al file di dati di origine e un ID di specifica di connessione.

Per creare una connessione di origine, è inoltre necessario definire un valore enum per l&#39;attributo del formato dati.

Utilizzate i seguenti valori enum per i connettori basati su file:

| Formato dati | Valore Enum |
| ----------- | ---------- |
| Delimitato | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Per tutti i connettori basati su tabelle, impostare il valore `tabular`.

**Formato API**

```http
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
        "name": "Source connection for Customer Success",
        "connectionId": "f1da3694-38a9-403d-9a36-9438a9203d42",
        "description": "Source connection for a Customer Success connector",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "Account"
        },
        "connectionSpec": {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `connectionId` | L&#39;ID di connessione univoco del sistema di successo cliente di terze parti a cui si accede. |
| `params.path` | Percorso del file di origine. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione associato allo specifico sistema di successo cliente di terze parti. Per un elenco degli ID delle specifiche di connessione, vedere l&#39; [appendice](#appendix). |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata. Questo ID è richiesto nei passaggi successivi per creare una connessione di destinazione.

```json
{
    "id": "17faf955-2cf8-4b15-baf9-552cf88b1540",
    "etag": "\"2900a761-0000-0200-0000-5ed18cea0000\""
}
```

## Creare uno schema XDM di destinazione {#target-schema}

Affinché i dati di origine siano utilizzati in Piattaforma, è necessario creare uno schema di destinazione per strutturare i dati di origine in base alle esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati della piattaforma in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST all&#39;API del Registro di sistema [Schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

**Formato API**

```http
POST /tenant/schemas
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
        "title": "Target schema for a Customer Success connector",
        "description": "Target schema for a customer success connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
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

Una risposta corretta restituisce i dettagli dello schema appena creato, compreso l&#39;identificatore univoco (`$id`). Questo ID è richiesto nei passaggi successivi per creare un set di dati di destinazione, una mappatura e un flusso di dati.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
    "meta:altId": "_{TENANT_ID}.schemas.b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a Customer Success connector",
    "type": "object",
    "description": "Target schema for a customer success connector",
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
        "repo:createdDate": 1590791550228,
        "repo:lastModifiedDate": 1590791550228,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "d730441903b95425145d9c742647ab4426d86549159182913e5f99cc904be5b1",
        "meta:globalLibVersion": "1.10.4.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creare un dataset di destinazione

È possibile creare un set di dati di destinazione eseguendo una richiesta POST all&#39; [API del servizio catalogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornendo l&#39;ID dello schema di destinazione all&#39;interno del payload.

**Formato API**

```http
POST catalog/dataSets
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
        "name": "Target dataset for a Customer Success connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `schemaRef.id` | `$id` dello schema XDM di destinazione. |

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L&#39;ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API. Archiviate l&#39;ID del set di dati di destinazione come richiesto nei passaggi successivi per creare una connessione di destinazione e un flusso di dati.

```json
[
    "@/dataSets/5ed18e0f4f90b719196f44a9"
]
```

## Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui i dati acquisiti entrano. Per creare una connessione di destinazione, è necessario fornire l&#39;ID di specifica di connessione fisso associato al Data Lake. Questo ID della specifica di connessione è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora sono disponibili gli identificatori univoci, uno schema di destinazione, un set di dati di destinazione e l&#39;ID delle specifiche di connessione al data Lake. Utilizzando l&#39;API [!DNL Flow Service], potete creare una connessione di destinazione specificando questi identificatori insieme al dataset che conterrà i dati di origine in ingresso.

**Formato API**

```http
POST /targetConnections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a customer success connector",
        "description": "Target Connection for a customer success connector",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e543e8a60b15218ad44b95f"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.schema.id` | `$id` dello schema XDM di destinazione. |
| `params.dataSetId` | ID del set di dati di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione utilizzata per connettersi al Data Lake. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo valore è richiesto in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
}
```

## Creare una mappatura {#mapping}

Affinché i dati di origine siano assimilati in un set di dati di destinazione, devono essere mappati sullo schema di destinazione a cui aderisce il set di dati di destinazione. Questo si ottiene eseguendo una richiesta POST all&#39;API [!DNL Conversion Service] con mappature dati definite all&#39;interno del payload della richiesta.

**Formato API**

```http
POST /mappingSets
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "CreatedDate",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `xdmSchema` | `$id` dello schema XDM di destinazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova mappatura creata, incluso il relativo identificatore univoco (`id`). Questo ID è richiesto in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "7c3547d3cfc14f568a51c32b4c0ed739",
    "version": 0,
    "createdDate": 1590792069173,
    "modifiedDate": 1590792069173,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recupero delle specifiche del flusso di dati {#specs}

Un flusso di dati è responsabile della raccolta di dati da origini e del loro inserimento in Platform. Per creare un flusso di dati, è innanzitutto necessario ottenere le specifiche del flusso di dati eseguendo una richiesta di GET all&#39;API del servizio di flusso. Le specifiche di Dataflow sono responsabili della raccolta di dati da un sistema di successo cliente di terze parti.

**Formato API**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della specifica del flusso di dati responsabile dell&#39;inserimento dei dati dall&#39;origine nella piattaforma. La risposta include la specifica di flusso univoca `id` necessaria per creare un nuovo flusso di dati.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "3416976c-a9ca-4bba-901a-1f08f66978ff",
                "38ad80fe-8b06-4938-94f4-d4ee80266b07",
                "d771e9c1-4f26-40dc-8617-ce58c4b53702",
                "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
                "3000eb99-cd47-43f3-827c-43caf170f015",
                "26d738e0-8963-47ea-aadf-c60de735468a",
                "74a1c565-4e59-48d7-9d67-7c03b8a13137",
                "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
                "cb66ab34-8619-49cb-96d1-39b37ede86ea",
                "eb13cb25-47ab-407f-ba89-c0125281c563",
                "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
                "37b6bf40-d318-4655-90be-5cd6f65d334b",
                "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
                "221c7626-58f6-4eec-8ee2-042b0226f03b",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "102706fb-a5cd-42ee-afe0-bc42f017ff43",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "1fe283f6-9bec-11ea-bb37-0242ac130002"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "optionSpec": {
                "name": "OptionSpec",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "errorDiagnosticsEnabled": {
                            "title": "Error diagnostics.",
                            "description": "Flag to enable detailed and sample error diagnostics summary.",
                            "type": "boolean",
                            "default": false
                        },
                        "partialIngestionPercent": {
                            "title": "Partial ingestion threshold.",
                            "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                            "type": "number",
                            "exclusiveMinimum": 0
                        }
                    }
                }
            },
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
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "once",
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "once"
                            }
                        }
                    },
                    "then": {
                        "allOf": [
                            {
                                "not": {
                                    "required": [
                                        "interval"
                                    ]
                                }
                            },
                            {
                                "not": {
                                    "required": [
                                        "backfill"
                                    ]
                                }
                            }
                        ]
                    },
                    "else": {
                        "required": [
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
            },
            "attributes": {
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Creare un flusso di dati

L&#39;ultimo passo verso la raccolta dei dati è creare un flusso di dati. A questo punto, è necessario che siano preparati i seguenti valori obbligatori:

* [ID connessione di origine](#source)
* [ID connessione di destinazione](#target)
* [ID mappatura](#mapping)
* [ID specifica Dataflow](#specs)

Per pianificare un&#39;assimilazione, è innanzitutto necessario impostare il valore dell&#39;ora di inizio in modo che l&#39;ora dell&#39;epoch sia espressa in secondi. Quindi, è necessario impostare il valore della frequenza su una delle cinque opzioni: `once`, `minute`, `hour`, `day` o `week`. Il valore dell&#39;intervallo indica il periodo tra due assimilazioni consecutive e la creazione di un&#39;assimilazione una tantum non richiede l&#39;impostazione di un intervallo. Per tutte le altre frequenze, il valore dell&#39;intervallo deve essere impostato su uguale o maggiore di `15`.

**Formato API**

```http
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
        "name": "Creating a dataflow for a Customer Success connector",
        "description": "Creating a dataflow for a Customer Success connector",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "17faf955-2cf8-4b15-baf9-552cf88b1540"
        ],
        "targetConnectionIds": [
            "bc36ecd6-3b04-4067-b6ec-d63b04b0673d"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "7c3547d3cfc14f568a51c32b4c0ed739",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1590792316",
            "frequency": "minute",
            "interval": "15",
            "backfill": "true"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `flowSpec.id` | ID [specifica di flusso](#specs) recuperato nel passaggio precedente. |
| `sourceConnectionIds` | L&#39; [ID connessione di origine](#source) recuperato in un passaggio precedente. |
| `targetConnectionIds` | L&#39; [ID connessione di destinazione](#target-connection) recuperato in un passaggio precedente. |
| `transformations.params.mappingId` | L&#39; [ID di mappatura](#mapping) recuperato in un passaggio precedente. |
| `transformations.params.deltaColum` | Colonna designata utilizzata per distinguere tra dati nuovi ed esistenti. I dati incrementali verranno acquisiti in base alla marca temporale della colonna selezionata. Il formato di data supportato per `deltaColumn` è `yyyy-MM-dd HH:mm:ss`. |
| `transformations.params.mappingId` | L&#39;ID di mappatura associato al database. |
| `scheduleParams.startTime` | Ora di inizio per il flusso di dati in epoch time. |
| `scheduleParams.frequency` | Frequenza con cui il flusso di dati raccoglie i dati. I valori accettabili sono: `once`, `minute`, `hour`, `day` o `week`. |
| `scheduleParams.interval` | L&#39;intervallo indica il periodo tra due esecuzioni di flusso consecutive. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. L&#39;intervallo non è richiesto quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per gli altri valori di frequenza. |

**Risposta**

Una risposta corretta restituisce l&#39;ID `id` del flusso di dati appena creato.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Monitorare il flusso di dati

Una volta creato il flusso di dati, è possibile monitorare i dati che vengono acquisiti attraverso di esso per visualizzare informazioni sulle esecuzioni del flusso, lo stato di completamento e gli errori. Per ulteriori informazioni su come monitorare i flussi di dati, vedete l&#39;esercitazione sui flussi di dati di [monitoraggio nell&#39;API ](../monitor.md)

## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore di origine per raccogliere i dati da un sistema di successo cliente su base programmata. I dati in entrata possono ora essere utilizzati dai servizi a valle [!DNL Platform] quali [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
* [Panoramica di Analysis Workspace](../../../../data-science-workspace/home.md)

## Appendice

Nella sezione seguente sono elencati i diversi connettori di origine dell&#39;archivio cloud e le relative specifiche di connessione.

### Specifica di connessione

| Nome connettore | Specifica di connessione |
| -------------- | --------------- |
| [!DNL Salesforce Service Cloud] | `cb66ab34-8619-49cb-96d1-39b37ede86ea` |
| [!DNL ServiceNow] | `eb13cb25-47ab-407f-ba89-c0125281c563` |