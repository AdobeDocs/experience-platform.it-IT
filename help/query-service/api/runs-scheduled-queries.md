---
keywords: Experience Platform;home;argomenti popolari;servizio query;eseguire query pianificate;eseguire query pianificate;servizio query;query pianificate;query pianificate;
solution: Experience Platform
title: Endpoint API per l'esecuzione della query pianificata
topic-legacy: runs for scheduled queries
description: Nelle sezioni seguenti sono illustrate le varie chiamate API che è possibile effettuare per l’esecuzione di query pianificate con l’API del servizio query.
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# Endpoint di esecuzione della query pianificata

## Chiamate API di esempio

Ora che capisci quali intestazioni utilizzare, sei pronto per iniziare a effettuare chiamate a [!DNL Query Service] API. Le sezioni seguenti illustrano le varie chiamate API che puoi effettuare utilizzando [!DNL Query Service] API. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

### Recupera un elenco di tutte le esecuzioni per una query pianificata specificata

È possibile recuperare un elenco di tutte le esecuzioni per una query pianificata specifica, indipendentemente dal fatto che siano attualmente in esecuzione o già completate. A tal fine, invia una richiesta GET al `/schedules/{SCHEDULE_ID}/runs` punto finale, dove `{SCHEDULE_ID}` è `id` valore della query pianificata di cui si desidera recuperare le esecuzioni.

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La `id` valore della query pianificata che si desidera recuperare. |
| `{QUERY_PARAMETERS}` | (*Facoltativo*) Parametri aggiunti al percorso della richiesta che configurano i risultati restituiti nella risposta. È possibile includere più parametri, separati da e commerciale (`&`). I parametri disponibili sono elencati di seguito. |

**Parametri query**

Di seguito è riportato un elenco dei parametri di query disponibili per le esecuzioni di elenchi per una query pianificata specificata. Tutti questi parametri sono facoltativi. Effettuare una chiamata a questo endpoint senza parametri recupererà tutte le esecuzioni disponibili per la query pianificata specificata.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Specifica il campo in base al quale ordinare i risultati. I campi supportati sono `created` e `updated`. Ad esempio: `orderby=created` ordinerà i risultati in base a quelli creati in ordine crescente. Aggiunta di un `-` prima della creazione (`orderby=-created`) ordina gli elementi in base a quelli creati in ordine decrescente. |
| `limit` | Specifica il limite di dimensioni della pagina per controllare il numero di risultati inclusi in una pagina. (*Valore predefinito: 20*) |
| `start` | Esegue l&#39;offset dell&#39;elenco di risposte utilizzando la numerazione basata su zero. Ad esempio: `start=2` restituirà un elenco a partire dalla terza query elencata. (*Valore predefinito: 0*) |
| `property` | Filtrare i risultati in base ai campi. I filtri **deve** essere HTML fuggito. Le virgole vengono utilizzate per combinare più set di filtri. I campi supportati sono `created`, `state`e `externalTrigger`. L’elenco degli operatori supportati è `>` (maggiore di), `<` (minore di), e  `==` (uguale a), e `!=` (diverso da). Ad esempio: `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` restituirà tutte le esecuzioni create, completate e create manualmente dopo il 20 aprile 2019. |

**Richiesta**

La richiesta seguente recupera gli ultimi quattro esecuzioni per la query pianificata specificata.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di esecuzioni per la query pianificata specificata come JSON. La risposta seguente restituisce gli ultimi quattro esecuzioni per la query pianificata specificata.

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
>Puoi utilizzare il valore di `_links.cancel` a [interrompe un&#39;esecuzione per una query pianificata specificata](#immediately-stop-a-run-for-a-specific-scheduled-query).

### Attiva immediatamente un&#39;esecuzione per una query pianificata specifica

È possibile attivare immediatamente un&#39;esecuzione per una query pianificata specificata effettuando una richiesta di POST al `/schedules/{SCHEDULE_ID}/runs` punto finale, dove `{SCHEDULE_ID}` è `id` valore della query pianificata di cui si desidera attivare l&#39;esecuzione.

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

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Recupera i dettagli di un&#39;esecuzione per una query pianificata specifica

È possibile recuperare i dettagli relativi a un&#39;esecuzione per una query pianificata specifica effettuando una richiesta di GET al `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` e fornisce sia l’ID della query pianificata che l’esecuzione nel percorso della richiesta.

**Formato API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La `id` valore della query pianificata di cui si desidera recuperare i dettagli nell&#39;esecuzione. |
| `{RUN_ID}` | La `id` valore dell&#39;esecuzione che si desidera recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli dell&#39;esecuzione specificata.

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

### Interrompere immediatamente un&#39;esecuzione per una query pianificata specifica

È possibile interrompere immediatamente un&#39;esecuzione per una query pianificata specifica effettuando una richiesta di PATCH al `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` e fornisce sia l’ID della query pianificata che l’esecuzione nel percorso della richiesta.

**Formato API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La `id` valore della query pianificata di cui si desidera recuperare i dettagli nell&#39;esecuzione. |
| `{RUN_ID}` | La `id` valore dell&#39;esecuzione che si desidera recuperare. |

**Richiesta**

Questa richiesta API utilizza la sintassi della patch JSON per il relativo payload. Per ulteriori informazioni sul funzionamento della patch JSON, consulta il documento di base API .

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

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) con il seguente messaggio.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
