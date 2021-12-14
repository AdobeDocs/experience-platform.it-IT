---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;creare un set di dati;creare un set di dati
solution: Experience Platform
title: Creare un set di dati utilizzando le API
topic-legacy: datasets
description: Questo documento fornisce passaggi generali per la creazione di un set di dati utilizzando le API di Adobe Experience Platform e la compilazione del set di dati utilizzando un file .
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 2%

---

# Creare un set di dati utilizzando le API

Questo documento fornisce passaggi generali per la creazione di un set di dati utilizzando le API di Adobe Experience Platform e la compilazione del set di dati utilizzando un file .

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Acquisizione batch](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] consente di acquisire i dati come file batch.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate al [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* Tipo di contenuto: application/json

## Tutorial

Per creare un set di dati, è innanzitutto necessario definire uno schema. Uno schema è un insieme di regole che facilitano la rappresentazione dei dati. Oltre a descrivere la struttura dei dati, gli schemi forniscono vincoli e aspettative che possono essere applicati e utilizzati per convalidare i dati mentre vengono spostati tra i sistemi.

Queste definizioni standard consentono l’interpretazione coerente dei dati, indipendentemente dall’origine, e rimuovono la necessità di tradurre tra le applicazioni. Per ulteriori informazioni sulla composizione degli schemi, consulta la guida nella sezione [nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md)

## Cercare uno schema di set di dati

Questa esercitazione inizia dove [Esercitazione API del Registro di sistema dello schema](../../xdm/tutorials/create-schema-api.md) termina, utilizzando lo schema Membri fedeltà creato durante l&#39;esercitazione.

Se non hai completato il [!DNL Schema Registry] esercitazione, inizia da qui e continua con questa esercitazione sui set di dati solo dopo aver composto lo schema necessario.

La seguente chiamata può essere utilizzata per visualizzare lo schema Membri fedeltà creato durante il [!DNL Schema Registry] Esercitazione API:

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

Il formato dell’oggetto di risposta dipende dall’intestazione Accept inviata nella richiesta. Le singole proprietà in questa risposta sono state ridotte a icona per lo spazio.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `schemaRef.id` | URI `$id` valore per lo schema XDM su cui verrà basato il set di dati. |
| `schemaRef.contentType` | Indica il formato e la versione dello schema. Vedi la sezione su [versione dello schema](../../xdm/api/getting-started.md#versioning) nella guida API XDM per ulteriori informazioni. |

>[!NOTE]
>
>Questa esercitazione utilizza la funzione [Parquet Apache](https://parquet.apache.org/documentation/latest/) formato file per tutti i relativi esempi. Un esempio che utilizza il formato di file JSON si trova nella [guida per gli sviluppatori di batch ingestion](../../ingestion/batch-ingestion/api-overview.md)

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto di risposta costituito da un array contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto di risposta contenente i dettagli del batch appena creato, incluso il relativo `id`, una stringa generata dal sistema di sola lettura.

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

## Caricare file in un batch

Dopo aver creato correttamente un nuovo batch per il caricamento, ora puoi caricare i file nel set di dati specifico. È importante ricordare che quando hai definito il set di dati, hai specificato il formato di file come Parquet. Pertanto, i file caricati devono essere in quel formato.

>[!NOTE]
>
>Il file di caricamento dati più grande supportato è 512 MB. Se il file di dati è più grande di questo, deve essere suddiviso in blocchi non superiori a 512 MB, per essere caricato uno alla volta. Puoi caricare ogni file nello stesso batch ripetendo questo passaggio per ogni file, utilizzando lo stesso ID batch. Non c&#39;è alcun limite al numero se i file possono essere caricati come parte di un batch.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{BATCH_ID}` | La `id` del batch a cui si sta caricando. |
| `{DATASET_ID}` | La `id` del set di dati in cui il batch sarà mantenuto. |
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

## Completamento batch del segnale

Dopo aver caricato tutti i file di dati sul batch, puoi segnalare il batch per il completamento. Il completamento del segnale causa la creazione del servizio [!DNL Catalog] `DataSetFile` voci per i file caricati e associali al batch generato in precedenza. La [!DNL Catalog] batch è contrassegnato con successo, che attiva tutti i flussi a valle che possono quindi funzionare sui dati ora disponibili.

**Formato API**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parametro | Descrizione |
| --- | --- |
| `{BATCH_ID}` | La `id` del batch da contrassegnare come completo. |

**Richiesta**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Risposta**

Un batch completato correttamente restituisce un corpo di risposta vuoto e lo stato HTTP 200 (OK).

## Acquisizione monitor

A seconda delle dimensioni dei dati, il caricamento dei batch richiede diversi periodi di tempo. Puoi monitorare lo stato di un batch aggiungendo un `batch` richiede il parametro contenente l&#39;ID del batch a un `GET /batches` richiesta. L’API controlla il set di dati per lo stato del batch dall’acquisizione fino al `status` nella risposta indica il completamento (&quot;successo&quot; o &quot;errore&quot;).

**Formato API**

```HTTP
GET /batches?batch={BATCH_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{BATCH_ID}` | La `id` del batch da monitorare. |

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

Una risposta negativa restituisce un oggetto con il valore di `"failed"` nella sua `"status"` e include tutti i messaggi di errore pertinenti:

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

## Leggere i dati dal set di dati

Con l’ID batch, puoi utilizzare l’API di accesso ai dati per leggere e verificare tutti i file caricati nel batch. La risposta restituisce un array contenente un elenco di ID file, ciascuno contenente un riferimento a un file nel batch.

È inoltre possibile utilizzare l&#39;API di accesso ai dati per restituire il nome, la dimensione in byte e un collegamento per scaricare il file o la cartella.

I passaggi dettagliati per l’utilizzo dell’API di accesso ai dati sono disponibili nella sezione [Guida per gli sviluppatori di Data Access](../../data-access/home.md).

## Aggiornare lo schema del set di dati

Puoi aggiungere campi e inserire dati aggiuntivi nei set di dati creati. A questo scopo, devi prima aggiornare lo schema aggiungendo proprietà aggiuntive che definiscono i nuovi dati. È possibile eseguire questa operazione utilizzando le operazioni di PATCH e/o PUT per aggiornare lo schema esistente.

Per ulteriori informazioni sull’aggiornamento degli schemi, consulta la sezione [Guida per gli sviluppatori API del Registro di schema](../../xdm/api/getting-started.md).

Dopo aver aggiornato lo schema, puoi seguire nuovamente i passaggi descritti in questa esercitazione per acquisire nuovi dati conformi allo schema rivisto.

È importante tenere presente che l’evoluzione dello schema è puramente additiva, il che significa che non è possibile introdurre una modifica interrompente a uno schema una volta salvato nel Registro di sistema e utilizzato per l’inserimento dei dati. Per ulteriori informazioni sulle best practice per la composizione dello schema da utilizzare con Adobe Experience Platform, consulta la guida nella sezione [nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md).
