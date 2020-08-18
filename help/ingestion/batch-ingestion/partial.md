---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sull’assimilazione parziale di Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: ac75b1858b6a731915bbc698107f0be6043267d8
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 1%

---



# Iniezione parziale del batch

L&#39;assimilazione parziale dei batch è la capacità di assimilare i dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono trasferire correttamente tutti i dati corretti in Adobe Experience Platform mentre tutti i dati errati vengono raggruppati separatamente, insieme ai dettagli sul motivo per cui non sono validi.

Questo documento fornisce un’esercitazione per la gestione dell’assimilazione parziale dei batch.

Inoltre, l&#39; [appendice](#appendix) di questa esercitazione fornisce un riferimento per i tipi di errori di caricamento batch parziale.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei diversi servizi Adobe Experience Platform coinvolti nell&#39;assimilazione parziale dei batch. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Caricamento](./overview.md)batch: Metodo che [!DNL Platform] raccoglie e memorizza i dati dai file di dati, come CSV e Parquet.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate alle [!DNL Platform] API.

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

## Abilitare un batch per l&#39;assimilazione parziale dei batch nell&#39;API {#enable-api}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l&#39;assimilazione parziale dei batch mediante l&#39;API. Per istruzioni sull’utilizzo dell’interfaccia utente, leggete il passaggio [Abilita batch per l’inserimento parziale dei batch nell’interfaccia utente](#enable-ui) .

Potete creare un nuovo batch con l’assimilazione parziale abilitata.

Per creare un nuovo batch, segui i passaggi descritti nella guida [per gli sviluppatori per l’assimilazione](./api-overview.md)batch. Una volta raggiunto il **[!UICONTROL Create batch]** passaggio, aggiungete il seguente campo all’interno del corpo della richiesta:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `enableErrorDiagnostics` | Flag che consente [!DNL Platform] di generare messaggi di errore dettagliati sul batch. |
| `partialIngestionPercentage` | Percentuale di errori accettabili prima che l&#39;intero batch non riesca. Quindi, in questo esempio, un massimo del 5% del batch può essere costituito da errori, prima che venga meno. |


## Abilitare un batch per l’assimilazione parziale dei batch nell’interfaccia utente {#enable-ui}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l’assimilazione parziale dei batch utilizzando l’interfaccia utente. Se avete già attivato un batch per l&#39;assimilazione parziale dei batch utilizzando l&#39;API, potete passare alla sezione successiva.

Per abilitare un batch per l’assimilazione parziale nell’ [!DNL Platform] interfaccia utente, potete creare un nuovo batch tramite connessioni sorgente, creare un nuovo batch in un set di dati esistente o creare un nuovo batch tramite il[!UICONTROL Map CSV to XDM flow]&quot;.

### Creare una nuova connessione di origine {#new-source}

Per creare una nuova connessione di origine, segui i passaggi elencati nella panoramica [](../../sources/home.md)Origini. Una volta raggiunto il **[!UICONTROL Dataflow detail]** passaggio, prendete nota dei **[!UICONTROL Partial ingestion]** campi e **[!UICONTROL Error diagnostics]** .

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

L’ **[!UICONTROL Partial ingestion]** interruttore consente di attivare o disattivare l’inserimento parziale dei batch.

L&#39; **[!UICONTROL Error diagnostics]** interruttore viene visualizzato solo quando l&#39; **[!UICONTROL Partial ingestion]** interruttore è disattivato. Questa funzione consente [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39; *[!UICONTROL Partial ingestion]* interruttore è attivato, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Consente di **[!UICONTROL Error threshold]** impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

### Utilizzare un dataset esistente {#existing-dataset}

Per utilizzare un set di dati esistente, iniziare selezionando un set di dati. La barra laterale a destra include informazioni sul set di dati.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

L’ **[!UICONTROL Partial ingestion]** interruttore consente di attivare o disattivare l’inserimento parziale dei batch.

L&#39; **[!UICONTROL Error diagnostics]** interruttore viene visualizzato solo quando l&#39; **[!UICONTROL Partial ingestion]** interruttore è disattivato. Questa funzione consente [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39; **[!UICONTROL Partial ingestion]** interruttore è attivato, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Consente di **[!UICONTROL Error threshold]** impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

Ora puoi caricare i dati tramite il pulsante **Aggiungi dati** e li assimilerai parzialmente.

### Utilizzare il flusso &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Per usare il flusso[!UICONTROL Map CSV to XDM schema]&quot;di prova&quot;, segui i passaggi elencati nell’esercitazione [Mappa un file CSV](../tutorials/map-a-csv-file.md). Una volta raggiunto il **[!UICONTROL Add data]** passaggio, prendete nota dei **[!UICONTROL Partial ingestion]** campi e **[!UICONTROL Error diagnostics]** .

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

L’ **[!UICONTROL Partial ingestion]** interruttore consente di attivare o disattivare l’inserimento parziale dei batch.

L&#39; **[!UICONTROL Error diagnostics]** interruttore viene visualizzato solo quando l&#39; **[!UICONTROL Partial ingestion]** interruttore è disattivato. Questa funzione consente [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39; **[!UICONTROL Partial ingestion]** interruttore è attivato, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Consente di **[!UICONTROL Error threshold]** impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

## Download dei metadati a livello di file {#download-metadata}

Adobe Experience Platform consente agli utenti di scaricare i metadati dei file di input. I metadati verranno conservati entro [!DNL Platform] un massimo di 30 giorni.

### Elenca i file di input {#list-files}

La seguente richiesta consente di visualizzare un elenco di tutti i file forniti in un batch finalizzato.

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituirà lo stato HTTP 200 con oggetti JSON contenenti oggetti percorso con dettagli sulla posizione in cui sono stati salvati i metadati.

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
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Recupero dei metadati del file di input {#retrieve-metadata}

Dopo aver recuperato un elenco di tutti i diversi file di input, potete recuperare i metadati del singolo file utilizzando il seguente endpoint.

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituirà lo stato HTTP 200 con oggetti JSON contenenti oggetti percorso con dettagli sulla posizione in cui sono stati salvati i metadati.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Recupero degli errori di caricamento batch parziale {#retrieve-errors}

Se i batch contengono errori, sarà necessario recuperare le informazioni di errore relative a tali errori in modo da poter nuovamente assimilare i dati.

### Verifica stato {#check-status}

Per verificare lo stato del batch assimilato, dovete fornire l&#39;ID del batch nel percorso di una richiesta di GET.

**Formato API**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | Il `id` valore del batch di cui si desidera controllare lo stato. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta senza errori**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sullo stato del batch.

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
| `metrics.failedRecordCount` | Numero di righe che non è stato possibile elaborare a causa di analisi, conversione o convalida. Questo valore può essere derivato sottraendo il `inputRecordCount` dal `outputRecordCount`. Questo valore verrà generato su tutti i batch, indipendentemente dal fatto che `errorDiagnostics` sia attivato. |

**Risposta con errori**

Se il batch presenta uno o più errori e la diagnostica degli errori è abilitata, lo stato sarà `success` con ulteriori informazioni sugli errori forniti sia all&#39;interno della risposta che in un file di errore scaricabile.

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
| `metrics.failedRecordCount` | Numero di righe che non è stato possibile elaborare a causa di analisi, conversione o convalida. Questo valore può essere derivato sottraendo il `inputRecordCount` dal `outputRecordCount`. Questo valore verrà generato su tutti i batch, indipendentemente dal fatto che `errorDiagnostics` sia attivato. |
| `errors.recordCount` | Il numero di righe che non sono riuscite per il codice di errore specificato. Questo valore viene generato **solo** se `errorDiagnostics` è attivato. |

>[!NOTE]
>
>Se la diagnostica degli errori non è disponibile, verrà visualizzato il seguente messaggio di errore:
> 
```json
> {
>         "errors": [{
>                 "code": "INGEST-1211-400",
>                 "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>         }]
> }
> ```

## Passaggi successivi {#next-steps}

In questa esercitazione è stato illustrato come creare o modificare un dataset per abilitare l’assimilazione parziale dei batch. Per ulteriori informazioni sull&#39;assimilazione batch, leggere la guida [per gli sviluppatori di](./api-overview.md)inserimento batch.

## Tipi di errori di assimilazione parziale dei batch {#appendix}

L’assimilazione parziale dei batch presenta tre tipi di errore diversi durante l’assimilazione dei dati.

- [File illeggibili](#unreadable)
- [Schemi o intestazioni non validi](#schemas-headers)
- [Righe non analizzabili](#unparsable)

### File illeggibili {#unreadable}

Se il batch ingerito contiene file illeggibili, gli errori del batch verranno allegati al batch stesso. Ulteriori informazioni sul recupero del batch non riuscito sono disponibili nella guida [al](../quality/retrieve-failed-batches.md)recupero dei batch non riusciti.

### Schemi o intestazioni non validi {#schemas-headers}

Se lo schema del batch ingerito non è valido o le intestazioni non sono valide, gli errori del batch verranno collegati al batch stesso. Ulteriori informazioni sul recupero del batch non riuscito sono disponibili nella guida [al](../quality/retrieve-failed-batches.md)recupero dei batch non riusciti.

### Righe non analizzabili {#unparsable}

Se il batch che hai acquisito contiene righe non analizzabili, puoi utilizzare il seguente endpoint per visualizzare un elenco di file che contengono errori.

**Formato API**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | Il `id` valore del batch da cui si recuperano le informazioni sull&#39;errore. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco dei file con errori.

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

Potete quindi recuperare informazioni dettagliate sugli errori utilizzando l’endpoint [di recupero](#retrieve-metadata)dei metadati.

Di seguito è riportato un esempio di risposta al recupero del file di errore:

```json
{
    "_corrupt_record": "{missingQuotes: "v1"}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
