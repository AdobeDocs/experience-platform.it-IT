---
keywords: Experience Platform;home;argomenti popolari;servizio query;guida api;query;query;servizio query;
solution: Experience Platform
title: Endpoint API query
description: Nelle sezioni seguenti sono descritte le chiamate dettagliate che è possibile effettuare utilizzando l’endpoint /query nell’API del servizio query.
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: 08e19149a84273231c6261d2a4e09584dfb6e38d
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 3%

---

# Endpoint query

## Chiamate API di esempio

Nelle sezioni seguenti vengono descritte le chiamate che è possibile effettuare utilizzando `/queries` punto finale [!DNL Query Service] API. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recupera un elenco di query

Puoi recuperare un elenco di tutte le query per la tua organizzazione IMS effettuando una richiesta di GET al `/queries` punto finale.

**Formato API**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facoltativo*) Parametri aggiunti al percorso della richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e commerciale (`&`). I parametri disponibili sono elencati di seguito.

**Parametri query**

Di seguito è riportato un elenco dei parametri di query disponibili per l’elenco delle query. Tutti questi parametri sono facoltativi. Effettuare una chiamata a questo endpoint senza parametri recupererà tutte le query disponibili per la tua organizzazione.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio: `orderby=created` ordinerà i risultati in base a quelli creati in ordine crescente. Aggiunta di un `-` prima della creazione (`orderby=-created`) ordina gli elementi in base a quelli creati in ordine decrescente. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Esegue l&#39;offset dell&#39;elenco di risposte utilizzando la numerazione basata su zero. Ad esempio: `start=2` restituirà un elenco a partire dalla terza query elencata. (*Valore predefinito: 0*) |
| `property` | Filtrare i risultati in base ai campi. I filtri **deve** essere HTML fuggito. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `created`, `updated`, `state`e `id`. L’elenco degli operatori supportati è `>` (maggiore di), `<` (inferiore a), `>=` (maggiore o uguale a), `<=` (minore o uguale a), `==` (uguale a), `!=` (diverso da), e `~` (contiene). Ad esempio: `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituirà tutte le query con l’ID specificato. |
| `excludeSoftDeleted` | Indica se includere una query che è stata eliminata tramite soft. Ad esempio: `excludeSoftDeleted=false` sarà **include** query eliminate soft. (*Valore booleano predefinito: true*) |
| `excludeHidden` | Indica se visualizzare query non basate su utenti. Se questo valore viene impostato su false, verrà **include** query non basate su utenti, ad esempio definizioni CURSOR, FETCH o query con metadati. (*Valore booleano predefinito: true*) |
| `isPrevLink` | La `isPrevLink` il parametro query viene utilizzato per l’impaginazione. I risultati della chiamata API vengono ordinati in base ai rispettivi `created` la marca temporale e `orderby` proprietà. Durante la navigazione nelle pagine dei risultati, `isPrevLink` è impostato su true quando si esegue il paging all&#39;indietro. Annulla l’ordine della query. Vedi i collegamenti &quot;successivo&quot; e &quot;precedente&quot; come esempi. |

**Richiesta**

La richiesta seguente recupera la query più recente creata per la tua organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di query per l’organizzazione IMS specificata come JSON. La risposta seguente restituisce l’ultima query creata per la tua organizzazione IMS.

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

Puoi creare una nuova query effettuando una richiesta POST al `/queries` punto finale.

**Formato API**

```http
POST /queries
```

**Richiesta**

La seguente richiesta crea una nuova query con un&#39;istruzione SQL fornita nel payload:

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
| `dbName` | Nome del database per cui si sta creando una query SQL. |
| `sql` | Query SQL da creare. |
| `name` | Nome della query SQL. |
| `description` | Descrizione della query SQL. |
| `queryParameters` | Associazione di valori chiave per sostituire eventuali valori con parametri nell&#39;istruzione SQL. È richiesto solo **if** si stanno utilizzando sostituzioni di parametri all&#39;interno dell&#39;SQL fornito. Per queste coppie di valori chiave non verrà eseguito alcun controllo del tipo di valore. |
| `templateId` | Identificatore univoco per una query preesistente. È possibile specificare questo anziché un&#39;istruzione SQL. |
| `insertIntoParameters` | (Facoltativo) Se questa proprietà è definita, questa query verrà convertita in una query INSERT INTO. |
| `ctasParameters` | (Facoltativo) Se questa proprietà è definita, questa query verrà convertita in una query CTAS. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (accettato) con i dettagli della query appena creata. Al termine dell’attivazione della query e dell’esecuzione della query, la `state` cambia da `SUBMITTED` a `SUCCESS`.

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
>Puoi utilizzare il valore di `_links.cancel` a [annulla query creata](#cancel-a-query).

### Recupera una query per ID

È possibile recuperare informazioni dettagliate su una query specifica effettuando una richiesta di GET al `/queries` endpoint e fornitura della query `id` nel percorso della richiesta.

**Formato API**

```http
GET /queries/{QUERY_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_ID}` | La `id` valore della query da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>Puoi utilizzare il valore di `_links.cancel` a [annulla query creata](#cancel-a-query).

### Annullare o eliminare in modo soft una query

È possibile richiedere l’annullamento o l’eliminazione soft di una query specificata effettuando una richiesta di PATCH al `/queries` endpoint e fornitura della query `id` nel percorso della richiesta.

**Formato API**

```http
PATCH /queries/{QUERY_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{QUERY_ID}` | La `id` valore della query su cui si desidera eseguire l&#39;operazione. |


**Richiesta**

Questa richiesta API utilizza la sintassi della patch JSON per il relativo payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento di base API .

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
| `op` | Tipo di operazione da eseguire sulla risorsa. I valori accettati sono `cancel` e `soft_delete`. Per annullare la query, è necessario impostare il parametro op con il valore `cancel `. L’operazione di eliminazione soft impedisce la restituzione della query sulle richieste GET ma non la elimina dal sistema. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
