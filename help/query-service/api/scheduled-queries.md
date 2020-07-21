---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Query Service
topic: scheduled queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 3%

---


# Query pianificate

## Chiamate API di esempio

Ora che hai compreso quali intestazioni utilizzare, sei pronto a iniziare a effettuare chiamate all&#39; [!DNL Query Service] API. Le sezioni seguenti descrivono le varie chiamate API che potete effettuare tramite l&#39; [!DNL Query Service] API. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recupero di un elenco di query pianificate

È possibile recuperare un elenco di tutte le query pianificate per l&#39;organizzazione IMS effettuando una richiesta GET all&#39; `/schedules` endpoint.

**Formato API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facoltativo*) Parametri aggiunti al percorso di richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e-mail (`&`). I parametri disponibili sono elencati di seguito. |

**Parametri query**

Di seguito è riportato un elenco di parametri di query disponibili per elencare le query pianificate. Tutti questi parametri sono facoltativi. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperate tutte le query pianificate disponibili per l&#39;organizzazione.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio, `orderby=created` ordinerà i risultati in base alla creazione in ordine crescente. Se si aggiunge un elemento `-` prima della creazione (`orderby=-created`), gli elementi verranno ordinati in base alla creazione in ordine decrescente. |
| `limit` | Specifica il limite delle dimensioni di pagina per controllare il numero di risultati inclusi in una pagina. (valore *predefinito: 20*) |
| `start` | Consente di scostare l&#39;elenco di risposte utilizzando la numerazione basata su zero. Ad esempio, `start=2` restituirà un elenco a partire dalla terza query elencata. (valore *predefinito: 0*) |
| `property` | Filtrare i risultati in base ai campi. I filtri **devono** essere con escape HTML. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `created`, `templateId`e `userId`. L&#39;elenco degli operatori supportati è `>` (maggiore di), `<` (minore di) e `==` (uguale a). Ad esempio, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituisce tutte le query pianificate in cui l&#39;ID utente è specificato. |

**Richiesta**

La richiesta seguente recupera la query pianificata più recente creata per l&#39;organizzazione IMS.

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

### Creazione di una nuova query pianificata

Potete creare una nuova query pianificata effettuando una richiesta POST all&#39; `/schedules` endpoint.

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
| `query.dbName` | Nome del database per il quale si sta creando una query pianificata. |
| `query.sql` | Query SQL da creare. |
| `query.name` | Nome della query pianificata. |
| `schedule.schedule` | Pianificazione cron per la query. Per ulteriori informazioni sulle pianificazioni cron, consulta la documentazione sul formato [delle espressioni](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. In questo esempio, &quot;30 * * * * * *&quot; significa che la query verrà eseguita ogni ora con l&#39;indicatore dei 30 minuti. |
| `schedule.startDate` | Data di inizio della query pianificata, scritta come marca temporale UTC. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con i dettagli della query pianificata appena creata. Una volta terminata l&#39;attivazione della query pianificata, la query `state` passerà da `REGISTERING` a `ENABLED`.

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
>È possibile utilizzare il valore di `_links.delete` per [eliminare la query](#delete-a-specified-scheduled-query)pianificata creata.

### Dettagli richiesta di una query pianificata specificata

Potete recuperare informazioni per una specifica query pianificata effettuando una richiesta GET all&#39; `/schedules` endpoint e fornendo il relativo ID nel percorso della richiesta.

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata che si desidera recuperare. |

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
>È possibile utilizzare il valore di `_links.delete` per [eliminare la query](#delete-a-specified-scheduled-query)pianificata creata.

### Aggiorna i dettagli di una query pianificata specificata

È possibile aggiornare i dettagli di una query pianificata specificata effettuando una richiesta PATCH all&#39; `/schedules` endpoint fornendo il relativo ID nel percorso della richiesta.

La richiesta PATCH supporta due percorsi diversi: `/state` e `/schedule/schedule`.

### Aggiorna stato query pianificato

È possibile utilizzare `/state` per aggiornare lo stato della query pianificata selezionata - ENABLED o DISABLED. Per aggiornare lo stato, è necessario impostare il valore come `enable` o `disable`.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata che si desidera recuperare. |


**Richiesta**

Questa richiesta API utilizza la sintassi della patch JSON per il payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento sui fondamentali dell&#39;API.

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
| `path` | Percorso del valore da applicare alla patch. In questo caso, poiché si aggiorna lo stato della query pianificata, è necessario impostare il valore di `path` a `/state`. |
| `value` | Il valore aggiornato dell&#39; `/state`. Questo valore può essere impostato come `enable` o `disable` per abilitare o disabilitare la query pianificata. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Aggiorna pianificazione query pianificata

È possibile utilizzare `/schedule/schedule` per aggiornare la pianificazione cron della query pianificata. Per ulteriori informazioni sulle pianificazioni cron, consulta la documentazione sul formato [delle espressioni](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata che si desidera recuperare. |

**Richiesta**

Questa richiesta API utilizza la sintassi della patch JSON per il payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento sui fondamentali dell&#39;API.

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
| `path` | Percorso del valore da applicare alla patch. In questo caso, poiché si sta aggiornando la pianificazione della query pianificata, è necessario impostare il valore di `path` a `/schedule/schedule`. |
| `value` | Il valore aggiornato dell&#39; `/schedule`. Questo valore deve essere sotto forma di programmazione cron. In questo esempio, la query pianificata verrà eseguita ogni ora con l&#39;indicatore dei 45 minuti. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Elimina una query pianificata specificata

È possibile eliminare una query pianificata specificata effettuando una richiesta di DELETE all&#39; `/schedules` endpoint e fornendo l&#39;ID della query pianificata che si desidera eliminare nel percorso della richiesta.

>[!NOTE]
>
>La pianificazione **deve** essere disattivata prima di essere eliminata.

**Formato API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata che si desidera recuperare. |

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
