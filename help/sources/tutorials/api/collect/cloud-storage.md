---
keywords: Experience Platform;home;argomenti comuni;dati di archiviazione cloud
solution: Experience Platform
title: Raccolta di dati di archiviazione cloud tramite connettori di origine e API
topic-legacy: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi per recuperare i dati da un archivio cloud di terze parti e inserirli in Platform utilizzando i connettori sorgente e le API.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 10f04044e970158131677e0c630edf761d4577bd
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 2%

---

# Raccogliere dati di archiviazione cloud utilizzando connettori di origine e API

Questa esercitazione descrive i passaggi per recuperare i dati da un archivio cloud di terze parti e inserirli in Platform tramite i connettori sorgente e il [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa esercitazione richiede l’accesso a un archivio cloud di terze parti tramite una connessione valida e informazioni sul file che desideri inserire in Platform, compreso il percorso e la struttura del file. Se non disponi di queste informazioni, consulta l’esercitazione su [esplorazione di un cloud storage di terze parti tramite [!DNL Flow Service] API](../explore/cloud-storage.md) prima di provare questa esercitazione.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Guida per gli sviluppatori del Registro di sistema dello schema](../../../../xdm/api/getting-started.md): Include informazioni importanti da conoscere per eseguire correttamente le chiamate all’API del Registro di sistema dello schema. Questo include `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni richieste per effettuare richieste (con particolare attenzione all’intestazione Accept e ai suoi possibili valori).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catalogo è il sistema di registrazione per la posizione dei dati e la derivazione all&#39;interno di Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): L’API di acquisizione in batch consente di inserire dati in Experience Platform come file batch.
- [Sandbox](../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.
Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un archivio cloud utilizzando [!DNL Flow Service] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in Experience Platform, comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

- `Content-Type: application/json`

## Creazione di una connessione sorgente {#source}

È possibile creare una connessione sorgente effettuando una richiesta di POST al [!DNL Flow Service] API. Una connessione di origine è costituita da un ID connessione, un percorso del file di dati di origine e un ID della specifica di connessione.

Per creare una connessione di origine, è inoltre necessario definire un valore enum per l&#39;attributo del formato dati.

Utilizza i seguenti valori enum per le origini basate su file:

| Formato dati | Valore Enum |
| ----------- | ---------- |
| Delimitato | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Per tutte le origini basate su tabella, impostare il valore su `tabular`.

- [Creazione di una connessione sorgente tramite file delimitati personalizzati](#using-custom-delimited-files)
- [Creazione di una connessione sorgente tramite file compressi](#using-compressed-files)

**Formato API**

```http
POST /sourceConnections
```

### Creazione di una connessione sorgente tramite file delimitati personalizzati {#using-custom-delimited-files}

**Richiesta**

È possibile acquisire un file delimitato con un delimitatore personalizzato specificando un `columnDelimiter` come proprietà. Qualsiasi valore di carattere singolo è un delimitatore di colonna consentito. Se non viene fornita, viene visualizzata una virgola `(,)` viene utilizzato come valore predefinito.

Nell&#39;esempio seguente viene creata una connessione di origine per un tipo di file delimitato utilizzando valori separati da tabulazioni.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for delimited files",
        "description": "Cloud storage source connector",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "columnDelimiter": "\t"
        },
        "params": {
            "path": "/ingestion-demos/leads/tsv_data/*.tsv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `baseConnectionId` | ID di connessione univoco del sistema di archiviazione cloud di terze parti a cui si accede. |
| `data.format` | Valore enum che definisce l’attributo del formato dati. |
| `data.columnDelimiter` | È possibile utilizzare qualsiasi carattere di delimitazione di colonna singolo per raccogliere file flat. Questa proprietà è necessaria solo per l’acquisizione di file CSV o TSV. |
| `params.path` | Percorso del file di origine a cui si accede. |
| `connectionSpec.id` | ID delle specifiche di connessione associato al sistema di archiviazione cloud di terze parti specifico. Consulta la sezione [appendice](#appendix) per un elenco degli ID delle specifiche di connessione. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Creazione di una connessione sorgente tramite file compressi {#using-compressed-files}

**Richiesta**

Puoi anche acquisire file JSON compressi o delimitati specificandone i valori `compressionType` come proprietà. L’elenco dei tipi di file compressi supportati è:

- `bzip2`
- `gzip`
- `deflate`
- `zipDeflate`
- `tarGzip`
- `tar`

Nell&#39;esempio seguente viene creata una connessione sorgente per un file delimitato compresso utilizzando un `gzip` tipo di file.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for compressed files",
        "description": "Cloud storage source connection for compressed files",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "properties": {
                "compressionType" : "gzip"
            }
        },
        "params": {
            "path": "/compressed/files.gzip"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
     }'
```

| Proprietà | Descrizione |
| --- | --- |
| `data.properties.compressionType` | Determina il tipo di file compresso da acquisire. Questa proprietà è necessaria solo durante l’acquisizione di file JSON compressi o delimitati. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Creare uno schema XDM di destinazione {#target-schema}

Affinché i dati di origine possano essere utilizzati in Platform, è necessario creare uno schema di destinazione per strutturare i dati di origine in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione effettuando una richiesta POST al [API del Registro di sistema dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**Formato API**

```http
POST /schemaregistry/tenant/schemas
```

**Richiesta**

La seguente richiesta di esempio crea uno schema XDM che estende la classe Profilo individuale XDM.

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
        "title": "Target schema for a Cloud Storage connector",
        "description": "Target schema for a Cloud Storage connector",
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

Una risposta corretta restituisce i dettagli dello schema appena creato, incluso il relativo identificatore univoco (`$id`). Questo ID è necessario nei passaggi successivi per creare un set di dati di destinazione, una mappatura e un flusso di dati.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:altId": "_{TENANT_ID}.schemas.995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema cloud storage",
    "type": "object",
    "description": "Target schema for cloud storage",
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
        "repo:createdDate": 1597783248870,
        "repo:lastModifiedDate": 1597783248870,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "596661ec6c7a9c6ae530676e98290a4a58ca29540ed92489cf4478b2bf013a65",
        "meta:globalLibVersion": "1.13.3"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "{TENANT_ID}"
}
```

## Creare un set di dati di destinazione

È possibile creare un set di dati di destinazione eseguendo una richiesta di POST al [API del servizio catalogo](https://www.adobe.io/experience-platform-apis/references/catalog/), fornendo l’ID dello schema di destinazione all’interno del payload.

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
        "name": "Target dataset for cloud storage",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `schemaRef.id` | ID dello schema XDM di destinazione. |
| `schemaRef.contentType` | Versione dello schema. Questo valore deve essere impostato `application/vnd.adobe.xed-full-notext+json;version=1`, che restituisce la versione secondaria più recente dello schema. |

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API. L’ID del set di dati di destinazione è necessario nei passaggi successivi per creare una connessione di destinazione e un flusso di dati.

```json
[
    "@/dataSets/5f3c3cedb2805c194ff0b69a"
]
```

## Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui i dati acquisiti arrivano. Per creare una connessione di destinazione, devi fornire l’ID di specifica di connessione fisso associato al Data Lake. Questo ID della specifica di connessione è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci di uno schema di destinazione di un set di dati di destinazione e dell’ID delle specifiche di connessione di Data Lake. Utilizzando questi identificatori, puoi creare una connessione di destinazione utilizzando [!DNL Flow Service] API per specificare il set di dati che conterrà i dati di origine in entrata.

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.schema.id` | La `$id` dello schema XDM di destinazione. |
| `data.schema.version` | Versione dello schema. Questo valore deve essere impostato `application/vnd.adobe.xed-full+json;version=1`, che restituisce la versione secondaria più recente dello schema. |
| `params.dataSetId` | ID del set di dati di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione fissa al Data Lake. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è necessario nei passaggi successivi.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Creare una mappatura {#mapping}

Affinché i dati di origine possano essere acquisiti in un set di dati di destinazione, devono prima essere mappati sullo schema di destinazione a cui il set di dati di destinazione aderisce. Questo si ottiene eseguendo una richiesta POST al servizio di conversione con mappature dati definite all’interno del payload della richiesta.

>[!TIP]
>
>È possibile mappare tipi di dati complessi, ad esempio array in file JSON, utilizzando un connettore di origine dell’archiviazione cloud.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
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
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
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

Una risposta corretta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo valore è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recupera specifiche del flusso di dati {#specs}

Un flusso di dati è responsabile della raccolta dei dati da origini e del loro inserimento in Platform. Per creare un flusso di dati, è innanzitutto necessario ottenere le specifiche del flusso di dati responsabili della raccolta dei dati di archiviazione cloud.

**Formato API**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della specifica del flusso di dati responsabile dell’inserimento dei dati dall’origine in Platform. La risposta include le specifiche di flusso univoche `id` necessario per creare un nuovo flusso di dati.

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
                "ecadc60c-7455-4d87-84dc-2a0e293d997b",
                "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
                "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
                "32e8f412-cdf7-464c-9885-78184cb113fd",
                "b7bf2577-4520-42c9-bae9-cad01560f7bc",
                "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
                "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8"
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

L’ultimo passo verso la raccolta dei dati di archiviazione cloud è la creazione di un flusso di dati. A questo punto sono stati preparati i seguenti valori richiesti:

- [ID connessione di origine](#source)
- [ID connessione di destinazione](#target)
- [ID mappatura](#mapping)
- [ID specifica del flusso di dati](#specs)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. È possibile creare un flusso di dati eseguendo una richiesta di POST fornendo al contempo i valori precedentemente menzionati all’interno del payload.

>[!NOTE]
>
>Per l’acquisizione batch, ogni flusso di dati successivo seleziona i file da acquisire dalla sorgente in base ai relativi **ultima modifica** timestamp. Ciò significa che i flussi di dati batch selezionano i file dall’origine nuovi o modificati dall’ultima esecuzione del flusso di dati.

Per pianificare un’acquisizione, è innanzitutto necessario impostare il valore dell’ora di inizio in modo che l’ora di inizio sia espressa in secondi. Quindi, è necessario impostare il valore della frequenza su una delle cinque opzioni: `once`, `minute`, `hour`, `day`oppure `week`. Il valore dell’intervallo indica il periodo tra due acquisizioni consecutive e la creazione di un’acquisizione una tantum non richiede l’impostazione di un intervallo. Per tutte le altre frequenze, il valore dell&#39;intervallo deve essere impostato su uguale o maggiore di `15`.

>[!IMPORTANT]
>
>Si consiglia vivamente di pianificare il flusso di dati per l’inserimento una tantum quando si utilizza il [Connettore FTP](../../../connectors/cloud-storage/ftp.md).

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
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `flowSpec.id` | La [ID delle specifiche di flusso](#specs) recuperato nel passaggio precedente. |
| `sourceConnectionIds` | La [ID connessione di origine](#source) recuperato in un passaggio precedente. |
| `targetConnectionIds` | La [ID connessione di destinazione](#target-connection) recuperato in un passaggio precedente. |
| `transformations.params.mappingId` | La [ID mappatura](#mapping) recuperato in un passaggio precedente. |
| `scheduleParams.startTime` | Ora di inizio del flusso di dati in epoch time. |
| `scheduleParams.frequency` | Frequenza con cui il flusso di dati raccoglie i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day`oppure `week`. |
| `scheduleParams.interval` | L&#39;intervallo indica il periodo tra due esecuzioni di flusso consecutive. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. L&#39;intervallo non è necessario quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per altri valori di frequenza. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sulle esecuzioni del flusso, lo stato di completamento e gli errori. Per ulteriori informazioni su come monitorare i flussi di dati, consulta l’esercitazione su [monitoraggio dei flussi di dati nell’API](../monitor.md)

## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore di origine per raccogliere i dati dall’archiviazione cloud su base pianificata. I dati in arrivo possono ora essere utilizzati dai servizi della piattaforma a valle, come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
- [Panoramica di Data Science Workspace](../../../../data-science-workspace/home.md)

## Appendice {#appendix}

Nella sezione seguente sono elencati i diversi connettori sorgente di archiviazione cloud e le relative specifiche di connessione.

### Specifica di connessione

| Nome del connettore | Specifiche di connessione |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (Hubs evento) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
