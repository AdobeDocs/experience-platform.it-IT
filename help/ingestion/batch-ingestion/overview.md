---
keywords: Experience Platform;home;argomenti popolari;inserimento dati;batch;abilita set di dati;panoramica acquisizione batch;panoramica;panoramica acquisizione batch;
solution: Experience Platform
title: Panoramica API di acquisizione in batch
topic-legacy: overview
description: L’API di acquisizione dati di Adobe Experience Platform consente di acquisire dati in Platform come file batch. I dati da acquisire possono essere i dati di profilo di un file flat in un sistema CRM (ad esempio un file Parquet) o dati conformi a uno schema noto nel registro Experience Data Model (XDM).
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 6%

---

# Panoramica API per l’acquisizione in batch

L’API di acquisizione dati di Adobe Experience Platform consente di acquisire dati in Platform come file batch. I dati da acquisire possono essere dati di profilo provenienti da un file flat (ad esempio un file Parquet) o dati conformi a uno schema noto nel [!DNL Experience Data Model] (XDM).

La [Riferimento API per l’acquisizione dei dati](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) fornisce informazioni aggiuntive su queste chiamate API.

Il diagramma seguente illustra il processo di acquisizione batch:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte del [API di acquisizione dati](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

### [!DNL Data Ingestion] prerequisiti

- I dati da caricare devono essere in formato Parquet o JSON.
- Un set di dati creato in [[!DNL Catalog services]](../../catalog/home.md).
- Il contenuto del file Parquet deve corrispondere a un sottoinsieme dello schema del set di dati in cui viene caricato.
- Richiedi il token di accesso univoco dopo l’autenticazione.

### Best practice per l’acquisizione in batch

- La dimensione consigliata del batch è compresa tra 256 MB e 100 GB.
- Ogni batch deve contenere al massimo 1500 file.

### Vincoli di inserimento in batch

L’inserimento dei dati in batch presenta alcuni vincoli:

- Numero massimo di file per batch: 1500
- Dimensione massima del batch: 100 GB
- Numero massimo di proprietà o campi per riga: 10000
- Numero massimo di batch al minuto per utente: 138

>[!NOTE]
>
>Per caricare un file di dimensioni superiori a 512 MB, è necessario suddividerlo in blocchi più piccoli. Le istruzioni per caricare un file di grandi dimensioni si trovano nella sezione [sezione caricamento file di grandi dimensioni del documento](#large-file-upload---create-file).

### Tipi

Durante l’acquisizione dei dati, è importante comprendere come [!DNL Experience Data Model] Gli schemi (XDM) funzionano. Per ulteriori informazioni sulla mappatura dei tipi di campo XDM su formati diversi, consulta la sezione [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md).

È possibile acquisire i dati in modo flessibile: se un tipo non corrisponde a quello presente nello schema di destinazione, i dati verranno convertiti nel tipo di destinazione espresso. In caso contrario, il batch non riuscirà con un `TypeCompatibilityException`.

Ad esempio, né JSON né CSV hanno un `date` o `date-time` digitare. Di conseguenza, questi valori vengono espressi utilizzando [Stringhe formattate ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) o Tempo Unix formattato in millisecondi (1531263959000) e convertito al momento dell’acquisizione nel tipo XDM di destinazione.

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

## Mediante l’API

La [!DNL Data Ingestion] L’API ti consente di acquisire i dati come batch (un’unità di dati costituita da uno o più file da acquisire come una singola unità) in [!DNL Experience Platform] in tre fasi di base:

1. Crea un nuovo batch.
2. Carica i file in un set di dati specifico che corrisponde allo schema XDM dei dati.
3. Segnala la fine del batch.

## Creare un batch

Prima di poter aggiungere dati a un set di dati, questi devono essere collegati a un batch che verrà successivamente caricato in un set di dati specifico.

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `datasetId` | ID del set di dati in cui caricare i file. |

**Risposta**

```JSON
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

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID del batch appena creato (utilizzato nelle richieste successive). |
| `relatedObjects.id` | ID del set di dati in cui caricare i file. |

## Caricamento file

Dopo aver creato correttamente un nuovo batch per il caricamento, i file possono quindi essere caricati in un set di dati specifico.

Puoi caricare i file utilizzando l’API di caricamento file di piccole dimensioni. Tuttavia, se i file sono troppo grandi e il limite del gateway viene superato (ad esempio timeout estesi, richieste di dimensioni del corpo superate e altre restrizioni), puoi passare all’API di caricamento file di grandi dimensioni. Questa API carica il file in blocchi e unisce i dati utilizzando la chiamata API di caricamento file di grandi dimensioni Complete.

>[!NOTE]
>
>L’acquisizione in batch può essere utilizzata per aggiornare gradualmente i dati nell’archivio profili. Per ulteriori informazioni, consulta la sezione su [aggiornamento di un batch](#patch-a-batch) in [guida per gli sviluppatori di batch ingestion](api-overview.md).

>[!INFO]
>
>Gli esempi seguenti utilizzano il [Parquet Apache](https://parquet.apache.org/docs/) formato di file. Un esempio che utilizza il formato di file JSON si trova nella [guida per gli sviluppatori di batch ingestion](api-overview.md).

### Caricamento di file di piccole dimensioni

Una volta creato un batch, i dati possono essere caricati in un set di dati preesistente.  Il file caricato deve corrispondere al relativo schema XDM di riferimento.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch. |
| `{DATASET_ID}` | ID del set di dati per caricare i file. |
| `{FILE_NAME}` | Il nome del file come verrà visualizzato nel set di dati. |

**Richiesta**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Il percorso e il nome del file da caricare nel set di dati. |

**Risposta**

```JSON
#Status 200 OK, with empty response body
```

### Caricamento di file di grandi dimensioni - crea file

Per caricare un file di grandi dimensioni, è necessario suddividerlo in blocchi più piccoli e caricarlo uno alla volta.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch. |
| `{DATASET_ID}` | ID del set di dati che acquisisce i file. |
| `{FILE_NAME}` | Il nome del file come verrà visualizzato nel set di dati. |

**Richiesta**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta**

```JSON
#Status 201 CREATED, with empty response body
```

### Caricamento di file di grandi dimensioni - caricamento di parti successive

Dopo la creazione del file, è possibile caricare tutti i blocchi successivi effettuando richieste PATCH ripetute, una per ogni sezione del file.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch. |
| `{DATASET_ID}` | ID del set di dati in cui caricare i file. |
| `{FILE_NAME}` | Nome del file come verrà visualizzato nel set di dati. |

**Richiesta**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Il percorso e il nome del file da caricare nel set di dati. |

**Risposta**

```JSON
#Status 200 OK, with empty response
```

## Completamento batch del segnale

Dopo che tutti i file sono stati caricati nel batch, il batch può essere segnalato per il completamento. Facendo questo, il [!DNL Catalog] Le voci DataSetFile vengono create per i file completati e associate al batch generato in precedenza. La [!DNL Catalog] batch viene quindi contrassegnato come riuscito, che attiva i flussi a valle per acquisire i dati disponibili.

**Richiesta**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch da caricare nel set di dati. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**Risposta**

```JSON
#Status 200 OK, with empty response
```

## Verifica stato batch

In attesa del caricamento dei file nel batch, è possibile controllare lo stato del batch per verificarne l&#39;avanzamento.

**Formato API**

```http
GET /batch/{BATCH_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch da controllare. |

**Richiesta**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{USER_ID}` | ID dell&#39;utente che ha creato o aggiornato il batch. |

La `"status"` Il campo indica lo stato corrente del batch richiesto. I batch possono avere uno dei seguenti stati:

## Stati di inserimento batch

| Stato | Descrizione |
| ------ | ----------- |
| Abbandonato | Il batch non è stato completato nell&#39;intervallo di tempo previsto. |
| Interrotto | Operazione di interruzione **esplicitamente** è stato chiamato (tramite l’API di acquisizione batch) per il batch specificato. Una volta che il batch è in stato &quot;Caricato&quot;, non può essere interrotto. |
| Attivo | Il batch è stato promosso con successo ed è disponibile per il consumo a valle. Questo stato può essere utilizzato in modo intercambiabile con &quot;Success&quot;. |
| Eliminato | I dati per il batch sono stati rimossi completamente. |
| Non riuscito | Stato terminale che risulta da una configurazione errata e/o da dati non validi. I dati per un batch con errore **not** si faccia vivo. Questo stato può essere utilizzato in modo intercambiabile con &quot;Failure&quot; (Errore). |
| Inattivo | La promozione del batch è stata completata, ma è stata ripristinata o è scaduta. Il batch non è più disponibile per il consumo a valle. |
| Caricato | I dati per il batch sono completi e il batch è pronto per la promozione. |
| Caricamento | I dati per questo batch vengono caricati e il batch è attualmente **not** pronti per essere promossi. |
| Nuovo | I dati per questo batch sono in fase di elaborazione. Tuttavia, a causa di un errore di sistema o temporaneo, il batch non è riuscito - di conseguenza, questo batch viene riprovato. |
| Staging | La fase di staging del processo di promozione per un batch è completata e il processo di acquisizione è stato eseguito. |
| Staging | Elaborazione dei dati per il batch in corso. |
| In stallo | Elaborazione dei dati per il batch in corso. Tuttavia, la promozione batch si è arrestata dopo diversi tentativi. |
