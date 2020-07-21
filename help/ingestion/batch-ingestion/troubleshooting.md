---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida alla risoluzione dei problemi di inserimento batch  Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---


# Guida alla risoluzione dei problemi di inserimento batch

Questa documentazione aiuterà a rispondere alle domande frequenti sulle [!DNL Batch Data Ingestion] API  Adobe Experience Platform.

## Chiamate API batch

### I batch sono attivi immediatamente dopo aver ricevuto un OK HTTP 200 dall’API CompleteBatch?

La `200 OK` risposta dell&#39;API indica che il batch è stato accettato per l&#39;elaborazione; non è attivo fino al passaggio al suo stato finale, ad esempio Attivo o Insuccesso.

### È sicuro riprovare la chiamata all&#39;API CompleteBatch dopo l&#39;errore?

Sì, è sicuro riprovare la chiamata API. Nonostante il fallimento, è possibile che l&#39;operazione ha avuto successo e il batch è stato accettato con successo. Tuttavia, è previsto che i client dispongano di meccanismi di ripetizione in caso di errore dell&#39;API e che, di fatto, siano incoraggiati a riprovare. Se l&#39;operazione ha avuto esito positivo, l&#39;API restituirà il successo, anche dopo un nuovo tentativo.

### Quando utilizzare l&#39;API di caricamento dei file di grandi dimensioni?

La dimensione file consigliata per l&#39;utilizzo dell&#39;API di caricamento dei file di grandi dimensioni è pari o superiore a 256 MB. Ulteriori informazioni sull&#39;utilizzo dell&#39;API di caricamento dei file di grandi dimensioni sono disponibili [qui](./api-overview.md#ingest-large-parquet-files).

### Perché la chiamata API Large File Complete non riesce?

Se blocchi di un file di grandi dimensioni si sovrappongono o mancano, il server risponde con una richiesta HTTP 400 non valida. Ciò può verificarsi perché è possibile caricare blocchi sovrapposti, poiché le convalide degli intervalli vengono effettuate al momento del completamento del file, quando i blocchi del file vengono uniti.

## Supporto per l&#39;inserimento

### Quali sono i formati di assimilazione supportati?

Attualmente, sia Parquet che JSON sono supportati. Il CSV è supportato su base legacy; i dati verranno promossi a controlli principali e non saranno supportate funzioni moderne, come conversione, partizionamento o convalida delle righe.

### Dove deve essere specificato il formato di input batch?

Il formato di input deve essere specificato al momento della creazione del batch all&#39;interno del payload. Di seguito è riportato un esempio di come specificare il formato di immissione batch:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Come viene assimilato JSON multi-riga?

Per acquisire JSON multiriga, il `isMultiLineJson` flag deve essere impostato al momento della creazione del batch. Un esempio è riportato di seguito:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### Qual è la differenza tra le righe JSON (Single Line JSON) e JSON multi-riga?

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

### L’assimilazione CSV è supportata?

L’assimilazione CSV è supportata solo per gli schemi flat. Al momento, l’assimilazione di dati gerarchici in CSV non è supportata.

Per ottenere tutte le funzioni di inserimento dei dati, è necessario utilizzare i formati JSON o Parquet.

### Quali tipi di convalida vengono eseguiti sui dati?

I dati sono caratterizzati da tre livelli di convalida:

- Schema - L&#39;inserimento in batch assicura che lo schema dell&#39;elemento dei dati acquisiti corrisponda allo schema del set di dati.
- Tipo di dati - L&#39;inserimento batch assicura che il tipo per ciascun campo assimilato corrisponda al tipo definito nello schema del dataset.
- Vincoli - L&#39;inserimento batch assicura che i vincoli, come &quot;Obbligatorio&quot;, &quot;enum&quot; e &quot;formato&quot;, siano definiti correttamente nella definizione dello schema.

### Come sostituire un batch già inserito?

Un batch già acquisito può essere sostituito utilizzando la funzione Riproduzione batch. Ulteriori informazioni sulla riproduzione batch sono disponibili [qui](./api-overview.md#replay-a-batch).

### Come viene monitorata l&#39;assimilazione batch?

Una volta segnalato un batch per la promozione batch, l&#39;avanzamento dell&#39;inserimento batch può essere controllato con la seguente richiesta:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Con questa richiesta, riceverete una risposta simile a questa:

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

Un batch può, nel suo ciclo di vita, attraversare i seguenti stati:

| Stato | Dati scritti in Master | Descrizione |
| ------ | ---------------------- | ----------- |
| Abbandonato |  | Il client non è riuscito a completare il batch nell&#39;intervallo di tempo previsto. |
| Interrotto |  | Il client ha esplicitamente chiamato, tramite le [!DNL Batch Data Ingestion] API, un&#39;operazione di interruzione per il batch specificato. Una volta che un batch è nello stato Caricato, il batch non può essere interrotto. |
| Attivo/Successo | x | Il batch è stato promosso con successo da fase a master ed è ora disponibile per il consumo a valle. **Nota:** Active e Success sono utilizzati in modo intercambiabile. |
| Archiviato |  | La partita è stata archiviata in deposito frigorifero. |
| Errore/Errore |  | Uno stato terminale che risulta da una configurazione non corretta e/o da dati non corretti. Viene registrato un errore fruibile, insieme al batch, per consentire ai client di correggere e reinviare i dati. **Nota:** I guasti e i guasti vengono utilizzati in modo intercambiabile. |
| Inattivo | x | Il batch è stato promosso con successo, ma è stato ripristinato o è scaduto. Il batch non sarà più disponibile per il consumo a valle, ma i dati sottostanti rimarranno in Master finché non saranno stati conservati, archiviati o eliminati in altro modo. |
| Caricamento |  | Il client sta attualmente scrivendo i dati per il batch. Al momento, il batch **non** è pronto per la promozione. |
| Caricato |  | Il client ha completato la scrittura dei dati per il batch. Il batch è pronto per la promozione. |
| Mantenuto |  | I dati sono stati estratti da Master e archiviati in un archivio designato in Adobe Data Lake. |
| Gestione temporanea |  | Il client ha segnalato il batch per la promozione e i dati sono stati messi in fase di consumo a valle. |
| Nuovo |  | Il client ha segnalato il batch per la promozione, ma a causa di un errore, il batch viene riprovato da un servizio di monitoraggio batch. Questo stato può essere utilizzato per indicare ai client che potrebbe verificarsi un ritardo nell’assimilazione dei dati. |
| Bloccato |  | Il client ha segnalato il batch per la promozione, ma dopo `n` i tentativi di un servizio di monitoraggio batch, la promozione batch è stata bloccata. |

### Cosa significa &quot;Staging&quot; per i batch?

Quando un batch è in &quot;Gestione temporanea&quot;, significa che il batch è stato segnalato per la promozione e che i dati sono stati messi in fase di consumo a valle.

### Che cosa significa quando un batch è &quot;Nuovo&quot;?

Quando un batch si trova in &quot;Riprova&quot;, significa che l&#39;inserimento dei dati del batch è stato temporaneamente interrotto a causa di problemi intermittenti. In questo caso, non richiede alcun intervento da parte del cliente.

### Cosa significa quando un batch è &quot;Bloccato&quot;?

Quando un batch è in &quot;Bloccato&quot;, significa che [!DNL Data Ingestion Services] sta riscontrando difficoltà nel caricamento del batch e che tutti i tentativi sono stati esauriti.

### Cosa significa se un batch è ancora &quot;Caricamento&quot;?

Quando un batch è in &quot;Caricamento&quot;, significa che l&#39;API CompleteBatch non è stata chiamata per promuovere il batch.

### Esiste un modo per sapere se un batch è stato correttamente assimilato?

Una volta che lo stato del batch è &quot;Attivo&quot;, il batch è stato assimilato correttamente. Per conoscere lo stato del batch, segui i passaggi descritti [in precedenza](#how-is-batch-ingestion-monitored).

### Cosa succede dopo il fallimento di un batch?

Quando un batch ha esito negativo, il motivo per cui ha avuto esito negativo può essere identificato nella `errors` sezione del payload. Di seguito sono riportati alcuni esempi di errori:

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

Anziché eliminare direttamente i batch, [!DNL Catalog]è necessario rimuovere i batch utilizzando uno dei metodi indicati di seguito:

1. Se il batch è in corso, il batch deve essere interrotto.
2. Se la masterizzazione del batch ha avuto esito positivo, il batch deve essere ripristinato.

### Quali metriche a livello di batch sono disponibili?

Le metriche a livello di batch seguenti sono disponibili per i batch nello stato Attivo/Successo:

| Metrica | Descrizione |
| ------ | ----------- |
| inputByteSize | Il numero totale di byte in fase [!DNL Data Ingestion Services] da elaborare. |
| inputRecordSize | Il numero totale di righe in cui è stato eseguito lo stage [!DNL Data Ingestion Services] per l&#39;elaborazione. |
| outputByteSize | Il numero totale di byte emessi da [!DNL Data Ingestion Services] a [!DNL Data Lake]. |
| outputRecordSize | Il numero totale di righe emesse da [!DNL Data Ingestion Services] a [!DNL Data Lake]. |
| partizioniCount | Numero totale di partizioni scritte in [!DNL Data Lake]. |

### Perché le metriche non sono disponibili in alcuni batch?

Esistono due motivi per cui le metriche potrebbero non essere disponibili nel batch:

1. Il batch non è mai stato eseguito correttamente nello stato Attivo/Successo.
2. Il batch è stato promosso utilizzando un percorso di promozione legacy, ad esempio l’assimilazione CSV.

### Cosa significano i diversi codici di stato?

| Codice di stato | Descrizione |
| ----------- | ----------- |
| 106 | Il file del set di dati è vuoto. |
| 118 | Il file CSV contiene una riga di intestazione vuota. |
| 200 | Il batch è stato accettato per l&#39;elaborazione e passerà allo stato finale, ad esempio Attivo o Errore. Una volta inviato, il batch può essere monitorato utilizzando l&#39; `GetBatch` endpoint. |
| 400 | Richiesta non valida. Restituito se in un batch sono presenti blocchi mancanti o sovrapposti. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
