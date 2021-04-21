---
keywords: Experience Platform;home;argomenti popolari;inserimento batch;inserimento batch;acquisizione;guida per sviluppatori;guida per gli sviluppatori;api;caricare;acquisire parquet;ingest json;
solution: Experience Platform
title: Guida all’API di acquisizione in batch
topic-legacy: developer guide
description: Questo documento fornisce una panoramica completa dell’utilizzo delle API di acquisizione batch.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 6%

---

# Guida all’API per l’acquisizione in batch

Questo documento fornisce una panoramica completa sull’utilizzo delle API di acquisizione batch [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

L&#39;appendice di questo documento fornisce informazioni per la [formattazione dei dati da utilizzare per l&#39;acquisizione](#data-transformation-for-batch-ingestion), inclusi file di dati CSV e JSON di esempio.

## Introduzione

L’acquisizione dei dati fornisce un’API RESTful tramite la quale puoi eseguire operazioni CRUD di base sui tipi di oggetto supportati.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere o disporre di disponibilità per effettuare correttamente le chiamate all’API di acquisizione in batch.

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Acquisizione](./overview.md) batch: Consente di acquisire dati in Adobe Experience Platform come file batch.
- [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
- [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Le richieste che contengono un payload (POST, PUT, PATCH) possono richiedere un’intestazione aggiuntiva `Content-Type`. I valori accettati specifici per ogni chiamata sono forniti nei parametri della chiamata .

## Tipi

Durante l’acquisizione dei dati, è importante comprendere il funzionamento degli schemi [!DNL Experience Data Model] (XDM). Per ulteriori informazioni sulla mappatura dei tipi di campo XDM su formati diversi, consulta la [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md).

È possibile acquisire i dati in modo flessibile: se un tipo non corrisponde a quello presente nello schema di destinazione, i dati verranno convertiti nel tipo di destinazione espresso. Se non è in grado di farlo, il batch non verrà completato con un valore `TypeCompatibilityException`.

Ad esempio, né JSON né CSV hanno un tipo di data o ora. Di conseguenza, questi valori vengono espressi utilizzando [ISO 8061 stringhe formattate](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) o Unix Time formattato in millisecondi (15312639 59000) e vengono convertiti al momento dell’acquisizione al tipo XDM di destinazione.

La tabella seguente mostra le conversioni supportate durante l’acquisizione dei dati.

| In entrata (riga) rispetto a Target (col) | Stringa | Byte | Breve | Intero | Lunga | Doppio | Data | Data e ora | Oggetto | Mappa |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Stringa | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Breve | X | X | X | X | X | X |  |  |  |  |
| Intero | X | X | X | X | X | X |  |  |  |  |
| Lunga | X | X | X | X | X | X | X | X |  |  |
| Doppio | X | X | X | X | X | X |  |  |  |  |
| Data |  |  |  |  |  |  | X |  |  |  |
| Data e ora |  |  |  |  |  |  |  | X |  |  |
| Oggetto |  |  |  |  |  |  |  |  | X | X |
| Mappa |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>I booleani e gli array non possono essere convertiti in altri tipi.

## Vincoli di acquisizione

L’inserimento dei dati in batch presenta alcuni vincoli:
- Numero massimo di file per batch: 1500
- Dimensione massima del batch: 100 GB
- Numero massimo di proprietà o campi per riga: 10000
- Numero massimo di batch al minuto per utente: 138

## Inserire file JSON

>[!NOTE]
>
>I seguenti passaggi sono applicabili per i file di piccole dimensioni (256 MB o inferiore). Se si verifica un timeout del gateway o si verificano errori di dimensioni del corpo della richiesta, è necessario passare al caricamento di file di grandi dimensioni.

### Crea batch

Innanzitutto, devi creare un batch, con JSON come formato di input. Quando crei il batch, dovrai fornire un ID set di dati. Sarà inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito.

>[!NOTE]
>
>Gli esempi seguenti sono per JSON a riga singola. Per acquisire JSON con più righe, è necessario impostare il flag `isMultiLineJson` . Per ulteriori informazioni, consulta la [guida alla risoluzione dei problemi di inserimento batch](./troubleshooting.md).

**Formato API**

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | ID del set di dati a cui si fa riferimento. |

### Caricare file

Dopo aver creato un batch, puoi utilizzare `batchId` da prima per caricare i file nel batch. Puoi caricare più file nel batch.

>[!NOTE]
>
>Vedi la sezione dell&#39;appendice per un [esempio di un file di dati JSON formattato correttamente](#data-transformation-for-batch-ingestion).

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Questo percorso del file è il percorso in cui il file verrà salvato sul lato Adobe. |

**Richiesta**

>[!NOTE]
>
>L’API supporta il caricamento in singola parte. Assicurati che il tipo di contenuto sia application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. Questo percorso del file è il percorso del file locale, ad esempio `Users/sample-user/Downloads/sample.json`. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```http
200 OK
```

## Inserire file di parquet

>[!NOTE]
>
>I seguenti passaggi sono applicabili per i file di piccole dimensioni (256 MB o inferiore). Se raggiungi un timeout del gateway o richiedi errori di dimensione del corpo, dovrai passare al caricamento di file di grandi dimensioni.

### Crea batch

In primo luogo, sarà necessario creare un batch, con Parquet come formato di input. Quando crei il batch, dovrai fornire un ID set di dati. Sarà inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito.

**Richiesta**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
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
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | ID del set di dati a cui si fa riferimento. |
| `{USER_ID}` | ID dell&#39;utente che ha creato il batch. |

### Caricare file

Dopo aver creato un batch, puoi utilizzare `batchId` da prima per caricare i file nel batch. Puoi caricare più file nel batch.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Questo percorso del file è il percorso in cui il file verrà salvato sul lato Adobe. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento in singola parte. Assicurati che il tipo di contenuto sia application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. Questo percorso del file è il percorso del file locale, ad esempio `Users/sample-user/Downloads/sample.json`. |

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
| `{BATCH_ID}` | L&#39;ID del batch da segnalare è pronto per il completamento. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
200 OK
```

## Inserire file Parquet di grandi dimensioni

>[!NOTE]
>
>Questa sezione descrive come caricare file di dimensioni superiori a 256 MB. I file di grandi dimensioni vengono caricati in blocchi e quindi uniti tramite un segnale API.

### Crea batch

In primo luogo, sarà necessario creare un batch, con Parquet come formato di input. Quando crei il batch, dovrai fornire un ID set di dati. Sarà inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito.

**Formato API**

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | ID del set di dati a cui si fa riferimento. |
| `{USER_ID}` | ID dell&#39;utente che ha creato il batch. |

### Inizializza file di grandi dimensioni

Dopo aver creato il batch, sarà necessario inizializzare il file di grandi dimensioni prima di caricare i blocchi nel batch.

**Formato API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch appena creato. |
| `{DATASET_ID}` | ID del set di dati a cui si fa riferimento. |
| `{FILE_NAME}` | Nome del file che sta per essere inizializzato. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
201 Created
```

### Caricare blocchi di file di grandi dimensioni

Dopo la creazione del file, è possibile caricare tutti i blocchi successivi effettuando richieste PATCH ripetute, una per ogni sezione del file.

**Formato API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Questo percorso del file è il percorso in cui il file verrà salvato sul lato Adobe. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento in singola parte. Assicurati che il tipo di contenuto sia application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONTENT_RANGE}` | In numeri interi, l’inizio e la fine dell’intervallo richiesto. |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. Questo percorso del file è il percorso del file locale, ad esempio `Users/sample-user/Downloads/sample.json`. |


**Risposta**

```http
200 OK
```

### File di grandi dimensioni completi

Dopo aver creato un batch, puoi utilizzare `batchId` da prima per caricare i file nel batch. Puoi caricare più file nel batch.

**Formato API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch di cui si desidera segnalare il completamento. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file di cui si desidera segnalare il completamento. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{BATCH_ID}` | L&#39;ID del batch da segnalare è completo. |


**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
200 OK
```

## Inserire file CSV

Per acquisire file CSV, dovrai creare una classe, uno schema e un set di dati che supporti CSV. Per informazioni dettagliate su come creare la classe e lo schema necessari, segui le istruzioni fornite nell&#39; [tutorial per la creazione di schemi ad hoc](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>I seguenti passaggi sono applicabili per i file di piccole dimensioni (256 MB o inferiore). Se raggiungi un timeout del gateway o richiedi errori di dimensione del corpo, dovrai passare al caricamento di file di grandi dimensioni.

### Creare un set di dati

Dopo aver seguito le istruzioni riportate sopra per creare la classe e lo schema necessari, dovrai creare un set di dati che supporti CSV.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{TENANT_ID}` | Questo ID viene utilizzato per garantire che le risorse create siano spaccate correttamente e contenute all’interno dell’organizzazione IMS. |
| `{SCHEMA_ID}` | ID dello schema creato. |

### Crea batch

Successivamente, dovrai creare un batch con CSV come formato di input. Quando crei il batch, dovrai fornire un ID set di dati. Inoltre, dovrai accertarti che tutti i file caricati come parte del batch siano conformi allo schema collegato al set di dati fornito.

**Formato API**

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | ID del set di dati a cui si fa riferimento. |
| `{USER_ID}` | ID dell&#39;utente che ha creato il batch. |

### Caricare file

Dopo aver creato un batch, puoi utilizzare `batchId` da prima per caricare i file nel batch. Puoi caricare più file nel batch.

>[!NOTE]
>
>Vedi la sezione dell&#39;appendice per un [esempio di un file di dati CSV formattato correttamente](#data-transformation-for-batch-ingestion).

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Questo percorso del file è il percorso in cui il file verrà salvato sul lato Adobe. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento in singola parte. Assicurati che il tipo di contenuto sia application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. Questo percorso del file è il percorso del file locale, ad esempio `Users/sample-user/Downloads/sample.json`. |


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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```http
200 OK
```

## Annullare un batch

Durante l&#39;elaborazione del batch, può comunque essere annullato. Tuttavia, una volta finalizzato un batch (ad esempio uno stato riuscito o non riuscito), il batch non può essere annullato.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
200 OK
```

## Eliminare un batch {#delete-a-batch}

È possibile eliminare un batch eseguendo la seguente richiesta POST con il parametro di query `action=REVERT` all’ID del batch da eliminare. Il batch è contrassegnato come &quot;inattivo&quot;, rendendolo idoneo per la raccolta degli oggetti inattivi. Il batch verrà raccolto in modo asincrono, in cui verrà contrassegnato come &quot;eliminato&quot;.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
200 OK
```

## Riproduci un batch

Se si desidera sostituire un batch già acquisito, è possibile farlo con &quot;riproduzione batch&quot;: questa azione equivale all’eliminazione del batch precedente e all’acquisizione di un nuovo batch.

### Crea batch

Innanzitutto, devi creare un batch, con JSON come formato di input. Quando crei il batch, dovrai fornire un ID set di dati. Sarà inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito. Inoltre, sarà necessario fornire i vecchi batch come riferimento nella sezione di ripetizione. Nell’esempio seguente, riproduci batch con ID `batchIdA` e `batchIdB`.

**Formato API**

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | ID del set di dati a cui si fa riferimento. |
| `{USER_ID}` | ID dell&#39;utente che ha creato il batch. |


### Caricare file

Dopo aver creato un batch, puoi utilizzare `batchId` da prima per caricare i file nel batch. Puoi caricare più file nel batch.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch in cui desideri caricare. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. Questo percorso del file è il percorso in cui il file verrà salvato sul lato Adobe. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento in singola parte. Assicurati che il tipo di contenuto sia application/octet-stream. Non utilizzare l’opzione curl -F, in quanto per impostazione predefinita viene richiesta in più parti incompatibile con l’API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. Questo percorso del file è il percorso del file locale, ad esempio `Users/sample-user/Downloads/sample.json`. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```http
200 OK
```

## Appendice

### Trasformazione dei dati per l’acquisizione batch

Per acquisire un file di dati in [!DNL Experience Platform], la struttura gerarchica del file deve essere conforme allo schema [Experience Data Model (XDM)](../../xdm/home.md) associato al set di dati a cui si sta caricando.

Le informazioni su come mappare un file CSV per conformarsi a uno schema XDM si trovano nel documento [trasformazioni di esempio](../../etl/transformations.md), insieme a un esempio di file di dati JSON formattato correttamente. I file di esempio forniti nel documento sono disponibili qui:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
