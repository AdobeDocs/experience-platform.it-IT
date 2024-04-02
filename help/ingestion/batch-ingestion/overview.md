---
keywords: Experience Platform;home;argomenti comuni;inserimento dati;batch;abilitare set di dati;panoramica acquisizione batch;panoramica acquisizione batch;panoramica acquisizione batch;home;popular topic;data ingestion;batch;Batch;enable dataset;Batch ingestion overview;overview;batch ingestion overview;
solution: Experience Platform
title: Panoramica dell’API per l’acquisizione in batch
description: L’API per l’acquisizione in batch di Adobe Experience Platform consente di acquisire i dati in Platform come file batch. I dati da acquisire possono essere i dati di profilo provenienti da un file flat in un sistema di gestione delle relazioni con i clienti (ad esempio un file Parquet) o i dati conformi a uno schema noto nel registro Experience Data Model (XDM).
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 9d3a8aac120119ce0361685f9cb8d3bfc28dc7fd
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 7%

---

# Panoramica dell’API per l’acquisizione in batch

L’API per l’acquisizione in batch di Adobe Experience Platform consente di acquisire i dati in Platform come file batch. I dati da acquisire possono essere dati di profilo da un file flat (ad esempio un file Parquet) o dati conformi a uno schema noto in [!DNL Experience Data Model] (XDM).

Il [Riferimento API per acquisizione in batch](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) fornisce informazioni aggiuntive su queste chiamate API.

Il diagramma seguente illustra il processo di acquisizione batch:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Introduzione

Gli endpoint API utilizzati in questa guida fanno parte del [API di acquisizione in batch](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Prima di continuare, controlla [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experienci Platform.

### [!DNL Data Ingestion] prerequisiti

- I dati da caricare devono essere in formato Parquet o JSON.
- Un set di dati creato in [[!DNL Catalog services]](../../catalog/home.md).
- Il contenuto del file Parquet deve corrispondere a un sottoinsieme dello schema del set di dati in cui viene caricato.
- Disporre di un token di accesso univoco dopo l’autenticazione.

### Best practice per l’acquisizione in batch

- La dimensione del batch consigliata è compresa tra 256 MB e 100 GB.
- Ogni batch può contenere al massimo 1500 file.

### Vincoli di acquisizione in batch

L’acquisizione di dati batch presenta alcuni vincoli:

- Numero massimo di file per batch: 1500
- Dimensione massima batch: 100 GB
- Numero massimo di proprietà o campi per riga: 10000
- Numero massimo di batch nel data lake al minuto per utente: 138

>[!NOTE]
>
>Per caricare un file di dimensioni superiori a 512 MB, è necessario suddividerlo in blocchi più piccoli. Le istruzioni per caricare un file di grandi dimensioni sono disponibili nella sezione [sezione caricamento file di grandi dimensioni di questo documento](#large-file-upload---create-file).

### Tipi

Durante l’acquisizione dei dati, è importante comprendere in che modo [!DNL Experience Data Model] Gli schemi (XDM) funzionano. Per ulteriori informazioni su come i tipi di campo XDM si associano a formati diversi, consulta [Guida per gli sviluppatori del registro dello schema](../../xdm/api/getting-started.md).

È disponibile una certa flessibilità durante l’acquisizione dei dati: se un tipo non corrisponde a quello presente nello schema di destinazione, i dati verranno convertiti nel tipo di destinazione espresso. In caso contrario, il batch avrà esito negativo con un `TypeCompatibilityException`.

Ad esempio, né JSON né CSV hanno un `date` o `date-time` tipo. Di conseguenza, questi valori sono espressi utilizzando [Stringhe formattate ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) o il tempo Unix formattato in millisecondi (1531263959000) e vengono convertiti al momento dell’acquisizione nel tipo XDM di destinazione.

La tabella seguente mostra le conversioni supportate durante l’acquisizione dei dati.

| In entrata (riga) e Target (colonna) | Stringa | Byte | Breve | Intero | Lungo | Doppio | Data | Data-ora | Oggetto | Mappa |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Stringa | X | X | X | X | X | X | X | X |   |   |
| Byte | X | X | X | X | X | X |   |   |   |   |
| Breve | X | X | X | X | X | X |   |   |   |   |
| Intero | X | X | X | X | X | X |   |   |   |   |
| Lungo | X | X | X | X | X | X | X | X |   |   |
| Doppio | X | X | X | X | X | X |   |   |   |   |
| Data |   |   |   |   |   |   | X |   |   |   |
| Data-ora |   |   |   |   |   |   |   | X |   |   |
| Oggetto |   |   |   |   |   |   |   |   | X | X |
| Mappa |   |   |   |   |   |   |   |   | X | X |

>[!NOTE]
>
>I booleani e gli array non possono essere convertiti in altri tipi.

## Mediante l’API

Il [!DNL Data Ingestion] API consente di acquisire i dati come batch (un’unità di dati costituita da uno o più file da acquisire come una singola unità) in [!DNL Experience Platform] in tre passaggi fondamentali:

1. Crea un nuovo batch.
2. Carica i file in un set di dati specificato che corrisponde allo schema XDM dei dati.
3. Segnala la fine del batch.

## Creare un batch

Prima di poter aggiungere dati a un set di dati, questi devono essere collegati a un batch, che in seguito verrà caricato in un set di dati specificato.

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

Dopo aver creato correttamente un nuovo batch per il caricamento, i file possono essere caricati in un set di dati specifico.

Puoi caricare i file utilizzando l’API Caricamento file di piccole dimensioni. Tuttavia, se i file sono troppo grandi e il limite del gateway viene superato (ad esempio timeout estesi, richieste di dimensioni del corpo superate e altre limitazioni), puoi passare all’API di caricamento file di grandi dimensioni. Questa API carica il file in blocchi e unisce i dati utilizzando la chiamata API Caricamento di file di grandi dimensioni completato.

>[!NOTE]
>
>L’acquisizione batch può essere utilizzata per aggiornare in modo incrementale i dati nell’archivio profili. Per ulteriori informazioni, consulta la sezione su [aggiornamento di un batch](#patch-a-batch) nel [guida per gli sviluppatori sull’acquisizione batch](api-overview.md).

>[!INFO]
>
>Gli esempi seguenti utilizzano [Apache Parquet](https://parquet.apache.org/docs/) formato file. Un esempio che utilizza il formato di file JSON si trova in [guida per gli sviluppatori sull’acquisizione batch](api-overview.md).

### Caricamento di file di piccole dimensioni

Una volta creato un batch, i dati possono essere caricati in un set di dati preesistente.  Il file caricato deve corrispondere al relativo schema XDM di riferimento.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch. |
| `{DATASET_ID}` | ID del set di dati per caricare i file. |
| `{FILE_NAME}` | Nome del file come verrà visualizzato nel set di dati. |

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
| `{FILE_PATH_AND_NAME}` | Percorso e nome del file da caricare nel set di dati. |

**Risposta**

```JSON
#Status 200 OK, with empty response body
```

### Caricamento di file di grandi dimensioni - Crea file

Per caricare un file di grandi dimensioni, il file deve essere diviso in blocchi più piccoli e caricato uno alla volta.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch. |
| `{DATASET_ID}` | ID del set di dati che acquisisce i file. |
| `{FILE_NAME}` | Nome del file come verrà visualizzato nel set di dati. |

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

Dopo la creazione del file, tutti i blocchi successivi possono essere caricati effettuando ripetute richieste PATCH, una per ogni sezione del file.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch. |
| `{DATASET_ID}` | ID del set di dati in cui caricare i file. |
| `{FILE_NAME}` | Nome del file che verrà visualizzato nel set di dati. |

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
| `{FILE_PATH_AND_NAME}` | Percorso e nome del file da caricare nel set di dati. |

**Risposta**

```JSON
#Status 200 OK, with empty response
```

## Completamento batch segnale

Dopo che tutti i file sono stati caricati nel batch, il batch può essere segnalato per il completamento. In questo modo, il [!DNL Catalog] Le voci DataSetFile vengono create per i file completati e associate al batch generato in precedenza. Il [!DNL Catalog] Il batch viene quindi contrassegnato come riuscito, che attiva i flussi a valle per acquisire i dati disponibili.

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

In attesa che i file vengano caricati nel batch, è possibile controllare lo stato del batch per verificarne l’avanzamento.

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
| `{USER_ID}` | ID dell’utente che ha creato o aggiornato il batch. |

Il `"status"` campo che mostra lo stato corrente del batch richiesto. I batch possono avere uno dei seguenti stati:

## Stati di acquisizione in batch

| Stato | Descrizione |
| ------ | ----------- |
| Abbandonato | Il batch non è stato completato entro il periodo di tempo previsto. |
| Interrotto | Un&#39;operazione di interruzione ha **esplicitamente** chiamato (tramite API Batch Ingest) per il batch specificato. Una volta che il batch è in uno stato &quot;Loaded&quot; (Caricato), non può essere interrotto. |
| Attivo | Il batch è stato promosso correttamente ed è disponibile per il consumo a valle. Questo stato può essere utilizzato in modo intercambiabile con &quot;Success&quot; (Completato). |
| Eliminato | I dati per il batch sono stati completamente rimossi. |
| Non riuscito | Stato del terminale causato da configurazione e/o dati non validi. I dati per un batch non riuscito **non** vieni a trovarti. Questo stato può essere utilizzato in modo intercambiabile con &quot;Errore&quot;. |
| Inattivo | Il batch è stato promosso correttamente, ma è stato ripristinato o è scaduto. Il batch non è più disponibile per il consumo a valle. |
| Caricato | I dati per il batch sono completi e il batch è pronto per la promozione. |
| Caricamento | I dati per questo batch sono in fase di caricamento e il batch è attualmente **non** pronto per essere promosso. |
| Nuovo tentativo | Elaborazione dei dati per questo batch in corso. Tuttavia, a causa di un errore di sistema o transitorio, il batch non è riuscito. Di conseguenza, si sta tentando di nuovo di eseguire il batch. |
| In staging | La fase di staging del processo di promozione per un batch è stata completata e il processo di acquisizione è stato eseguito. |
| Staging | Dati per il batch in fase di elaborazione. |
| In stallo | I dati per il batch sono in fase di elaborazione. Tuttavia, la promozione batch si è bloccata dopo una serie di tentativi. |
