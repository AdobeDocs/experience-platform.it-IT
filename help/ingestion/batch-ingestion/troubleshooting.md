---
keywords: Experience Platform;home;argomenti comuni;dati acquisiti;risoluzione dei problemi;FAQ;acquisizione;inserimento batch;acquisizione batch;
solution: Experience Platform
title: Guida alla risoluzione dei problemi di acquisizione in batch
topic-legacy: troubleshooting
description: Questa documentazione risponderà alle domande frequenti relative alle API di acquisizione di dati in batch di Adobe Experience Platform.
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# Guida alla risoluzione dei problemi di inserimento in batch

Questa documentazione è utile per rispondere alle domande frequenti su Adobe Experience Platform [!DNL Batch Data Ingestion] API.

## Chiamate API in batch

### I batch sono attivi immediatamente dopo aver ricevuto un OK HTTP 200 dall’API CompleteBatch?

La `200 OK` la risposta dell’API indica che il batch è stato accettato per l’elaborazione e non è attivo fino al passaggio al suo stato finale, ad esempio Attivo o Errore.

### È sicuro riprovare la chiamata API CompleteBatch dopo l&#39;errore?

Sì: puoi riprovare la chiamata API. Nonostante il guasto, è possibile che l&#39;operazione sia riuscita effettivamente e il batch è stato accettato con successo. Tuttavia, i client devono disporre di meccanismi per l’esecuzione di nuovi tentativi in caso di errore dell’API e, di fatto, devono riprovare. Se l’operazione ha avuto successo, l’API restituisce il successo, anche dopo un nuovo tentativo.

### Quando deve essere utilizzata l’API di caricamento file di grandi dimensioni?

La dimensione file consigliata per l’utilizzo dell’API per il caricamento di file di grandi dimensioni è pari o superiore a 256 MB. Per ulteriori informazioni sull’utilizzo dell’API di caricamento file di grandi dimensioni, consulta [qui](./api-overview.md#ingest-large-parquet-files).

### Perché la chiamata API Large File Complete non riesce?

Se vengono trovati blocchi di un file di grandi dimensioni sovrapposti o mancanti, il server risponde con una richiesta HTTP 400 Bad. Questo può verificarsi perché è possibile caricare blocchi sovrapposti, poiché le convalide degli intervalli vengono eseguite al momento del completamento del file, quando i blocchi di file sono uniti.

## Supporto per l’acquisizione

### Quali sono i formati di acquisizione supportati?

Attualmente, sono supportati sia Parquet che JSON. Il CSV è supportato su base legacy; i dati verranno promossi a master e verranno eseguiti controlli preliminari; non saranno supportate funzioni moderne, ad esempio conversione, partizionamento o convalida delle righe.

### Dove specificare il formato di input batch?

Il formato di input deve essere specificato al momento della creazione del batch all&#39;interno del payload. Di seguito è riportato un esempio di come specificare il formato di input batch:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
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

Affinché i dati vengano visualizzati nel set di dati, il batch deve essere contrassegnato come completo. Tutti i file da acquisire devono essere caricati prima di contrassegnare il batch come completo. Di seguito è riportato un esempio di marcatura completa di un batch:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Come viene acquisito JSON multi-riga?

Per acquisire JSON con più righe, l’ `isMultiLineJson` Il flag deve essere impostato al momento della creazione del batch. Di seguito è riportato un esempio:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
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

### Qual è la differenza tra le righe JSON (JSON a riga singola) e JSON a riga singola?

Per le righe JSON esiste un oggetto JSON per riga. Esempio:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Per JSON su più righe, un oggetto può occupare più righe, mentre tutti gli oggetti sono racchiusi in un array JSON. Esempio:

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

L’acquisizione CSV è supportata solo per gli schemi piatti. Al momento, l’acquisizione di dati gerarchici in CSV non è supportata.

Per ottenere tutte le funzioni di acquisizione dei dati, è necessario utilizzare i formati JSON o Parquet.

### Quali tipi di convalida vengono eseguiti sui dati?

I dati vengono convalidati in tre livelli:

- Schema: l’acquisizione in batch assicura che lo schema dei dati acquisiti corrisponda allo schema del set di dati.
- Tipo di dati : l’acquisizione in batch assicura che il tipo per ciascun campo acquisito corrisponda al tipo definito nello schema del set di dati.
- Vincoli: l’acquisizione in batch assicura che i vincoli, come &quot;Obbligatorio&quot;, &quot;enum&quot; e &quot;formato&quot;, siano definiti correttamente nella definizione dello schema.

### Come può essere sostituito un batch già acquisito?

È possibile sostituire un batch già acquisito utilizzando la funzione Riproduzione batch. Ulteriori informazioni sulla riproduzione in batch sono disponibili [qui](./api-overview.md#replay-a-batch).

### Come viene monitorata l’acquisizione batch?

Una volta che un batch è stato segnalato per la promozione batch, l&#39;avanzamento dell&#39;acquisizione batch può essere monitorato con la seguente richiesta:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Con questa richiesta riceverai una risposta simile a questa:

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
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

### Quali sono i possibili stati batch?

Un batch può, nel suo ciclo di vita, superare i seguenti stati:

| Stato | Dati scritti sul master | Descrizione |
| ------ | ---------------------- | ----------- |
| Abbandonato |  | Il client non è riuscito a completare il batch nell&#39;intervallo di tempo previsto. |
| Interrotto |  | Il client ha esplicitamente chiamato tramite il [!DNL Batch Data Ingestion] API, un’operazione di interruzione per il batch specificato. Una volta che un batch è nello stato caricato, il batch non può essere interrotto. |
| Attivo/Completato | x | Il batch è stato promosso con successo da stage a master ed è ora disponibile per il consumo a valle. **Nota:** Le opzioni Attivo e Successo vengono utilizzate in modo intercambiabile. |
| Archiviato |  | Il lotto è stato archiviato in deposito frigorifero. |
| Non riuscito/Errore |  | Stato terminale che risulta da una configurazione errata e/o da dati non validi. Viene registrato un errore actionable insieme al batch, per consentire ai client di correggere e reinviare i dati. **Nota:** Con errore e con errore vengono utilizzati in modo intercambiabile. |
| Inattivo | x | La promozione del batch è stata completata, ma è stata ripristinata o è scaduta. Il batch non sarà più disponibile per il consumo a valle, ma i dati sottostanti rimarranno in Master fino a quando non sarà stato conservato, archiviato o eliminato in altro modo. |
| Caricamento |  | Il client sta attualmente scrivendo dati per il batch. Il batch è **not** pronto per la promozione, a questo punto. |
| Caricato |  | Il client ha completato la scrittura dei dati per il batch. Il batch è pronto per la promozione. |
| Mantenuti |  | I dati sono stati estratti da Master e in un archivio designato in Adobe Data Lake. |
| Staging |  | Il client ha segnalato il batch per la promozione e i dati sono in fase di staging per il consumo a valle. |
| Nuovo |  | Il client ha segnalato il batch per la promozione, ma a causa di un errore, il batch viene ritentato da un servizio di monitoraggio batch. Questo stato può essere utilizzato per informare i clienti che potrebbe esserci un ritardo nell’acquisizione dei dati. |
| In stallo |  | Il cliente ha segnalato il batch per la promozione, ma dopo `n` tentativi da parte di un servizio di monitoraggio batch, la promozione batch è stata bloccata. |

### Cosa significa &quot;staging&quot; per i batch?

Quando un batch si trova in &quot;Staging&quot;, significa che il batch è stato segnalato con successo per la promozione e che i dati sono in fase di staging per il consumo a valle.

### Cosa significa quando un batch è &quot;Nuovo tentativo&quot;?

Quando un batch si trova in &quot;Nuovo tentativo&quot;, significa che l&#39;inserimento dei dati del batch è stato temporaneamente interrotto a causa di problemi intermittenti. In questo caso, non richiede alcun intervento da parte del cliente.

### Cosa significa quando un batch è &quot;Bloccato&quot;?

Quando un batch si trova in &quot;Bloccato&quot;, significa che [!DNL Data Ingestion Services] sta riscontrando difficoltà nell&#39;acquisizione del batch e tutti i tentativi sono stati esauriti.

### Cosa significa se un batch è ancora &quot;Caricamento&quot;?

Quando un batch è in &quot;Caricamento&quot;, significa che l&#39;API CompleteBatch non è stata chiamata per promuovere il batch.

### Esiste un modo per sapere se un batch è stato acquisito correttamente?

Una volta che lo stato del batch è &quot;Attivo&quot;, il batch è stato acquisito correttamente. Per scoprire lo stato del batch, segui i passaggi dettagliati [precedente](#how-is-batch-ingestion-monitored).

### Cosa succede dopo un errore di un batch?

Quando un batch non riesce, il motivo per cui non riesce può essere identificato nel `errors` sezione del payload. Di seguito sono riportati alcuni esempi di errori:

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

Invece di eliminare direttamente da [!DNL Catalog], i batch devono essere rimossi con uno dei metodi seguenti:

1. Se il batch è in corso, il batch deve essere interrotto.
2. Se il batch viene gestito correttamente, il batch deve essere ripristinato.

### Quali metriche a livello di batch sono disponibili?

Le seguenti metriche a livello di batch sono disponibili per i batch nello stato Attivo/Successo:

| Metrica | Descrizione |
| ------ | ----------- |
| inputByteSize | Numero totale di byte per cui è stato eseguito lo staging [!DNL Data Ingestion Services] da elaborare. |
| inputRecordSize | Numero totale di righe per le quali è stata eseguita la staging [!DNL Data Ingestion Services] da elaborare. |
| outputByteSize | Numero totale di byte generati da [!DNL Data Ingestion Services] a [!DNL Data Lake]. |
| outputRecordSize | Numero totale di righe generate da [!DNL Data Ingestion Services] a [!DNL Data Lake]. |
| partitionCount | Numero totale di partizioni scritte in [!DNL Data Lake]. |

### Perché le metriche non sono disponibili su alcuni batch?

Esistono due motivi per cui le metriche potrebbero non essere disponibili nel batch:

1. Il batch non è mai stato eseguito correttamente nello stato Attivo/Successo.
2. Il batch è stato promosso utilizzando un percorso di promozione legacy, ad esempio l’acquisizione CSV.

### Cosa significano i diversi codici di stato?

| Codice di stato | Descrizione |
| ----------- | ----------- |
| 106 | Il file del set di dati è vuoto. |
| 118 | Il file CSV contiene una riga di intestazione vuota. |
| 200 | Il batch è stato accettato per l&#39;elaborazione e passerà a uno stato finale, ad esempio Attivo o Errore. Una volta inviato, il batch può essere monitorato utilizzando `GetBatch` punto finale. |
| 400 | Richiesta non valida. Restituito se sono presenti blocchi mancanti o sovrapposti in un batch. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
