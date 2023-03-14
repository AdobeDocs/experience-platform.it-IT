---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;avviso;
title: Endpoint sottoscrizioni avvisi
description: Questa guida fornisce esempi di richieste HTTP e risposte per le varie chiamate API che puoi effettuare all’endpoint di abbonamenti agli avvisi con l’API Query Service.
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 2%

---

# Endpoint &quot;Alert Subscriptions&quot;

Adobe Experience Platform Query Service consente di ricevere avvisi sia per le query ad hoc che per quelle pianificate. Gli avvisi possono essere ricevuti tramite e-mail, nell’interfaccia di Platform o in entrambe le modalità. Il contenuto della notifica è lo stesso per gli avvisi e-mail in-Platform. Attualmente, gli avvisi di query possono essere sottoscritti solo utilizzando [API servizio query](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>Per ricevere gli avvisi e-mail devi prima abilitare questa impostazione nell’interfaccia utente. Consulta la documentazione per [istruzioni su come abilitare gli avvisi e-mail](../../observability/alerts/ui.md#enable-email-alerts).

La tabella seguente spiega i tipi di avviso supportati per i diversi tipi di query:

| Tipo di query | Tipi di avviso supportati |
|---|---|
| Query ad hoc | `success` o `failed` esecuzioni. |
| Query pianificate | `start`, `success`, o `failed` esecuzioni. |

>[!NOTE]
>
>Tutte le query non SELECT supportano le sottoscrizioni di avvisi e non è necessario essere l&#39;autore della query per sottoscrivere un avviso. Anche altri utenti possono effettuare la registrazione per gli avvisi relativi a una query che non hanno creato.

Gli avvisi seguenti si applicano senza un abbonamento agli avvisi:

* Al termine di un processo di query batch, gli utenti ricevono una notifica.
* Quando la durata di un processo di query batch supera una soglia, viene attivato un avviso per la persona che ha pianificato la query.

>[!NOTE]
>
>Le query utilizzate per il test possono essere escluse da questi avvisi se configurate in modo appropriato.

## Chiamate API di esempio

Le sezioni seguenti descrivono le varie chiamate API che è possibile effettuare utilizzando l’API di Query Service. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

## Recuperare un elenco di tutti gli avvisi per un’organizzazione e una sandbox {#get-list-of-org-alert-subs}

Recuperare un elenco di tutti gli avvisi per una sandbox dell’organizzazione effettuando una richiesta GET al `/alert-subscriptions` endpoint.

**Formato API**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | (Facoltativo) Sono stati aggiunti dei parametri al percorso della richiesta per configurare i risultati restituiti nella risposta. È possibile includere più parametri, separati dal simbolo &amp;. I parametri disponibili sono elencati di seguito. |

**Parametri query**

Di seguito è riportato un elenco dei parametri di query disponibili per l&#39;elenco delle query. Tutti questi parametri sono facoltativi. Effettuando una chiamata a questo endpoint senza parametri, verranno recuperate tutte le query disponibili per la tua organizzazione.

| Parametro | Descrizione |
| --------- | ----------- |
| `orderby` | Campo che specifica l&#39;ordine dei risultati. I campi supportati sono `created` e `updated`. Anteponi il nome della proprietà a `+` per ascendente e `-` per ordine decrescente. Il valore predefinito è `-created`. Si noti che il segno più (`+`) deve essere evaso con `%2B`. Ad esempio `%2Bcreated` è il valore di un ordine creato crescente. |
| `pagesize` | Utilizza questo parametro per controllare il numero di record che desideri recuperare dalla chiamata API per pagina. Il limite predefinito è impostato al massimo di 50 record per pagina. |
| `page` | Indicare il numero di pagina dei risultati restituiti per i quali si desidera visualizzare i record. |
| `property` | Filtra i risultati in base ai campi selezionati. I filtri **deve** essere HTML in escape. Le virgole vengono utilizzate per combinare più set di filtri. Le seguenti proprietà consentono l’applicazione di filtri: <ul><li>id</li><li>assetId</li><li>stato</li><li>alertType</li></ul> Gli operatori supportati sono `==` (uguale a) Ad esempio: `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituirà l’avviso con un ID corrispondente. |

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

Una risposta corretta restituisce lo stato HTTP 200 e il `alerts` array con informazioni sulla paginazione e sulla versione. Il `alerts` array contiene i dettagli di tutti gli avvisi per un’organizzazione e una particolare sandbox. Per ogni risposta sono disponibili al massimo tre avvisi, uno per ogni tipo di avviso è contenuto nel corpo della risposta.

>[!NOTE]
>
>Il `alerts._links` oggetto in `alerts` l&#39;array è stato troncato per brevità. Un esempio completo del `alerts._links` L&#39;oggetto si trova nel [risposta della richiesta POST](#subscribe-users).

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
| `alerts.assetId` | ID della query che ha associato l’avviso a una determinata query. |
| `alerts.id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è costituito dalla cartella in cui è memorizzato l’avviso, il `alertType`e l’ID del flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `alerts.status` | L’avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled`, e `disabling`. Un avviso è l’ascolto attivo degli eventi, messo in pausa per utilizzi futuri mantenendo tutti gli abbonati e le impostazioni rilevanti, oppure la transizione tra questi stati. |
| `alerts.alertType` | Tipo di avviso. Un avviso può avere tre valori: <ul><li>`start`: avvisa l’utente quando viene avviata l’esecuzione della query.</li><li>`success`: avvisa l’utente al completamento della query.</li><li>`failure`: avvisa l’utente se la query non riesce.</li></ul> |
| `alerts._links` | Fornisce informazioni sui metodi e gli endpoint disponibili che possono essere utilizzati per recuperare, aggiornare, modificare o eliminare informazioni relative a questo ID avviso. |
| `_page` | L&#39;oggetto contiene proprietà che descrivono l&#39;ordine, la dimensione, il numero totale di pagine e la pagina corrente. |
| `_links` | L’oggetto contiene riferimenti URI che possono essere utilizzati per ottenere la pagina successiva o precedente delle risorse. |

## Recuperare le informazioni sulla sottoscrizione dell’avviso per una particolare query o ID pianificazione {#retrieve-all-alert-subscriptions-by-id}

Recupera le informazioni sulla sottoscrizione dell’avviso per un determinato ID di query o ID di pianificazione effettuando una richiesta di GET al `/alert-subscriptions/{QUERY_ID}` o `/alert-subscriptions/{SCHEDULE_ID}` endpoint.

**Formato API**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{QUERY_ID}` | ID della query per la quale si desidera restituire le informazioni di abbonamento. |
| `{SCHEDULE_ID}` | ID della query pianificata per la quale si desidera restituire le informazioni di abbonamento. |

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

Una risposta corretta restituisce lo stato HTTP 200 e il `alerts` array che contiene le informazioni di abbonamento per l’ID di query o pianificazione fornito.

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
| `assetId` | L’avviso è associato a questo ID. L’ID può essere un ID query o un ID pianificazione. |
| `id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è costituito dalla cartella in cui è memorizzato l’avviso, il `alertType`e l’ID del flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `status` | L’avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled`, e `disabling`. Un avviso è l’ascolto attivo degli eventi, messo in pausa per utilizzi futuri mantenendo tutti gli abbonati e le impostazioni rilevanti, oppure la transizione tra questi stati. |
| `alertType` | Ogni avviso può avere tre tipi diversi di avviso. Sono: <ul><li>`start`: avvisa l’utente quando viene avviata l’esecuzione della query.</li><li>`success`: avvisa l’utente al completamento della query.</li><li>`failure`: avvisa l’utente se la query non riesce.</li></ul> |
| `subscriptions.emailNotifications` | Un array di Adobi di indirizzi e-mail registrati per gli utenti che si sono abbonati a ricevere e-mail per l’avviso. |
| `subscriptions.inContextNotifications` | Un array di Adobi di indirizzi e-mail registrati per gli utenti che si sono abbonati alle notifiche dell’interfaccia utente per l’avviso. |

## Recuperare le informazioni di sottoscrizione degli avvisi per una query o un ID pianificazione e un tipo di avviso specifici {#get-alert-info-by-id-and-alert-type}

Recuperare le informazioni sull’abbonamento agli avvisi per un determinato ID e tipo di avviso effettuando una richiesta GET al `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` endpoint. Questo è applicabile sia agli ID query che a quelli pianificati.

**Formato API**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parametri | Descrizione |
| -------- | ----------- |
| `ALERT_TYPE` | Questa proprietà descrive lo stato di esecuzione della query che attiva un avviso. La risposta includerà solo le informazioni di abbonamento agli avvisi per avvisi di questo tipo. Ogni avviso può avere tre tipi diversi di avviso. Sono: <ul><li>`start`: avvisa l’utente quando viene avviata l’esecuzione della query.</li><li>`success`: avvisa l’utente al completamento della query.</li><li>`failure`: avvisa l’utente se la query non riesce.</li></ul> |
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 e tutti gli avvisi a cui è abbonato. Ciò include l’ID dell’avviso, il tipo di avviso, gli ID e-mail registrati dell’Adobe dell’abbonato e il relativo canale di notifica preferito.

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
| `assetId` | ID della query che ha associato l’avviso a una determinata query. |
| `alertType` | Tipo di avviso. Un avviso può avere tre valori: <ul><li>`start`: avvisa l’utente quando viene avviata l’esecuzione della query.</li><li>`success`: avvisa l’utente al completamento della query.</li><li>`failure`: avvisa l’utente se la query non riesce.</li></ul> |
| `subscriptions` | Oggetto utilizzato per trasmettere gli ID e-mail registrati dell’Adobe associati agli avvisi e i canali in cui gli utenti riceveranno gli avvisi. |
| `subscriptions.inContextNotifications` | Un array di Adobi di indirizzi e-mail registrati per gli utenti che si sono abbonati alle notifiche dell’interfaccia utente per l’avviso. |
| `subscriptions.emailNotifications` | Un array di Adobi di indirizzi e-mail registrati per gli utenti che si sono abbonati a ricevere e-mail per l’avviso. |

## Recuperare un elenco di tutti gli avvisi a cui è abbonato un utente {#get-alert-subscription-list}

Recupera un elenco di tutti gli avvisi a cui un utente è abbonato effettuando una richiesta GET al `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` endpoint. La risposta include il nome, gli ID, lo stato, il tipo di avviso e i canali di notifica dell’avviso.

**Formato API**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parametri | Descrizione |
| -------- | ----------- |
| `{EMAIL_ID}` | Un indirizzo e-mail registrato su un account di Adobe viene utilizzato per identificare gli utenti abbonati agli avvisi. |
| `orderby` | Campo che specifica l&#39;ordine dei risultati. I campi supportati sono `created` e `updated`. Anteponi il nome della proprietà a `+` per ascendente e `-` per ordine decrescente. Il valore predefinito è `-created`. Si noti che il segno più (`+`) deve essere evaso con `%2B`. Ad esempio `%2Bcreated` è il valore di un ordine creato crescente. |
| `pagesize` | Utilizza questo parametro per controllare il numero di record che desideri recuperare dalla chiamata API per pagina. Il limite predefinito è impostato al massimo di 50 record per pagina. |
| `page` | Indicare il numero di pagina dei risultati restituiti per i quali si desidera visualizzare i record. |
| `property` | Filtra i risultati in base ai campi selezionati. I filtri **deve** essere HTML in escape. Le virgole vengono utilizzate per combinare più set di filtri. Le seguenti proprietà consentono il filtraggio: <ul><li>id</li><li>assetId</li><li>stato</li><li>alertType</li></ul> Gli operatori supportati sono `==` (uguale a) Ad esempio: `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituirà l’avviso con un ID corrispondente. |

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

Una risposta corretta restituisce lo stato HTTP 200 e il `items` con i dettagli degli avvisi a cui si è iscritto il `emailId` fornite.

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
| `name` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è costituito dalla cartella in cui è memorizzato l’avviso, il `alertType`e l’ID del flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `assetId` | ID della query che ha associato l’avviso a una determinata query. |
| `status` | L’avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled`, e `disabling`. Un avviso è l’ascolto attivo degli eventi, messo in pausa per utilizzi futuri mantenendo tutti gli abbonati e le impostazioni rilevanti, oppure la transizione tra questi stati. |
| `alertType` | Tipo di avviso. Un avviso può avere tre valori: <ul><li>`start`: avvisa l’utente quando viene avviata l’esecuzione della query.</li><li>`success`: avvisa l’utente al completamento della query.</li><li>`failure`: avvisa l’utente se la query non riesce.</li></ul> |
| `subscriptions` | Oggetto utilizzato per trasmettere gli ID e-mail registrati dell’Adobe associati agli avvisi e i canali in cui gli utenti riceveranno gli avvisi. |
| `subscriptions.inContextNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. A `true` Il valore conferma che gli avvisi devono essere forniti tramite l’interfaccia utente. A `false` garantisce che gli utenti non ricevano notifiche tramite tale canale. |
| `subscriptions.emailNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. A `true` Il valore conferma che gli avvisi devono essere forniti tramite e-mail. A `false` garantisce che gli utenti non ricevano notifiche tramite tale canale. |

## Creare un avviso e abbonare gli utenti {#subscribe-users}

Per creare un avviso e abbonare un utente affinché lo riceva, effettua una `POST` richiesta al `/alert-subscriptions` endpoint. Questa richiesta associa una query a un avviso appena creato utilizzando un `assetId` e invia avvisi agli utenti per tale query tramite l&#39;utilizzo di `emailIds`.

>[!IMPORTANT]
>
>Puoi trasmettere fino a cinque ID e-mail registrati come Adobe in una singola richiesta. Per segnalare un avviso a più di cinque utenti, è necessario effettuare richieste successive.

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
| `assetId` | L’avviso è associato a questo ID. L’ID può essere un ID query o un ID pianificazione. |
| `alertType` | Tipo di avviso. Un avviso può avere tre valori: <ul><li>`start`: avvisa l’utente quando viene avviata l’esecuzione della query.</li><li>`success`: avvisa l’utente al completamento della query.</li><li>`failure`: avvisa l’utente se la query non riesce.</li></ul> |
| `subscriptions` | Oggetto utilizzato per trasmettere gli ID e-mail registrati dell’Adobe associati agli avvisi e i canali in cui gli utenti riceveranno gli avvisi. |
| `subscriptions.emailIds` | Un array di indirizzi e-mail per identificare gli utenti che devono ricevere gli avvisi. Gli indirizzi e-mail **deve** essere registrati su un account di Adobe. |
| `subscriptions.inContextNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. A `true` Il valore conferma che gli avvisi devono essere forniti tramite l’interfaccia utente. A `false` garantisce che gli utenti non ricevano notifiche tramite tale canale. |
| `subscriptions.emailNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. A `true` Il valore conferma che gli avvisi devono essere forniti tramite e-mail. A `false` garantisce che gli utenti non ricevano notifiche tramite tale canale. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accettato) con i dettagli dell’avviso appena creato.

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
| `id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è costituito dalla cartella in cui è memorizzato l’avviso, il `alertType`e l’ID del flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `_links` | Fornisce informazioni sui metodi e gli endpoint disponibili che possono essere utilizzati per recuperare, aggiornare, modificare o eliminare informazioni relative a questo ID avviso. |

## Attivare o disattivare un avviso {#enable-or-disable-alert}

Questa richiesta fa riferimento a un determinato avviso utilizzando una query o un ID pianificazione e un tipo di avviso e aggiorna lo stato dell’avviso impostandolo su `enable` o `disable`. È possibile aggiornare lo stato di un avviso effettuando una `PATCH` richiesta al `/alert-subscriptions/{queryId}/{alertType}` o `/alert-subscriptions/{scheduleId}/{alertType}` endpoint.

**Formato API**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parametri | Descrizione |
| -------- | ----------- |
| `ALERT_TYPE` | Tipo di avviso. Un avviso può avere tre valori: <ul><li>`start`: avvisa l’utente quando viene avviata l’esecuzione della query.</li><li>`success`: avvisa l’utente al completamento della query.</li><li>`failure`: avvisa l’utente se la query non riesce.</li></ul>È necessario specificare il tipo di avviso corrente nello spazio dei nomi dell&#39;endpoint per modificarlo. |
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
| `op` | Operazione da eseguire. Attualmente, l’unico valore accettato è `replace`. |
| `path` | Questo valore si riferisce allo spazio dei nomi nell’endpoint. Attualmente, l’unico valore accettato è `/status`. |
| `value` | In caso di esito positivo, la richiesta PATCH cambia il `status` valore dell’avviso. Attualmente, i valori accettati sono `enable` o `disable`. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli dello stato, del tipo e dell’ID dell’avviso, nonché la query a cui si riferisce.

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
| `id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell’avviso è costituito dalla cartella in cui è memorizzato l’avviso, il `alertType`e l’ID del flusso. Le informazioni sugli avvisi disponibili sono disponibili nella sezione [Documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `assetId` | L’avviso è associato a questo ID. L’ID può essere un ID query o un ID pianificazione. |
| `alertType` | Ogni avviso può avere tre tipi diversi di avviso. Sono: <ul><li>`start`: avvisa l’utente quando viene avviata l’esecuzione della query.</li><li>`success`: avvisa l’utente al completamento della query.</li><li>`failure`: avvisa l’utente se la query non riesce.</li></ul> |
| `status` | L’avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled`, e `disabling`. Un avviso è l’ascolto attivo degli eventi, messo in pausa per utilizzi futuri mantenendo tutti gli abbonati e le impostazioni rilevanti, oppure la transizione tra questi stati. |

## Eliminare l&#39;avviso per una query e un tipo di avviso specifici {#delete-alert-info-by-id-and-alert-type}

Eliminare un avviso per una particolare query o ID pianificazione e tipo di avviso effettuando una richiesta DELETE al `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` o `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` endpoint.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parametri | Descrizione |
| -------- | ----------- |
| `ALERT_TYPE` | Tipo di avviso. Un avviso può avere tre valori: <ul><li>`start`: avvisa l’utente quando viene avviata l’esecuzione della query.</li><li>`success`: avvisa l’utente al completamento della query.</li><li>`failure`: avvisa l’utente se la query non riesce.</li></ul> La richiesta DELETE si applica solo al tipo di avviso specifico fornito. |
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 e un messaggio di conferma che include l’ID della risorsa e il tipo di avviso dell’avviso eliminato.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Passaggi successivi

Questa guida trattava l&#39;utilizzo di `/alert-subscriptions` nell’API del servizio di query. Dopo aver letto questa guida, avrai acquisito maggiori informazioni su come creare un avviso per una query, abbonare gli utenti all’avviso, i tipi di avvisi disponibili e come recuperare, aggiornare ed eliminare le informazioni di abbonamento agli avvisi.

Consulta la [Guida API di Query Service](./getting-started.md) per ulteriori informazioni su altre funzioni e operazioni disponibili.
