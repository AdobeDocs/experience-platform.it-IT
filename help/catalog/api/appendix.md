---
keywords: Experience Platform;home;argomenti popolari;Catalog service;catalog api;appendice
solution: Experience Platform
title: Appendice alla guida API di Catalog Service
description: Questo documento contiene informazioni aggiuntive per aiutarti a lavorare con l’API Catalog in Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# Appendice alla guida API [!DNL Catalog Service]

Questo documento contiene informazioni aggiuntive utili per l&#39;utilizzo dell&#39;API [!DNL Catalog].

## Visualizzare oggetti correlati {#view-interrelated-objects}

Alcuni oggetti [!DNL Catalog] possono essere correlati con altri oggetti [!DNL Catalog]. Tutti i campi con prefisso `@` nei payload di risposta indicano gli oggetti correlati. I valori per questi campi assumono la forma di un URI, che può essere utilizzato in una richiesta di GET separata per recuperare gli oggetti correlati che rappresentano.

Il set di dati di esempio restituito nel documento in [ricerca di un set di dati specifico](look-up-object.md) contiene un campo `files` con il seguente valore URI: `"@/datasetFiles?datasetId={DATASET_ID}"`. È possibile visualizzare il contenuto del campo `files` utilizzando questo URI come percorso per una nuova richiesta GET.

**Formato API**

```http
GET {OBJECT_URI}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_URI}` | URI fornito dal campo oggetto intercorrelato, escluso il simbolo `@`. |

**Richiesta**

La richiesta seguente utilizza l’URI fornito con la proprietà `files` del set di dati di esempio per recuperare un elenco dei file associati al set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di oggetti correlati. In questo esempio viene restituito un elenco di file di set di dati.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Intestazioni di richiesta aggiuntive

[!DNL Catalog] fornisce diverse convenzioni di intestazione che consentono di mantenere l&#39;integrità dei dati durante gli aggiornamenti.

### If-Match

È consigliabile utilizzare il controllo delle versioni degli oggetti per evitare il tipo di danneggiamento dei dati che si verifica quando un oggetto viene salvato da più utenti quasi contemporaneamente.

La best practice per aggiornare un oggetto prevede innanzitutto una chiamata API per visualizzare (GET) l’oggetto da aggiornare. Contenuto nella risposta (e in qualsiasi chiamata in cui la risposta contiene un singolo oggetto) è un&#39;intestazione `E-Tag` contenente la versione dell&#39;oggetto. Se si aggiunge la versione dell&#39;oggetto come intestazione di richiesta denominata `If-Match` nelle chiamate di aggiornamento (PUT o PATCH), l&#39;aggiornamento avrà esito positivo solo se la versione è ancora la stessa, evitando conflitti di dati.

Se le versioni non corrispondono (l’oggetto è stato modificato da un altro processo dopo averlo recuperato), riceverai lo stato HTTP 412 (Precondizione non riuscita) che indica che l’accesso alla risorsa di destinazione è stato negato.

### Pragma

In alcuni casi, può essere utile convalidare un oggetto senza salvare le informazioni. L&#39;utilizzo dell&#39;intestazione `Pragma` con un valore di `validate-only` consente di inviare richieste POST o PUT solo a scopo di convalida, impedendo la persistenza di eventuali modifiche ai dati.

## Compattazione dei dati

Compaction è un servizio [!DNL Experience Platform] che unisce i dati di file di piccole dimensioni in file di dimensioni maggiori senza modificare i dati. Per motivi di prestazioni, a volte è utile combinare un set di file di piccole dimensioni in file di grandi dimensioni per fornire un accesso più rapido ai dati quando viene eseguita una query.

Quando i file in un batch acquisito sono stati compattati, l&#39;oggetto [!DNL Catalog] associato viene aggiornato a scopo di monitoraggio.
