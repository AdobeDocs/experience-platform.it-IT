---
keywords: ' Experience Platform;home;argomenti popolari;inserimento batch;inserimento batch;assimilazione parziale;inserimento parziale;recupero errori;recupero errori;recupero errori;recupero errori;inserimento parziale batch;parziale;inserimento batch;parziale;inserimento;inserimento;ingestione;diagnosi errore;recupero diagnostica errori;ottenere errori diagnostici;ottenere errori;ottenere errori;ottenere errori;recuperare errori;'
solution: Experience Platform
title: Recupero della diagnostica degli errori di inserimento dati
topic: overview
description: Questo documento fornisce informazioni sul monitoraggio dell’inserimento batch, sulla gestione degli errori di inserimento batch parziale e un riferimento per i tipi di inserimento batch parziale.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 2%

---


# Recupero della diagnostica degli errori di caricamento dei dati

Adobe Experience Platform offre due metodi per caricare e acquisire i dati. Potete utilizzare l&#39;assimilazione batch, che consente di inserire i dati utilizzando vari tipi di file (come i CSV), oppure l&#39;assimilazione in streaming, che consente di inserire i dati in [!DNL Platform] utilizzando gli endpoint in streaming in tempo reale.

Questo documento fornisce informazioni sul monitoraggio dell’inserimento batch, sulla gestione degli errori di inserimento batch parziale e un riferimento per i tipi di inserimento batch parziale.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md): I metodi con cui i dati possono essere inviati  [!DNL Experience Platform].

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

## Download della diagnostica degli errori {#download-diagnostics}

Adobe Experience Platform consente agli utenti di scaricare la diagnostica degli errori dei file di input. La diagnostica verrà mantenuta entro [!DNL Platform] per un massimo di 30 giorni.

### Elenca i file di input {#list-files}

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituirà gli oggetti JSON con dettagli sulla posizione di salvataggio della diagnostica.

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

### Recupero della diagnostica dei file di input {#retrieve-diagnostics}

Una volta recuperato un elenco di tutti i diversi file di input, è possibile recuperare la diagnostica del singolo file utilizzando la richiesta seguente.

**Formato API**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch che stai cercando. |
| `{FILE}` | Il nome del file a cui si accede. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituirà oggetti JSON contenenti oggetti `path` con dettagli su dove sono state salvate le operazioni di diagnostica. La risposta restituirà gli oggetti `path` in formato [JSON Lines](https://jsonlines.org/).

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Recupera errori di inserimento batch {#retrieve-errors}

Se i batch contengono errori, è necessario recuperare le informazioni di errore relative a tali errori in modo da poter nuovamente assimilare i dati.

### Verifica stato {#check-status}

Per verificare lo stato del batch assimilato, dovete fornire l&#39;ID del batch nel percorso di una richiesta di GET.

**Formato API**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | Il valore `id` del batch di cui si desidera controllare lo stato. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta senza errori**

Una risposta corretta restituisce informazioni dettagliate sullo stato del batch.

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
        "imsOrg": "{IMS_ORG}",
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
| `metrics.failedRecordCount` | Numero di righe che non è stato possibile elaborare a causa di analisi, conversione o convalida. Questo valore può essere derivato sottraendo la `inputRecordCount` dalla `outputRecordCount`. Questo valore viene generato su tutti i batch, indipendentemente dal fatto che `errorDiagnostics` sia attivato. |

**Risposta con errori**

Se il batch presenta uno o più errori e la diagnostica degli errori è abilitata, la risposta restituisce ulteriori informazioni sugli errori, sia all&#39;interno del payload stesso che in un file di errore scaricabile. Lo stato di un batch contenente errori potrebbe avere ancora uno stato di successo.

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
        "imsOrg": "{IMS_ORG}",
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
| `metrics.failedRecordCount` | Numero di righe che non è stato possibile elaborare a causa di analisi, conversione o convalida. Questo valore può essere derivato sottraendo la `inputRecordCount` dalla `outputRecordCount`. Questo valore viene generato su tutti i batch, indipendentemente dal fatto che `errorDiagnostics` sia attivato. |
| `errors.recordCount` | Il numero di righe che non sono riuscite per il codice di errore specificato. Questo valore è generato **solo** se è abilitato `errorDiagnostics`. |

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

Questa esercitazione ha descritto come monitorare gli errori di caricamento batch parziale. Per ulteriori informazioni sull&#39;assimilazione batch, leggere la [guida per gli sviluppatori di assimilazione batch](../batch-ingestion/api-overview.md).

## Appendice {#appendix}

Questa sezione fornisce informazioni supplementari sui tipi di errori di assimilazione.

### Tipi di errore di assimilazione parziale dei batch {#partial-ingestion-types}

L’assimilazione parziale dei batch presenta tre tipi di errore diversi durante l’assimilazione dei dati:

- [File illeggibili](#unreadable)
- [Schemi o intestazioni non validi](#schemas-headers)
- [Righe non analizzabili](#unparsable)

### File non leggibili {#unreadable}

Se il batch ingerito contiene file illeggibili, gli errori del batch verranno allegati al batch stesso. Ulteriori informazioni sul recupero del batch non riuscito sono disponibili nella [guida per il recupero dei batch non riusciti](../quality/retrieve-failed-batches.md).

### Schemi o intestazioni non validi {#schemas-headers}

Se lo schema del batch ingerito non è valido o le intestazioni non sono valide, gli errori del batch verranno collegati al batch stesso. Ulteriori informazioni sul recupero del batch non riuscito sono disponibili nella [guida per il recupero dei batch non riusciti](../quality/retrieve-failed-batches.md).

### Righe non analizzabili {#unparsable}

Se il batch che hai acquisito contiene righe non analizzabili, puoi utilizzare la seguente richiesta per visualizzare un elenco di file contenenti errori.

**Formato API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | Il valore `id` del batch da cui si recuperano le informazioni sull&#39;errore. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco dei file con errori.

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

È quindi possibile recuperare informazioni dettagliate sugli errori utilizzando l&#39;endpoint di recupero [diagnostica](#retrieve-diagnostics).

Di seguito è riportato un esempio di risposta al recupero del file di errore:

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
