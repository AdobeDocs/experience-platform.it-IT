---
keywords: ' Experience Platform;home;argomenti comuni;servizio query;guida API;query;servizio query;servizio query;'
solution: Experience Platform
title: Endpoint API query
topic: queries
description: Le sezioni seguenti descrivono le chiamate che potete effettuare utilizzando l'endpoint /query nell'API del servizio di query.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 2%

---


# Endpoint query

## Chiamate API di esempio

Le sezioni seguenti descrivono le chiamate che potete effettuare utilizzando l&#39;endpoint `/queries` nell&#39;API [!DNL Query Service]. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recupero di un elenco di query

È possibile recuperare un elenco di tutte le query per l&#39;organizzazione IMS effettuando una richiesta di GET all&#39;endpoint `/queries`.

**Formato API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facoltativo*) Parametri aggiunti al percorso di richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e-mail (`&`). I parametri disponibili sono elencati di seguito.

**Parametri query**

Di seguito è riportato un elenco di parametri di query disponibili per l&#39;elenco delle query. Tutti questi parametri sono facoltativi. Effettuando una chiamata a questo endpoint senza parametri, tutte le query disponibili per l&#39;organizzazione verranno recuperate.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio, `orderby=created` ordinerà i risultati in base alla creazione in ordine crescente. L&#39;aggiunta di un `-` prima della creazione (`orderby=-created`) consente di ordinare gli elementi in base alla creazione in ordine decrescente. |
| `limit` | Specifica il limite delle dimensioni di pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Consente di scostare l&#39;elenco di risposte utilizzando la numerazione basata su zero. Ad esempio, `start=2` restituirà un elenco a partire dalla terza query elencata. (*Valore predefinito: 0*) |
| `property` | Filtrare i risultati in base ai campi. I filtri **devono essere preceduti da una sequenza di escape HTML.** Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `created`, `updated`, `state` e `id`. L&#39;elenco degli operatori supportati è `>` (maggiore di), `<` (minore di), `>=` (maggiore o uguale a), `<=` (minore o uguale a), `==` (uguale a), `!=` (non uguale a) e `~` (contiene). Ad esempio, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituirà tutte le query con l&#39;ID specificato. |
| `excludeSoftDeleted` | Indica se includere o meno una query che è stata eliminata in modo soft. Ad esempio, `excludeSoftDeleted=false` includerà **query eliminate soft**. (*Booleano, valore predefinito: true*) |
| `excludeHidden` | Indica se devono essere visualizzate query non guidate dall&#39;utente. Impostando questo valore su false, **verranno incluse query non guidate dall&#39;utente, come definizioni CURSOR, FETCH o query di metadati.** (*Booleano, valore predefinito: true*) |

**Richiesta**

La richiesta seguente recupera la query più recente creata per la vostra organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di query per l’organizzazione IMS specificata come JSON. La risposta seguente restituisce l’ultima query creata per l’organizzazione IMS.

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

### Creazione di una query

Potete creare una nuova query eseguendo una richiesta di POST all&#39;endpoint `/queries`.

**Formato API**

```http
POST /queries
```

**Richiesta**

La richiesta seguente crea una nuova query, configurata dai valori forniti nel payload:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query"
        "description": "Sample Description"
    }  
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `dbName` | Nome del database per il quale si sta creando una query SQL. |
| `sql` | Query SQL da creare. |
| `name` | Nome della query SQL. |
| `description` | Descrizione della query SQL. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con i dettagli della query appena creata. Una volta terminata l&#39;attivazione della query ed eseguita correttamente, la `state` passerà da `SUBMITTED` a `SUCCESS`.

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
>È possibile utilizzare il valore di `_links.cancel` per annullare la query creata](#cancel-a-query).[

### Recuperare una query per ID

È possibile recuperare informazioni dettagliate su una query specifica effettuando una richiesta di GET all&#39;endpoint `/queries` e fornendo il valore `id` della query nel percorso della richiesta.

**Formato API**

```http
GET /queries/{QUERY_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_ID}` | Il valore `id` della query da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla query specificata.

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
>È possibile utilizzare il valore di `_links.cancel` per annullare la query creata](#cancel-a-query).[

### Annullamento di una query

È possibile richiedere di eliminare una query specificata effettuando una richiesta di PATCH all&#39;endpoint `/queries` e fornendo il valore `id` della query nel percorso della richiesta.

**Formato API**

```http
PATCH /queries/{QUERY_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_ID}` | Il valore `id` della query da annullare. |


**Richiesta**

Questa richiesta API utilizza la sintassi della patch JSON per il payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento sui fondamentali dell&#39;API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `op` | Per annullare la query, è necessario impostare il parametro op con il valore `cancel `. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
