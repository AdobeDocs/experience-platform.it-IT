---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' Guida per lo sviluppatore Batch Ingestion'
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '2552'
ht-degree: 6%

---


# Guida per sviluppatori per l&#39;inserimento di batch

Questo documento fornisce una panoramica completa dell’utilizzo delle API di assimilazione [batch](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

L&#39;appendice di questo documento contiene informazioni sulla [formattazione dei dati da utilizzare per l&#39;assimilazione](#data-transformation-for-batch-ingestion), inclusi file di dati CSV e JSON di esempio.

## Introduzione

L&#39;assimilazione dei dati fornisce un&#39;API RESTful tramite la quale è possibile eseguire operazioni CRUD di base rispetto ai tipi di oggetto supportati.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o avere a disposizione per eseguire correttamente le chiamate all&#39;API di ingestione batch.

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

- [Caricamento](./overview.md)batch: Consente di assimilare i dati  Adobe Experience Platform come file batch.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
- [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Le richieste che contengono un payload (POST, PUT, PATCH) possono richiedere un&#39; `Content-Type` intestazione aggiuntiva. I valori accettati specifici per ogni chiamata vengono forniti nei parametri della chiamata. In questa guida vengono utilizzati i seguenti tipi di contenuto:

- Content-Type: application/json
- Content-Type: application/ottet-stream

## Tipi

Durante l&#39;assimilazione dei dati, è importante comprendere il funzionamento degli schemi [!DNL Experience Data Model] (XDM). Per ulteriori informazioni sulla mappatura dei tipi di campo XDM in formati diversi, consultare la guida [per gli sviluppatori del Registro di](../../xdm/api/getting-started.md)schema.

Durante l&#39;assimilazione dei dati vi è una certa flessibilità: se un tipo non corrisponde a quello presente nello schema di destinazione, i dati verranno convertiti nel tipo di destinazione espresso. In caso contrario, il batch non riuscirà con un `TypeCompatibilityException`.

Ad esempio, né JSON né CSV hanno un tipo data o ora. Di conseguenza, questi valori vengono espressi utilizzando stringhe [formattate](https://www.iso.org/iso-8601-date-and-time-format.html) ISO 8061 (&quot;2018-07-10T15:05:59.000-08:00&quot;) o Tempo Unix formattato in millisecondi (15312639590 00) e sono convertiti al momento dell&#39;assimilazione nel tipo XDM di destinazione.

La tabella seguente mostra le conversioni supportate durante l’assimilazione dei dati.

| In entrata (riga) e Target (col) | Stringa | Byte | Breve | Intero | Long | Doppio | Data | Data-Ora | Oggetto | Mappa |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Stringa | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Breve | X | X | X | X | X | X |  |  |  |  |
| Intero | X | X | X | X | X | X |  |  |  |  |
| Long | X | X | X | X | X | X | X | X |  |  |
| Doppio | X | X | X | X | X | X |  |  |  |  |
| Data |  |  |  |  |  |  | X |  |  |  |
| Data-Ora |  |  |  |  |  |  |  | X |  |  |
| Oggetto |  |  |  |  |  |  |  |  | X | X |
| Mappa |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>I booleani e gli array non possono essere convertiti in altri tipi.

## Limiti di inserimento

L&#39;assimilazione dei dati del batch presenta alcuni vincoli:
- Numero massimo di file per batch: 1500
- Dimensione massima batch: 100 GB
- Numero massimo di proprietà o campi per riga: 10000
- Numero massimo di batch per minuto, per utente: 138

## Caricamento di file JSON

>[!NOTE]
>
>Per i file di piccole dimensioni (256 MB o inferiore) sono applicabili i seguenti passaggi. Se si verificano errori relativi al timeout del gateway o alla dimensione del corpo della richiesta, è necessario passare al caricamento di file di grandi dimensioni.

### Crea batch

In primo luogo, sarà necessario creare un batch, con JSON come formato di input. Durante la creazione del batch, dovrete fornire un ID di set di dati. Sarà inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito.

>[!NOTE]
>
>Gli esempi di seguito sono per JSON a riga singola. Per acquisire JSON con più righe, è necessario impostare il `isMultiLineJson` flag. Per ulteriori informazioni, consulta la guida [alla risoluzione dei problemi di caricamento](./troubleshooting.md)batch.

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
| `{DATASET_ID}` | ID del set di dati di riferimento. |

### Caricare i file

Dopo aver creato un batch, potete usare il file `batchId` da prima per caricare i file nel batch. Potete caricare più file nel batch.

>[!NOTE]
>
>Consulta la sezione appendice per un [esempio di file](#data-transformation-for-batch-ingestion)di dati JSON formattati correttamente.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L’ID del batch in cui desiderate eseguire il caricamento. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. |

**Richiesta**

>[!NOTE]
>
>L&#39;API supporta il caricamento di singole parti. Verificate che il tipo di contenuto sia application/ottet-stream.

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
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. |

**Risposta**

```http
200 OK
```

### Completa batch

Dopo aver caricato tutte le diverse parti del file, dovrete segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L’ID del batch in cui desiderate eseguire il caricamento. |

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

## Assegna file di parquet

>[!NOTE]
>
>Per i file di piccole dimensioni (256 MB o inferiore) sono applicabili i seguenti passaggi. Se si verificano errori di timeout del gateway o di dimensioni del corpo della richiesta, sarà necessario passare al caricamento di file di grandi dimensioni.

### Crea batch

In primo luogo, sarà necessario creare un batch, con Parquet come formato di input. Durante la creazione del batch, dovrete fornire un ID di set di dati. Sarà inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito.

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
| `{DATASET_ID}` | ID del set di dati di riferimento. |
| `{USER_ID}` | L&#39;ID dell&#39;utente che ha creato il batch. |

### Caricare i file

Dopo aver creato un batch, potete usare il file `batchId` da prima per caricare i file nel batch. Potete caricare più file nel batch.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L’ID del batch in cui desiderate eseguire il caricamento. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento di singole parti. Verificate che il tipo di contenuto sia application/ottet-stream.

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
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. |

**Risposta**

```http
200 OK
```

### Completa batch

Dopo aver caricato tutte le diverse parti del file, dovrete segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L&#39;ID del batch che si desidera segnalare è pronto per il completamento. |

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

## Caricamento di file Parquet di grandi dimensioni

>[!NOTE]
>
>In questa sezione viene illustrato come caricare i file di dimensioni superiori a 256 MB. I file di grandi dimensioni vengono caricati in blocchi e quindi cuciti tramite un segnale API.

### Crea batch

In primo luogo, sarà necessario creare un batch, con Parquet come formato di input. Durante la creazione del batch, dovrete fornire un ID di set di dati. Sarà inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito.

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
| `{DATASET_ID}` | ID del set di dati di riferimento. |
| `{USER_ID}` | L&#39;ID dell&#39;utente che ha creato il batch. |

### Inizializza file grande

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Risposta**

```http
201 Created
```

### Caricare blocchi di file di grandi dimensioni

Ora che il file è stato creato, tutti i blocchi successivi possono essere caricati effettuando ripetute richieste PATCH, una per ogni sezione del file.

**Formato API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L’ID del batch in cui desiderate eseguire il caricamento. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento di singole parti. Verificate che il tipo di contenuto sia application/ottet-stream.

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
| `{CONTENT_RANGE}` | In numeri interi, l&#39;inizio e la fine dell&#39;intervallo richiesto. |
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. |


**Risposta**

```http
200 OK
```

### Completa file di grandi dimensioni

Dopo aver creato un batch, potete usare il file `batchId` da prima per caricare i file nel batch. Potete caricare più file nel batch.

**Formato API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID del batch di cui si desidera indicare il completamento. |
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

### Completa batch

Dopo aver caricato tutte le diverse parti del file, dovrete segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

**Formato API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L&#39;ID del batch che si desidera segnalare è completo. |


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

## Caricamento di file CSV

Per assimilare i file CSV, dovrete creare una classe, uno schema e un set di dati che supporti il CSV. Per informazioni dettagliate su come creare la classe e lo schema necessari, seguire le istruzioni fornite nell&#39;esercitazione [sulla creazione dello schema](../../xdm/api/ad-hoc.md)ad hoc.

>[!NOTE]
>
>Per i file di piccole dimensioni (256 MB o inferiore) sono applicabili i seguenti passaggi. Se si verificano errori di timeout del gateway o di dimensioni del corpo della richiesta, sarà necessario passare al caricamento di file di grandi dimensioni.

### Crea set di dati

Dopo aver seguito le istruzioni riportate sopra per creare la classe e lo schema necessari, dovrete creare un set di dati in grado di supportare il CSV.

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
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{TENANT_ID}` | Questo ID viene utilizzato per garantire che le risorse create siano correttamente denominate e contenute all’interno dell’organizzazione IMS. |
| `{SCHEMA_ID}` | ID dello schema creato. |

Una spiegazione di cosa la parte diversa della sezione &quot;fileDescription&quot; del corpo JSON può essere visto di seguito:

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `format` | Il formato del file master, non il formato del file di input. |
| `delimiters` | Il carattere da utilizzare come delimitatore. |
| `quotes` | Il carattere da utilizzare per le virgolette. |
| `escapes` | Il carattere da utilizzare come carattere di escape. |
| `header` | Il file caricato **deve** contenere intestazioni. Poiché la convalida dello schema è stata eseguita, è necessario impostare questo valore su true. Inoltre, le intestazioni **non** possono contenere spazi. Se avete degli spazi nell’intestazione, sostituiteli con caratteri di sottolineatura. |
| `charset` | Un campo facoltativo. Altri charset supportati includono &quot;US-ASCII&quot; e &quot;ISO-8869-1&quot;. Se lasciato vuoto, per impostazione predefinita viene utilizzato UTF-8. |

Il set di dati a cui si fa riferimento deve avere il blocco di descrizione del file elencato sopra e deve puntare a uno schema valido nel Registro di sistema. In caso contrario, il file non verrà masterizzato in parquet.

### Crea batch

Successivamente, sarà necessario creare un batch con CSV come formato di input. Durante la creazione del batch, dovrete fornire un ID di set di dati. Sarà inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema collegato al set di dati fornito.

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
| `{DATASET_ID}` | ID del set di dati di riferimento. |
| `{USER_ID}` | L&#39;ID dell&#39;utente che ha creato il batch. |

### Caricare i file

Dopo aver creato un batch, potete usare il file `batchId` da prima per caricare i file nel batch. Potete caricare più file nel batch.

>[!NOTE]
>
>Consultate la sezione appendice per un [esempio di file](#data-transformation-for-batch-ingestion)di dati CSV con formattazione corretta.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L’ID del batch in cui desiderate eseguire il caricamento. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento di singole parti. Verificate che il tipo di contenuto sia application/ottet-stream.

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
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. |


**Risposta**

```http
200 OK
```

### Completa batch

Dopo aver caricato tutte le diverse parti del file, dovrete segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

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

## Annullamento di un batch

Durante l&#39;elaborazione del batch, può essere comunque annullato. Tuttavia, una volta completato un batch (ad esempio uno stato di esito positivo o negativo), il batch non può essere annullato.

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

Un batch può essere eliminato eseguendo la seguente richiesta POST con il parametro `action=REVERT` query all’ID del batch che si desidera eliminare. Il batch è contrassegnato come &quot;inattivo&quot; e può quindi essere utilizzato per la raccolta dei rifiuti. Il batch verrà raccolto in modo asincrono, al momento in cui verrà contrassegnato come &quot;eliminato&quot;.

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

## Riproduzione di un batch

Se desiderate sostituire un batch già assimilato, potete farlo con &quot;riproduzione batch&quot;; questa azione equivale a eliminare il vecchio batch e a assimilarne uno nuovo.

### Crea batch

In primo luogo, sarà necessario creare un batch, con JSON come formato di input. Durante la creazione del batch, dovrete fornire un ID di set di dati. Sarà inoltre necessario assicurarsi che tutti i file caricati come parte del batch siano conformi allo schema XDM collegato al set di dati fornito. Inoltre, sarà necessario fornire i vecchi batch come riferimento nella sezione di ripetizione. Nell’esempio seguente, vengono riprodotti i batch con ID `batchIdA` e `batchIdB`.

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
| `{DATASET_ID}` | ID del set di dati di riferimento. |
| `{USER_ID}` | L&#39;ID dell&#39;utente che ha creato il batch. |


### Caricare i file

Dopo aver creato un batch, potete usare il file `batchId` da prima per caricare i file nel batch. Potete caricare più file nel batch.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L’ID del batch in cui desiderate eseguire il caricamento. |
| `{DATASET_ID}` | ID del set di dati di riferimento del batch. |
| `{FILE_NAME}` | Nome del file da caricare. |

**Richiesta**

>[!CAUTION]
>
>Questa API supporta il caricamento di singole parti. Verificate che il tipo di contenuto sia application/ottet-stream. Non utilizzate l&#39;opzione curl -F, in quanto per impostazione predefinita la richiesta con più parti è incompatibile con l&#39;API.

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
| `{FILE_PATH_AND_NAME}` | Percorso e nome completi del file che si sta tentando di caricare. |

**Risposta**

```http
200 OK
```

### Completa batch

Dopo aver caricato tutte le diverse parti del file, dovrete segnalare che i dati sono stati completamente caricati e che il batch è pronto per la promozione.

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

### Trasformazione dei dati per l’assimilazione batch

Per assimilare un file di dati in [!DNL Experience Platform], la struttura gerarchica del file deve essere conforme allo schema [Experience Data Model (XDM)](../../xdm/home.md) associato al set di dati in fase di caricamento.

Informazioni su come mappare un file CSV per conformarsi a uno schema XDM sono disponibili nel documento di trasformazione [di](../../etl/transformations.md) esempio, insieme a un esempio di file di dati JSON formattato correttamente. I file di esempio forniti nel documento sono disponibili qui:

- [CRM_profile.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profile.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)