---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Raccogliere i dati del protocollo tramite connettori di origine e API
topic: overview
translation-type: tm+mt
source-git-commit: d5a21462b9f0362414dfe4f73a6c4e4a2c92af61
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 1%

---


# Raccogliere i dati del protocollo tramite connettori di origine e API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione descrive i passaggi necessari per recuperare i dati da un&#39;applicazione protocolli e trasferirli [!DNL Platform] attraverso connettori e API di origine.

## Introduzione

Questa esercitazione richiede l&#39;accesso a un sistema di protocollo tramite una connessione di base valida e informazioni sul file in cui si desidera eseguire l&#39;operazione, [!DNL Platform]incluso il percorso e la struttura della tabella. Se non disponi di tali informazioni, consulta l’esercitazione sull’ [esplorazione dei sistemi di protocollo tramite l’API](../explore/protocols.md) del servizio di flusso prima di provare a seguire questa esercitazione.

* [Sistema](../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Schema Guida](../../../../xdm/api/getting-started.md)per lo sviluppatore del Registro di sistema: Include informazioni importanti che è necessario conoscere per eseguire correttamente le chiamate all&#39;API del Registro di sistema dello schema. Ciò include il vostro `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all’intestazione Accetta e ai suoi possibili valori).
* [Servizio](../../../../catalog/home.md)catalogo: Catalogo è il sistema di registrazione per la posizione dei dati e la linea all&#39;interno [!DNL Experience Platform].
* [Caricamento](../../../../ingestion/batch-ingestion/overview.md)batch: L&#39;API Batch Ingestion consente di assimilare i dati in [!DNL Experience Platform] file batch.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un&#39;applicazione di protocolli utilizzando l&#39; [!DNL Flow Service] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Creare una classe e uno schema XDM ad hoc

Per inserire dati esterni nei connettori di origine, è necessario creare una classe e uno schema XDM ad hoc per i dati di origine non elaborati. [!DNL Platform]

Per creare una classe e uno schema ad hoc, segui i passaggi descritti nell&#39;esercitazione [sullo schema](../../../../xdm/tutorials/ad-hoc.md)ad hoc. Quando create una classe ad hoc, tutti i campi trovati nei dati di origine devono essere descritti all&#39;interno del corpo della richiesta.

Continuate a seguire i passaggi descritti nella guida per gli sviluppatori fino a quando non avete creato uno schema ad hoc. Ottenete e archiviate l&#39;identificatore univoco (`$id`) dello schema ad hoc, quindi passate alla fase successiva dell&#39;esercitazione.

## Creazione di una connessione di origine {#source}

Con la creazione di uno schema XDM ad hoc, ora è possibile creare una connessione di origine utilizzando una richiesta di POST all&#39; [!DNL Flow Service] API. Una connessione di origine è costituita da un ID connessione, un file di dati di origine e un riferimento allo schema che descrive i dati di origine.

Per creare una connessione di origine, è inoltre necessario definire un valore enum per l&#39;attributo del formato dati.

Utilizzate i seguenti valori enum per i connettori **basati su** file:

| Data.format | Valore Enum |
| ----------- | ---------- |
| File delimitati | `delimited` |
| File JSON | `json` |
| Parquet, file | `parquet` |

Per tutti i connettori **basati su** tabelle, utilizzate il valore enum: `tabular`.

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
        "name": "Protocols source connection",
        "baseConnectionId": "a5c6b647-e784-4b58-86b6-47e784ab580b",
        "description": "Protocols source connection to ingest Orders",
        "data": {
            "format": "tabular",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/9e800522521c1ed7d05d3782897f6bd78ee8c2302169bc19",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "Orders"
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `baseConnectionId` | L&#39;ID connessione dell&#39;applicazione protocolli |
| `data.schema.id` | Indica `$id` lo schema XDM ad hoc. |
| `params.path` | Percorso del file di origine. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione dell&#39;applicazione protocolli. |

**Risposta**

Una risposta corretta restituisce l’identificatore univoco (`id`) della connessione di origine appena creata. Questo ID è richiesto nei passaggi successivi per creare una connessione di destinazione.

```json
{
    "id": "0a768941-ddfb-499d-b689-41ddfbf99db0",
    "etag": "\"8f00753e-0000-0200-0000-5e8a547d0000\""
}
```

## Creare uno schema XDM di destinazione {#target}

Nei passaggi precedenti, era stato creato uno schema XDM ad hoc per strutturare i dati di origine. Affinché i dati di origine siano utilizzati in [!DNL Platform], è necessario creare anche uno schema di destinazione per strutturare i dati di origine in base alle esigenze. Lo schema di destinazione viene quindi utilizzato per creare un [!DNL Platform] dataset in cui sono contenuti i dati di origine. Questo schema XDM di destinazione estende anche la [!DNL Individual Profile] classe XDM.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST all&#39;API [del Registro di](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)schema. Se si preferisce utilizzare l&#39;interfaccia utente in [!DNL Experience Platform], l&#39;esercitazione [Editor](../../../../xdm/tutorials/create-schema-ui.md) schema fornisce istruzioni dettagliate per eseguire azioni simili nell&#39;Editor schema.
**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La seguente richiesta di esempio crea uno schema XDM che estende la [!DNL Individual Profile] classe XDM.

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
        "title": "Target schema for protocols",
        "description": "Target schema for protocols",
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

Una risposta corretta restituisce i dettagli dello schema appena creato, incluso il relativo identificatore univoco (`$id`). Questo ID è richiesto nei passaggi successivi per creare un set di dati di destinazione, una mappatura e un flusso di dati.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:altId": "_{TENANT_ID}.schemas.e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Protocols target schema",
    "type": "object",
    "description": "Protocols target schema",
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
    "imsOrg": "7DC732555AECDB4C0A494036@AdobeOrg",
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
        "repo:createdDate": 1586124086523,
        "repo:lastModifiedDate": 1586124086523,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "8b281c23af03ff6a8b7d8061c62d73f7bcbfa1fc7dbabebfb4d8ca77130576ca"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creare un dataset di destinazione

Un set di dati di destinazione può essere creato eseguendo una richiesta di POST all’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog Service, fornendo l’ID dello schema di destinazione all’interno del payload.

**Formato API**

```http
POST /dataSets
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
        "name": "Protocols target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
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
    "@/dataSets/5e8a55ca53662c18af37a83a"
]
```

## Creare una connessione di destinazione

Una connessione di destinazione rappresenta la connessione alla destinazione in cui i dati acquisiti entrano. Per creare una connessione di destinazione, è necessario fornire l&#39;ID di specifica di connessione fisso associato al data Lake. Questo ID della specifica di connessione è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora sono disponibili gli identificatori univoci, uno schema di destinazione, un set di dati di destinazione e l&#39;ID delle specifiche di connessione al data Lake. Utilizzando questi identificatori, potete creare una connessione di destinazione utilizzando l&#39; [!DNL Flow Service] API per specificare il dataset che conterrà i dati di origine in ingresso.

**Formato API**

```http
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
        "name": "Target Connection for protocols",
        "description": "Target Connection for protocols",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            }
        },
        "params": {
            "dataSetId": "5e8a55ca53662c18af37a83a"
        },
            "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.schema.id` | Il valore `$id` dello schema XDM di destinazione. |
| `params.dataSetId` | ID del set di dati di destinazione. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione fissa al data Lake. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione di destinazione. Questo valore è richiesto in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "576d5ecf-f114-4587-ad5e-cff1144587f4",
    "etag": "\"13013506-0000-0200-0000-5e8a56d80000\""
}
```

## Creare una mappatura {#mapping}

Affinché i dati di origine siano assimilati in un set di dati di destinazione, devono essere mappati sullo schema di destinazione a cui aderisce il set di dati di destinazione. Questo si ottiene eseguendo una richiesta POST all&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml) Conversion Service con mappature dati definite all&#39;interno del payload della richiesta.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "OrderID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "CustomerID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "EmployeeID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "createdByBatchID",
                "sourceAttribute": "OrderDate",
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
| `xdmSchema` | Il valore `$id` dello schema XDM di destinazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è richiesto in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "37409d3017e24a3eb4a2dc21020f7a5b",
    "version": 0,
    "createdDate": 1586124873209,
    "modifiedDate": 1586124873209,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## Ricerca delle specifiche del flusso di dati {#specs}

Un flusso di dati è responsabile della raccolta di dati provenienti da origini e del loro inserimento in [!DNL Platform]. Per creare un flusso di dati, è innanzitutto necessario ottenere le specifiche del flusso di dati eseguendo una richiesta di GET all&#39; [!DNL Flow Service] API. Le specifiche di Dataflow sono responsabili della raccolta di dati da un&#39;applicazione di protocolli esterni.

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

Una risposta corretta restituisce i dettagli della specifica del flusso di dati che è responsabile dell&#39;inserimento dei dati dall&#39;applicazione dei protocolli in [!DNL Platform]. Questo ID è richiesto nel passaggio successivo per creare un nuovo flusso di dati.

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

L&#39;ultimo passo verso la raccolta dei dati è creare un flusso di dati. A questo punto, è necessario che siano preparati i seguenti valori obbligatori:

* [ID connessione di origine](#source)
* [ID connessione Target](#target)
* [ID mappatura](#mapping)
* [ID specifica Dataflow](#specs)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un&#39;origine. È possibile creare un flusso di dati eseguendo una richiesta di POST fornendo al contempo i valori indicati in precedenza all&#39;interno del payload.

Per pianificare un&#39;assimilazione, è innanzitutto necessario impostare il valore dell&#39;ora di inizio in modo che l&#39;ora dell&#39;epoch sia espressa in secondi. Quindi, è necessario impostare il valore della frequenza su una delle cinque opzioni: `once`, `minute`, `hour`, `day`o `week`. Il valore dell&#39;intervallo indica il periodo tra due assimilazioni consecutive e la creazione di un&#39;assimilazione una tantum non richiede l&#39;impostazione di un intervallo. Per tutte le altre frequenze, il valore dell&#39;intervallo deve essere impostato su uguale o maggiore di `15`.


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
        "name": "Creating a dataflow for a protocols source",
        "description": "Creating a dataflow for a protocols source",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "0a768941-ddfb-499d-b689-41ddfbf99db0"
        ],
        "targetConnectionIds": [
            "576d5ecf-f114-4587-ad5e-cff1144587f4"
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
                    "mappingId": "7409d3017e24a3eb4a2dc21020f7a5b",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `flowSpec.id` | L&#39;ID della specifica del flusso di dati associato all&#39;origine dei protocolli di terze parti. |
| `sourceConnectionIds` | L&#39;ID di connessione di origine associato all&#39;origine dei protocolli di terze parti. |
| `targetConnectionIds` | L&#39;ID connessione di destinazione associato all&#39;origine dei protocolli di terze parti. |
| `transformations.params.deltaColum` | Colonna designata utilizzata per distinguere tra dati nuovi ed esistenti. I dati incrementali verranno acquisiti in base alla marca temporale della colonna selezionata. |
| `transformations.params.mappingId` | L&#39;ID di mappatura associato all&#39;origine dei protocolli di terze parti. |
| `scheduleParams.startTime` | Ora di inizio per il flusso di dati, espressa in secondi. |
| `scheduleParams.frequency` | I valori di frequenza selezionabili includono: `once`, `minute`, `hour`, `day`o `week`. |
| `scheduleParams.interval` | L&#39;intervallo indica il periodo tra due esecuzioni di flusso consecutive. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. L&#39;intervallo non è richiesto quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per altri valori di frequenza. |

**Risposta**

Una risposta corretta restituisce l’ID `id` del flusso di dati appena creato.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un connettore di origine per raccogliere i dati da un&#39;applicazione protocolli su base pianificata. I dati in entrata possono ora essere utilizzati dai [!DNL Platform] servizi a valle come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
* [Panoramica di Analysis Workspace](../../../../data-science-workspace/home.md)