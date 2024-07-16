---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query pianificate;query pianificate;query pianificate;
solution: Experience Platform
title: Endpoint Schedules
description: Le sezioni seguenti descrivono le varie chiamate API che è possibile effettuare per le query pianificate con l’API Query Service.
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 3%

---

# Endpoint Schedules

## Chiamate API di esempio

Ora che sai quali intestazioni utilizzare, puoi iniziare ad effettuare chiamate all&#39;API [!DNL Query Service]. Le sezioni seguenti descrivono le varie chiamate API che è possibile effettuare utilizzando l&#39;API [!DNL Query Service]. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recuperare un elenco di query pianificate

Per recuperare un elenco di tutte le query pianificate per l&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/schedules`.

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
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio, `orderby=created` ordinerà i risultati in base alla creazione in ordine crescente. L&#39;aggiunta di un `-` prima della creazione (`orderby=-created`) ordinerà gli elementi in base alla creazione in ordine decrescente. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Specifica una marca temporale in formato ISO per ordinare i risultati. Se non viene specificata una data di inizio, la chiamata API restituirà prima la query pianificata creata più datata, quindi continuerà a elencare i risultati più recenti.<br> Le marche temporali ISO consentono diversi livelli di granularità in data e ora. I timestamp ISO di base assumono il formato di: `2020-09-07` per esprimere la data 7 settembre 2020. Un esempio più complesso verrebbe scritto come `2022-11-05T08:15:30-05:00` e corrisponde al 5 novembre 2022, 8:15:30, ora standard orientale USA. È possibile fornire un fuso orario con scostamento UTC ed è indicato dal suffisso &quot;Z&quot; (`2020-01-01T01:01:01Z`). Se non viene fornito alcun fuso orario, per impostazione predefinita viene impostato su zero. |
| `property` | Filtra i risultati in base ai campi. I filtri **devono** avere escape HTML. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `created`, `templateId` e `userId`. L&#39;elenco degli operatori supportati è `>` (maggiore di), `<` (minore di) e `==` (uguale a). `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec`, ad esempio, restituirà tutte le query pianificate in cui l&#39;ID utente corrisponde a quello specificato. |

**Richiesta**

La richiesta seguente recupera la query pianificata più recente creata per la tua organizzazione.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di query pianificate per l’organizzazione specificata. La risposta seguente restituisce l’ultima query pianificata creata per la tua organizzazione.

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

Per creare una nuova query pianificata, eseguire una richiesta POST all&#39;endpoint `/schedules`. Quando crei una query pianificata nell’API, questa viene visualizzata anche nell’editor delle query. Per ulteriori informazioni sulle query pianificate nell&#39;interfaccia utente, leggere la [documentazione dell&#39;editor delle query](../ui/user-guide.md#scheduled-queries).

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
| `schedule.schedule` | Pianificazione cron per la query. Per ulteriori informazioni sulle pianificazioni cron, leggere la documentazione relativa al formato di espressione cron [cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). In questo esempio, &quot;30 * * *&quot; significa che la query verrà eseguita ogni ora al segno dei 30 minuti.<br><br>In alternativa, è possibile utilizzare le seguenti espressioni abbreviate:<ul><li>`@once`: la query viene eseguita una sola volta.</li><li>`@hourly`: la query viene eseguita ogni ora all&#39;inizio dell&#39;ora. Equivale all&#39;espressione cron `0 * * * *`.</li><li>`@daily`: la query viene eseguita una volta al giorno a mezzanotte. Equivale all&#39;espressione cron `0 0 * * *`.</li><li>`@weekly`: la query viene eseguita una volta alla settimana, la domenica, a mezzanotte. Equivale all&#39;espressione cron `0 0 * * 0`.</li><li>`@monthly`: la query viene eseguita una volta al mese, il primo giorno del mese, a mezzanotte. Equivale all&#39;espressione cron `0 0 1 * *`.</li><li>`@yearly`: la query viene eseguita una volta all&#39;anno, il 1° gennaio, a mezzanotte. Equivale all&#39;espressione cron `1 0 0 1 1 *`. |
| `schedule.startDate` | Data di inizio per la query pianificata, scritta come timestamp UTC. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con i dettagli della query pianificata appena creata. Al termine dell&#39;attivazione della query pianificata, `state` passerà da `REGISTERING` a `ENABLED`.

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
>Puoi usare il valore di `_links.delete` per [eliminare la query pianificata creata](#delete-a-specified-scheduled-query).

### Dettagli richiesta di una query pianificata specificata

Per recuperare informazioni per una query pianificata specifica, eseguire una richiesta GET all&#39;endpoint `/schedules` e fornire il relativo ID nel percorso della richiesta.

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valore `id` della query pianificata da recuperare. |

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
>Puoi usare il valore di `_links.delete` per [eliminare la query pianificata creata](#delete-a-specified-scheduled-query).

### Aggiorna i dettagli di una query pianificata specificata

Per aggiornare i dettagli di una query pianificata specificata, eseguire una richiesta PATCH all&#39;endpoint `/schedules` e specificare il relativo ID nel percorso della richiesta.

La richiesta PATCH supporta due percorsi diversi: `/state` e `/schedule/schedule`.

### Aggiorna stato query pianificata

È possibile aggiornare lo stato della query pianificata selezionata impostando la proprietà `path` su `/state` e la proprietà `value` come `enable` o `disable`.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valore `id` della query pianificata di cui si desidera eseguire il PATCH. |


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
| `path` | Percorso del valore a cui applicare la patch. In questo caso, poiché si sta aggiornando lo stato della query pianificata, è necessario impostare il valore di `path` su `/state`. |
| `value` | Valore aggiornato di `/state`. Questo valore può essere impostato come `enable` o `disable` per abilitare o disabilitare la query pianificata. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con il seguente messaggio.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Aggiorna pianificazione query pianificata

È possibile aggiornare la pianificazione cron della query pianificata impostando la proprietà `path` su `/schedule/schedule` nel corpo della richiesta. Per ulteriori informazioni sulle pianificazioni cron, leggere la documentazione relativa al formato di espressione cron [cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valore `id` della query pianificata di cui si desidera eseguire il PATCH. |

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
| `path` | Percorso del valore a cui applicare la patch. In questo caso, poiché si sta aggiornando la pianificazione della query pianificata, è necessario impostare il valore di `path` su `/schedule/schedule`. |
| `value` | Valore aggiornato di `/schedule`. Questo valore deve essere sotto forma di una pianificazione cron. In questo esempio, la query pianificata verrà eseguita ogni ora al minuto 45. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con il seguente messaggio.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Elimina una query pianificata specificata

È possibile eliminare una query pianificata specificata effettuando una richiesta DELETE all&#39;endpoint `/schedules` e fornendo l&#39;ID della query pianificata che si desidera eliminare nel percorso della richiesta.

>[!NOTE]
>
>La pianificazione **deve** essere disabilitata prima di essere eliminata.

**Formato API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valore `id` della query pianificata di cui si desidera eseguire il DELETE. |

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
