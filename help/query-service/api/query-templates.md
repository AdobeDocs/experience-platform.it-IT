---
keywords: Experience Platform;home;argomenti popolari;servizio query;modelli di query;guida api;modelli;servizio query;
solution: Experience Platform
title: Endpoint API per i modelli di query
description: Questa guida descrive le varie chiamate API del modello di query che puoi effettuare utilizzando l’API del servizio query.
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 5%

---

# Endpoint dei modelli di query

## Chiamate API di esempio

Le sezioni seguenti descrivono le varie chiamate API che puoi effettuare utilizzando [!DNL Query Service] API. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

Consulta la sezione [Documentazione sui modelli di query dell’interfaccia utente](../ui/query-templates.md) per informazioni sulla creazione di modelli tramite l’interfaccia utente di Experience Platform.

### Recupera un elenco di modelli di query

Puoi recuperare un elenco di tutti i modelli di query per la tua organizzazione IMS effettuando una richiesta di GET al `/query-templates` punto finale.

**Formato API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facoltativo*) Parametri aggiunti al percorso della richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e commerciale (`&`). I parametri disponibili sono elencati di seguito. |

**Parametri query**

Di seguito è riportato un elenco dei parametri di query disponibili per elencare i modelli di query. Tutti questi parametri sono facoltativi. Effettuare una chiamata a questo endpoint senza parametri recupererà tutti i modelli di query disponibili per la tua organizzazione.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio: `orderby=created` ordinerà i risultati in base a quelli creati in ordine crescente. Aggiunta di un `-` prima della creazione (`orderby=-created`) ordina gli elementi in base a quelli creati in ordine decrescente. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Esegue l&#39;offset dell&#39;elenco di risposte utilizzando la numerazione basata su zero. Ad esempio: `start=2` restituirà un elenco a partire dalla terza query elencata. (*Valore predefinito: 0*) |
| `property` | Filtrare i risultati in base ai campi. I filtri **deve** essere HTML fuggito. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `name` e `userId`. L’unico operatore supportato è `==` (uguale a). Ad esempio: `name==my_template` restituirà tutti i modelli di query con il nome `my_template`. |

**Richiesta**

La richiesta seguente recupera l’ultimo modello di query creato per la tua organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di modelli di query per l&#39;organizzazione IMS specificata. La risposta seguente restituisce l’ultimo modello di query creato per la tua organizzazione IMS.

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
                    "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
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
>Puoi utilizzare il valore di `_links.delete` a [elimina il modello di query](#delete-a-specified-query-template).

### Creare un modello di query

È possibile creare un modello di query effettuando una richiesta POST al `/query-templates` punto finale.

**Formato API**

```http
POST /query-templates
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una risposta corretta restituisce lo stato HTTP 202 (accettato) con i dettagli del modello di query appena creato.

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puoi utilizzare il valore di `_links.delete` a [elimina il modello di query](#delete-a-specified-query-template).

### Recupera un modello di query specificato

È possibile recuperare un modello di query specifico effettuando una richiesta di GET al `/query-templates/{TEMPLATE_ID}` e fornisce l’ID del modello di query nel percorso della richiesta.

**Formato API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | La `id` del modello di query che si desidera recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puoi utilizzare il valore di `_links.delete` a [elimina il modello di query](#delete-a-specified-query-template).

### Aggiornare un modello di query specificato

È possibile aggiornare un modello di query specifico effettuando una richiesta PUT al `/query-templates/{TEMPLATE_ID}` e fornisce l’ID del modello di query nel percorso della richiesta.

**Formato API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{TEMPLATE_ID}` | La `id` del modello di query che si desidera recuperare. |

**Richiesta**

>[!NOTE]
>
>La richiesta di PUT richiede la compilazione sia del campo sql che del campo name e **sovrascrivere** il contenuto corrente di tale modello di query.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una risposta corretta restituisce lo stato HTTP 202 (accettato) con le informazioni aggiornate per il modello di query specificato.

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Puoi utilizzare il valore di `_links.delete` a [elimina il modello di query](#delete-a-specified-query-template).

### Elimina un modello di query specificato

È possibile eliminare un modello di query specifico effettuando una richiesta di DELETE al `/query-templates/{TEMPLATE_ID}` e fornendo l&#39;ID del modello di query nel percorso della richiesta.

**Formato API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{TEMPLATE_ID}` | La `id` del modello di query che si desidera recuperare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
