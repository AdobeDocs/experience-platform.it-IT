---
keywords: Experience Platform;home;argomenti popolari;inserimento dati;batch;abilita set di dati;panoramica acquisizione batch;panoramica;panoramica acquisizione batch;
solution: Experience Platform
title: Panoramica sull’acquisizione in batch
topic-legacy: overview
description: L’API di acquisizione dati di Adobe Experience Platform consente di acquisire dati in Platform come file batch. I dati da acquisire possono essere i dati di profilo di un file flat in un sistema CRM (ad esempio un file Parquet) o dati conformi a uno schema noto nel registro Experience Data Model (XDM).
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 3%

---

# Panoramica sull’acquisizione in batch

L’API di acquisizione dati di Adobe Experience Platform consente di acquisire dati in Platform come file batch. I dati da acquisire possono essere i dati di profilo di un file flat in un sistema CRM (ad esempio un file Parquet) o dati conformi a uno schema noto nel registro [!DNL Experience Data Model] (XDM).

Il [Riferimento API di acquisizione dati](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) fornisce informazioni aggiuntive su queste chiamate API.

Il diagramma seguente illustra il processo di acquisizione batch:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Mediante l’API

L’ API [!DNL Data Ingestion] ti consente di acquisire dati come batch (un’unità di dati costituita da uno o più file da acquisire come singola unità) in [!DNL Experience Platform] in tre passaggi fondamentali:

1. Crea un nuovo batch.
2. Carica i file in un set di dati specifico che corrisponde allo schema XDM dei dati.
3. Segnala la fine del batch.


### [!DNL Data Ingestion] prerequisiti

- I dati da caricare devono essere in formato Parquet o JSON.
- Un set di dati creato in [[!DNL Catalog services]](../../catalog/home.md).
- Il contenuto del file Parquet deve corrispondere a un sottoinsieme dello schema del set di dati in cui viene caricato.
- Richiedi il token di accesso univoco dopo l’autenticazione.

### Best practice per l’acquisizione in batch

- La dimensione consigliata del batch è compresa tra 256 MB e 100 GB.
- Ogni batch deve contenere al massimo 1500 file.

Per caricare un file di dimensioni superiori a 512 MB, è necessario suddividerlo in blocchi più piccoli. Le istruzioni per caricare un file di grandi dimensioni si trovano [qui](#large-file-upload---create-file).

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

### Creare un batch

Prima di poter aggiungere dati a un set di dati, questi devono essere collegati a un batch che verrà successivamente caricato in un set di dati specifico.

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

Dopo aver creato correttamente un nuovo batch per il caricamento, i file possono quindi essere caricati in un set di dati specifico.

Puoi caricare i file utilizzando l’API di caricamento file di piccole dimensioni. Tuttavia, se i file sono troppo grandi e il limite del gateway viene superato (ad esempio timeout estesi, richieste di dimensioni del corpo superate e altre restrizioni), puoi passare all’API di caricamento file di grandi dimensioni. Questa API carica il file in blocchi e unisce i dati utilizzando la chiamata API di caricamento file di grandi dimensioni Complete.

>[!NOTE]
>
>Gli esempi seguenti utilizzano il formato file [Apache Parquet](https://parquet.apache.org/documentation/latest/) . Un esempio che utilizza il formato di file JSON si trova nella [guida per gli sviluppatori per l’acquisizione batch](./api-overview.md).

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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
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

Dopo che tutti i file sono stati caricati nel batch, il batch può essere segnalato per il completamento. In questo modo, le voci [!DNL Catalog] DataSetFile vengono create per i file completati e associate al batch generato in precedenza. Il batch [!DNL Catalog] viene quindi contrassegnato come riuscito, il che attiva i flussi a valle per acquisire i dati disponibili.

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
| `{USER_ID}` | ID dell&#39;utente che ha creato o aggiornato il batch. |

Il campo `"status"` mostra lo stato corrente del batch richiesto. I batch possono avere uno dei seguenti stati:

## Stati di inserimento batch

| Stato | Descrizione |
| ------ | ----------- |
| Abbandonato | Il batch non è stato completato nell&#39;intervallo di tempo previsto. |
| Interrotto | Un&#39;operazione di interruzione è stata chiamata **esplicitamente** (tramite l&#39;API di acquisizione in batch) per il batch specificato. Una volta che il batch è in stato &quot;Caricato&quot;, non può essere interrotto. |
| Attivo | Il batch è stato promosso con successo ed è disponibile per il consumo a valle. Questo stato può essere utilizzato in modo intercambiabile con &quot;Success&quot;. |
| Eliminato | I dati per il batch sono stati rimossi completamente. |
| Non riuscito | Stato terminale che risulta da una configurazione errata e/o da dati non validi. I dati per un batch non riuscito **non** vengono visualizzati. Questo stato può essere utilizzato in modo intercambiabile con &quot;Failure&quot; (Errore). |
| Inattivo | La promozione del batch è stata completata, ma è stata ripristinata o è scaduta. Il batch non è più disponibile per il consumo a valle. |
| Caricato | I dati per il batch sono completi e il batch è pronto per la promozione. |
| Caricamento | I dati per questo batch vengono caricati e il batch è attualmente **non** pronto per essere promosso. |
| Nuovo | I dati per questo batch sono in fase di elaborazione. Tuttavia, a causa di un errore di sistema o temporaneo, il batch non è riuscito - di conseguenza, questo batch viene riprovato. |
| Staging | La fase di staging del processo di promozione per un batch è completata e il processo di acquisizione è stato eseguito. |
| Staging | Elaborazione dei dati per il batch in corso. |
| In stallo | Elaborazione dei dati per il batch in corso. Tuttavia, la promozione batch si è arrestata dopo diversi tentativi. |
