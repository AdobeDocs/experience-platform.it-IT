---
keywords: Experience Platform;home;argomenti popolari;servizio query;modelli query;guida api;modelli;servizio query;
solution: Experience Platform
title: Endpoint API per modelli di query
description: Questa guida descrive le varie chiamate API dei modelli di query che puoi effettuare utilizzando l’API di Query Service.
role: Developer
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 3%

---

# Endpoint &quot;query templates&quot;

## Chiamate API di esempio

Le sezioni seguenti descrivono le varie chiamate API che è possibile effettuare utilizzando l&#39;API [!DNL Query Service]. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

Per informazioni sulla creazione di modelli tramite l&#39;interfaccia utente di Experience Platform, vedere la [documentazione dei modelli di query dell&#39;interfaccia utente](../ui/query-templates.md).

### Recuperare un elenco di modelli di query

Per recuperare un elenco di tutti i modelli di query per l&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/query-templates`.

**Formato API**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facoltativo*) Parametri aggiunti al percorso della richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e commerciali (`&`). I parametri disponibili sono elencati di seguito. |

**Parametri query**

Di seguito è riportato un elenco dei parametri di query disponibili per l&#39;elenco dei modelli di query. Tutti questi parametri sono facoltativi. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperati tutti i modelli di query disponibili per la tua organizzazione.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio, `orderby=created` ordinerà i risultati in base alla creazione in ordine crescente. L&#39;aggiunta di un `-` prima della creazione (`orderby=-created`) ordinerà gli elementi in base alla creazione in ordine decrescente. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Specifica una marca temporale in formato ISO per ordinare i risultati. Se non viene specificata alcuna data di inizio, la chiamata API restituirà prima i modelli creati più datati, quindi continuerà a elencare i risultati più recenti.<br> Le marche temporali ISO consentono diversi livelli di granularità in data e ora. I timestamp ISO di base assumono il formato di: `2020-09-07` per esprimere la data 7 settembre 2020. Un esempio più complesso verrebbe scritto come `2022-11-05T08:15:30-05:00` e corrisponde al 5 novembre 2022, 8:15:30, ora standard orientale USA. È possibile fornire un fuso orario con scostamento UTC ed è indicato dal suffisso &quot;Z&quot; (`2020-01-01T01:01:01Z`). Se non viene fornito alcun fuso orario, per impostazione predefinita viene impostato su zero. |
| `property` | Filtra i risultati in base ai campi. I filtri **devono** avere escape HTML. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `name` e `userId`. L&#39;unico operatore supportato è `==` (uguale a). Ad esempio, `name==my_template` restituirà tutti i modelli di query con il nome `my_template`. |

**Richiesta**

La richiesta seguente recupera il modello di query più recente creato per la tua organizzazione.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di modelli di query per l’organizzazione specificata. La risposta seguente restituisce l’ultimo modello di query creato per la tua organizzazione.

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
>È possibile utilizzare il valore di `_links.delete` per [eliminare il modello di query](#delete-a-specified-query-template).

### Creare un modello di query

È possibile creare un modello di query effettuando una richiesta POST all&#39;endpoint `/query-templates`.

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
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "name": "Sample query template",
        "queryParameters": {
            user_id : {USER_ID}
            }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `sql` | La query SQL da creare. È possibile utilizzare SQL standard o un parametro sostitutivo. Per utilizzare una sostituzione dei parametri nel codice SQL, è necessario anteporre la chiave del parametro a `$`. Ad esempio, `$key`, e forniscono i parametri utilizzati in SQL come coppie di valori chiave JSON nel campo `queryParameters`. I valori qui passati saranno i parametri predefiniti utilizzati nel modello. Se desideri ignorare questi parametri, devi sostituirli nella richiesta POST. |
| `name` | Nome del modello di query. |
| `queryParameters` | Associazione di valori chiave per sostituire eventuali valori con parametri nell&#39;istruzione SQL. È necessario solo **se** si stanno utilizzando sostituzioni di parametri all&#39;interno del codice SQL fornito. Su queste coppie chiave-valore non verrà eseguito alcun controllo del tipo di valore. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accettato) con i dettagli del modello di query appena creato.

```json
{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
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
>È possibile utilizzare il valore di `_links.delete` per [eliminare il modello di query](#delete-a-specified-query-template).

### Recuperare un modello di query specificato

È possibile recuperare un modello di query specifico effettuando una richiesta di GET all&#39;endpoint `/query-templates/{TEMPLATE_ID}` e fornendo l&#39;ID del modello di query nel percorso della richiesta.

**Formato API**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | Valore `id` del modello di query che si desidera recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del modello di query specificato.

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
>È possibile utilizzare il valore di `_links.delete` per [eliminare il modello di query](#delete-a-specified-query-template).

### Aggiornare un modello di query specificato

È possibile aggiornare un modello di query specifico effettuando una richiesta PUT all&#39;endpoint `/query-templates/{TEMPLATE_ID}` e fornendo l&#39;ID del modello di query nel percorso della richiesta.

**Formato API**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Valore `id` del modello di query che si desidera recuperare. |

**Richiesta**

>[!NOTE]
>
>La richiesta PUT richiede la compilazione sia del campo sql che del campo name e **sovrascrive** il contenuto corrente del modello di query.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "queryParameters": {
            user_id : {USER_ID}
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `sql` | La query SQL da creare. È possibile utilizzare SQL standard o un parametro sostitutivo. Per utilizzare una sostituzione dei parametri nel codice SQL, è necessario anteporre la chiave del parametro a `$`. Ad esempio, `$key`, e forniscono i parametri utilizzati in SQL come coppie di valori chiave JSON nel campo `queryParameters`. I valori qui passati saranno i parametri predefiniti utilizzati nel modello. Se desideri ignorare questi parametri, devi sostituirli nella richiesta POST. |
| `name` | Nome del modello di query. |
| `queryParameters` | Associazione di valori chiave per sostituire eventuali valori con parametri nell&#39;istruzione SQL. È necessario solo **se** si stanno utilizzando sostituzioni di parametri all&#39;interno del codice SQL fornito. Su queste coppie chiave-valore non verrà eseguito alcun controllo del tipo di valore. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con le informazioni aggiornate per il modello di query specificato.

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
>È possibile utilizzare il valore di `_links.delete` per [eliminare il modello di query](#delete-a-specified-query-template).

### Eliminare un modello di query specificato

È possibile eliminare un modello di query specifico effettuando una richiesta DELETE a `/query-templates/{TEMPLATE_ID}` e fornendo l&#39;ID del modello di query nel percorso della richiesta.

**Formato API**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Valore `id` del modello di query che si desidera recuperare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con il seguente messaggio.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
