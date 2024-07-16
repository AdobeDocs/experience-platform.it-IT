---
keywords: Experience Platform;home;argomenti popolari;inserimento batch;inserimento batch;inserimento parziale;inserimento parziale;inserimento parziale;recuperare errore;recuperare errore;inserimento batch parziale;inserimento batch parziale;inserimento parziale;inserimento;inserimento;diagnostica degli errori;recuperare diagnostica degli errori;ottenere diagnostica degli errori;ottenere errore;ottenere errori;recuperare errori;recuperare errori;
solution: Experience Platform
title: Recupero della diagnostica degli errori di acquisizione dati
description: Questo documento fornisce informazioni sul monitoraggio dell’acquisizione batch, sulla gestione degli errori di acquisizione batch parziale e fornisce un riferimento per i tipi di acquisizione batch parziale.
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 9%

---

# Recupero diagnostica errori di acquisizione dati

Adobe Experience Platform fornisce due metodi per caricare e acquisire i dati. È possibile utilizzare l&#39;acquisizione in batch, che consente di inserire dati utilizzando vari tipi di file (ad esempio CSV), oppure l&#39;acquisizione in streaming, che consente di inserire i dati in [!DNL Platform] utilizzando endpoint di streaming in tempo reale.

Questo documento fornisce informazioni sul monitoraggio dell’acquisizione batch, sulla gestione degli errori di acquisizione batch parziale e fornisce un riferimento per i tipi di acquisizione batch parziale.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md): i metodi tramite i quali i dati possono essere inviati a [!DNL Experience Platform].

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

## Download della diagnostica degli errori {#download-diagnostics}

Adobe Experience Platform consente agli utenti di scaricare la diagnostica degli errori dei file di input. La diagnostica verrà mantenuta entro [!DNL Platform] per un massimo di 30 giorni.

### Elencare i file di input {#list-files}

La richiesta seguente recupera un elenco di tutti i file forniti in un batch finalizzato.

**Formato API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch che stai cercando. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce oggetti JSON che definiscono nei dettagli dove sono state salvate le attività di diagnostica.

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Recupera diagnostica file di input {#retrieve-diagnostics}

Dopo aver recuperato un elenco di tutti i diversi file di input, puoi recuperare la diagnostica del singolo file utilizzando la seguente richiesta.

**Formato API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch che stai cercando. |
| `{FILE}` | Nome del file a cui si sta effettuando l&#39;accesso. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituirà oggetti JSON contenenti `path` oggetti che specificano dove sono state salvate le attività di diagnostica. La risposta restituirà gli oggetti `path` in formato [JSON Lines](https://jsonlines.readthedocs.io/en/latest/).

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Recuperare gli errori di acquisizione batch {#retrieve-errors}

Se i batch contengono errori, è necessario recuperare le informazioni relative a tali errori in modo da poter riacquisire i dati.

### Verifica stato {#check-status}

Per controllare lo stato del batch acquisito, devi fornire l’ID del batch nel percorso di una richiesta GET. Per ulteriori informazioni sull&#39;utilizzo di questa chiamata API, leggere la [guida dell&#39;endpoint del catalogo](../../catalog/api/list-objects.md).

**Formato API**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | Il valore `id` del batch di cui si desidera controllare lo stato. |
| `{FILTER}` | Parametro di query utilizzato per filtrare i risultati restituiti nella risposta. Più parametri separati da e commerciali (`&`). Per ulteriori informazioni, consulta la guida su [filtraggio dei dati del catalogo](../../catalog/api/filter-data.md). |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta senza errori**

In caso di esito positivo, la risposta restituisce informazioni dettagliate sullo stato del batch.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{ORG_ID}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `metrics.failedRecordCount` | Numero di righe che non è stato possibile elaborare a causa di analisi, conversione o convalida. Questo valore può essere derivato sottraendo `inputRecordCount` da `outputRecordCount`. Questo valore viene generato in tutti i batch, indipendentemente dal fatto che `errorDiagnostics` sia abilitato. |

**Risposta con errori**

Se il batch presenta uno o più errori e la diagnostica degli errori è abilitata, la risposta restituisce ulteriori informazioni sugli errori, sia all’interno del payload stesso che in un file di errore scaricabile. Si noti che lo stato di un batch contenente errori può comunque avere uno stato di successo.

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{ORG_ID}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `metrics.failedRecordCount` | Numero di righe che non è stato possibile elaborare a causa di analisi, conversione o convalida. Questo valore può essere derivato sottraendo `inputRecordCount` da `outputRecordCount`. Questo valore viene generato in tutti i batch, indipendentemente dal fatto che `errorDiagnostics` sia abilitato. |
| `errors.recordCount` | Numero di righe non riuscite per il codice di errore specificato. Questo valore è **only** generato se `errorDiagnostics` è abilitato. |

>[!NOTE]
>
>Se la diagnostica degli errori non è disponibile, verrà visualizzato il seguente messaggio di errore:
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## Passaggi successivi {#next-steps}

Questo tutorial illustra come monitorare gli errori di acquisizione in blocco parziale. Per ulteriori informazioni sull&#39;acquisizione batch, consulta la [guida per gli sviluppatori sull&#39;acquisizione batch](../batch-ingestion/api-overview.md).

## Appendice {#appendix}

Questa sezione fornisce informazioni supplementari sui tipi di errore di acquisizione.

### Tipi di errore per acquisizione batch parziale {#partial-ingestion-types}

L’acquisizione in blocco parziale presenta tre diversi tipi di errore durante l’acquisizione dei dati:

- [File illeggibili](#unreadable)
- [Schemi o intestazioni non validi](#schemas-headers)
- [Righe non analizzabili](#unparsable)

### File illeggibili {#unreadable}

Se il batch acquisito contiene file illeggibili, gli errori del batch verranno allegati al batch stesso. Ulteriori informazioni sul recupero del batch non riuscito sono disponibili nella [guida al recupero dei batch non riusciti](../quality/retrieve-failed-batches.md).

### Schemi o intestazioni non validi {#schemas-headers}

Se il batch acquisito ha uno schema o intestazioni non validi, gli errori del batch verranno allegati al batch stesso. Ulteriori informazioni sul recupero del batch non riuscito sono disponibili nella [guida al recupero dei batch non riusciti](../quality/retrieve-failed-batches.md).

### Righe non analizzabili {#unparsable}

Se il batch acquisito ha righe non analizzabili, puoi utilizzare la seguente richiesta per visualizzare un elenco di file che contengono errori.

**Formato API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | Valore `id` del batch da cui si stanno recuperando le informazioni sull&#39;errore. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco dei file che presentano errori.

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

È quindi possibile recuperare informazioni dettagliate sugli errori utilizzando l&#39;[endpoint di recupero diagnostica](#retrieve-diagnostics).

Di seguito è riportato un esempio di risposta relativa al recupero del file di errore:

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
