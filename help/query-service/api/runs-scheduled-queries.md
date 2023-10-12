---
keywords: Experience Platform;home;argomenti popolari;servizio query;eseguire query pianificate;eseguire query pianificate;servizio query;query pianificate;query pianificate;query pianificate;home;popular topic;query service;run scheduled queries;run scheduled query;Query service;Scheduled queries;scheduled query;
solution: Experience Platform
title: La query pianificata esegue l’endpoint API
description: Le sezioni seguenti descrivono le varie chiamate API che è possibile effettuare per eseguire query pianificate con l’API di Query Service.
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: e9639cb90a561adc59388ac77984edaf90f4bfdd
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 3%

---

# La query pianificata esegue l’endpoint

## Chiamate API di esempio

Ora che sai quali intestazioni utilizzare, puoi iniziare a effettuare chiamate al [!DNL Query Service] API. Le sezioni seguenti descrivono le varie chiamate API che puoi effettuare utilizzando [!DNL Query Service] API. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recuperare un elenco di tutte le esecuzioni per una query pianificata specificata

È possibile recuperare un elenco di tutte le esecuzioni per una query pianificata specifica, indipendentemente dal fatto che siano attualmente in esecuzione o già completate. A tale scopo, invia una richiesta GET al `/schedules/{SCHEDULE_ID}/runs` endpoint, dove `{SCHEDULE_ID}` è il `id` valore della query pianificata di cui si desidera recuperare le esecuzioni.

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata da recuperare. |
| `{QUERY_PARAMETERS}` | (*Facoltativo*) Parametri aggiunti al percorso della richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e commerciali (`&`). I parametri disponibili sono elencati di seguito. |

**Parametri query**

Di seguito è riportato un elenco dei parametri di query disponibili per l&#39;elenco delle esecuzioni per una query pianificata specificata. Tutti questi parametri sono facoltativi. Se si effettua una chiamata a questo endpoint senza parametri, verranno recuperate tutte le esecuzioni disponibili per la query pianificata specificata.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio: `orderby=created` I risultati verranno ordinati in base alla creazione in ordine crescente. Aggiunta di un `-` prima della creazione (`orderby=-created`) ordinerà gli elementi in base a quelli creati in ordine decrescente. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Specifica una marca temporale in formato ISO per ordinare i risultati. Se non viene specificata una data di inizio, la chiamata API restituirà prima le esecuzioni più vecchie, quindi continuerà a elencare i risultati più recenti<br> Le marche temporali ISO consentono diversi livelli di granularità in data e ora. Le marche temporali ISO di base hanno il formato di: `2020-09-07` per esprimere la data del 7 settembre 2020. Un esempio più complesso sarebbe scritto come `2022-11-05T08:15:30-05:00` e corrisponde al 5 novembre 2022, 8:15:30:00, ora standard USA orientale. È possibile fornire un fuso orario con scostamento UTC ed è indicato dal suffisso &quot;Z&quot; (`2020-01-01T01:01:01Z`). Se non viene fornito alcun fuso orario, per impostazione predefinita viene impostato su zero. |
| `property` | Filtra i risultati in base ai campi. I filtri **deve** essere HTML in escape. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `created`, `state`, e `externalTrigger`. L’elenco degli operatori supportati è `>` (maggiore di), `<` (minore di), e  `==` (uguale a), e `!=` (diverso da). Ad esempio: `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` restituirà tutte le esecuzioni create, riuscite e create manualmente dopo il 20 aprile 2019. |

**Richiesta**

La richiesta seguente recupera le ultime quattro esecuzioni per la query pianificata specificata.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di esecuzioni per la query pianificata specificata come JSON. La risposta seguente restituisce le ultime quattro esecuzioni per la query pianificata specificata.

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE]
>
>Puoi utilizzare il valore di `_links.cancel` a [interrompere un&#39;esecuzione per una query pianificata specificata](#immediately-stop-a-run-for-a-specific-scheduled-query).

### Attiva immediatamente un&#39;esecuzione per una query pianificata specifica

Puoi attivare immediatamente un’esecuzione per una query pianificata specificata effettuando una richiesta POST al `/schedules/{SCHEDULE_ID}/runs` endpoint, dove `{SCHEDULE_ID}` è il `id` valore della query pianificata di cui desideri attivare l’esecuzione.

**Formato API**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con il seguente messaggio.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Recuperare i dettagli di un&#39;esecuzione per una query pianificata specifica

Per recuperare i dettagli di un’esecuzione per una query pianificata specifica, effettua una richiesta GET al `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` e fornendo sia l’ID della query pianificata che l’esecuzione nel percorso della richiesta.

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata di cui si desidera recuperare i dettagli. |
| `{RUN_ID}` | Il `id` valore dell’esecuzione da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli dell’esecuzione specificata.

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### Interrompere immediatamente l&#39;esecuzione di una query pianificata specifica

Per interrompere immediatamente l’esecuzione di una query pianificata specifica, invia una richiesta PATCH al `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` e fornendo sia l’ID della query pianificata che l’esecuzione nel percorso della richiesta.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Il `id` valore della query pianificata di cui si desidera recuperare i dettagli. |
| `{RUN_ID}` | Il `id` valore dell’esecuzione da recuperare. |

**Richiesta**

Questa richiesta API utilizza la sintassi Patch JSON per il suo payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento API Fundals.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) con il seguente messaggio.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
