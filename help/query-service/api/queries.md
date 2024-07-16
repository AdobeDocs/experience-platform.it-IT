---
keywords: Experience Platform;home;argomenti popolari;servizio query;guida api;query;query;servizio query;
solution: Experience Platform
title: Endpoint API per query
description: Le sezioni seguenti descrivono le chiamate che puoi effettuare utilizzando l’endpoint /queries nell’API del servizio di query.
role: Developer
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 2%

---

# Endpoint &quot;query&quot;

## Chiamate API di esempio

Nelle sezioni seguenti vengono esaminate le chiamate che è possibile effettuare utilizzando l&#39;endpoint `/queries` nell&#39;API [!DNL Query Service]. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recuperare un elenco di query

Per recuperare un elenco di tutte le query per l&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/queries`.

**Formato API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facoltativo*) Parametri aggiunti al percorso della richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e commerciali (`&`). I parametri disponibili sono elencati di seguito.

**Parametri query**

Di seguito è riportato un elenco dei parametri di query disponibili per l&#39;elenco delle query. Tutti questi parametri sono facoltativi. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperate tutte le query disponibili per la tua organizzazione.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio, `orderby=created` ordinerà i risultati in base alla creazione in ordine crescente. L&#39;aggiunta di un `-` prima della creazione (`orderby=-created`) ordinerà gli elementi in base alla creazione in ordine decrescente. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Specifica una marca temporale in formato ISO per ordinare i risultati. Se non viene specificata una data di inizio, la chiamata API restituirà prima la query creata più datata, quindi continuerà a elencare i risultati più recenti.<br> Le marche temporali ISO consentono diversi livelli di granularità in data e ora. I timestamp ISO di base assumono il formato di: `2020-09-07` per esprimere la data 7 settembre 2020. Un esempio più complesso verrebbe scritto come `2022-11-05T08:15:30-05:00` e corrisponde al 5 novembre 2022, 8:15:30, ora standard orientale USA. È possibile fornire un fuso orario con scostamento UTC ed è indicato dal suffisso &quot;Z&quot; (`2020-01-01T01:01:01Z`). Se non viene fornito alcun fuso orario, per impostazione predefinita viene impostato su zero. |
| `property` | Filtra i risultati in base ai campi. I filtri **devono** avere escape HTML. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `created`, `updated`, `state` e `id`. L&#39;elenco degli operatori supportati è `>` (maggiore di), `<` (minore di), `>=` (maggiore o uguale a), `<=` (minore o uguale a), `==` (uguale a), `!=` (diverso da) e `~` (contiene). Ad esempio, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituirà tutte le query con l&#39;ID specificato. |
| `excludeSoftDeleted` | Indica se deve essere inclusa una query che è stata eliminata temporaneamente. Ad esempio, `excludeSoftDeleted=false` **includerà** query eliminate temporaneamente. (*Booleano, valore predefinito: true*) |
| `excludeHidden` | Indica se devono essere visualizzate le query non guidate dall&#39;utente. Se questo valore è impostato su false, **includerà** query non guidate dall&#39;utente, ad esempio le definizioni CURSOR, FETCH o query di metadati. (*Booleano, valore predefinito: true*) |
| `isPrevLink` | Il parametro di query `isPrevLink` viene utilizzato per l&#39;impaginazione. I risultati della chiamata API sono ordinati in base alla marca temporale `created` e alla proprietà `orderby`. Durante la navigazione nelle pagine dei risultati, `isPrevLink` è impostato su true quando si esegue il paging all&#39;indietro. Inverte l’ordine della query. Consulta i collegamenti &quot;successivo&quot; e &quot;precedente&quot; come esempi. |

**Richiesta**

La richiesta seguente recupera la query più recente creata per la tua organizzazione.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di query per l’organizzazione specificata come JSON. La risposta seguente restituisce la query più recente creata per l’organizzazione.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### Creare una query

È possibile creare una nuova query effettuando una richiesta POST all&#39;endpoint `/queries`.

**Formato API**

```http
POST /queries
```

**Richiesta**

La richiesta seguente crea una nuova query, con un’istruzione SQL fornita nel payload:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "queryParameters": {
            user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

L’esempio di richiesta seguente crea una nuova query utilizzando un ID modello di query esistente.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "templateID": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `dbName` | Nome del database per il quale si sta creando una query SQL. |
| `sql` | La query SQL da creare. |
| `name` | Nome della query SQL. |
| `description` | Descrizione della query SQL. |
| `queryParameters` | Associazione di valori chiave per sostituire eventuali valori con parametri nell&#39;istruzione SQL. È necessario solo **se** si stanno utilizzando sostituzioni di parametri all&#39;interno del codice SQL fornito. Su queste coppie chiave-valore non verrà eseguito alcun controllo del tipo di valore. |
| `templateId` | L’identificatore univoco di una query preesistente. È possibile fornire questa istruzione anziché un&#39;istruzione SQL. |
| `insertIntoParameters` | (Facoltativo) Se questa proprietà è definita, la query verrà convertita in una query INSERT INTO. |
| `ctasParameters` | (Facoltativo) Se questa proprietà è definita, questa query verrà convertita in una query CTAS. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con i dettagli della query appena creata. Una volta completata l&#39;attivazione della query ed eseguita correttamente, `state` cambierà da `SUBMITTED` a `SUCCESS`.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>È possibile utilizzare il valore di `_links.cancel` per [annullare la query creata](#cancel-a-query).

### Recuperare una query per ID

Per recuperare informazioni dettagliate su una query specifica, eseguire una richiesta GET all&#39;endpoint `/queries` e specificare il valore `id` della query nel percorso della richiesta.

**Formato API**

```http
GET /queries/{QUERY_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_ID}` | Valore `id` della query da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sulla query specificata.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>È possibile utilizzare il valore di `_links.cancel` per [annullare la query creata](#cancel-a-query).

### Annullare o eliminare temporaneamente una query

È possibile richiedere l&#39;annullamento o l&#39;eliminazione temporanea di una query specificata effettuando una richiesta PATCH all&#39;endpoint `/queries` e fornendo il valore `id` della query nel percorso della richiesta.

**Formato API**

```http
PATCH /queries/{QUERY_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{QUERY_ID}` | Valore `id` della query su cui si desidera eseguire l&#39;operazione. |


**Richiesta**

Questa richiesta API utilizza la sintassi Patch JSON per il suo payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento API Fundals.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `op` | Tipo di operazione da eseguire sulla risorsa. I valori accettati sono `cancel` e `soft_delete`. Per annullare la query, è necessario impostare il parametro op con il valore `cancel `. L’operazione di eliminazione temporanea interrompe la restituzione della query nelle richieste di GET, ma non la elimina. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con il seguente messaggio:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
