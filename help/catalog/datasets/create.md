---
keywords: Experience Platform;home;argomenti comuni;set di dati;set di dati;creare un set di dati;home;popular topic;dataset;Dataset;create a dataset;create dataset
solution: Experience Platform
title: Creare un set di dati utilizzando le API
description: Questo documento descrive i passaggi generali per la creazione di un set di dati utilizzando le API di Adobe Experience Platform e per il popolamento del set di dati utilizzando un file.
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: e2f16f532b98e6948ffd7f331e630137b3972f0f
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 7%

---

# Creare un set di dati utilizzando le API

Questo documento descrive i passaggi generali per la creazione di un set di dati utilizzando le API di Adobe Experience Platform e per il popolamento del set di dati utilizzando un file.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Acquisizione batch](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] consente di acquisire dati come file batch.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate alle API [!DNL Platform].

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione `Content-Type: application/json` aggiuntiva. Per le richieste JSON+PATCH, `Content-Type` deve essere `application/json-patch+json`.

## Tutorial

Per creare un set di dati, è necessario prima definire uno schema. Uno schema è un insieme di regole che facilitano la rappresentazione dei dati. Oltre a descrivere la struttura dei dati, gli schemi forniscono vincoli e aspettative che possono essere applicati e utilizzati per convalidare i dati durante lo spostamento tra sistemi diversi.

Queste definizioni standard consentono di interpretare i dati in modo coerente, indipendentemente dall’origine, ed eliminano la necessità di traduzione tra le applicazioni. Per ulteriori informazioni sulla composizione degli schemi, consulta la guida sulle [nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md)

## Cercare uno schema di set di dati

Questa esercitazione inizia nel punto in cui termina l&#39;esercitazione [Schema Registry API](../../xdm/tutorials/create-schema-api.md), utilizzando lo schema Membri fedeltà creato durante l&#39;esercitazione.

Se non hai completato l&#39;esercitazione di [!DNL Schema Registry], inizia da lì e continua con questa esercitazione sul set di dati solo dopo aver composto lo schema necessario.

La chiamata seguente può essere utilizzata per visualizzare lo schema Membri fedeltà creato durante l&#39;esercitazione API [!DNL Schema Registry]:

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Il formato dell’oggetto di risposta dipende dall’intestazione Accept inviata nella richiesta. Le singole proprietà di questa risposta sono state ridotte a icona per motivi di spazio.

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
    "imsOrg": "{ORG_ID}",
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

## Creare un set di dati

Con lo schema Membri fedeltà attivo, ora puoi creare un set di dati che fa riferimento allo schema.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `schemaRef.id` | Il valore URI `$id` per lo schema XDM su cui sarà basato il set di dati. |
| `schemaRef.contentType` | Indica il formato e la versione dello schema. Per ulteriori informazioni, consulta la sezione sul controllo delle versioni dello schema [1} nella guida dell&#39;API XDM.](../../xdm/api/getting-started.md#versioning) |

>[!NOTE]
>
>Questa esercitazione utilizza il formato di file [Apache Parquet](https://parquet.apache.org/docs/) per tutti i relativi esempi. Un esempio che utilizza il formato di file JSON è disponibile nella [guida per gli sviluppatori sull&#39;acquisizione batch](../../ingestion/batch-ingestion/api-overview.md)

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e un oggetto di risposta costituito da un array contenente l’ID del set di dati appena creato in formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema e utilizzata per fare riferimento al set di dati nelle chiamate API.

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

Il corpo della richiesta include un campo &quot;datasetId&quot; il cui valore è `{DATASET_ID}` generato nel passaggio precedente.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e un oggetto di risposta. L&#39;oggetto di risposta è costituito da un array contenente l&#39;ID del batch appena creato nel formato `"@/batches/{BATCH_ID}"`. L’ID batch è una stringa di sola lettura generata dal sistema e utilizzata per fare riferimento al batch nelle chiamate API.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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

## Carica file in un batch

Dopo aver creato correttamente un nuovo batch per il caricamento, ora puoi caricare i file nel set di dati specifico. È importante ricordare che quando hai definito il set di dati, hai specificato il formato di file come Parquet. Pertanto, i file caricati devono essere in tale formato.

>[!NOTE]
>
>Il file di caricamento dati più grande supportato è 512 MB. Se il file di dati è più grande di questo, deve essere suddiviso in blocchi non più grandi di 512 MB, per essere caricato uno alla volta. Puoi caricare ogni file nello stesso batch ripetendo questo passaggio per ogni file, utilizzando lo stesso ID batch. Non esiste alcun limite al numero di file che è possibile caricare come parte di un batch.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{BATCH_ID}` | `id` del batch in cui si sta caricando. |
| `{DATASET_ID}` | `id` del set di dati in cui verrà mantenuto il batch. |
| `{FILE_NAME}` | Nome del file che stai caricando. |

**Richiesta**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Risposta**

Un file caricato correttamente restituisce un corpo di risposta vuoto e lo stato HTTP 200 (OK).

## Completamento batch segnale

Dopo aver caricato tutti i file di dati nel batch, puoi segnalare il completamento del batch. Il completamento della segnalazione fa sì che il servizio crei [!DNL Catalog] voci `DataSetFile` per i file caricati e le associ al batch generato in precedenza. Il batch [!DNL Catalog] è contrassegnato come riuscito, il che attiva tutti i flussi a valle che possono quindi funzionare sui dati ora disponibili.

**Formato API**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parametro | Descrizione |
| --- | --- |
| `{BATCH_ID}` | `id` del batch contrassegnato come completato. |

**Richiesta**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Risposta**

Un batch completato correttamente restituisce un corpo di risposta vuoto e lo stato HTTP 200 (OK).

## Monitorare l’acquisizione

A seconda delle dimensioni dei dati, l’acquisizione dei batch richiede tempi diversi. È possibile monitorare lo stato di un batch aggiungendo l&#39;ID di un batch a una richiesta `GET /batches`.

**Formato API**

```HTTP
GET /batches/{BATCH_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{BATCH_ID}` | `id` del batch che si desidera monitorare. |

**Richiesta**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Risposta**

Una risposta positiva restituisce un oggetto con il relativo attributo `status` contenente il valore di `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{ORG_ID}",
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

Una risposta negativa restituisce un oggetto con il valore di `"failed"` nel relativo attributo `"status"` e include tutti i messaggi di errore rilevanti:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{ORG_ID}",
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

## Leggi dati dal set di dati

Con l’ID batch, puoi utilizzare l’API di accesso ai dati per rileggere e verificare tutti i file caricati nel batch. La risposta restituisce un array contenente un elenco di ID file, ciascuno dei quali fa riferimento a un file nel batch.

È inoltre possibile utilizzare l&#39;API di accesso ai dati per restituire il nome, la dimensione in byte e un collegamento per scaricare il file o la cartella.

I passaggi dettagliati per l&#39;utilizzo dell&#39;API di accesso ai dati sono disponibili nella [Guida per gli sviluppatori di Accesso ai dati](../../data-access/home.md).

## Aggiornare lo schema del set di dati

Puoi aggiungere campi e acquisire dati aggiuntivi nei set di dati creati. A questo scopo, devi innanzitutto aggiornare lo schema aggiungendo ulteriori proprietà che definiscono i nuovi dati. Questa operazione può essere eseguita utilizzando operazioni PATCH e/o PUT per aggiornare lo schema esistente.

Per ulteriori informazioni sull&#39;aggiornamento degli schemi, vedere la [Guida per gli sviluppatori API del registro degli schemi](../../xdm/api/getting-started.md).

Dopo aver aggiornato lo schema, puoi seguire nuovamente i passaggi descritti in questo tutorial per acquisire nuovi dati conformi allo schema rivisto.

È importante ricordare che l’evoluzione dello schema è puramente additiva, il che significa che non è possibile introdurre una modifica che interrompa uno schema dopo che è stato salvato nel registro e utilizzato per l’acquisizione dei dati. Per ulteriori informazioni sulle best practice per la composizione di schemi da utilizzare con Adobe Experience Platform, consulta la guida sulle [nozioni di base sulla composizione di schemi](../../xdm/schema/composition.md).
