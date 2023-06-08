---
keywords: Experience Platform;home;argomenti popolari;Catalog service;catalog api;appendice
solution: Experience Platform
title: Appendice alla guida API di Catalog Service
description: Questo documento contiene informazioni aggiuntive per aiutarti a lavorare con l’API Catalog in Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# [!DNL Catalog Service] Appendice alla guida API

Questo documento contiene informazioni aggiuntive utili per l&#39;utilizzo di [!DNL Catalog] API.

## Visualizzare oggetti correlati {#view-interrelated-objects}

Alcuni [!DNL Catalog] gli oggetti possono essere correlati con altri [!DNL Catalog] oggetti. Qualsiasi campo con prefisso `@` nei payload di risposta, gli oggetti correlati sono indicati. I valori per questi campi assumono la forma di un URI, che può essere utilizzato in una richiesta di GET separata per recuperare gli oggetti correlati che rappresentano.

Set di dati di esempio restituito nel documento il [ricerca di un set di dati specifico](look-up-object.md) contiene un `files` con il seguente valore URI: `"@/datasetFiles?datasetId={DATASET_ID}"`. Contenuto della `files` può essere visualizzato utilizzando questo URI come percorso per una nuova richiesta GET.

**Formato API**

```http
GET {OBJECT_URI}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_URI}` | URI fornito dal campo oggetto intercorrelato (escluso `@` ). |

**Richiesta**

La seguente richiesta utilizza l’URI fornito del set di dati di esempio `files` per recuperare un elenco dei file associati al set di dati.

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

[!DNL Catalog] fornisce diverse convenzioni di intestazione per mantenere l’integrità dei dati durante gli aggiornamenti.

### If-Match

È consigliabile utilizzare il controllo delle versioni degli oggetti per evitare il tipo di danneggiamento dei dati che si verifica quando un oggetto viene salvato da più utenti quasi contemporaneamente.

La best practice per aggiornare un oggetto prevede innanzitutto una chiamata API per visualizzare (GET) l’oggetto da aggiornare. Contenuto nella risposta (e in qualsiasi chiamata in cui la risposta contiene un singolo oggetto) è un `E-Tag` intestazione contenente la versione dell’oggetto. Aggiunta della versione dell’oggetto come intestazione di richiesta denominata `If-Match` nelle chiamate di aggiornamento (PUT o PATCH) l’aggiornamento avrà esito positivo solo se la versione è ancora la stessa, evitando conflitti di dati.

Se le versioni non corrispondono (l’oggetto è stato modificato da un altro processo dopo averlo recuperato), riceverai lo stato HTTP 412 (Precondizione non riuscita) che indica che l’accesso alla risorsa di destinazione è stato negato.

### Pragma

In alcuni casi, può essere utile convalidare un oggetto senza salvare le informazioni. Utilizzo di `Pragma` intestazione con valore `validate-only` consente di inviare richieste POST o PUT solo a scopo di convalida, evitando che eventuali modifiche apportate ai dati vengano mantenute.

## Compattazione dei dati

La compattazione è un [!DNL Experience Platform] servizio che unisce i dati di file di piccole dimensioni in file di dimensioni maggiori senza modificare i dati. Per motivi di prestazioni, a volte è utile combinare un set di file di piccole dimensioni in file di grandi dimensioni per fornire un accesso più rapido ai dati quando viene eseguita una query.

Quando i file in un batch acquisito sono stati compattati, il relativo [!DNL Catalog] l&#39;oggetto viene aggiornato a scopo di monitoraggio.
