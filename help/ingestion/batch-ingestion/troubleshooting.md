---
keywords: Experience Platform;home;argomenti popolari;dati acquisiti;risoluzione dei problemi;faq;acquisizione;inserimento batch;inserimento batch;
solution: Experience Platform
title: Guida alla risoluzione dei problemi di acquisizione in batch
description: Questa documentazione sarà utile per rispondere alle domande frequenti sulle API di acquisizione dati in batch di Adobe Experience Platform.
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: 37b241f15f297263cc7aa20f382c115a2d131c7e
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 1%

---

# Guida alla risoluzione dei problemi di acquisizione in batch

Questa documentazione consente di rispondere alle domande frequenti relative alle API [!DNL Batch Data Ingestion] di Adobe Experience Platform.

## Chiamate API batch

### I batch sono immediatamente attivi dopo aver ricevuto un OK HTTP 200 dall’API CompleteBatch?

La risposta `200 OK` dell&#39;API indica che il batch è stato accettato per l&#39;elaborazione. Non è attivo finché non passa al suo stato finale, ad esempio Attivo o Non riuscito.

### È sicuro riprovare la chiamata API CompleteBatch dopo l’errore?

Sì, è possibile riprovare la chiamata API. Nonostante l’errore, è possibile che l’operazione sia riuscita e che il batch sia stato accettato correttamente. Tuttavia, i client devono disporre di meccanismi di esecuzione di nuovi tentativi in caso di errore API e sono, di fatto, incoraggiati a riprovare. Se l’operazione è riuscita, l’API restituirà il successo anche dopo un nuovo tentativo.

### Quando deve essere utilizzata l’API di caricamento file di grandi dimensioni?

La dimensione del file consigliata per l’utilizzo dell’API di caricamento file di grandi dimensioni è pari o superiore a 256 MB. Ulteriori informazioni sull&#39;utilizzo dell&#39;API di caricamento file di grandi dimensioni sono disponibili [qui](./api-overview.md#ingest-large-parquet-files).

### Perché la chiamata API Large File Complete non riesce?

Se vengono trovati blocchi di un file di grandi dimensioni sovrapposti o mancanti, il server risponde con una richiesta HTTP 400 non valida. Ciò può verificarsi perché è possibile caricare blocchi sovrapposti, poiché le convalide degli intervalli vengono eseguite al momento del completamento del file, quando i blocchi di file vengono uniti tra loro.

## Supporto acquisizione

### Quali sono i formati di acquisizione supportati?

Attualmente, sono supportati sia Parquet che JSON. Il file CSV è supportato da versioni precedenti: anche se i dati verranno promossi a master e verranno eseguiti controlli preliminari, non saranno supportate funzioni moderne come la conversione, il partizionamento o la convalida delle righe.

### Specificare il formato di input batch

Il formato di input deve essere specificato al momento della creazione del batch all’interno del payload. Di seguito è riportato un esempio di come specificare il formato di input batch:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Perché i dati caricati non vengono visualizzati nel set di dati?

Affinché i dati vengano visualizzati nel set di dati, il batch deve essere contrassegnato come completo. Tutti i file che desideri acquisire devono essere caricati prima di contrassegnare il batch come completato. Di seguito è riportato un esempio di contrassegno di completamento di un batch:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Come viene acquisito il JSON su più righe?

Per acquisire il JSON su più righe, il flag `isMultiLineJson` deve essere impostato al momento della creazione batch. Di seguito è riportato un esempio:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### Qual è la differenza tra righe JSON (JSON a riga singola) e JSON su più righe?

Per le righe JSON, esiste un oggetto JSON per riga. Ad esempio:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Per il JSON su più righe, un oggetto può occupare più righe, mentre tutti gli oggetti sono racchiusi in un array JSON. Ad esempio:

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

Per impostazione predefinita, [!DNL Batch Data Ingestion] utilizza JSON a riga singola.

### L’acquisizione CSV è supportata?

L’acquisizione CSV è supportata solo per gli schemi flat. Attualmente, l’acquisizione di dati gerarchici in CSV non è supportata.

Per ottenere tutte le funzioni di acquisizione dei dati, è necessario utilizzare i formati JSON o Parquet.

### Quali tipi di convalida vengono eseguiti sui dati?

Esistono tre livelli di convalida eseguiti sui dati:

- Schema: l’acquisizione in batch garantisce che lo schema del dei dati acquisiti corrisponda allo schema del set di dati.
- Tipo di dati: l’acquisizione in batch assicura che il tipo di ogni campo acquisito corrisponda al tipo definito nello schema del set di dati.
- Vincoli: l’acquisizione in batch garantisce che i vincoli, come &quot;Obbligatorio&quot;, &quot;enum&quot; e &quot;formato&quot;, siano definiti correttamente nella definizione dello schema.

### Come può essere sostituito un batch già acquisito?

Un batch già acquisito può essere sostituito utilizzando la funzione Ripetizione batch. Ulteriori informazioni sulla ripetizione batch sono disponibili [qui](./api-overview.md#replay-a-batch).

### Come viene monitorata l’acquisizione batch?

Una volta segnalato un batch per la promozione batch, l’avanzamento dell’acquisizione batch può essere monitorato con la seguente richiesta:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Con questa richiesta, riceverai una risposta simile alla seguente:

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{ORG_ID}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## Stati batch

### Quali sono i possibili stati del batch?

Un batch può, nel suo ciclo di vita, passare attraverso i seguenti stati:

| Stato | Dati scritti nel master | Descrizione |
| ------ | ---------------------- | ----------- |
| Abbandonato | | Il client non è riuscito a completare il batch nel periodo di tempo previsto. |
| Interrotto | | Il client ha chiamato esplicitamente, tramite le API [!DNL Batch Data Ingestion], un&#39;operazione di interruzione per il batch specificato. Una volta che un batch è nello stato Loaded, non può essere interrotto. |
| Attivo/Completato | x | Il batch è stato promosso correttamente dall’ambiente di staging a quello principale ed è ora disponibile per il consumo a valle. **Nota:** Attivo e Completato sono utilizzati in modo intercambiabile. |
| Archiviato | | Il batch è stato archiviato in un magazzino frigorifero. |
| Non riuscito/non riuscito | | Stato del terminale causato da configurazione e/o dati non validi. Viene registrato un errore actionable, insieme al batch, per consentire ai client di correggere e inviare nuovamente i dati. **Nota:** errore e errore sono utilizzati in modo intercambiabile. |
| Non attivo | x | Il batch è stato promosso correttamente, ma è stato ripristinato o è scaduto. Il batch non sarà più disponibile per il consumo a valle, ma i dati sottostanti rimarranno nel master fino a quando non saranno stati conservati, archiviati o altrimenti eliminati. |
| Caricamento in corso | | Il client sta scrivendo dati per il batch. Il batch è **non** pronto per la promozione, al momento. |
| Caricato | | Il client ha completato la scrittura dei dati per il batch. Il batch è pronto per la promozione. |
| Mantenuto | | I dati sono stati estratti dal Master e in un archivio designato nel Data Lake Adobe. |
| Staging | | Il client ha segnalato correttamente il batch per la promozione e i dati vengono posizionati nell&#39;area intermedia per il consumo a valle. |
| Nuovo tentativo | | Il client ha segnalato il batch per la promozione, ma a causa di un errore il batch viene ritentato da un servizio di monitoraggio batch. Questo stato può essere utilizzato per informare i client che potrebbe verificarsi un ritardo nell’acquisizione dei dati. |
| Bloccato | | Il client ha segnalato il batch per la promozione, ma dopo `n` nuovi tentativi da parte di un servizio di monitoraggio batch, la promozione batch è stata arrestata. |

### Cosa significa &quot;Staging&quot; per i batch?

Quando un batch si trova in &quot;Staging&quot;, significa che il batch è stato segnalato correttamente per la promozione e che i dati vengono posizionati nell’area intermedia per il consumo a valle.

### Che cosa significa quando un batch è &quot;Nuovo tentativo&quot;?

Quando un batch è in &quot;Nuovo tentativo&quot;, significa che l’acquisizione dei dati del batch è stata temporaneamente interrotta a causa di problemi intermittenti. Quando ciò accade, non richiede l’intervento del cliente.

### Cosa significa quando un batch è &quot;Bloccato&quot;?

Quando un batch si trova in &quot;Stalled&quot;, significa che [!DNL Data Ingestion Services] ha difficoltà a acquisirlo e che tutti i tentativi sono stati esauriti.

### Cosa significa se un batch è ancora in fase di &quot;caricamento&quot;?

Quando un batch si trova in &quot;Caricamento&quot;, significa che l’API CompleteBatch non è stata chiamata per promuovere il batch.

### Esiste un modo per sapere se un batch è stato acquisito correttamente?

Sì, una volta che lo stato del batch è &quot;Attivo&quot;, il batch è stato correttamente acquisito. Per conoscere lo stato del batch, segui i passaggi dettagliati [precedenti](#how-is-batch-ingestion-monitored).

### Cosa succede in caso di errore di un batch? {#what-if-a-batch-fails}

Quando un batch non riesce, il processo si arresta e restituisce lo stato `Failure`. Il motivo dell&#39;errore può essere identificato nella sezione `errors` del payload. Di seguito sono riportati alcuni esempi di errori:

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

Una volta corretti gli errori, il batch può essere ricaricato.

## Supporto batch

### Come eliminare i batch?

Anziché eliminare direttamente da [!DNL Catalog], è necessario rimuovere i batch utilizzando uno dei metodi seguenti:

1. Se il batch è in corso, deve essere interrotto.
2. Se la masterizzazione del batch è riuscita, il batch deve essere ripristinato.

### Quali metriche a livello di batch sono disponibili?

Per i batch in stato Attivo/Completato sono disponibili le seguenti metriche a livello di batch:

| Metrica | Descrizione |
| ------ | ----------- |
| inputByteSize | Numero totale di byte posizionati nell&#39;area intermedia per [!DNL Data Ingestion Services] da elaborare. |
| inputRecordSize | Numero totale di righe posizionate nell&#39;area intermedia per [!DNL Data Ingestion Services] da elaborare. |
| outputByteSize | Numero totale di byte restituiti da [!DNL Data Ingestion Services] a [!DNL Data Lake]. |
| outputRecordSize | Numero totale di righe elaborate da [!DNL Data Ingestion Services] in [!DNL Data Lake]. |
| partitionCount | Numero totale di partizioni scritte in [!DNL Data Lake]. |

### Perché le metriche non sono disponibili in alcuni batch?

Esistono due motivi per cui le metriche potrebbero non essere disponibili nel batch:

1. Il batch non è mai stato portato allo stato Attivo/Completato.
2. Il batch è stato promosso utilizzando un percorso di promozione legacy, ad esempio l’acquisizione CSV.

### Cosa significano i diversi codici di stato?

| Codice di stato | Descrizione |
| ----------- | ----------- |
| 106 | Il file del set di dati è vuoto. |
| 118 | Il file CSV contiene una riga di intestazione vuota. |
| 200 | Il batch è stato accettato per l’elaborazione e passerà a uno stato finale, ad esempio Attivo o Non riuscito. Una volta inviato, il batch può essere monitorato utilizzando l&#39;endpoint `GetBatch`. |
| 400 | Richiesta non valida. Restituito se in un batch sono presenti blocchi mancanti o sovrapposti. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
