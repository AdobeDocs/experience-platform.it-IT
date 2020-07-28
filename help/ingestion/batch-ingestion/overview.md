---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sull'inserimento dei batch di  Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 2%

---


# [!DNL Batch Ingestion]panoramica

L&#39; [!DNL Batch Ingestion] API consente di trasferire i dati  Adobe Experience Platform come file batch. I dati che si desidera acquisire possono essere i dati di profilo provenienti da un file semplice in un sistema CRM (ad esempio un file parquet), o i dati conformi a uno schema noto nel Registro di sistema [!DNL Experience Data Model] (XDM).

Il riferimento [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) Data Ingestion fornisce informazioni aggiuntive su queste chiamate API.

Il diagramma seguente illustra il processo di assimilazione dei batch:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Utilizzo dell&#39;API

L&#39; [!DNL Data Ingestion] API consente di assimilare i dati come batch (un&#39;unità di dati costituita da uno o più file da assimilare come singola unità) in [!DNL Experience Platform] tre passaggi fondamentali:

1. Creare un nuovo batch.
2. Caricate i file in un set di dati specificato che corrisponde allo schema XDM dei dati.
3. Segnala la fine del batch.


### [!DNL Data Ingestion] prerequisiti

- I dati da caricare devono essere in formato Parquet o JSON.
- Un set di dati creato in [!DNL Catalog services](../../catalog/home.md).
- Il contenuto del file parquet deve corrispondere a un sottoinsieme dello schema del set di dati in fase di caricamento.
- Dopo l&#39;autenticazione, avrai il tuo token di accesso univoco.

### Best practice per l’assimilazione dei batch

- La dimensione del batch consigliata è compresa tra 256 MB e 100 GB.
- Ogni batch deve contenere al massimo 1500 file.

Per caricare un file di dimensioni superiori a 512 MB, è necessario dividere il file in blocchi più piccoli. Le istruzioni per caricare un file di grandi dimensioni sono disponibili [qui](#large-file-upload---create-file).

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

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

### Creare un batch

Prima di poter aggiungere dati a un dataset, questi devono essere collegati a un batch, che verrà poi caricato in un set di dati specificato.

```http
POST /batches
```

**Richiesta**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
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

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID del batch appena creato (utilizzato nelle richieste successive). |
| `relatedObjects.id` | ID del set di dati in cui caricare i file. |

## Caricamento file

Dopo aver creato un nuovo batch per il caricamento, i file possono essere caricati in un set di dati specifico.

Potete caricare i file mediante l’API **di caricamento dei file** piccoli. Tuttavia, se i file sono troppo grandi e il limite del gateway viene superato (ad esempio timeout estesi, richieste di dimensioni del corpo superate e altre restrizioni), potete passare all&#39;API **di caricamento dei file di** grandi dimensioni. Questa API carica il file in blocchi e unisce i dati utilizzando la chiamata API **** Large File Upload Complete.

>[!NOTE]
>
>Gli esempi seguenti utilizzano il formato di file [parquet](https://parquet.apache.org/documentation/latest/) . Un esempio che utilizza il formato di file JSON è disponibile nella guida [per gli sviluppatori per l’assimilazione](./api-overview.md)batch.

### Caricamento di file di piccole dimensioni

Una volta creato un batch, i dati possono essere caricati in un dataset preesistente.  Il file caricato deve corrispondere allo schema XDM di riferimento.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch. |
| `{DATASET_ID}` | ID del set di dati per caricare i file. |
| `{FILE_NAME}` | Nome del file che verrà visualizzato nel set di dati. |

**Richiesta**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome del file da caricare nel dataset. |

**Risposta**

```JSON
#Status 200 OK, with empty response body
```

### Caricamento di file di grandi dimensioni - creazione di file

Per caricare un file di grandi dimensioni, il file deve essere suddiviso in blocchi più piccoli e caricato uno alla volta.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch. |
| `{DATASET_ID}` | L’ID del set di dati per l’assimilazione dei file. |
| `{FILE_NAME}` | Nome del file che verrà visualizzato nel set di dati. |

**Richiesta**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta**

```JSON
#Status 201 CREATED, with empty response body
```

### Caricamento di file di grandi dimensioni - caricamento di parti successive

Dopo la creazione del file, tutti i blocchi successivi possono essere caricati effettuando ripetute richieste di PATCH, una per ogni sezione del file.

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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Percorso e nome del file da caricare nel dataset. |

**Risposta**

```JSON
#Status 200 OK, with empty response
```

## Completamento batch segnale

Dopo aver caricato tutti i file nel batch, il batch può essere segnalato per il completamento. In questo modo, le voci [!DNL Catalog] DataSetFile **** vengono create per i file completati e associate al batch generato in precedenza. Il [!DNL Catalog] batch viene quindi contrassegnato come riuscito, che attiva i flussi a valle per l&#39;acquisizione dei dati disponibili.

**Richiesta**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch da caricare nel set di dati. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Risposta**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
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
| `{USER_ID}` | L&#39;ID dell&#39;utente che ha creato o aggiornato il batch. |

Il `"status"` campo indica lo stato corrente del batch richiesto. I batch possono avere uno dei seguenti stati:

## Stati di inserimento batch

| Stato | Descrizione |
| ------ | ----------- |
| Abbandonato | Il batch non è stato completato nel periodo di tempo previsto. |
| Interrotto | Un&#39;operazione di interruzione è stata **esplicitamente** chiamata (tramite l&#39;API Batch Ingest) per il batch specificato. Una volta che il batch è in stato **caricato** , non può essere interrotto. |
| Attivo | Il batch è stato promosso con successo ed è disponibile per il consumo a valle. Questo stato può essere utilizzato in modo intercambiabile con **Success**. |
| Eliminato | I dati per il batch sono stati rimossi completamente. |
| Non riuscito | Uno stato terminale che risulta da una configurazione non corretta e/o da dati non corretti. I dati per un batch con errore **non** vengono visualizzati. Questo stato può essere utilizzato in modo intercambiabile con **Errore**. |
| Inattivo | Il batch è stato promosso con successo, ma è stato ripristinato o è scaduto. Il batch non è più disponibile per il consumo a valle. |
| Caricato | I dati per il batch sono completi e il batch è pronto per la promozione. |
| Caricamento | I dati per questo batch vengono caricati e il batch **non** è attualmente pronto per essere promosso. |
| Nuovo | Elaborazione dei dati per questo batch in corso. Tuttavia, a causa di un errore di sistema o temporaneo, il batch non è riuscito, come risultato, il batch viene riprovato. |
| In pila | La fase intermedia del processo di promozione per un batch è completa e il processo di assimilazione è stato eseguito. |
| Gestione temporanea | Elaborazione dei dati per il batch in corso. |
| Bloccato | Elaborazione dei dati per il batch in corso. Tuttavia, la promozione batch si è arrestata dopo diversi tentativi. |