---
keywords: Experience Platform;home;argomenti comuni;dati di archiviazione cloud;dati in streaming;streaming
solution: Experience Platform
title: Creare un flusso di dati in streaming per i dati non elaborati utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi per recuperare i dati in streaming e inserirli in Platform utilizzando i connettori sorgente e le API.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 4%

---

# Crea un flusso di dati in streaming per i dati non elaborati utilizzando [!DNL Flow Service] API

Questa esercitazione descrive i passaggi per recuperare i dati non elaborati da un connettore di origine streaming e portarli ad Experience Platform utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Guida per gli sviluppatori del Registro di sistema dello schema](../../../../xdm/api/getting-started.md): Include informazioni importanti da conoscere per eseguire correttamente le chiamate all’API del Registro di sistema dello schema. Questo include `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni richieste per effettuare richieste (con particolare attenzione all’intestazione Accept e ai suoi possibili valori).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog è il sistema di registrazione per la posizione e la derivazione dei dati in Experience Platform.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): L’acquisizione in streaming per Platform fornisce agli utenti un metodo per inviare in tempo reale dati da dispositivi lato client e lato server ad Experience Platform.
- [Sandbox](../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).

### Creazione di una connessione sorgente {#source}

Questa esercitazione richiede anche un ID di connessione sorgente valido per un connettore streaming. Se non disponi di queste informazioni, consulta le seguenti esercitazioni sulla creazione di una connessione sorgente di streaming prima di provare questa esercitazione:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## Creare uno schema XDM di destinazione {#target-schema}

Affinché i dati di origine possano essere utilizzati in Platform, è necessario creare uno schema di destinazione per strutturare i dati di origine in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine. Questo schema XDM di destinazione estende anche XDM [!DNL Individual Profile] classe.

Per creare uno schema XDM di destinazione, effettua una richiesta POST al `/schemas` punto finale [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La seguente richiesta di esempio crea uno schema XDM che estende XDM [!DNL Individual Profile] classe.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
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

Una risposta corretta restituisce i dettagli dello schema appena creato, incluso il relativo identificatore univoco (`$id`). Questo ID è necessario nei passaggi successivi per creare un set di dati di destinazione, una mappatura e un flusso di dati.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
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
    "imsOrg": "{ORG_ID}",
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
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creare un set di dati di destinazione

Con uno schema XDM di destinazione creato e il relativo univoco `$id` ora puoi creare un set di dati di destinazione per contenere i dati di origine. Per creare un set di dati di destinazione, effettua una richiesta POST al `dataSets` punto finale [API del servizio catalogo](https://www.adobe.io/experience-platform-apis/references/catalog/), fornendo al tempo stesso l’ID dello schema di destinazione all’interno del payload.

**Formato API**

```http
POST /catalog/dataSets
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome del set di dati da creare. |
| `schemaRef.id` | URI `$id` per lo schema XDM su cui si baserà il set di dati. |
| `schemaRef.contentType` | Versione dello schema. Questo valore deve essere impostato su `application/vnd.adobe.xed-full-notext+json;version=1`, che restituisce la versione secondaria più recente dello schema. Vedi la sezione su [versione dello schema](../../../../xdm/api/getting-started.md#versioning) nella guida API XDM per ulteriori informazioni. |

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API. L’ID del set di dati di destinazione è necessario nei passaggi successivi per creare una connessione di destinazione e un flusso di dati.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Creare una connessione di destinazione {#target-connection}

Le connessioni di Target creano e gestiscono una connessione di destinazione a Platform o qualsiasi posizione in cui i dati trasferiti verranno trasferiti. Le connessioni di Target contengono informazioni sulla destinazione dei dati, il formato dei dati e l’ID di connessione di destinazione necessari per creare un flusso di dati. Le istanze di connessione di destinazione sono specifiche per un tenant e un’organizzazione IMS.

Per creare una connessione di destinazione, invia una richiesta POST al `/targetConnections` punto finale [!DNL Flow Service] API. Come parte della richiesta, devi fornire il formato dati, il `dataSetId` recuperati nel passaggio precedente e l’ID della specifica di connessione fissa associato a [!DNL Data Lake]. Questo ID è `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `connectionSpec.id` | ID della specifica di connessione utilizzato per la connessione al [!DNL Data Lake]. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Il formato specificato dei dati a cui si sta portando [!DNL Data Lake]. |
| `params.dataSetId` | ID del set di dati di destinazione recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è necessario nei passaggi successivi.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Creare una mappatura {#mapping}

Affinché i dati di origine possano essere acquisiti in un set di dati di destinazione, devono prima essere mappati sullo schema di destinazione a cui aderisce il set di dati di destinazione.

Per creare un set di mappatura, invia una richiesta POST al gruppo `mappingSets` punto finale [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) fornendo lo schema XDM di destinazione `$id` e i dettagli dei set di mappatura che desideri creare.

**Formato API**

```http
POST /mappingSets
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "firstName",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "lastName",
                "identity": false,
                "version": 0
            }
        ]
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `xdmSchema` | La `$id` dello schema XDM di destinazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recupera un elenco di specifiche del flusso di dati {#specs}

Un flusso di dati è responsabile della raccolta dei dati da origini e del loro inserimento in Platform. Per creare un flusso di dati, devi prima ottenere le specifiche del flusso di dati eseguendo una richiesta di GET al [!DNL Flow Service] API.

**Formato API**

```http
GET /flowSpecs
```

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di specifiche del flusso di dati. ID della specifica del flusso di dati da recuperare per creare un flusso di dati utilizzando uno qualsiasi dei [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]oppure  [!DNL Google PubSub], `d69717ba-71b4-4313-b654-49f9cf126d7a`.

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        },
    ]
}
```

## Creare un flusso di dati

L’ultimo passo verso la raccolta dei dati in streaming è quello di creare un flusso di dati. A questo punto sono stati preparati i seguenti valori richiesti:

- [ID connessione di origine](#source)
- [ID connessione di destinazione](#target)
- [ID mappatura](#mapping)
- [ID specifica del flusso di dati](#specs)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. È possibile creare un flusso di dati eseguendo una richiesta di POST fornendo al contempo i valori precedentemente menzionati all’interno del payload.

**Formato API**

```http
POST /flows
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `flowSpec.id` | La [ID delle specifiche di flusso](#specs) recuperato nel passaggio precedente. |
| `sourceConnectionIds` | La [ID connessione di origine](#source) recuperato in un passaggio precedente. |
| `targetConnectionIds` | La [ID connessione di destinazione](#target-connection) recuperato in un passaggio precedente. |
| `transformations.params.mappingId` | La [ID mappatura](#mapping) recuperato in un passaggio precedente. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un flusso di dati per raccogliere i dati in streaming dal connettore streaming. I dati in arrivo possono ora essere utilizzati dai servizi della piattaforma a valle, come [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
- [Panoramica di Data Science Workspace](../../../../data-science-workspace/home.md)
