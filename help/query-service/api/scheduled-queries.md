---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query pianificate;query pianificate;
solution: Experience Platform
title: Endpoint API per query pianificate
topic-legacy: scheduled queries
description: Nelle sezioni seguenti sono illustrate le varie chiamate API che è possibile effettuare per query pianificate con l’API del servizio query.
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 3%

---

# Endpoint di query pianificate

## Chiamate API di esempio

Ora che conosci le intestazioni da utilizzare, sei pronto per iniziare a effettuare chiamate all’ API [!DNL Query Service]. Le sezioni seguenti illustrano le varie chiamate API che puoi effettuare tramite l’ API [!DNL Query Service] . Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recupera un elenco di query pianificate

Puoi recuperare un elenco di tutte le query pianificate per la tua organizzazione IMS effettuando una richiesta di GET all’ endpoint `/schedules` .

**Formato API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facoltativo*) Parametri aggiunti al percorso della richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e commerciali (`&`). I parametri disponibili sono elencati di seguito. |

**Parametri query**

Di seguito è riportato un elenco dei parametri di query disponibili per l’elenco delle query pianificate. Tutti questi parametri sono facoltativi. Effettuare una chiamata a questo endpoint senza parametri recupererà tutte le query pianificate disponibili per la tua organizzazione.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio, `orderby=created` ordinerà i risultati per creati in ordine crescente. L&#39;aggiunta di un `-` prima della creazione (`orderby=-created`) ordinerà gli elementi in base all&#39;ordine decrescente creato. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Esegue l&#39;offset dell&#39;elenco di risposte utilizzando la numerazione basata su zero. Ad esempio, `start=2` restituirà un elenco a partire dalla terza query elencata. (*Valore predefinito: 0*) |
| `property` | Filtrare i risultati in base ai campi. I filtri **devono essere in sequenza HTML.** Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `created`, `templateId` e `userId`. L’elenco degli operatori supportati è `>` (maggiore di), `<` (minore di) e `==` (uguale a). Ad esempio, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituirà tutte le query pianificate in cui l’ID utente è specificato. |

**Richiesta**

La richiesta seguente recupera la query pianificata più recente creata per la tua organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di query pianificate per l&#39;organizzazione IMS specificata. La risposta seguente restituisce l’ultima query pianificata creata per l’organizzazione IMS.

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### Crea una nuova query pianificata

Puoi creare una nuova query pianificata effettuando una richiesta di POST all’endpoint `/schedules` .

**Formato API**

```http
POST /schedules
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `query.dbName` | Nome del database per cui si sta creando una query pianificata. |
| `query.sql` | Query SQL da creare. |
| `query.name` | Nome della query pianificata. |
| `schedule.schedule` | La pianificazione cron per la query. Per ulteriori informazioni sulle pianificazioni cron, leggere la documentazione [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . In questo esempio, &quot;30 * * * * *&quot; significa che la query verrà eseguita ogni ora alla soglia dei 30 minuti. |
| `schedule.startDate` | La data di inizio della query pianificata, scritta come timestamp UTC. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (accettato) con i dettagli della query pianificata appena creata. Al termine dell’attivazione della query pianificata, la `state` passerà da `REGISTERING` a `ENABLED`.

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Puoi utilizzare il valore di `_links.delete` per [eliminare la query pianificata creata](#delete-a-specified-scheduled-query).

### Richiedi i dettagli di una query pianificata specificata

Puoi recuperare informazioni per una query pianificata specifica effettuando una richiesta di GET all’endpoint `/schedules` e fornendo il relativo ID nel percorso della richiesta.

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della query pianificata che si desidera recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della query pianificata specificata.

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Puoi utilizzare il valore di `_links.delete` per [eliminare la query pianificata creata](#delete-a-specified-scheduled-query).

### Aggiorna i dettagli di una query pianificata specificata

Puoi aggiornare i dettagli di una query pianificata specificata effettuando una richiesta PATCH all’endpoint `/schedules` e fornendo il relativo ID nel percorso della richiesta.

La richiesta di PATCH supporta due percorsi diversi: `/state` e `/schedule/schedule`.

### Aggiorna stato query pianificato

È possibile utilizzare `/state` per aggiornare lo stato della query pianificata selezionata - ENABLED o DISABLED. Per aggiornare lo stato, è necessario impostare il valore come `enable` o `disable`.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della query pianificata che si desidera recuperare. |


**Richiesta**

Questa richiesta API utilizza la sintassi della patch JSON per il relativo payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento di base API .

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `path` | Percorso del valore a cui si desidera applicare la patch. In questo caso, poiché stai aggiornando lo stato della query pianificata, devi impostare il valore di `path` su `/state`. |
| `value` | Il valore aggiornato di `/state`. Questo valore può essere impostato come `enable` o `disable` per abilitare o disabilitare la query pianificata. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Aggiorna pianificazione query pianificata

È possibile utilizzare `/schedule/schedule` per aggiornare la pianificazione cron della query pianificata. Per ulteriori informazioni sulle pianificazioni cron, leggere la documentazione [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) .

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della query pianificata che si desidera recuperare. |

**Richiesta**

Questa richiesta API utilizza la sintassi della patch JSON per il relativo payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento di base API .

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `path` | Percorso del valore a cui si desidera applicare la patch. In questo caso, poiché si aggiorna la pianificazione della query pianificata, è necessario impostare il valore di `path` su `/schedule/schedule`. |
| `value` | Il valore aggiornato di `/schedule`. Questo valore deve essere sotto forma di programma cron. In questo esempio, la query pianificata verrà eseguita ogni ora alla soglia di 45 minuti. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Elimina una query pianificata specificata

È possibile eliminare una query pianificata specificata effettuando una richiesta DELETE all’endpoint `/schedules` e fornendo l’ID della query pianificata che si desidera eliminare nel percorso della richiesta.

>[!NOTE]
>
>La pianificazione **deve** essere disabilitata prima di essere eliminata.

**Formato API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il valore `id` della query pianificata che si desidera recuperare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
