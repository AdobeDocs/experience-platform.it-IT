---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creazione di un set di dati tramite le API
topic: datasets
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 1%

---


# Creazione di un set di dati tramite le API

Questo documento fornisce passaggi generali per la creazione di un dataset utilizzando  API di Adobe Experience Platform e la compilazione del dataset tramite un file.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Caricamento](../../ingestion/batch-ingestion/overview.md)batch:  Experience Platform consente di assimilare i dati come file batch.
* [Sistema](../../xdm/home.md)XDM (Experience Data Model): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
* [Sandbox](../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API Platform.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Esercitazione

Per creare un set di dati, è innanzitutto necessario definire uno schema. Uno schema è un insieme di regole per la rappresentazione dei dati. Oltre a descrivere la struttura dei dati, gli schemi forniscono vincoli e aspettative che possono essere applicati e utilizzati per convalidare i dati mentre vengono spostati tra i sistemi.

Queste definizioni standard consentono l&#39;interpretazione coerente dei dati, indipendentemente dall&#39;origine, e rimuovono la necessità di una traduzione tra le applicazioni. Per ulteriori informazioni sulla composizione degli schemi, vedere la guida sulle [nozioni di base della composizione dello schema](../../xdm/schema/composition.md)

## Cercare uno schema di set di dati

Questa esercitazione inizia nel punto in cui termina l&#39;esercitazione [API](../../xdm/tutorials/create-schema-api.md) Schema del Registro di sistema, utilizzando lo schema Membri fedeltà creato durante tale esercitazione.

Se non è stata completata l&#39;esercitazione del Registro di sistema dello schema, iniziare da tale esercitazione e continuare con l&#39;esercitazione del dataset solo dopo aver composto lo schema necessario.

La seguente chiamata può essere utilizzata per visualizzare lo schema Membri fedeltà creato durante l&#39;esercitazione API del Registro di sistema dello schema:

**Formato API**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Richiesta**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Il formato dell&#39;oggetto response dipende dall&#39;intestazione Accept inviata nella richiesta. Le singole proprietà di questa risposta sono state ridotte a icona per lo spazio.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Creare un dataset

Con lo schema Membri fedeltà attivo, ora è possibile creare un set di dati che faccia riferimento allo schema.

**Formato API**

```HTTP
POST /dataSets
```

**Richiesta**

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

>[!NOTE]
>
>Questa esercitazione utilizza il formato di file [parquet](https://parquet.apache.org/documentation/latest/) per tutti i relativi esempi. Un esempio che utilizza il formato di file JSON è disponibile nella guida per gli sviluppatori di assimilazione [batch](../../ingestion/batch-ingestion/api-overview.md)

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto response costituito da un array contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L&#39;ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Creare un batch

Prima di poter aggiungere dati a un set di dati, è necessario creare un batch collegato al set di dati. Il batch verrà quindi utilizzato per il caricamento.

**Formato API**

```HTTP
POST /batches
```

**Richiesta**

Il corpo della richiesta include un campo &quot;datasetId&quot;, il cui valore è `{DATASET_ID}` generato nel passaggio precedente.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto risposta contenente i dettagli del batch appena creato, inclusa `id`una stringa generata dal sistema di sola lettura.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## Caricare i file in batch

Dopo aver creato un nuovo batch per il caricamento, ora potete caricare i file nel set di dati specifico. È importante ricordare che quando avete definito il dataset, avete specificato il formato di file come parquet. Pertanto, i file caricati devono essere in quel formato.

>[!NOTE]
>
>Il file di caricamento dei dati più grande supportato è 512 MB. Se il file di dati è più grande di questo, deve essere suddiviso in blocchi non superiori a 512 MB, per essere caricato uno alla volta. Potete caricare ciascun file nello stesso batch ripetendo questo passaggio per ciascun file, utilizzando lo stesso ID batch. Non esiste alcun limite al numero se i file possono essere caricati come parte di un batch.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{BATCH_ID}` | Indica `id` il batch in cui si sta caricando. |
| `{DATASET_ID}` | Il `id` set di dati in cui sarà mantenuto il batch. |
| `{FILE_NAME}` | Nome del file che si sta caricando. |

**Richiesta**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Risposta**

Un file caricato correttamente restituisce un corpo di risposta vuoto e lo stato HTTP 200 (OK).

## Completamento batch segnale

Dopo aver caricato tutti i file di dati nel batch, potete segnalare il batch per il completamento. Il completamento della segnalazione determina la creazione da parte del servizio di `DataSetFile` voci di catalogo per i file caricati e la loro associazione con il batch generato in precedenza. Il batch di cataloghi viene contrassegnato con esito positivo, che attiva tutti i flussi a valle che possono quindi funzionare sui dati ora disponibili.

**Formato API**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parametro | Descrizione |
| --- | --- |
| `{BATCH_ID}` | Indica `id` il batch da contrassegnare come completo. |

**Richiesta**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Risposta**

Un batch completato correttamente restituisce un corpo di risposta vuoto e lo stato HTTP 200 (OK).

## Caricamento del monitor

A seconda delle dimensioni dei dati, il caricamento dei batch richiede tempi diversi. Potete monitorare lo stato di un batch aggiungendo a una `batch` richiesta un parametro di `GET /batches` richiesta contenente l’ID del batch. L&#39;API controlla il set di dati per lo stato del batch dall&#39;assimilazione fino a quando `status` nella risposta non viene indicato completamento (&quot;success&quot; o &quot;failure&quot;).

**Formato API**

```HTTP
GET /batches?batch={BATCH_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{BATCH_ID}` | Indica `id` il batch da monitorare. |

**Richiesta**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Risposta**

Una risposta positiva restituisce un oggetto con il relativo `status` attributo contenente il valore di `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

Una risposta negativa restituisce un oggetto con il valore di `"failed"` nel relativo `"status"` attributo e include eventuali messaggi di errore rilevanti:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{IMS_ORG}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE]
>
>Un intervallo di polling consigliato è di due minuti.

## Leggere i dati dal dataset

Con l’ID batch, potete utilizzare l’API di accesso ai dati per la lettura e la verifica di tutti i file caricati nel batch. La risposta restituisce un array contenente un elenco di ID file, ciascuno dei quali fa riferimento a un file nel batch.

È inoltre possibile utilizzare l&#39;API di accesso ai dati per restituire il nome, la dimensione in byte e un collegamento per scaricare il file o la cartella.

I passaggi dettagliati per l&#39;utilizzo dell&#39;API Data Access sono disponibili nella guida [per gli sviluppatori](../../data-access/home.md)Data Access.

## Aggiornare lo schema del set di dati

È possibile aggiungere campi e inserire dati aggiuntivi nei set di dati creati. A questo scopo, è innanzitutto necessario aggiornare lo schema aggiungendo proprietà aggiuntive che definiscono i nuovi dati. Questo può essere fatto utilizzando le operazioni PATCH e/o PUT per aggiornare lo schema esistente.

Per ulteriori informazioni sull&#39;aggiornamento degli schemi, vedere la [Schema Registry API Developer Guide](../../xdm/api/getting-started.md).

Una volta aggiornato lo schema, è possibile seguire nuovamente i passaggi di questa esercitazione per acquisire nuovi dati conformi allo schema modificato.

È importante ricordare che l&#39;evoluzione dello schema è puramente additiva, il che significa che non è possibile introdurre una modifica di interruzione a uno schema una volta che è stato salvato nel Registro di sistema e utilizzato per l&#39;inserimento dei dati. Per ulteriori informazioni sulle procedure ottimali per la composizione dello schema da utilizzare con  Adobe Experience Platform, vedere la guida sulle [nozioni di base della composizione](../../xdm/schema/composition.md)dello schema.