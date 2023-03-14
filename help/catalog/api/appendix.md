---
keywords: Experience Platform;home;argomenti popolari;Catalog service;catalog api;appendice
solution: Experience Platform
title: Appendice alla guida API di Catalog Service
description: Questo documento contiene informazioni aggiuntive per aiutarti a lavorare con l’API Catalog in Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] Appendice alla guida API

Questo documento contiene informazioni aggiuntive utili per l&#39;utilizzo di [!DNL Catalog] API.

## Visualizzare oggetti correlati {#view-interrelated-objects}

Alcuni [!DNL Catalog] gli oggetti possono essere correlati con altri [!DNL Catalog] oggetti. Qualsiasi campo con prefisso `@` nei payload di risposta, gli oggetti correlati sono indicati. I valori per questi campi assumono la forma di un URI, che può essere utilizzato in una richiesta di GET separata per recuperare gli oggetti correlati che rappresentano.

Set di dati di esempio restituito nel documento il [ricerca di un set di dati specifico](look-up-object.md) contiene un `files` con il seguente valore URI: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. Contenuto della `files` può essere visualizzato utilizzando questo URI come percorso per una nuova richiesta GET.

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
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
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

## Effettuare più richieste in una singola chiamata

Endpoint principale del [!DNL Catalog] API consente di effettuare più richieste all’interno di una singola chiamata. Il payload della richiesta contiene un array di oggetti che rappresentano le normali richieste singole, che vengono quindi eseguite in ordine.

Se queste richieste sono modifiche o aggiunte a [!DNL Catalog] e se una qualsiasi delle modifiche non riesce, tutte le modifiche verranno ripristinate.

**Formato API**

```http
POST /
```

**Richiesta**

La richiesta seguente crea un nuovo set di dati, quindi crea viste correlate per quel set di dati. Questo esempio illustra l’utilizzo del linguaggio dei modelli per accedere ai valori restituiti nelle chiamate precedenti e utilizzarli nelle chiamate successive.

Ad esempio, se desideri fare riferimento a un valore restituito da una sottorichiesta precedente, puoi creare un riferimento nel formato: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (dove `{REQUEST_ID}` è l’ID fornito dall’utente per la sottorichiesta, come illustrato di seguito). Puoi fare riferimento a qualsiasi attributo disponibile nel corpo di un oggetto di risposta di una richiesta secondaria precedente utilizzando questi modelli.

>[!NOTE]
>
>Quando una sottorichiesta eseguita restituisce solo il riferimento a un oggetto (come è l’impostazione predefinita per la maggior parte delle richieste POST e PUT nell’API Catalog), questo riferimento viene associato al valore `id` e possono essere utilizzati come  `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID fornito dall’utente e allegato all’oggetto di risposta, in modo da poter associare le richieste alle risposte. [!DNL Catalog] non memorizza questo valore e lo restituisce semplicemente nella risposta a scopo di riferimento. |
| `resource` | Percorso della risorsa relativo alla radice del [!DNL Catalog] API. Il protocollo e il dominio non devono far parte di questo valore e devono avere il prefisso &quot;/&quot;. <br/><br/> Quando si utilizza PATCH o DELETE come richiesta secondaria di `method`, includi l&#39;ID oggetto nel percorso della risorsa. Da non confondere con il software fornito dall&#39;utente `id`, il percorso della risorsa utilizza l’ID del [!DNL Catalog] oggetto stesso (ad esempio, `resource: "/dataSets/1234567890"`). |
| `method` | Nome del metodo (GET, PUT, POST, PATCH o DELETE) relativo all’azione eseguita nella richiesta. |
| `body` | Documento JSON che verrebbe normalmente trasmesso come payload in una richiesta POST, PUT o PATCH. Questa proprietà non è necessaria per le richieste GET o DELETE. |

**Risposta**

In caso di esito positivo, la risposta restituisce un array di oggetti contenenti `id` che hai assegnato a ogni richiesta, il codice di stato HTTP per la singola richiesta e la risposta `body`. Poiché le tre richieste di esempio dovevano tutte creare nuovi oggetti, il `body` di ciascun oggetto è un array contenente solo l’ID del nuovo oggetto creato, così come lo standard con la maggior parte delle risposte di successo dei POST in [!DNL Catalog].

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

Presta attenzione quando esamini la risposta a una richiesta multipla, in quanto dovrai verificare il codice di ogni singola richiesta secondaria e non affidarti esclusivamente al codice di stato HTTP per la richiesta POST principale.  È possibile che una singola sottorichiesta restituisca un valore 404 (ad esempio una richiesta GET su una risorsa non valida), mentre la richiesta complessiva restituisce 200.

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
