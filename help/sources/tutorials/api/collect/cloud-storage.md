---
keywords: Experience Platform;home;argomenti popolari;cloud storage data
solution: Experience Platform
title: Creare un flusso di dati per le origini di archiviazione cloud utilizzando l’API del servizio Flusso
type: Tutorial
description: Questo tutorial illustra i passaggi necessari per recuperare i dati da un’archiviazione cloud di terze parti e importarli in Platform utilizzando i connettori e le API di origine.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 48aef63cffbdc52a6a96ef69e5db4f54274144b6
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 3%

---

# Creare un flusso di dati per le origini di archiviazione cloud utilizzando l&#39;API [!DNL Flow Service]

Questa esercitazione descrive i passaggi per recuperare i dati da un&#39;origine di archiviazione cloud e portarli a Platform utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Per creare un flusso di dati, è necessario disporre già di un ID connessione di base valido con un’origine di archiviazione cloud. Se non disponi di questo ID, consulta la [panoramica origini](../../../home.md#cloud-storage) per un elenco delle origini dell&#39;archiviazione cloud con cui puoi creare una connessione di base.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Guida per gli sviluppatori del Registro di schema](../../../../xdm/api/getting-started.md): include informazioni importanti che è necessario conoscere per eseguire correttamente le chiamate all&#39;API del Registro di schema. Ciò include `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all&#39;intestazione Accept e ai suoi possibili valori).
- [[!DNL Catalog Service]](../../../../catalog/home.md): il catalogo è il sistema di registrazione per la posizione e la derivazione dei dati all&#39;interno di Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): l&#39;API di acquisizione batch consente di acquisire dati in Experience Platform come file batch.
- [Sandbox](../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).

## Creare una connessione sorgente {#source}

È possibile creare una connessione di origine effettuando una richiesta POST all&#39;endpoint `sourceConnections` dell&#39;API [!DNL Flow Service] e fornendo l&#39;ID della connessione di base, il percorso del file di origine che si desidera acquisire e l&#39;ID della specifica di connessione corrispondente dell&#39;origine.

Quando si crea una connessione di origine, è necessario definire anche un valore enum per l&#39;attributo del formato dati.

Utilizzare i seguenti valori enum per le origini basate su file:

| Formato dei dati | Valore enum |
| ----------- | ---------- |
| Delimitato | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Per tutte le origini basate su tabelle, impostare il valore su `tabular`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited",
          "properties": {
              "columnDelimiter": "{COLUMN_DELIMITER}",
              "encoding": "{ENCODING}",
              "compressionType": "{COMPRESSION_TYPE}"
          }
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `baseConnectionId` | ID della connessione di base dell’origine di archiviazione cloud. |
| `data.format` | Il formato dei dati che desideri inserire in Platform. I valori supportati sono: `delimited`, `JSON` e `parquet`. |
| `data.properties` | (Facoltativo) Insieme di proprietà che è possibile applicare ai dati durante la creazione di una connessione di origine. |
| `data.properties.columnDelimiter` | (Facoltativo) Un delimitatore di colonna a carattere singolo che è possibile specificare durante la raccolta di file flat. Qualsiasi valore di carattere singolo è un delimitatore di colonna consentito. Se non viene specificato, verrà utilizzata una virgola (`,`) come valore predefinito. **Nota**: la proprietà `columnDelimiter` può essere utilizzata solo durante l&#39;acquisizione di file delimitati. |
| `data.properties.encoding` | (Facoltativo) Proprietà che definisce il tipo di codifica da utilizzare per l’acquisizione dei dati in Platform. I tipi di codifica supportati sono: `UTF-8` e `ISO-8859-1`. **Nota**: il parametro `encoding` è disponibile solo per l&#39;acquisizione di file CSV delimitati. Altri tipi di file verranno acquisiti con la codifica predefinita, `UTF-8`. |
| `data.properties.compressionType` | (Facoltativo) Proprietà che definisce il tipo di file compresso da acquisire. I tipi di file compressi supportati sono: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip` e `tar`. **Nota**: la proprietà `compressionType` può essere utilizzata solo durante l&#39;acquisizione di file delimitati o JSON. |
| `params.path` | Percorso del file di origine a cui si sta effettuando l&#39;accesso. Questo parametro punta a un singolo file o a un&#39;intera cartella.  **Nota**: è possibile utilizzare un asterisco al posto del nome del file per specificare l&#39;acquisizione di un&#39;intera cartella. Ad esempio: `/acme/summerCampaign/*.csv` acquisirà l&#39;intera cartella `/acme/summerCampaign/`. |
| `params.type` | Tipo di file del file di dati di origine che si sta acquisendo. Utilizzare il tipo `file` per acquisire un singolo file e il tipo `folder` per acquisire un&#39;intera cartella. |
| `connectionSpec.id` | ID della specifica di connessione associato all’origine di archiviazione cloud specifica. Per un elenco degli ID delle specifiche di connessione, vedere [appendice](#appendix). |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Utilizza espressioni regolari per selezionare un set specifico di file da acquisire {#regex}

È possibile utilizzare espressioni regolari per acquisire un particolare set di file dall’origine a Platform durante la creazione di una connessione sorgente.

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

Nell’esempio seguente, nel percorso del file viene utilizzata l’espressione regolare per specificare l’acquisizione di tutti i file CSV il cui nome contiene `premium`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/*premium*.csv",
          "type": "folder"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

### Configurare una connessione di origine per acquisire i dati in modo ricorsivo

Durante la creazione di una connessione di origine, è possibile utilizzare il parametro `recursive` per acquisire dati da cartelle nidificate in modo profondo.

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

Nell&#39;esempio seguente, il parametro `recursive: true` informa [!DNL Flow Service] di leggere tutte le sottocartelle in modo ricorsivo durante il processo di acquisizione.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source with recursive ingestion",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/customers/premium/buyers/recursive",
          "type": "folder",
          "recursive": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

## Creare uno schema XDM di destinazione {#target-schema}

Per utilizzare i dati sorgente in Platform, è necessario creare uno schema di destinazione che strutturi i dati sorgente in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST all&#39;API [Schema Registry](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l&#39;esercitazione su [creazione di uno schema utilizzando l&#39;API](../../../../xdm/api/schemas.md).

## Creare un set di dati di destinazione {#target-dataset}

È possibile creare un set di dati di destinazione eseguendo una richiesta POST all&#39;API [Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornendo l&#39;ID dello schema di destinazione all&#39;interno del payload.

Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l&#39;esercitazione su [creazione di un set di dati utilizzando l&#39;API](../../../../catalog/api/create-dataset.md).

## Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui arrivano i dati acquisiti. Per creare una connessione di destinazione, devi fornire l’ID della specifica di connessione fissa associato al Data Lake. ID della specifica di connessione: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci, di uno schema di destinazione, di un set di dati di destinazione e dell’ID della specifica di connessione al Data Lake. Utilizzando questi identificatori, è possibile creare una connessione di destinazione utilizzando l&#39;API [!DNL Flow Service] per specificare il set di dati che conterrà i dati di origine in entrata.

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
| `data.schema.id` | `$id` dello schema XDM di destinazione. |
| `data.schema.version` | Versione dello schema. Questo valore deve essere impostato `application/vnd.adobe.xed-full+json;version=1`, che restituisce la versione secondaria più recente dello schema. |
| `params.dataSetId` | ID del set di dati di destinazione generato nel passaggio precedente. **Nota**: è necessario fornire un ID set di dati valido durante la creazione di una connessione di destinazione. Un ID di set di dati non valido genererà un errore. |
| `connectionSpec.id` | ID della specifica di connessione utilizzato per connettersi al data lake. ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è richiesto nei passaggi successivi.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Creare una mappatura {#mapping}

Per poter acquisire i dati di origine in un set di dati di destinazione, è necessario prima mapparli sullo schema di destinazione a cui il set di dati di destinazione aderisce.

Per creare un set di mappatura, effettua una richiesta POST all&#39;endpoint `mappingSets` dell&#39;[[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) fornendo allo stesso tempo lo schema XDM di destinazione `$id` e i dettagli dei set di mappatura che desideri creare.

>[!TIP]
>
>Puoi mappare tipi di dati complessi, ad esempio array, in file JSON utilizzando un connettore di origine dell’archiviazione cloud.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

In caso di esito positivo, la risposta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo valore è necessario in un passaggio successivo per creare un flusso di dati.

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

## Recuperare le specifiche del flusso di dati {#specs}

Un flusso di dati è responsabile della raccolta dei dati dalle origini e della loro introduzione in Platform. Per creare un flusso di dati, devi innanzitutto ottenere le specifiche del flusso di dati responsabili della raccolta dei dati dell’archiviazione cloud.

**Formato API**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!NOTE]
>
>Il payload di risposta JSON seguente è nascosto per brevità. Seleziona &quot;payload&quot; per visualizzare il payload di risposta.

+++ Visualizza payload

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della specifica del flusso di dati responsabili dell’importazione di dati dall’origine in Platform. La risposta include la specifica di flusso univoca `id` necessaria per creare un nuovo flusso di dati.

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
  "sourceConnectionSpecIds": [
    "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
    "ecadc60c-7455-4d87-84dc-2a0e293d997b",
    "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
    "4c10e202-c428-4796-9208-5f1f5732b1cf",
    "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
    "32e8f412-cdf7-464c-9885-78184cb113fd",
    "b7bf2577-4520-42c9-bae9-cad01560f7bc",
    "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
    "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
    "54e221aa-d342-4707-bcff-7a4bceef0001",
    "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
    "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
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
  },
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
  "transformationSpec": [
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
  "runSpec": {
      "name": "ProviderParams",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for creating flow run.",
        "properties": {
          "startTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
          },
          "windowStartTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "An integer that defines the end time of the window against which data is to be pulled.  The value is represented in Unix epoch time."
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime"
        ]
      }
    }
}
```

+++

## Creare un flusso di dati

L’ultimo passaggio per la raccolta dei dati di archiviazione cloud è la creazione di un flusso di dati. A questo punto sono stati preparati i seguenti valori obbligatori:

- [ID connessione Source](#source)
- [ID connessione di destinazione](#target)
- [ID di mappatura](#mapping)
- [ID specifica flusso di dati](#specs)

Un flusso di dati è responsabile della pianificazione e della raccolta di dati da un’origine. Puoi creare un flusso di dati eseguendo una richiesta POST e fornendo i valori precedentemente menzionati all’interno del payload.

>[!NOTE]
>
>Per l&#39;acquisizione in batch, ogni flusso di dati successivo seleziona i file da acquisire dall&#39;origine in base alla marca temporale **ultima modifica**. Ciò significa che i flussi di dati batch selezionano dall’origine i file che sono nuovi o che sono stati modificati dall’ultima esecuzione del flusso di dati.

Per pianificare un’acquisizione, devi prima impostare il valore dell’ora di inizio su tempo epoca in secondi. Impostare quindi il valore della frequenza su una delle cinque opzioni seguenti: `once`, `minute`, `hour`, `day` o `week`. Il valore di intervallo indica il periodo tra due acquisizioni consecutive e la creazione di un’acquisizione una tantum non richiede l’impostazione di un intervallo. Per tutte le altre frequenze, il valore dell&#39;intervallo deve essere impostato su uguale o maggiore di `15`.

>[!IMPORTANT]
>
>È consigliabile pianificare il flusso di dati per l&#39;acquisizione una tantum quando si utilizza il [connettore FTP](../../../connectors/cloud-storage/ftp.md).

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
                    "mappingVersion": 0
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
| `flowSpec.id` | L&#39;ID [specifica di flusso](#specs) recuperato nel passaggio precedente. |
| `sourceConnectionIds` | L&#39;[ID connessione di origine](#source) recuperato in un passaggio precedente. |
| `targetConnectionIds` | L&#39;[ID connessione di destinazione](#target-connection) recuperato in un passaggio precedente. |
| `transformations.params.mappingId` | [ID mappatura](#mapping) recuperato in un passaggio precedente. |
| `scheduleParams.startTime` | L’ora di inizio del flusso di dati in tempo epoca. |
| `scheduleParams.frequency` | La frequenza con cui il flusso di dati raccoglierà i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day` o `week`. |
| `scheduleParams.interval` | L’intervallo indica il periodo tra due esecuzioni consecutive del flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. Il valore dell&#39;intervallo minimo accettato per ciascuna frequenza è il seguente:<ul><li>**Una volta**: n/d</li><li>**Minuto**: 15</li><li>**Ora**: 1</li><li>**Giorno**: 1</li><li>**Settimana**: 1</li></ul> |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sulle esecuzioni del flusso, sullo stato di completamento e sugli errori. Per ulteriori informazioni su come monitorare i flussi di dati, consulta l&#39;esercitazione sul [monitoraggio dei flussi di dati nell&#39;API](../monitor.md)

## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore di origine per raccogliere i dati dall’archiviazione cloud in base a una pianificazione. I dati in arrivo possono ora essere utilizzati dai servizi Platform a valle come [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [Panoramica di profilo cliente in tempo reale](../../../../profile/home.md)
- [Panoramica di Data Science Workspace](../../../../data-science-workspace/home.md)

## Appendice {#appendix}

Nella sezione seguente sono elencati i diversi connettori di origine dell’archiviazione cloud e le relative specifiche di connessione.

### Specifica di connessione

| Nome connettore | Specifica di connessione |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (BLOB) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (hub eventi) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
