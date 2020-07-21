---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Appendice della guida per gli sviluppatori di Catalog Service
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# [!DNL Catalog Service] appendice della guida per sviluppatori

Questo documento contiene informazioni aggiuntive utili per l&#39;utilizzo dell&#39; [!DNL Catalog] API.

## Visualizzare gli oggetti correlati {#view-interrelated-objects}

Alcuni [!DNL Catalog] oggetti possono essere correlati ad altri [!DNL Catalog] oggetti. Tutti i campi con il prefisso `@` nei payload di risposta indicano gli oggetti correlati. I valori di questi campi sono costituiti da un URI, che può essere utilizzato in una richiesta GET separata per recuperare gli oggetti correlati che rappresentano.

Il set di dati di esempio restituito nel documento per la [ricerca di un set di dati](look-up-object.md) `files` specifico contiene un campo con il seguente valore URI: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. Il contenuto del `files` campo può essere visualizzato utilizzando questo URI come percorso per una nuova richiesta GET.

**Formato API**

```http
GET {OBJECT_URI}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_URI}` | URI fornito dal campo oggetto correlato (escluso il `@` simbolo). |

**Richiesta**

La richiesta seguente utilizza l&#39;URI fornito dalla `files` proprietà del dataset di esempio per recuperare un elenco dei file associati del dataset.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco degli oggetti correlati. In questo esempio, viene restituito un elenco di file di set di dati.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Eseguire più richieste in una singola chiamata

L&#39;endpoint principale dell&#39; [!DNL Catalog] API consente di effettuare più richieste all&#39;interno di una singola chiamata. Il payload della richiesta contiene un array di oggetti che rappresentano normalmente le singole richieste, che vengono quindi eseguite in ordine.

Se queste richieste sono modifiche o aggiunte [!DNL Catalog] e una delle modifiche non riesce, tutte le modifiche verranno ripristinate.

**Formato API**

```http
POST /
```

**Richiesta**

La richiesta seguente crea un nuovo dataset, quindi crea le viste correlate per tale dataset. Questo esempio illustra l’utilizzo del linguaggio dei modelli per accedere ai valori restituiti nelle chiamate precedenti e utilizzabili nelle chiamate successive.

Ad esempio, se desiderate fare riferimento a un valore restituito da una richiesta secondaria precedente, potete creare un riferimento nel formato seguente: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (dove `{REQUEST_ID}` è l’ID fornito dall’utente per la richiesta secondaria, come illustrato di seguito). È possibile fare riferimento a qualsiasi attributo disponibile nel corpo di un oggetto di risposta di una richiesta secondaria precedente utilizzando questi modelli.

>[!NOTE]
>
>Quando una sub-richiesta eseguita restituisce solo il riferimento a un oggetto (come è il valore predefinito per la maggior parte delle richieste POST e PUT nell&#39;API Catalog), il riferimento viene alias al valore `id` e può essere utilizzato come `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `id` | ID fornito dall&#39;utente che è allegato all&#39;oggetto response in modo da poter far corrispondere le richieste alle risposte. [!DNL Catalog] non memorizza questo valore e lo restituisce semplicemente nella risposta a scopo di riferimento. |
| `resource` | Percorso della risorsa relativo alla directory principale dell&#39; [!DNL Catalog] API. Il protocollo e il dominio non devono far parte di questo valore e devono avere il prefisso &quot;/&quot;. <br/><br/> Quando si utilizza PATCH o DELETE come richiesta secondaria `method`, includere l&#39;ID oggetto nel percorso della risorsa. Da non confondere con l&#39;oggetto fornito dall&#39;utente `id`, il percorso della risorsa utilizza l&#39;ID dell&#39; [!DNL Catalog] oggetto stesso (ad esempio, `resource: "/dataSets/1234567890"`). |
| `method` | Nome del metodo (GET, PUT, POST, PATCH o DELETE) relativo all’azione in corso nella richiesta. |
| `body` | Il documento JSON che normalmente viene passato come payload in una richiesta POST, PUT o PATCH. Questa proprietà non è necessaria per le richieste GET o DELETE. |

**Risposta**

Una risposta corretta restituisce un array di oggetti contenente gli oggetti `id` assegnati a ciascuna richiesta, il codice di stato HTTP per la singola richiesta e la risposta `body`. Poiché le tre richieste di esempio erano tutte volte a creare nuovi oggetti, `body` di ogni oggetto è un array contenente solo l’ID del nuovo oggetto creato, come lo standard con le risposte POST più efficaci in [!DNL Catalog].

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

Prestate attenzione durante l’analisi della risposta a una richiesta multipla, in quanto dovrete verificare il codice di ogni singola richiesta secondaria e non affidarvi esclusivamente al codice di stato HTTP per la richiesta POST padre.  È possibile che una singola richiesta secondaria restituisca una richiesta 404 (ad esempio una richiesta GET per una risorsa non valida) mentre la richiesta complessiva restituisce 200.

## Intestazioni di richiesta aggiuntive

[!DNL Catalog] fornisce diverse convenzioni di intestazione per mantenere l’integrità dei dati durante gli aggiornamenti.

### If-Match

È buona norma utilizzare il controllo delle versioni degli oggetti per evitare il tipo di danneggiamento dei dati che si verifica quando un oggetto viene salvato da più utenti quasi contemporaneamente.

Come procedura ottimale, quando si aggiorna un oggetto è necessario effettuare prima una chiamata API per visualizzare (GET) l&#39;oggetto da aggiornare. Contenuto nella risposta (e in qualsiasi chiamata in cui la risposta contiene un singolo oggetto) è un&#39; `E-Tag` intestazione contenente la versione dell&#39;oggetto. Se si aggiunge la versione dell&#39;oggetto come intestazione di richiesta denominata `If-Match` nelle chiamate di aggiornamento (PUT o PATCH), l&#39;aggiornamento avrà esito positivo solo se la versione è ancora la stessa, evitando così eventuali collisioni di dati.

Se le versioni non corrispondono (l&#39;oggetto è stato modificato da un altro processo dopo il recupero), riceverete lo stato HTTP 412 (Precondizione non riuscita) per indicare che l&#39;accesso alla risorsa di destinazione è stato negato.

### Praga

In alcuni casi, è possibile convalidare un oggetto senza salvare le informazioni. L&#39;utilizzo dell&#39; `Pragma` intestazione con il valore di `validate-only` consente di inviare richieste POST o PUT solo a scopo di convalida, impedendo la persistenza di eventuali modifiche ai dati.

## Compattazione dei dati

Compaction è un [!DNL Experience Platform] servizio che unisce i dati da file di piccole dimensioni a file più grandi senza modificare alcun dato. Per motivi di prestazioni, a volte è utile combinare un set di file di piccole dimensioni in file più grandi, in modo da fornire un accesso più rapido ai dati durante la query.

Quando i file di un batch assimilato sono stati compattati, l’ [!DNL Catalog] oggetto associato viene aggiornato a scopo di monitoraggio.