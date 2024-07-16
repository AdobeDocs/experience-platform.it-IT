---
keywords: Experience Platform;home;argomenti popolari;cloud storage data;streaming data;streaming data;streaming
solution: Experience Platform
title: Creare un flusso di dati in streaming per i dati non elaborati utilizzando l’API del servizio Flusso
type: Tutorial
description: Questo tutorial illustra i passaggi per recuperare i dati in streaming e importarli in Platform utilizzando i connettori e le API di origine.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 39b5a2b76c28033b9e98dcefc4cdcaa9964f4d2e
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 3%

---

# Creare un flusso di dati in streaming per i dati non elaborati utilizzando l&#39;API [!DNL Flow Service]

Questa esercitazione descrive i passaggi per recuperare dati non elaborati da un connettore di origine streaming e portarli ad Experience Platform utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Guida per gli sviluppatori del Registro di schema](../../../../xdm/api/getting-started.md): include informazioni importanti che è necessario conoscere per eseguire correttamente le chiamate all&#39;API del Registro di schema. Ciò include `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all&#39;intestazione Accept e ai suoi possibili valori).
- [[!DNL Catalog Service]](../../../../catalog/home.md): il catalogo è il sistema di registrazione per la posizione e la derivazione dei dati all&#39;interno di Experience Platform.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): l&#39;acquisizione in streaming per Platform fornisce agli utenti un metodo per inviare dati da dispositivi lato client e lato server a Experience Platform in tempo reale.
- [Sandbox](../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).

### Creare una connessione sorgente {#source}

Questo tutorial richiede anche un ID di connessione sorgente valido per un connettore di streaming. Se non disponi di queste informazioni, consulta le seguenti esercitazioni su come creare una connessione sorgente di streaming prima di provare questa esercitazione:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## Creare uno schema XDM di destinazione {#target-schema}

Per utilizzare i dati sorgente in Platform, è necessario creare uno schema di destinazione che strutturi i dati sorgente in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine. Questo schema XDM di destinazione estende anche la classe XDM [!DNL Individual Profile].

Per creare uno schema XDM di destinazione, effettua una richiesta POST all&#39;endpoint `/schemas` dell&#39;[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La richiesta di esempio seguente crea uno schema XDM che estende la classe XDM [!DNL Individual Profile].

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

In caso di esito positivo, la risposta restituisce i dettagli dello schema appena creato, incluso il relativo identificatore univoco (`$id`). Questo ID è necessario nei passaggi successivi per creare un set di dati di destinazione, una mappatura e un flusso di dati.

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

Con uno schema XDM di destinazione creato e il relativo `$id` univoco, ora puoi creare un set di dati di destinazione per contenere i dati di origine. Per creare un set di dati di destinazione, effettua una richiesta POST all&#39;endpoint `dataSets` dell&#39;[API Catalog Service](https://www.adobe.io/experience-platform-apis/references/catalog/), fornendo nel contempo l&#39;ID dello schema di destinazione all&#39;interno del payload.

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
| `schemaRef.id` | URI `$id` per lo schema XDM su cui sarà basato il set di dati. |
| `schemaRef.contentType` | Versione dello schema. Questo valore deve essere impostato su `application/vnd.adobe.xed-full-notext+json;version=1`, che restituisce la versione secondaria più recente dello schema. Per ulteriori informazioni, consulta la sezione sul controllo delle versioni dello schema [1} nella guida dell&#39;API XDM.](../../../../xdm/api/getting-started.md#versioning) |

**Risposta**

In caso di esito positivo, la risposta restituisce un array contenente l’ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema e utilizzata per fare riferimento al set di dati nelle chiamate API. L’ID del set di dati di destinazione è richiesto nei passaggi successivi per creare una connessione di destinazione e un flusso di dati.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Creare una connessione di destinazione {#target-connection}

Le connessioni di Target creano e gestiscono una connessione di destinazione a Platform o a qualsiasi posizione in cui verranno recapitati i dati trasferiti. Le connessioni di Target contengono informazioni relative alla destinazione dei dati, al formato dei dati e all’ID della connessione di Target necessari per creare un flusso di dati. Le istanze di connessione di Target sono specifiche per un tenant e un’organizzazione.

Per creare una connessione di destinazione, effettuare una richiesta POST all&#39;endpoint `/targetConnections` dell&#39;API [!DNL Flow Service]. Come parte della richiesta, devi fornire il formato dati, `dataSetId` recuperato nel passaggio precedente e l&#39;ID della specifica di connessione fissa associato a [!DNL Data Lake]. Questo ID è `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
| `data.format` | Il formato specificato dei dati che si stanno portando al data lake. |
| `params.dataSetId` | ID del set di dati di destinazione generato nel passaggio precedente. **Nota**: è necessario fornire un ID set di dati valido durante la creazione di una connessione di destinazione. Un ID di set di dati non valido genererà un errore. |
| `connectionSpec.id` | ID della specifica di connessione utilizzato per connettersi al data lake. ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è richiesto nei passaggi successivi.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Creare una mappatura {#mapping}

Per poter acquisire i dati di origine in un set di dati di destinazione, è necessario prima mapparli sullo schema di destinazione a cui il set di dati di destinazione aderisce.

Per creare un set di mappatura, effettua una richiesta POST all&#39;endpoint `mappingSets` dell&#39;[[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) fornendo allo stesso tempo lo schema XDM di destinazione `$id` e i dettagli dei set di mappatura che desideri creare.

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
| `xdmSchema` | `$id` dello schema XDM di destinazione. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

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

## Recuperare un elenco di specifiche del flusso di dati {#specs}

Un flusso di dati è responsabile della raccolta dei dati dalle origini e della loro introduzione in Platform. Per creare un flusso di dati, devi prima ottenere le specifiche del flusso di dati eseguendo una richiesta di GET all&#39;API [!DNL Flow Service].

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

In caso di esito positivo, la risposta restituisce un elenco di specifiche del flusso di dati. L&#39;ID di specifica del flusso di dati da recuperare per creare un flusso di dati utilizzando uno qualsiasi di [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] o [!DNL Google PubSub] è `d69717ba-71b4-4313-b654-49f9cf126d7a`.

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

L’ultimo passaggio per la raccolta dei dati in streaming è la creazione di un flusso di dati. A questo punto sono stati preparati i seguenti valori obbligatori:

- [ID connessione Source](#source)
- [ID connessione di destinazione](#target)
- [ID di mappatura](#mapping)
- [ID specifica flusso di dati](#specs)

Un flusso di dati è responsabile della pianificazione e della raccolta di dati da un’origine. Puoi creare un flusso di dati eseguendo una richiesta POST e fornendo i valori precedentemente menzionati all’interno del payload.

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
| `flowSpec.id` | L&#39;ID [specifica di flusso](#specs) recuperato nel passaggio precedente. |
| `sourceConnectionIds` | L&#39;[ID connessione di origine](#source) recuperato in un passaggio precedente. |
| `targetConnectionIds` | L&#39;[ID connessione di destinazione](#target-connection) recuperato in un passaggio precedente. |
| `transformations.params.mappingId` | [ID mappatura](#mapping) recuperato in un passaggio precedente. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Dati Post per l’acquisizione

Per esempi di codice JSON non elaborato o conforme a XDM da inviare per l’acquisizione, visualizza il payload di esempio riportato di seguito.

>[!NOTE]
>
>È necessario aggiungere un ritardo di almeno ~5 minuti tra la creazione del flusso di dati e l’acquisizione di eventuali dati in streaming. Questo consente di abilitare completamente il flusso di dati prima dell’acquisizione di qualsiasi dato.

Gli esempi seguenti si applicano a tutti:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

>[!BEGINTABS]

>[!TAB Dati non elaborati]

```json
'{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB Dati XDM]

```json
{
  "header": {
    "schemaRef": {
      "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
      "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
      }
    },
    "xdmEntity": {
      "_id": "acme",
      "workEmail": {
        "address": "mike@acme.com",
        "primary": true,
        "type": "work",
        "status": "active"
      },
      "person": {
        "gender": "male",
        "name": {
          "firstName": "Mike",
          "lastName": "Wazowski"
        },
        "birthDate": "1985-01-01"
      },
      "identityMap": {
        "ecid": [
          {
            "id": "01262118050522051420082102000000000000"
          }
        ]
      }
    }
  }
}
```

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai creato un flusso di dati per raccogliere i dati di streaming dal connettore di streaming. I dati in arrivo possono ora essere utilizzati dai servizi Platform a valle come [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [Panoramica di profilo cliente in tempo reale](../../../../profile/home.md)
- [Panoramica di Data Science Workspace](../../../../data-science-workspace/home.md)
