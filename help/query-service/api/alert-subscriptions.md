---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;avviso;
title: Endpoint API per sottoscrizioni di avvisi
description: Questa guida fornisce esempi di richieste HTTP e risposte per le varie chiamate API che puoi effettuare all’endpoint delle sottoscrizioni di avvisi con l’API del servizio query.
source-git-commit: cab7fcfda1bd8f6462af6e631f1fcee1f354d26b
workflow-type: tm+mt
source-wordcount: '2289'
ht-degree: 2%

---

# Endpoint API per sottoscrizioni di avvisi

Adobe Experience Platform Query Service consente di sottoscrivere avvisi per query ad hoc e pianificate. Gli avvisi possono essere ricevuti tramite e-mail, all’interno dell’interfaccia utente di Platform o per entrambi. Il contenuto delle notifiche è lo stesso per gli avvisi in-Platform e gli avvisi e-mail. Attualmente, gli avvisi di query possono essere abbonati solo a utilizzando [API del servizio query](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>Per ricevere avvisi e-mail, devi prima abilitare questa impostazione all’interno dell’interfaccia utente. Consulta la documentazione per [istruzioni su come abilitare gli avvisi e-mail](../../observability/alerts/ui.md#enable-email-alerts).

La tabella seguente spiega i tipi di avvisi supportati per diversi tipi di query:

| Tipo di query | Tipi di avviso supportati |
|---|---|
| Query ad hoc | `success` o `failed` esecuzioni. |
| Query pianificate | `start`, `success`oppure `failed` esecuzioni. |

>[!NOTE]
>
>Tutte le query non SELECT supportano le sottoscrizioni di avvisi e non è necessario essere il creatore di query per sottoscrivere un avviso. Altri utenti possono inoltre registrarsi per gli avvisi relativi a una query che non hanno creato.

I seguenti avvisi si applicano senza un abbonamento avvisi:

* Al termine di un processo di query batch, gli utenti ricevono una notifica.
* Quando la durata di un processo di query batch supera una soglia, viene attivato un avviso alla persona che ha pianificato la query.

>[!NOTE]
>
>Le query utilizzate per i test possono essere escluse da questi avvisi se configurati in modo appropriato.

## Chiamate API di esempio

Nelle sezioni seguenti sono descritte le varie chiamate API che è possibile effettuare tramite l’API del servizio query. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

## Recupera un elenco di tutti gli avvisi per un’organizzazione e una sandbox {#get-list-of-org-alert-subs}

Recupera un elenco di tutti gli avvisi per una sandbox organizzazione effettuando una richiesta di GET al `/alert-subscriptions` punto finale.

**Formato API**

```http
GET /alert-subscriptions
```

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Risposta**

Una risposta corretta restituisce uno stato HTTP 200 e il `alerts` con informazioni sull’impaginazione e sulla versione. La `alerts` array contiene i dettagli di tutti gli avvisi relativi a un&#39;organizzazione e a una particolare sandbox. Sono disponibili al massimo tre avvisi per risposta, un avviso per ogni tipo di avviso è contenuto nel corpo della risposta.

>[!NOTE]
>
>La `alerts._links` nell&#39;oggetto `alerts` l&#39;array è stato troncato per brevità. Un esempio completo del `alerts._links` si trova nella [risposta della richiesta POST](#subscribe-users).

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `alerts.assetId` | ID della query che ha associato l’avviso a una particolare query. |
| `alerts.id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è composto dalla cartella in cui è memorizzato l’avviso, il `alertType`e l&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard di Platform Alerts](../../observability/alerts/ui.md). |
| `alerts.status` | L’avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled`e `disabling`. Un avviso è l’ascolto attivo degli eventi, in pausa per un utilizzo futuro mantenendo tutti gli abbonati e le impostazioni pertinenti, o la transizione tra questi stati. |
| `alerts.alertType` | Tipo di avviso. Sono disponibili tre valori potenziali per un avviso: <ul><li>`start`: Notifica un utente quando l’esecuzione della query è iniziata.</li><li>`success`: Notifica all’utente il completamento della query.</li><li>`failure`: Notifica all’utente se la query non riesce.</li></ul> |
| `alerts._links` | Fornisce informazioni sui metodi e gli endpoint disponibili che possono essere utilizzati per recuperare, aggiornare, modificare o eliminare le informazioni relative a questo ID avviso. |
| `_page` | L&#39;oggetto contiene proprietà per descrivere l&#39;ordine, le dimensioni, il numero totale di pagine e la pagina corrente. |
| `_links` | L’oggetto contiene riferimenti URI che possono essere utilizzati per ottenere la pagina successiva o precedente di risorse. |

## Recupera le informazioni di sottoscrizione dell’avviso per un particolare ID query o pianificazione {#retrieve-all-alert-subscriptions-by-id}

Recupera le informazioni di sottoscrizione dell’avviso per un particolare ID query o ID pianificazione effettuando una richiesta di GET al `/alert-subscriptions/{QUERY_ID}` o `/alert-subscriptions/{SCHEDULE_ID}` punto finale.

**Formato API**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{QUERY_ID}` | ID della query per la quale si desidera restituire le informazioni sulla sottoscrizione. |
| `{SCHEDULE_ID}` | ID della query pianificata per la quale si desidera restituire le informazioni sulla sottoscrizione. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Risposta**

Una risposta corretta restituisce uno stato HTTP pari a 200 e il valore `alerts` array che contiene informazioni di sottoscrizione per l’ID di query o pianificazione fornito.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `assetId` | L&#39;avviso è associato a questo ID. L&#39;ID può essere un ID query o un ID pianificazione. |
| `id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è composto dalla cartella in cui è memorizzato l’avviso, il `alertType`e l&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard di Platform Alerts](../../observability/alerts/ui.md). |
| `status` | L’avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled`e `disabling`. Un avviso è l’ascolto attivo degli eventi, in pausa per un utilizzo futuro mantenendo tutti gli abbonati e le impostazioni pertinenti, o la transizione tra questi stati. |
| `alertType` | Ogni avviso può avere tre diversi tipi di avviso. Sono: <ul><li>`start`: Notifica un utente quando l’esecuzione della query è iniziata.</li><li>`success`: Notifica all’utente il completamento della query.</li><li>`failure`: Notifica all’utente se la query non riesce.</li></ul> |
| `subscriptions.emailNotifications` | Array di indirizzi e-mail registrati di Adobe per gli utenti che si sono abbonati per ricevere e-mail per l’avviso. |
| `subscriptions.inContextNotifications` | Array di indirizzi e-mail registrati di Adobe per gli utenti che si sono abbonati alle notifiche dell’interfaccia utente per l’avviso. |

## Recupera le informazioni sulla sottoscrizione dell’avviso per una particolare query o pianificazione ID e tipo di avviso {#get-alert-info-by-id-and-alert-type}

Recupera le informazioni di sottoscrizione dell’avviso per un determinato ID e tipo di avviso effettuando una richiesta di GET al `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` punto finale. Questo è applicabile sia agli ID query che agli ID query pianificati.

**Formato API**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parametri | Descrizione |
| -------- | ----------- |
| `ALERT_TYPE` | Ogni avviso può avere tre diversi tipi di avviso. Sono: <ul><li>`start`: Notifica un utente quando l’esecuzione della query è iniziata.</li><li>`success`: Notifica all’utente il completamento della query.</li><li>`failure`: Notifica all’utente se la query non riesce.</li></ul> |
| `QUERY_ID` | Identificatore univoco della query da aggiornare. |
| `SCHEDULE_ID` | Identificatore univoco della query pianificata da aggiornare. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Risposta**

Una risposta corretta restituisce uno stato HTTP pari a 200 e tutti gli avvisi sottoscritti. Questo include l&#39;ID dell&#39;avviso, il tipo di avviso, gli ID e-mail registrati dell&#39;Adobe dell&#39;utente e il relativo canale di notifica preferito.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `assetId` | ID della query che ha associato l’avviso a una particolare query. |
| `alertType` | Tipo di avviso. Sono disponibili tre valori potenziali per un avviso: <ul><li>`start`: Notifica un utente quando l’esecuzione della query è iniziata.</li><li>`success`: Notifica all’utente il completamento della query.</li><li>`failure`: Notifica all’utente se la query non riesce.</li></ul> |
| `subscriptions` | Un oggetto utilizzato per trasmettere gli ID e-mail registrati Adobi associati agli avvisi e i canali in cui gli utenti riceveranno gli avvisi. |
| `subscriptions.inContextNotifications` | Array di indirizzi e-mail registrati di Adobe per gli utenti che si sono abbonati alle notifiche dell’interfaccia utente per l’avviso. |
| `subscriptions.emailNotifications` | Array di indirizzi e-mail registrati di Adobe per gli utenti che si sono abbonati per ricevere e-mail per l’avviso. |

## Recupera un elenco di tutti gli avvisi ai quali un utente è iscritto {#get-alert-subscription-list}

Recupera un elenco di tutti gli avvisi ai quali un utente si è iscritto effettuando una richiesta di GET al `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` punto finale. La risposta include il nome dell’avviso, gli ID, lo stato, il tipo di avviso e i canali di notifica.

**Formato API**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parametri | Descrizione |
| -------- | ----------- |
| `{EMAIL_ID}` | Un indirizzo e-mail registrato in un account di Adobe viene utilizzato per identificare gli utenti abbonati agli avvisi. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 e il `items` array con i dettagli degli avvisi sottoscritti dal `emailId` fornito.

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è composto dalla cartella in cui è memorizzato l’avviso, il `alertType`e l&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard di Platform Alerts](../../observability/alerts/ui.md). |
| `assetId` | ID della query che ha associato l’avviso a una particolare query. |
| `status` | L’avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled`e `disabling`. Un avviso è l’ascolto attivo degli eventi, in pausa per un utilizzo futuro mantenendo tutti gli abbonati e le impostazioni pertinenti, o la transizione tra questi stati. |
| `alertType` | Tipo di avviso. Sono disponibili tre valori potenziali per un avviso: <ul><li>`start`: Notifica un utente quando l’esecuzione della query è iniziata.</li><li>`success`: Notifica all’utente il completamento della query.</li><li>`failure`: Notifica all’utente se la query non riesce.</li></ul> |
| `subscriptions` | Un oggetto utilizzato per trasmettere gli ID e-mail registrati Adobi associati agli avvisi e i canali in cui gli utenti riceveranno gli avvisi. |
| `subscriptions.inContextNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. A `true` value conferma che gli avvisi devono essere forniti tramite l’interfaccia utente di . A `false` assicura che gli utenti non ricevano notifiche tramite quel canale. |
| `subscriptions.emailNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. A `true` Il valore conferma che gli avvisi devono essere forniti tramite e-mail. A `false` assicura che gli utenti non ricevano notifiche tramite quel canale. |

## Creare un avviso e abbonare gli utenti {#subscribe-users}

Per creare un avviso e abbonare un utente per riceverlo, effettua un `POST` richiesta al `/alert-subscriptions` punto finale. Questa richiesta associa una query a un nuovo avviso creato utilizzando un `assetId` e sottoscrive gli utenti agli avvisi relativi a tale query utilizzando `emailIds`.

>[!IMPORTANT]
>
>Puoi trasmettere fino a cinque ID e-mail registrati di Adobe in una singola richiesta. Per inviare un avviso a più di cinque utenti, è necessario effettuare richieste successive.

**Formato API**

```http
POST /alert-subscriptions
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `assetId` | L&#39;avviso è associato a questo ID. L&#39;ID può essere un ID query o un ID pianificazione. |
| `alertType` | Tipo di avviso. Sono disponibili tre valori potenziali per un avviso: <ul><li>`start`: Notifica un utente quando l’esecuzione della query è iniziata.</li><li>`success`: Notifica all’utente il completamento della query.</li><li>`failure`: Notifica all’utente se la query non riesce.</li></ul> |
| `subscriptions` | Un oggetto utilizzato per trasmettere gli ID e-mail registrati Adobi associati agli avvisi e i canali in cui gli utenti riceveranno gli avvisi. |
| `subscriptions.emailIds` | Array di indirizzi e-mail per identificare gli utenti che devono ricevere gli avvisi. Gli indirizzi e-mail **deve** essere registrati su un account Adobe. |
| `subscriptions.inContextNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. A `true` value conferma che gli avvisi devono essere forniti tramite l’interfaccia utente di . A `false` assicura che gli utenti non ricevano notifiche tramite quel canale. |
| `subscriptions.emailNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. A `true` Il valore conferma che gli avvisi devono essere forniti tramite e-mail. A `false` assicura che gli utenti non ricevano notifiche tramite quel canale. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (accettato) con i dettagli del nuovo avviso creato.

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è composto dalla cartella in cui è memorizzato l’avviso, il `alertType`e l&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard di Platform Alerts](../../observability/alerts/ui.md). |
| `_links` | Fornisce informazioni sui metodi e gli endpoint disponibili che possono essere utilizzati per recuperare, aggiornare, modificare o eliminare le informazioni relative a questo ID avviso. |

## Attivare o disattivare un avviso {#enable-or-disable-alert}

Questa richiesta fa riferimento a un particolare avviso utilizzando un ID di query o di pianificazione e un tipo di avviso e aggiorna lo stato dell’avviso a `enable` o `disable`. È possibile aggiornare lo stato di un avviso effettuando una `PATCH` richiesta al `/alert-subscriptions/{queryId}/{alertType}` o `/alert-subscriptions/{scheduleId}/{alertType}` punto finale.

**Formato API**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parametri | Descrizione |
| -------- | ----------- |
| `ALERT_TYPE` | Tipo di avviso. Sono disponibili tre valori potenziali per un avviso: <ul><li>`start`: Notifica un utente quando l’esecuzione della query è iniziata.</li><li>`success`: Notifica all’utente il completamento della query.</li><li>`failure`: Notifica all’utente se la query non riesce.</li></ul>Per modificarlo, è necessario specificare il tipo di avviso corrente nello spazio dei nomi dell’endpoint. |
| `QUERY_ID` | Identificatore univoco della query da aggiornare. |
| `SCHEDULE_ID` | Identificatore univoco della query pianificata da aggiornare. |

**Richiesta**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `op` | Operazione da eseguire. Attualmente, l&#39;unico valore accettato è `replace`. |
| `path` | Questo valore si riferisce allo spazio dei nomi nell&#39;endpoint. Attualmente, l&#39;unico valore accettato è `/status`. |
| `value` | In una richiesta PATCH riuscita, viene modificato il `status` valore dell&#39;avviso. Attualmente, i valori accettati sono `enable` o `disable`. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli dello stato, del tipo e dell’ID dell’avviso e della query a cui si riferisce.

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è composto dalla cartella in cui è memorizzato l’avviso, il `alertType`e l&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard di Platform Alerts](../../observability/alerts/ui.md). |
| `assetId` | L&#39;avviso è associato a questo ID. L&#39;ID può essere un ID query o un ID pianificazione. |
| `alertType` | Ogni avviso può avere tre diversi tipi di avviso. Sono: <ul><li>`start`: Notifica un utente quando l’esecuzione della query è iniziata.</li><li>`success`: Notifica all’utente il completamento della query.</li><li>`failure`: Notifica all’utente se la query non riesce.</li></ul> |
| `status` | L’avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled`e `disabling`. Un avviso è l’ascolto attivo degli eventi, in pausa per un utilizzo futuro mantenendo tutti gli abbonati e le impostazioni pertinenti, o la transizione tra questi stati. |

## Eliminare l’avviso per una query e un tipo di avviso specifici {#delete-alert-info-by-id-and-alert-type}

Eliminare un avviso per una query o un ID di pianificazione particolare e un tipo di avviso effettuando una richiesta di DELETE al `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` o `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` punto finale.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parametri | Descrizione |
| -------- | ----------- |
| `ALERT_TYPE` | Tipo di avviso. Sono disponibili tre valori potenziali per un avviso: <ul><li>`start`: Notifica un utente quando l’esecuzione della query è iniziata.</li><li>`success`: Notifica all’utente il completamento della query.</li><li>`failure`: Notifica all’utente se la query non riesce.</li></ul> La richiesta DELETE si applica solo al tipo di avviso specifico fornito. |
| `QUERY_ID` | Identificatore univoco della query da aggiornare. |
| `SCHEDULE_ID` | Identificatore univoco della query pianificata da aggiornare. |

**Richiesta**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Risposta**

Una risposta corretta restituisce uno stato HTTP 200 e un messaggio di conferma che include l’ID risorsa e il tipo di avviso dell’avviso eliminato.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Passaggi successivi

Questa guida ha trattato l&#39;uso del `/alert-subscriptions` endpoint nell’API del servizio query. Dopo aver letto questa guida hai ora una migliore comprensione su come creare un avviso per una query, abbonare gli utenti all’avviso, i tipi di avvisi disponibili e come recuperare, aggiornare ed eliminare le informazioni sull’abbonamento agli avvisi.

Consulta la sezione [Guida all’API del servizio query](./getting-started.md) per ulteriori informazioni su altre funzioni e operazioni disponibili.
