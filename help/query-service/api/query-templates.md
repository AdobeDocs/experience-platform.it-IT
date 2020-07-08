---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Query Service
topic: query templates
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 3%

---


# Modelli di query

## Chiamate API di esempio

Ora che hai compreso le intestazioni da utilizzare, sei pronto a iniziare a effettuare chiamate all&#39;API di Servizio query. Le sezioni seguenti descrivono le varie chiamate API che potete effettuare tramite l&#39;API di Query Service. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recupero di un elenco di modelli di query

È possibile recuperare un elenco di tutti i modelli di query per l&#39;organizzazione IMS effettuando una richiesta GET all&#39; `/query-templates` endpoint.

**Formato API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facoltativo*) Parametri aggiunti al percorso di richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e-mail (`&`). I parametri disponibili sono elencati di seguito. |

**Parametri query**

Di seguito è riportato un elenco di parametri di query disponibili per elencare i modelli di query. Tutti questi parametri sono facoltativi. Se si effettua una chiamata a questo endpoint senza parametri, tutti i modelli di query disponibili per l&#39;organizzazione verranno recuperati.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio, `orderby=created` ordinerà i risultati in base alla creazione in ordine crescente. Se si aggiunge un elemento `-` prima della creazione (`orderby=-created`), gli elementi verranno ordinati in base alla creazione in ordine decrescente. |
| `limit` | Specifica il limite delle dimensioni di pagina per controllare il numero di risultati inclusi in una pagina. (valore *predefinito: 20*) |
| `start` | Consente di scostare l&#39;elenco di risposte utilizzando la numerazione basata su zero. Ad esempio, `start=2` restituirà un elenco a partire dalla terza query elencata. (valore *predefinito: 0*) |
| `property` | Filtrare i risultati in base ai campi. I filtri **devono** essere con escape HTML. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `name` e `userId`. L&#39;unico operatore supportato è `==` (uguale a). Ad esempio, `name==my_template` restituisce tutti i modelli di query con il nome `my_template`. |

**Richiesta**

La richiesta seguente recupera l’ultimo modello di query creato per l’organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di modelli di query per l&#39;organizzazione IMS specificata. La risposta seguente restituisce l’ultimo modello di query creato per l’organizzazione IMS.

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE]
>
>È possibile utilizzare il valore di `_links.delete` per [eliminare il modello](#delete-a-specified-query-template)di query.

### Creare un modello di query

Potete creare un modello di query effettuando una richiesta POST all&#39; `/query-templates` endpoint.

**Formato API**

```http
POST /query-templates
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `sql` | Query SQL da creare. |
| `name` | Nome del modello di query. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con i dettagli del modello di query appena creato.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>È possibile utilizzare il valore di `_links.delete` per [eliminare il modello](#delete-a-specified-query-template)di query.

### Recuperare un modello di query specificato

Potete recuperare un modello di query specifico eseguendo una richiesta GET all&#39; `/query-templates/{TEMPLATE_ID}` endpoint e fornendo l&#39;ID del modello di query nel percorso della richiesta.

**Formato API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | Il `id` valore del modello di query da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del modello di query specificato.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>È possibile utilizzare il valore di `_links.delete` per [eliminare il modello](#delete-a-specified-query-template)di query.

### Aggiornare un modello di query specificato

Potete aggiornare un modello di query specifico effettuando una richiesta PUT all&#39; `/query-templates/{TEMPLATE_ID}` endpoint e fornendo l&#39;ID del modello di query nel percorso della richiesta.

**Formato API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Il `id` valore del modello di query da recuperare. |

**Richiesta**

>[!NOTE]
>
>La richiesta PUT richiede la compilazione del campo sql e del campo name e **sovrascrive** il contenuto corrente del modello di query.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `sql` | Query SQL da aggiornare. |
| `name` | Nome della query pianificata. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con le informazioni aggiornate per il modello di query specificato.

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>È possibile utilizzare il valore di `_links.delete` per [eliminare il modello](#delete-a-specified-query-template)di query.

### Eliminare un modello di query specificato

È possibile eliminare un modello di query specifico effettuando una richiesta di DELETE al `/query-templates/{TEMPLATE_ID}` e fornendo l&#39;ID del modello di query nel percorso della richiesta.

**Formato API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Il `id` valore del modello di query da recuperare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
