---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sull’assimilazione parziale di Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---



# Iniezione parziale del batch

L&#39;assimilazione parziale dei batch è la capacità di assimilare i dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono trasferire con successo tutti i dati corretti in Adobe Experience Platform mentre tutti i dati errati vengono inseriti in batch separatamente, insieme ai dettagli sul motivo per cui non sono validi.

Questo documento fornisce un’esercitazione per la gestione dell’assimilazione parziale dei batch.

Inoltre, l&#39; [appendice](#partial-batch-ingestion-error-types) di questa esercitazione fornisce un riferimento per i tipi di errori di caricamento batch parziale.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei diversi servizi Adobe Experience Platform coinvolti nell&#39;assimilazione parziale dei batch. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Caricamento](./overview.md)batch: Il metodo che la piattaforma acquisisce e memorizza i dati dai file di dati, come CSV e Parquet.
- [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API della piattaforma.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Per ulteriori informazioni sulle sandbox in Piattaforma, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

## Abilitare un set di dati per l&#39;assimilazione parziale dei batch nell&#39;API

>[!NOTE] Questa sezione descrive come abilitare un dataset per l&#39;assimilazione parziale dei batch utilizzando l&#39;API. Per istruzioni sull’utilizzo dell’interfaccia utente, leggete il passaggio [Abilita un set di dati per l’inserimento parziale dei batch nel passaggio dell’interfaccia utente](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) .

È possibile creare un nuovo set di dati o modificare un set di dati esistente con l&#39;inserimento parziale abilitato.

Per creare un nuovo set di dati, seguite i passaggi descritti nell&#39;esercitazione [sulla](../../catalog/api/create-dataset.md)creazione di un set di dati. Una volta raggiunto il passaggio *Crea un dataset* , aggiungi il seguente campo all’interno del corpo della richiesta:

```json
{
    ...
    "tags" : {
        "partialBatchIngestion":["errorThresholdPercentage:5"]
    },
    ...
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `errorThresholdPercentage` | Percentuale di errori accettabili prima che l&#39;intero batch non riesca. |

Analogamente, per modificare un dataset esistente, seguite i passaggi descritti nella guida [per gli sviluppatori del](../../catalog/api/update-object.md)catalogo.

All&#39;interno del set di dati, dovrete aggiungere il tag descritto in precedenza.

## Abilitare un set di dati per l’assimilazione parziale dei batch nell’interfaccia utente

>[!NOTE] Questa sezione descrive come abilitare un dataset per l’assimilazione parziale dei batch utilizzando l’interfaccia utente. Se hai già attivato un dataset per l&#39;assimilazione parziale dei batch utilizzando l&#39;API, puoi passare alla sezione successiva.

Per abilitare un dataset per l&#39;assimilazione parziale tramite l&#39;interfaccia utente della piattaforma, fai clic su **Set** di dati nella sezione di navigazione a sinistra. È possibile [creare un nuovo dataset](#create-a-new-dataset-with-partial-batch-ingestion-enabled) o [modificare un dataset](#modify-an-existing-dataset-to-enable-partial-batch-ingestion)esistente.

### Creare un nuovo dataset con l&#39;inserimento batch parziale abilitato

Per creare un nuovo dataset, segui i passaggi descritti nella guida [utente del](../../catalog/datasets/user-guide.md)dataset. Una volta raggiunto il passaggio *Configura set di dati* , prendete nota dei campi *Ingestione* parziale e Diagnostica ** errori.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

L’ *opzione di inserimento* parziale consente di attivare o disattivare l’uso dell’inserimento parziale dei batch.

L&#39;interruttore *Diagnostica* errori viene visualizzato solo quando l&#39; *interruttore di inserimento* parziale è disattivato. Questa funzione consente alla piattaforma di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;opzione *Ingestione* parziale è attivata, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

La soglia *di* errore consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

### Modificare un dataset esistente per abilitare l&#39;assimilazione parziale dei batch

Per modificare un set di dati esistente, selezionare il set di dati da modificare. La barra laterale a destra include informazioni sul set di dati.

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

L’ *opzione di inserimento* parziale consente di attivare o disattivare l’uso dell’inserimento parziale dei batch.

La soglia *di* errore consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

## Recupero degli errori di caricamento batch parziale

Se i batch contengono errori, sarà necessario recuperare le informazioni di errore relative a tali errori in modo da poter nuovamente assimilare i dati.

### Verifica stato

Per verificare lo stato del batch assimilato, dovete fornire l&#39;ID del batch nel percorso di una richiesta GET.

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

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sullo stato del batch.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
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
            "outputRecordCount": 497
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

Se il batch presenta un errore e la diagnostica degli errori è abilitata, lo stato sarà &quot;success&quot; con ulteriori informazioni sull&#39;errore fornito in un file di errore scaricabile.

## Passaggi successivi

In questa esercitazione è stato illustrato come creare o modificare un dataset per abilitare l’assimilazione parziale dei batch. Per ulteriori informazioni sull&#39;assimilazione batch, leggere la guida [per gli sviluppatori di](./api-overview.md)inserimento batch.

## Tipi di errori di assimilazione parziale dei batch

L’assimilazione parziale dei batch presenta quattro tipi di errore diversi durante l’assimilazione dei dati.

- [File illeggibili](#unreadable)
- [Schemi o intestazioni non validi](#schemas-headers)
- [Righe non analizzabili](#unparsable)
- [Conversione XDM non valida](#conversion)

### File illeggibili {#unreadable}

Se il batch ingerito contiene file illeggibili, gli errori del batch verranno allegati al batch stesso. Ulteriori informazioni sul recupero del batch non riuscito sono disponibili nella guida [al](../quality/retrieve-failed-batches.md)recupero dei batch non riusciti.

### Schemi o intestazioni non validi {#schemas-headers}

Se lo schema del batch ingerito non è valido o le intestazioni non sono valide, gli errori del batch verranno collegati al batch stesso. Ulteriori informazioni sul recupero del batch non riuscito sono disponibili nella guida [al](../quality/retrieve-failed-batches.md)recupero dei batch non riusciti.

### Righe non analizzabili {#unparsable}

Se il batch ingerito contiene righe non analizzabili, gli errori del batch verranno memorizzati in un file a cui è possibile accedere utilizzando l&#39;endpoint indicato di seguito.

**Formato API**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | Il `id` valore del batch da cui si recuperano le informazioni sull&#39;errore. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli delle righe non analizzabili.

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### Conversione XDM non valida {#conversion}

Se il batch ingerito contiene conversioni XDM non valide, gli errori del batch verranno memorizzati in un file a cui è possibile accedere utilizzando il seguente endpoint.

**Formato API**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | Il `id` valore del batch da cui si recuperano le informazioni sull&#39;errore. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con dettagli sugli errori di conversione XDM.

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```
