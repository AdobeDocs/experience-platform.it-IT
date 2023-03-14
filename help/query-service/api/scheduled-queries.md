---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query pianificate;query pianificate;query pianificate;
solution: Experience Platform
title: Endpoint Schedules
description: Le sezioni seguenti descrivono le varie chiamate API che è possibile effettuare per le query pianificate con l’API Query Service.
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 3%

---

# Endpoint Schedules

## Chiamate API di esempio

Ora che sai quali intestazioni utilizzare, puoi iniziare a effettuare chiamate al [!DNL Query Service] API. Le sezioni seguenti descrivono le varie chiamate API che puoi effettuare utilizzando [!DNL Query Service] API. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recuperare un elenco di query pianificate

Per recuperare un elenco di tutte le query pianificate per la tua organizzazione IMS, devi effettuare una richiesta GET al `/schedules` endpoint.

**Formato API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facoltativo*) Parametri aggiunti al percorso della richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e commerciali (`&`). I parametri disponibili sono elencati di seguito. |

**Parametri query**

Di seguito è riportato un elenco dei parametri di query disponibili per l&#39;elenco delle query pianificate. Tutti questi parametri sono facoltativi. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperate tutte le query pianificate disponibili per la tua organizzazione.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio: `orderby=created` I risultati verranno ordinati in base alla creazione in ordine crescente. Aggiunta di un `-` prima della creazione (`orderby=-created`) ordinerà gli elementi in base a quelli creati in ordine decrescente. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Sposta l&#39;elenco di risposte utilizzando la numerazione a base zero. Ad esempio: `start=2` restituirà un elenco a partire dalla terza query elencata. (*Valore predefinito: 0*) |
| `property` | Filtra i risultati in base ai campi. I filtri **deve** essere HTML in escape. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `created`, `templateId`, e `userId`. L’elenco degli operatori supportati è `>` (maggiore di), `<` (minore di), e `==` (uguale a) Ad esempio: `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituirà tutte le query pianificate in cui l’ID utente corrisponde a quello specificato. |

**Richiesta**

La richiesta seguente recupera la query pianificata più recente creata per la tua organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di query pianificate per l’organizzazione IMS specificata. La risposta seguente restituisce l’ultima query pianificata creata per l’organizzazione IMS.

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

Per creare una nuova query pianificata, devi eseguire una richiesta POST al `/schedules` endpoint. Quando crei una query pianificata nell’API, questa viene visualizzata anche nell’editor delle query. Per ulteriori informazioni sulle query pianificate nell’interfaccia utente, leggi [Documentazione di Query Editor](../ui/user-guide.md#scheduled-queries).

**Formato API**

```http
POST /schedules
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `query.sql` | La query SQL da creare. |
| `query.name` | Nome della query pianificata. |
| `schedule.schedule` | Pianificazione cron per la query. Per ulteriori informazioni sulle pianificazioni cron, leggere la [formato espressione cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentazione. In questo esempio, &quot;30 * * *&quot; significa che la query verrà eseguita ogni ora al segno dei 30 minuti.<br><br>In alternativa, è possibile utilizzare le seguenti espressioni abbreviate:<ul><li>`@once`: la query viene eseguita una sola volta.</li><li>`@hourly`: la query viene eseguita ogni ora all’inizio dell’ora. Equivale all’espressione cron `0 * * * *`.</li><li>`@daily`: la query viene eseguita una volta al giorno a mezzanotte. Equivale all’espressione cron `0 0 * * *`.</li><li>`@weekly`: la query viene eseguita una volta alla settimana, la domenica, a mezzanotte. Equivale all’espressione cron `0 0 * * 0`.</li><li>`@monthly`: la query viene eseguita una volta al mese, il primo giorno del mese, a mezzanotte. Equivale all’espressione cron `0 0 1 * *`.</li><li>`@yearly`: la query viene eseguita una volta all’anno, il 1° gennaio, a mezzanotte. Equivale all’espressione cron `1 0 0 1 1 *`. |
| `schedule.startDate` | Data di inizio per la query pianificata, scritta come timestamp UTC. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con i dettagli della query pianificata appena creata. Al termine dell’attivazione della query pianificata, il `state` cambierà da `REGISTERING` a `ENABLED`.

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
>Puoi utilizzare il valore di `_links.delete` a [elimina la query pianificata creata](#delete-a-specified-scheduled-query).

### Dettagli richiesta di una query pianificata specificata

Per recuperare informazioni per una query pianificata specifica, effettua una richiesta GET al `/schedules` e fornendo il relativo ID nel percorso della richiesta.

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della query pianificata specificata.

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
>Puoi utilizzare il valore di `_links.delete` a [elimina la query pianificata creata](#delete-a-specified-scheduled-query).

### Aggiorna i dettagli di una query pianificata specificata

Per aggiornare i dettagli di una query pianificata specificata, effettua una richiesta PATCH al `/schedules` e fornendo il relativo ID nel percorso della richiesta.

La richiesta PATCH supporta due percorsi diversi: `/state` e `/schedule/schedule`.

### Aggiorna stato query pianificata

È possibile aggiornare lo stato della query pianificata selezionata impostando `path` proprietà a `/state` e `value` proprietà come `enable` o `disable`.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata di cui si desidera eseguire il PATCH. |


**Richiesta**

Questa richiesta API utilizza la sintassi Patch JSON per il suo payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento API Fundals.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Operazione da eseguire sulla pianificazione della query. Il valore accettato è `replace`. |
| `path` | Percorso del valore a cui applicare la patch. In questo caso, poiché si sta aggiornando lo stato della query pianificata, è necessario impostare il valore `path` a `/state`. |
| `value` | Il valore aggiornato del `/state`. Questo valore può essere impostato come `enable` o `disable` per attivare o disattivare la query pianificata. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con il seguente messaggio.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Aggiorna pianificazione query pianificata

È possibile aggiornare la pianificazione cron della query pianificata impostando `path` proprietà a `/schedule/schedule` nel corpo della richiesta. Per ulteriori informazioni sulle pianificazioni cron, leggere la [formato espressione cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentazione.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata di cui si desidera eseguire il PATCH. |

**Richiesta**

Questa richiesta API utilizza la sintassi Patch JSON per il suo payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento API Fundals.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Operazione da eseguire sulla pianificazione della query. Il valore accettato è `replace`. |
| `path` | Percorso del valore a cui applicare la patch. In questo caso, poiché stai aggiornando la pianificazione della query pianificata, devi impostare il valore di `path` a `/schedule/schedule`. |
| `value` | Il valore aggiornato del `/schedule`. Questo valore deve essere sotto forma di una pianificazione cron. In questo esempio, la query pianificata verrà eseguita ogni ora al minuto 45. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con il seguente messaggio.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Elimina una query pianificata specificata

Per eliminare una query pianificata specificata, devi eseguire una richiesta DELETE al `/schedules` e fornendo l’ID della query pianificata da eliminare nel percorso della richiesta.

>[!NOTE]
>
>La pianificazione **deve** prima di essere eliminato.

**Formato API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata di cui si desidera eseguire il DELETE. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con il seguente messaggio.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
