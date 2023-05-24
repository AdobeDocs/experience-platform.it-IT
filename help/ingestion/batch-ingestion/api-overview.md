---
keywords: Experience Platform;home;argomenti popolari;inserimento batch;inserimento batch;inserimento batch;inserimento;guida per sviluppatori;guida API;caricamento;acquisizione Parquet;acquisizione json;
solution: Experience Platform
title: Guida all’API per l’acquisizione in batch
description: Questo documento fornisce una guida completa per gli sviluppatori che lavorano con le API di acquisizione batch per Adobe Experience Platform.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 5%

---

# Guida per gli sviluppatori sull’acquisizione in batch

Questo documento fornisce una guida completa all’utilizzo di [endpoint API per acquisizione batch](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) in Adobe Experience Platform. Per una panoramica delle API di acquisizione batch, inclusi i prerequisiti e le best practice, leggi [panoramica dell’API per l’acquisizione batch](overview.md).

L&#39;appendice del presente documento fornisce informazioni per [formattazione dei dati da utilizzare per l’acquisizione](#data-transformation-for-batch-ingestion), inclusi file di dati CSV e JSON di esempio.

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte del [API di acquisizione in batch](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). L’acquisizione in batch viene fornita tramite un’API RESTful in cui puoi eseguire operazioni CRUD di base sui tipi di oggetto supportati.

Prima di continuare, controlla [panoramica dell’API per l’acquisizione batch](overview.md) e [guida introduttiva](getting-started.md).

## Acquisire file JSON

>[!NOTE]
>
>I seguenti passaggi sono applicabili ai file di piccole dimensioni (256 MB o meno). Se si riscontra un timeout del gateway o si richiedono errori di dimensioni del corpo, è necessario passare al caricamento di file di grandi dimensioni.

### Crea batch

Innanzitutto, devi creare un batch, con JSON come formato di input. Durante la creazione del batch, dovrai fornire un ID set di dati. È inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito.

>[!NOTE]
>
>Gli esempi seguenti sono per JSON a riga singola. Per acquisire JSON su più righe, `isMultiLineJson` sarà necessario impostare il flag. Per ulteriori informazioni, leggere [guida alla risoluzione dei problemi di acquisizione batch](./troubleshooting.md).

**Formato API**

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID del set di dati di riferimento. |

**Risposta**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch appena creato. |
| `{DATASET_ID}` | ID del set di dati di riferimento. |

### Carica file

Dopo aver creato un batch, puoi utilizzare l’ID batch dalla risposta di creazione del batch per caricare i file nel batch. Puoi caricare più file nel batch.

>[!NOTE]
>
>Vedere la sezione dell&#39;appendice per un [esempio di file di dati JSON formattato correttamente](#data-transformation-for-batch-ingestion).

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Assicurati di utilizzare un nome file univoco in modo che non si scontri con un altro file per il batch di file da inviare. |

**Richiesta**

>[!NOTE]
>
>L’API supporta il caricamento in una sola parte. Assicurati che il tipo di contenuto sia application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che stai tentando di caricare. Questo è il percorso del file locale, ad esempio `acme/customers/campaigns/summer.json`. |

**Risposta**

```http
200 OK
```

### Batch completo

Una volta completato il caricamento di tutte le diverse parti del file, dovrai segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |

**Richiesta**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```http
200 OK
```

## Acquisire file Parquet {#ingest-parquet-files}

>[!NOTE]
>
>I seguenti passaggi sono applicabili ai file di piccole dimensioni (256 MB o meno). Se si riscontra un timeout del gateway o si richiedono errori di dimensioni del corpo, sarà necessario passare al caricamento di file di grandi dimensioni.

### Crea batch

In primo luogo, è necessario creare un batch, con Parquet come formato di input. Durante la creazione del batch, dovrai fornire un ID set di dati. È inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito.

**Richiesta**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| Parametro | Descrizione |
| --------- | ------------ |
| `{DATASET_ID}` | ID del set di dati di riferimento. |

**Risposta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch appena creato. |
| `{DATASET_ID}` | ID del set di dati di riferimento. |
| `{USER_ID}` | ID dell’utente che ha creato il batch. |

### Carica file

Dopo aver creato un batch, puoi utilizzare `batchId` da prima di per caricare i file nel batch. Puoi caricare più file nel batch.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Assicurati di utilizzare un nome file univoco in modo che non si scontri con un altro file per il batch di file da inviare. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento in una sola parte. Assicurati che il tipo di contenuto sia application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che stai tentando di caricare. Questo è il percorso del file locale, ad esempio `acme/customers/campaigns/summer.parquet`. |

**Risposta**

```http
200 OK
```

### Batch completo

Una volta completato il caricamento di tutte le diverse parti del file, dovrai segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L’ID del batch che desideri segnalare è pronto per il completamento. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
200 OK
```

## Acquisire file Parquet di grandi dimensioni

>[!NOTE]
>
>Questa sezione descrive come caricare file di dimensioni superiori a 256 MB. I file di grandi dimensioni vengono caricati in blocchi e quindi uniti tramite un segnale API.

### Crea batch

In primo luogo, è necessario creare un batch, con Parquet come formato di input. Durante la creazione del batch, dovrai fornire un ID set di dati. È inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito.

**Formato API**

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID del set di dati di riferimento. |

**Risposta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch appena creato. |
| `{DATASET_ID}` | ID del set di dati di riferimento. |
| `{USER_ID}` | ID dell’utente che ha creato il batch. |

### Inizializza file di grandi dimensioni

Dopo aver creato il batch, sarà necessario inizializzare il file di grandi dimensioni prima di caricare i blocchi nel batch.

**Formato API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch appena creato. |
| `{DATASET_ID}` | ID del set di dati di riferimento. |
| `{FILE_NAME}` | Nome del file che sta per essere inizializzato. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
201 Created
```

### Carica blocchi di file di grandi dimensioni

Una volta creato il file, è possibile caricarne tutti i blocchi successivi effettuando ripetute richieste PATCH, una per ogni sezione del file.

**Formato API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Assicurati di utilizzare un nome file univoco in modo che non si scontri con un altro file per il batch di file da inviare. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento in una sola parte. Assicurati che il tipo di contenuto sia application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONTENT_RANGE}` | In numeri interi, l’inizio e la fine dell’intervallo richiesto. |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che stai tentando di caricare. Questo è il percorso del file locale, ad esempio `acme/customers/campaigns/summer.json`. |


**Risposta**

```http
200 OK
```

### Completa file di grandi dimensioni

Dopo aver creato un batch, puoi utilizzare `batchId` da prima di per caricare i file nel batch. Puoi caricare più file nel batch.

**Formato API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch di cui desideri segnalare il completamento. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file di cui si desidera segnalare il completamento. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
201 Created
```

### Batch completo

Una volta completato il caricamento di tutte le diverse parti del file, dovrai segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L’ID del batch che desideri segnalare è completo. |


**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
200 OK
```

## Acquisire file CSV

Per acquisire i file CSV, devi creare una classe, uno schema e un set di dati che supporti CSV. Per informazioni dettagliate su come creare la classe e lo schema necessari, segui le istruzioni fornite nella [tutorial sulla creazione di schemi ad hoc](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>I seguenti passaggi sono applicabili ai file di piccole dimensioni (256 MB o meno). Se si riscontra un timeout del gateway o si richiedono errori di dimensioni del corpo, sarà necessario passare al caricamento di file di grandi dimensioni.

### Creare un set di dati

Dopo aver seguito le istruzioni precedenti per creare la classe e lo schema necessari, dovrai creare un set di dati che possa supportare CSV.

**Formato API**

```http
POST /catalog/dataSets
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TENANT_ID}` | Questo ID viene utilizzato per garantire che le risorse create abbiano uno spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. |
| `{SCHEMA_ID}` | ID dello schema creato. |

### Crea batch

Successivamente, dovrai creare un batch con CSV come formato di input. Durante la creazione del batch, dovrai fornire un ID set di dati. È inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema collegato al set di dati fornito.

**Formato API**

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID del set di dati di riferimento. |

**Risposta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch appena creato. |
| `{DATASET_ID}` | ID del set di dati di riferimento. |
| `{USER_ID}` | ID dell’utente che ha creato il batch. |

### Carica file

Dopo aver creato un batch, puoi utilizzare `batchId` da prima di per caricare i file nel batch. Puoi caricare più file nel batch.

>[!NOTE]
>
>Vedere la sezione dell&#39;appendice per un [esempio di file di dati CSV formattato correttamente](#data-transformation-for-batch-ingestion).

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Assicurati di utilizzare un nome file univoco in modo che non si scontri con un altro file per il batch di file da inviare. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento in una sola parte. Assicurati che il tipo di contenuto sia application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che stai tentando di caricare. Questo è il percorso del file locale, ad esempio `acme/customers/campaigns/summer.csv`. |


**Risposta**

```http
200 OK
```

### Batch completo

Una volta completato il caricamento di tutte le diverse parti del file, dovrai segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```http
200 OK
```

## Annullare un batch

Durante l’elaborazione, il batch può comunque essere annullato. Tuttavia, una volta finalizzato un batch (ad esempio in caso di esito positivo o negativo), il batch non può essere annullato.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch da annullare. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
200 OK
```

## Eliminare un batch {#delete-a-batch}

È possibile eliminare un batch eseguendo la seguente richiesta POST con `action=REVERT` parametro di query per l’ID del batch da eliminare. Il batch è contrassegnato come &quot;inattivo&quot;, rendendolo idoneo per la raccolta di oggetti inattivi. Il batch verrà raccolto in modo asincrono e contrassegnato come &quot;eliminato&quot;.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch da eliminare. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
200 OK
```

## Applicazione di patch a un batch

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Adobe Experience Platform supporta l’aggiornamento o la patch dei dati dell’archivio profili tramite un’azione upsert o &quot;l’applicazione di patch a un batch&quot;.

>[!NOTE]
>
>Questi aggiornamenti sono consentiti solo sui record di profilo, non sugli eventi di esperienza.

Per applicare la patch a un batch è necessario quanto segue:

- **Un set di dati abilitato per gli aggiornamenti di profili e attributi.** Questa operazione viene eseguita tramite tag di set di dati e richiede un `isUpsert:true` aggiunta al tag `unifiedProfile` array. Per i passaggi dettagliati che mostrano come creare un set di dati o configurare un set di dati esistente per l’upsert, segui l’esercitazione per [abilitazione di un set di dati per gli aggiornamenti del profilo](../../catalog/datasets/enable-upsert.md).
- **Un file Parquet contenente i campi di cui applicare la patch e i campi di identità per il profilo.** Il formato dei dati per l’applicazione di patch a un batch è simile al normale processo di acquisizione batch. L’input richiesto è un file Parquet e, oltre ai campi da aggiornare, i dati caricati devono contenere i campi di identità in modo che corrispondano ai dati nell’archivio profili.

Dopo aver abilitato un set di dati per Profilo e upsert e un file Parquet contenente i campi a cui desideri applicare la patch e i campi di identità necessari, puoi seguire i passaggi per [acquisizione dei file Parquet](#ingest-parquet-files) al fine di completare la patch tramite l’acquisizione in batch.

## Ripetere un batch

Se desideri sostituire un batch già acquisito, puoi farlo con &quot;ripetizione batch&quot;: questa azione equivale all’eliminazione del batch precedente e all’acquisizione di un nuovo batch.

### Crea batch

Innanzitutto, devi creare un batch, con JSON come formato di input. Durante la creazione del batch, dovrai fornire un ID set di dati. È inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito. Inoltre, devi fornire i vecchi batch come riferimento nella sezione di ripetizione. Nell’esempio seguente, stai riproducendo i batch con ID `batchIdA` e `batchIdB`.

**Formato API**

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| Parametro | Descrizione |
| --------- | ----------- | 
| `{DATASET_ID}` | ID del set di dati di riferimento. |

**Risposta**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch appena creato. |
| `{DATASET_ID}` | ID del set di dati di riferimento. |
| `{USER_ID}` | ID dell’utente che ha creato il batch. |


### Carica file

Dopo aver creato un batch, puoi utilizzare `batchId` da prima di per caricare i file nel batch. Puoi caricare più file nel batch.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Assicurati di utilizzare un nome file univoco in modo che non si scontri con un altro file per il batch di file da inviare. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento in una sola parte. Assicurati che il tipo di contenuto sia application/octet-stream. Non utilizzare l’opzione curl -F, poiché per impostazione predefinita le richieste in più parti sono incompatibili con l’API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che stai tentando di caricare. Questo è il percorso del file locale, ad esempio `acme/customers/campaigns/summer.json`. |

**Risposta**

```http
200 OK
```

### Batch completo

Una volta completato il caricamento di tutte le diverse parti del file, dovrai segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch da completare. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```http
200 OK
```

## Appendice

La sezione seguente contiene informazioni aggiuntive per l’acquisizione di dati in Experience Platform tramite l’acquisizione batch.

### Trasformazione dei dati per l’acquisizione batch

Per acquisire un file di dati in [!DNL Experience Platform], la struttura gerarchica del file deve essere conforme alla [Experience Data Model (XDM)](../../xdm/home.md) schema associato al set di dati in fase di caricamento in.

Le informazioni su come mappare un file CSV in modo che sia conforme a uno schema XDM sono disponibili nella sezione [trasformazioni campione](../../etl/transformations.md) insieme a un esempio di un file di dati JSON formattato correttamente. I file di esempio forniti nel documento sono disponibili qui:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
