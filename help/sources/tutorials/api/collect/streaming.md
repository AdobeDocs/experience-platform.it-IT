---
keywords: Experience Platform;home;argomenti comuni;dati di archiviazione cloud;dati in streaming;streaming
solution: Experience Platform
title: Raccogliere dati in streaming utilizzando connettori sorgente e API
topic: ' - Panoramica'
type: Tutorial
description: Questa esercitazione descrive i passaggi per recuperare i dati in streaming e inserirli in Platform utilizzando i connettori sorgente e le API.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 2%

---


# Raccogliere dati in streaming utilizzando connettori sorgente e API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie sorgenti all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione descrive i passaggi per recuperare i dati da un connettore di origine streaming e portarli a [!DNL Experience Platform] utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa esercitazione richiede un ID di connessione valido per un connettore streaming. Se non disponi di queste informazioni, consulta le seguenti esercitazioni sulla creazione di una connessione sorgente di streaming prima di provare questa esercitazione:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL HTTP API]](../create/streaming/http.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Il framework standardizzato tramite il quale Experience Platform organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Guida](../../../../xdm/api/getting-started.md) per gli sviluppatori del Registro di schema: Include informazioni importanti da conoscere per eseguire correttamente le chiamate all’API del Registro di sistema dello schema. Questo include il tuo `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni richieste per fare richieste (con particolare attenzione all&#39;intestazione Accept e ai suoi possibili valori).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catalogo è il sistema di registrazione per la posizione dei dati e la derivazione all&#39;interno di  [!DNL Experience Platform].
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): L’acquisizione in streaming per  [!DNL Platform] fornisce agli utenti un metodo per inviare dati da dispositivi lato client e lato server a  [!DNL Experience Platform] in tempo reale.
- [Sandbox](../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per raccogliere correttamente i dati in streaming utilizzando l’ API [!DNL Flow Service] .

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

- `Content-Type: application/json`

## Creare una connessione sorgente {#source}

Puoi creare una connessione sorgente effettuando una richiesta POST all’ API [!DNL Flow Service] . Una connessione di origine è costituita da un ID connessione, un percorso del file di dati di origine e un ID della specifica di connessione.

Per creare una connessione di origine, è inoltre necessario definire un valore enum per l&#39;attributo del formato dati.

Utilizza i seguenti valori enum per i connettori basati su file:

| Formato dati | Valore Enum |
| ----------- | ---------- |
| Delimitato | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Per tutti i connettori basati su tabelle, imposta il valore su `tabular`.

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
        "name": "Test source connector for streaming data",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "connectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
        "description": "Test source connector for streaming data",
        "data": {
            "format": "delimited"
        },
            "connectionSpec": {
            "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `providerId` | ID provider del connettore streaming. |
| `connectionId` | ID di connessione univoco del connettore streaming. |
| `connectionSpec.id` | ID della specifica di connessione associata al connettore di streaming specifico. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "2abd97c4-91bb-4c93-bd97-c491bbfc933d",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Creare uno schema XDM di destinazione {#target-schema}

Affinché i dati di origine siano utilizzati in [!DNL Platform], è necessario creare uno schema di destinazione per strutturare i dati di origine in base alle proprie esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati [!DNL Platform] in cui sono contenuti i dati di origine. Questo schema XDM di destinazione estende anche la classe XDM [!DNL Individual Profile] .

Uno schema XDM di destinazione può essere creato eseguendo una richiesta POST all&#39; [API del Registro di sistema dello schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La seguente richiesta di esempio crea uno schema XDM che estende la classe XDM [!DNL Individual Profile] .

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

Una risposta corretta restituisce i dettagli dello schema appena creato, compreso l’identificatore univoco (`$id`). Questo ID è necessario nei passaggi successivi per creare un set di dati di destinazione, una mappatura e un flusso di dati.

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

Un set di dati di destinazione può essere creato eseguendo una richiesta POST all&#39; [API del servizio catalogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornendo l&#39;ID dello schema di destinazione all&#39;interno del payload.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.1"
        },
        "fileDescription": {
            "format": "parquet"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        },
        "name": "Test streaming dataset"
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `schemaRef.id` | ID dello schema XDM di destinazione. |

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API. L’ID del set di dati di destinazione è necessario nei passaggi successivi per creare una connessione di destinazione e un flusso di dati.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui i dati acquisiti arrivano. Per creare una connessione di destinazione, è necessario specificare l’ID di specifica di connessione fisso associato al data lake. Questo ID della specifica di connessione è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci di uno schema di destinazione di un set di dati di destinazione e dell’ID delle specifiche di connessione di un data lake. Utilizzando questi identificatori, puoi creare una connessione di destinazione utilizzando l’ API [!DNL Flow Service] per specificare il set di dati che conterrà i dati di origine in entrata.

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
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm"
        },
        "params": {
        "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `params.dataSetId` | ID del set di dati di destinazione. |
| `connectionSpec.id` | ID delle specifiche di connessione utilizzato per connettersi al Data Lake. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è necessario nei passaggi successivi.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Creare una mappatura {#mapping}

Affinché i dati di origine possano essere acquisiti in un set di dati di destinazione, devono prima essere mappati sullo schema di destinazione a cui il set di dati di destinazione aderisce. Questo si ottiene eseguendo una richiesta POST al servizio di conversione con mappature dei dati definite all’interno del payload della richiesta.

**Formato API**

```http
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
| `xdmSchema` | Il `$id` dello schema XDM di destinazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova mappatura creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

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

## Cerca specifiche del flusso di dati {#specs}

Un flusso di dati è responsabile della raccolta dei dati dalle origini e del loro inserimento in [!DNL Platform]. Per creare un flusso di dati, devi prima ottenere le specifiche del flusso di dati eseguendo una richiesta GET all’ API [!DNL Flow Service] . Le specifiche del flusso di dati sono responsabili della raccolta di dati da un connettore streaming.
**Formato API**

```http
GET /flowSpecs?property=name=="Steam data with transformation"
```

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="Steam data with transformation"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della specifica del flusso di dati responsabile dell’inserimento dei dati dal connettore di streaming in [!DNL Platform]. Questo ID è necessario nel passaggio successivo per creare un nuovo flusso di dati.

```json
{
    "items": [
        {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "name": "Steam data with transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "d27d4907-7351-47dd-bbc2-05a04365703d",
                "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from Raw to XDM",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        },
                        "required": [
                            "mappingId"
                        ]
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "deleteSupported": false,
                        "updateSupported": false,
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
        }
    ]
}
```

## Creare un flusso di dati

L’ultimo passo verso la raccolta dei dati in streaming è quello di creare un flusso di dati. A questo punto sono stati preparati i seguenti valori richiesti:

- [ID connessione di origine](#source)
- [ID connessione di destinazione](#target)
- [ID mappatura](#mapping)
- [ID specifica del flusso di dati](#specs)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. È possibile creare un flusso di dati eseguendo una richiesta POST fornendo i valori precedentemente menzionati all’interno del payload.

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
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "2abd97c4-91bb-4c93-bd97-c491bbfc933d"
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
| `flowSpec.id` | ID [delle specifiche di flusso](#specs) recuperato nel passaggio precedente. |
| `sourceConnectionIds` | L&#39; [ID connessione di origine](#source) recuperato in un passaggio precedente. |
| `targetConnectionIds` | L&#39; [ID connessione di destinazione](#target-connection) recuperato in un passaggio precedente. |
| `transformations.params.mappingId` | L&#39; [ID di mappatura](#mapping) recuperato in un passaggio precedente. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un flusso di dati per raccogliere i dati in streaming dal connettore streaming . I dati in entrata possono ora essere utilizzati dai servizi a valle [!DNL Platform] come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
- [Panoramica di Data Science Workspace](../../../../data-science-workspace/home.md)