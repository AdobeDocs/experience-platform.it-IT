---
keywords: Experience Platform;home;argomenti popolari;servizio catalogo;api catalogo;appendice
solution: Experience Platform
title: Appendice alla guida API del servizio catalogo
description: Questo documento contiene informazioni aggiuntive utili per l’utilizzo dell’API Catalogo in Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] Appendice della guida API

Questo documento contiene informazioni aggiuntive utili per l&#39;utilizzo delle [!DNL Catalog] API.

## Visualizzare gli oggetti correlati {#view-interrelated-objects}

Alcuni [!DNL Catalog] gli oggetti possono essere correlati ad altri [!DNL Catalog] oggetti. Qualsiasi campo con prefisso `@` nei payload di risposta indicano gli oggetti correlati. I valori di questi campi si presentano come un URI, che può essere utilizzato in una richiesta di GET separata per recuperare gli oggetti correlati che rappresentano.

Il set di dati di esempio restituito nel documento in [ricerca di un set di dati specifico](look-up-object.md) contiene `files` campo con il seguente valore URI: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. Contenuto della `files` Questo campo può essere visualizzato utilizzando questo URI come percorso per una nuova richiesta GET.

**Formato API**

```http
GET {OBJECT_URI}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_URI}` | URI fornito dal campo oggetto correlato (escluso il campo `@` simbolo). |

**Richiesta**

La richiesta seguente utilizza l’URI fornito dal set di dati di esempio `files` per recuperare un elenco dei file associati del set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di oggetti correlati. In questo esempio, viene restituito un elenco di file di set di dati.

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

Endpoint radice del [!DNL Catalog] L’API consente di effettuare più richieste all’interno di una singola chiamata. Il payload della richiesta contiene un array di oggetti che rappresentano normalmente le singole richieste, che vengono quindi eseguite in ordine.

Se queste richieste sono modifiche o aggiunte a [!DNL Catalog] e una delle modifiche non riesce, tutte le modifiche verranno ripristinate.

**Formato API**

```http
POST /
```

**Richiesta**

La seguente richiesta crea un nuovo set di dati, quindi crea visualizzazioni correlate per quel set di dati. Questo esempio illustra l’utilizzo del linguaggio dei modelli per accedere ai valori restituiti nelle chiamate precedenti e da utilizzare nelle chiamate successive.

Ad esempio, se desideri fare riferimento a un valore restituito da una richiesta secondaria precedente, puoi creare un riferimento nel formato seguente: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (4) `{REQUEST_ID}` è l’ID fornito dall’utente per la sottorichiesta, come illustrato di seguito). È possibile fare riferimento a qualsiasi attributo disponibile nel corpo di un oggetto di risposta di una richiesta secondaria precedente utilizzando questi modelli.

>[!NOTE]
>
>Quando una richiesta secondaria eseguita restituisce solo il riferimento a un oggetto (come è il valore predefinito per la maggior parte delle richieste di POST e PUT nell’API del catalogo), questo riferimento viene alias al valore `id` e può essere utilizzato come  `<<{OBJECT_ID}.id>>`.

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
| `id` | ID fornito dall’utente allegato all’oggetto di risposta in modo da poter associare le richieste alle risposte. [!DNL Catalog] non memorizza questo valore e lo restituisce semplicemente nella risposta a scopo di riferimento. |
| `resource` | Percorso della risorsa relativo alla directory principale [!DNL Catalog] API. Il protocollo e il dominio non devono far parte di questo valore e devono essere preceduti da &quot;/&quot;. <br/><br/> Quando utilizzi PATCH o DELETE come richiesta secondaria `method`, include l&#39;ID oggetto nel percorso della risorsa. Da non confondere con l&#39;utente fornito `id`, il percorso della risorsa utilizza l’ID di [!DNL Catalog] oggetto stesso (ad esempio, `resource: "/dataSets/1234567890"`). |
| `method` | Il nome del metodo (GET, PUT, POST, PATCH o DELETE) relativo all’azione in corso nella richiesta. |
| `body` | Il documento JSON che viene normalmente trasmesso come payload in una richiesta POST, PUT o PATCH. Questa proprietà non è necessaria per le richieste GET o DELETE. |

**Risposta**

Una risposta corretta restituisce un array di oggetti contenente `id` assegnato a ogni richiesta, il codice di stato HTTP per la singola richiesta e la risposta `body`. Poiché le tre richieste di esempio erano tutte per creare nuovi oggetti, il `body` di ogni oggetto è un array contenente solo l’ID dell’oggetto appena creato, così come lo standard con le risposte POST più efficaci in [!DNL Catalog].

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

Presta attenzione quando analizzi la risposta a una richiesta multipla, in quanto dovrai verificare il codice di ogni singola richiesta secondaria e non fare affidamento solo sul codice di stato HTTP per la richiesta POST padre.  È possibile che una singola richiesta secondaria restituisca un 404 (ad esempio una richiesta di GET su una risorsa non valida) mentre la richiesta complessiva restituisce 200.

## Intestazioni di richiesta aggiuntive

[!DNL Catalog] fornisce diverse convenzioni di intestazione per aiutarti a mantenere l’integrità dei dati durante gli aggiornamenti.

### If-Match

È buona prassi utilizzare il controllo delle versioni degli oggetti per evitare il tipo di danneggiamento dei dati che si verifica quando un oggetto viene salvato da più utenti in modo simile.

La procedura consigliata per l’aggiornamento di un oggetto prevede la prima esecuzione di una chiamata API per visualizzare (GET) l’oggetto da aggiornare. Contenuto nella risposta (e in qualsiasi chiamata in cui la risposta contiene un singolo oggetto) è un `E-Tag` intestazione contenente la versione dell&#39;oggetto. Aggiunta della versione dell’oggetto come intestazione di richiesta denominata `If-Match` nelle chiamate di aggiornamento (PUT o PATCH) l’aggiornamento avrà esito positivo solo se la versione è ancora la stessa, in modo da evitare conflitti tra dati.

Se le versioni non corrispondono (l’oggetto è stato modificato da un altro processo dopo il recupero), riceverai lo stato HTTP 412 (Precondizione non riuscita) per indicare che l’accesso alla risorsa di destinazione è stato negato.

### Pragma

In alcuni casi, è possibile convalidare un oggetto senza salvare le informazioni. Utilizzo della `Pragma` intestazione con un valore di `validate-only` consente di inviare richieste di POST o PUT solo a scopo di convalida, impedendo la persistenza di eventuali modifiche ai dati.

## Compattazione dei dati

La compattazione è [!DNL Experience Platform] servizio che unisce i dati da file di piccole dimensioni in file di grandi dimensioni senza modificare alcun dato. Per motivi di prestazioni, a volte è utile combinare un set di file di piccole dimensioni in file più grandi per fornire un accesso più rapido ai dati quando vengono eseguiti i query.

Quando i file di un batch acquisito sono stati compattati, i relativi [!DNL Catalog] l&#39;oggetto viene aggiornato a scopo di monitoraggio.
