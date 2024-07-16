---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;avviso;
title: Endpoint sottoscrizioni avvisi
description: Questa guida fornisce esempi di richieste HTTP e risposte per le varie chiamate API che puoi effettuare all’endpoint di abbonamenti agli avvisi con l’API Query Service.
role: Developer
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: 41c069ef1c0a19f34631e77afd7a80b8967c5060
workflow-type: tm+mt
source-wordcount: '3204'
ht-degree: 2%

---

# Endpoint &quot;Alert Subscriptions&quot;

Adobe Experience Platform Query Service consente di ricevere avvisi sia per le query ad hoc che per quelle pianificate. Gli avvisi possono essere ricevuti tramite e-mail, nell’interfaccia di Platform o in entrambe le modalità. Il contenuto della notifica è lo stesso per gli avvisi e-mail in-Platform.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39;API [Query Service di Adobe Experience Platform](https://developer.adobe.com/experience-platform-apis/references/query-service/). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura delle chiamate API di esempio.

>[!IMPORTANT]
>
>Per ricevere gli avvisi e-mail devi prima abilitare questa impostazione nell’interfaccia utente. Consulta la documentazione per [istruzioni su come abilitare gli avvisi e-mail](../../observability/alerts/ui.md#enable-email-alerts).

## Tipi di avviso {#alert-types}

La tabella seguente spiega i tipi di avviso per le query supportati:

>[!IMPORTANT]
>
>Il tipo di avviso `delay` o [!UICONTROL Ritardo esecuzione query] non è attualmente supportato dall&#39;API del servizio query. Questo avviso notifica se si verifica un ritardo nell&#39;esecuzione di una query pianificata oltre una soglia specificata. Per utilizzare questo avviso, è necessario impostare un&#39;ora personalizzata che attivi un avviso quando la query viene eseguita per tale durata senza completare o non riuscire. Per informazioni su come impostare questo avviso nell&#39;interfaccia utente, consulta la documentazione [pianificazioni query](../ui/query-schedules.md#alerts-for-query-status) o la [guida alle azioni query in linea](../ui/monitor-queries.md#query-run-delay).

| Tipo di avviso | Descrizione |
|---|---|
| `start` | Questo avviso avvisa quando viene avviata o avviata l&#39;elaborazione di una query pianificata. |
| `success` | Questo avviso informa l&#39;utente quando una query pianificata viene eseguita correttamente, indicando che la query è stata eseguita senza errori. |
| `failed` | Questo avviso viene attivato quando una query pianificata viene eseguita con un errore o non viene eseguita correttamente. Consente di identificare e risolvere tempestivamente i problemi. |
| `quarantine` | Questo avviso viene attivato quando un’esecuzione di query pianificata viene messa in quarantena. Quando le query vengono registrate nella funzione di quarantena, qualsiasi query pianificata che non supera dieci esecuzioni consecutive viene automaticamente impostata su uno stato [!UICONTROL In quarantena]. Quindi richiedono il tuo intervento prima che possano aver luogo ulteriori esecuzioni. |

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

Recuperare un elenco di tutti gli avvisi per una sandbox dell&#39;organizzazione effettuando una richiesta GET all&#39;endpoint `/alert-subscriptions`.

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
| `orderby` | Campo che specifica l&#39;ordine dei risultati. I campi supportati sono `created` e `updated`. Anteporre il nome della proprietà con `+` per crescente e `-` per decrescente. Il valore predefinito è `-created`. Il segno più (`+`) deve essere preceduto da un carattere di escape con `%2B`. Ad esempio `%2Bcreated` è il valore per un ordine creato crescente. |
| `pagesize` | Utilizza questo parametro per controllare il numero di record che desideri recuperare dalla chiamata API per pagina. Il limite predefinito è impostato al massimo di 50 record per pagina. |
| `page` | Indicare il numero di pagina dei risultati restituiti per i quali si desidera visualizzare i record. |
| `property` | Filtra i risultati in base ai campi selezionati. I filtri **devono** avere escape HTML. Le virgole vengono utilizzate per combinare più set di filtri. Le seguenti proprietà consentono l’applicazione di filtri: <ul><li>id</li><li>assetId</li><li>stato</li><li>alertType</li></ul> Gli operatori supportati sono `==` (uguale a). Ad esempio, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituirà l&#39;avviso con un ID corrispondente. |

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 e l&#39;array `alerts` con informazioni sulla paginazione e sulla versione. L&#39;array `alerts` contiene i dettagli di tutti gli avvisi per un&#39;organizzazione e una particolare sandbox. Per ogni risposta sono disponibili al massimo tre avvisi, uno per ogni tipo di avviso è contenuto nel corpo della risposta.

>[!NOTE]
>
>L&#39;oggetto `alerts._links` nell&#39;array `alerts` è stato troncato per brevità. Un esempio completo dell&#39;oggetto `alerts._links` è disponibile nella [risposta della richiesta POST](#subscribe-users).

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
| `alerts.id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell&#39;avviso è costituito dalla cartella in cui è memorizzato l&#39;avviso, da `alertType` e dall&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella [documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `alerts.status` | L&#39;avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled` e `disabling`. Un avviso è l’ascolto attivo degli eventi, messo in pausa per utilizzi futuri mantenendo tutti gli abbonati e le impostazioni rilevanti, oppure la transizione tra questi stati. |
| `alerts.alertType` | Tipo di avviso. Sono disponibili cinque stati di avviso per le query pianificate, anche se sono disponibili solo quattro stati di avviso per le query ad hoc. L&#39;avviso `quarantine` è disponibile solo per le query pianificate. Inoltre, è possibile impostare l&#39;avviso `delay` solo dall&#39;interfaccia utente di Platform. Per questo motivo `delay` non è descritto qui. Gli avvisi disponibili sono: <ul><li>`start`: notifica a un utente l&#39;avvio dell&#39;esecuzione della query.</li><li>`success`: invia una notifica all&#39;utente al completamento della query.</li><li>`failure`: invia una notifica all&#39;utente se la query non riesce.</li><li>`quarantine`: si attiva quando una query pianificata viene messa in quarantena.</li></ul> |
| `alerts._links` | Fornisce informazioni sui metodi e gli endpoint disponibili che possono essere utilizzati per recuperare, aggiornare, modificare o eliminare informazioni relative a questo ID avviso. |
| `_page` | L&#39;oggetto contiene proprietà che descrivono l&#39;ordine, la dimensione, il numero totale di pagine e la pagina corrente. |
| `_links` | L’oggetto contiene riferimenti URI che possono essere utilizzati per ottenere la pagina successiva o precedente delle risorse. |

## Recuperare le informazioni sulla sottoscrizione dell’avviso per una particolare query o ID pianificazione {#retrieve-all-alert-subscriptions-by-id}

Recuperare le informazioni sulla sottoscrizione dell&#39;avviso per un ID di query o un ID di pianificazione specifico effettuando una richiesta di GET all&#39;endpoint `/alert-subscriptions/{QUERY_ID}` o `/alert-subscriptions/{SCHEDULE_ID}`.

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 e l’array `alerts` che contiene le informazioni sulla sottoscrizione per l’ID di query o pianificazione fornito.

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
| `id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell&#39;avviso è costituito dalla cartella in cui è memorizzato l&#39;avviso, da `alertType` e dall&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella [documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `status` | L&#39;avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled` e `disabling`. Un avviso è l’ascolto attivo degli eventi, messo in pausa per utilizzi futuri mantenendo tutti gli abbonati e le impostazioni rilevanti, oppure la transizione tra questi stati. |
| `alertType` | Ogni avviso può avere tre tipi diversi di avviso. Sono: <ul><li>`start`: notifica a un utente l&#39;avvio dell&#39;esecuzione della query.</li><li>`success`: invia una notifica all&#39;utente al completamento della query.</li><li>`failure`: invia una notifica all&#39;utente se la query non riesce.</li></ul> |
| `subscriptions.emailNotifications` | Un array di Adobi di indirizzi e-mail registrati per gli utenti che si sono abbonati a ricevere e-mail per l’avviso. |
| `subscriptions.inContextNotifications` | Un array di Adobi di indirizzi e-mail registrati per gli utenti che si sono abbonati alle notifiche dell’interfaccia utente per l’avviso. |

## Recuperare le informazioni di sottoscrizione degli avvisi per una query o un ID pianificazione e un tipo di avviso specifici {#get-alert-info-by-id-and-alert-type}

Recuperare le informazioni sulla sottoscrizione degli avvisi per un ID e un tipo di avviso specifici effettuando una richiesta di GET all&#39;endpoint `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}`. Questo è applicabile sia agli ID query che a quelli pianificati.

**Formato API**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Elemento “parameters” | Descrizione |
| -------- | ----------- |
| `ALERT_TYPE` | Questa proprietà descrive lo stato di esecuzione della query che attiva un avviso. La risposta includerà solo le informazioni di abbonamento agli avvisi per avvisi di questo tipo. Ogni avviso può avere tre tipi diversi di avviso. Sono: <ul><li>`start`: notifica a un utente l&#39;avvio dell&#39;esecuzione della query.</li><li>`success`: invia una notifica all&#39;utente al completamento della query.</li><li>`failure`: invia una notifica all&#39;utente se la query non riesce.</li></ul> |
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
| `alertType` | Tipo di avviso. Sono disponibili cinque stati di avviso per le query pianificate, anche se sono disponibili solo quattro stati di avviso per le query ad hoc. L&#39;avviso `quarantine` è disponibile solo per le query pianificate. Inoltre, è possibile impostare l&#39;avviso `delay` solo dall&#39;interfaccia utente di Platform. Per questo motivo `delay` non è descritto qui. Gli avvisi disponibili sono: <ul><li>`start`: notifica a un utente l&#39;avvio dell&#39;esecuzione della query.</li><li>`success`: invia una notifica all&#39;utente al completamento della query.</li><li>`failure`: invia una notifica all&#39;utente se la query non riesce.</li><li>`quarantine`: si attiva quando una query pianificata viene messa in quarantena.</li></ul> |
| `subscriptions` | Oggetto utilizzato per trasmettere gli ID e-mail registrati dell’Adobe associati agli avvisi e i canali in cui gli utenti riceveranno gli avvisi. |
| `subscriptions.inContextNotifications` | Un array di Adobi di indirizzi e-mail registrati per gli utenti che si sono abbonati alle notifiche dell’interfaccia utente per l’avviso. |
| `subscriptions.emailNotifications` | Un array di Adobi di indirizzi e-mail registrati per gli utenti che si sono abbonati a ricevere e-mail per l’avviso. |

## Recuperare un elenco di tutti gli avvisi a cui è abbonato un utente {#get-alert-subscription-list}

Recuperare un elenco di tutti gli avvisi a cui un utente è abbonato effettuando una richiesta GET all&#39;endpoint `/alert-subscriptions/user-subscriptions/{EMAIL_ID}`. La risposta include il nome, gli ID, lo stato, il tipo di avviso e i canali di notifica dell’avviso.

**Formato API**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Elemento “parameters” | Descrizione |
| -------- | ----------- |
| `{EMAIL_ID}` | Un indirizzo e-mail registrato su un account di Adobe viene utilizzato per identificare gli utenti abbonati agli avvisi. |
| `orderby` | Campo che specifica l&#39;ordine dei risultati. I campi supportati sono `created` e `updated`. Anteporre il nome della proprietà con `+` per crescente e `-` per decrescente. Il valore predefinito è `-created`. Il segno più (`+`) deve essere preceduto da un carattere di escape con `%2B`. Ad esempio `%2Bcreated` è il valore per un ordine creato crescente. |
| `pagesize` | Utilizza questo parametro per controllare il numero di record che desideri recuperare dalla chiamata API per pagina. Il limite predefinito è impostato al massimo di 50 record per pagina. |
| `page` | Indicare il numero di pagina dei risultati restituiti per i quali si desidera visualizzare i record. |
| `property` | Filtra i risultati in base ai campi selezionati. I filtri **devono** avere escape HTML. Le virgole vengono utilizzate per combinare più set di filtri. Le seguenti proprietà consentono il filtraggio: <ul><li>id</li><li>assetId</li><li>stato</li><li>alertType</li></ul> Gli operatori supportati sono `==` (uguale a). Ad esempio, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` restituirà l&#39;avviso con un ID corrispondente. |

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 e l’array `items` con i dettagli degli avvisi a cui è abbonato `emailId` fornito.

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
| `name` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell&#39;avviso è costituito dalla cartella in cui è memorizzato l&#39;avviso, da `alertType` e dall&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella [documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `assetId` | ID della query che ha associato l’avviso a una determinata query. |
| `status` | L&#39;avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled` e `disabling`. Un avviso è l’ascolto attivo degli eventi, messo in pausa per utilizzi futuri mantenendo tutti gli abbonati e le impostazioni rilevanti, oppure la transizione tra questi stati. |
| `alertType` | Tipo di avviso. Sono disponibili cinque stati di avviso per le query pianificate, anche se sono disponibili solo quattro stati di avviso per le query ad hoc. L&#39;avviso `quarantine` è disponibile solo per le query pianificate. Inoltre, è possibile impostare l&#39;avviso `delay` solo dall&#39;interfaccia utente di Platform. Per questo motivo `delay` non è descritto qui. Gli avvisi disponibili sono: <ul><li>`start`: notifica a un utente l&#39;avvio dell&#39;esecuzione della query.</li><li>`success`: invia una notifica all&#39;utente al completamento della query.</li><li>`failure`: invia una notifica all&#39;utente se la query non riesce.</li><li>`quarantine`: si attiva quando una query pianificata viene messa in quarantena.</li></ul> |
| `subscriptions` | Oggetto utilizzato per trasmettere gli ID e-mail registrati dell’Adobe associati agli avvisi e i canali in cui gli utenti riceveranno gli avvisi. |
| `subscriptions.inContextNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. Un valore `true` conferma che gli avvisi devono essere forniti tramite l&#39;interfaccia utente. Un valore `false` garantisce che gli utenti non ricevano notifiche tramite tale canale. |
| `subscriptions.emailNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. Un valore `true` conferma che gli avvisi devono essere forniti tramite e-mail. Un valore `false` garantisce che gli utenti non ricevano notifiche tramite tale canale. |

## Creare un avviso e abbonare gli utenti {#subscribe-users}

Per creare un avviso e sottoscrivere un utente per riceverlo, effettuare una richiesta `POST` all&#39;endpoint `/alert-subscriptions`. Questa richiesta associa una query a un avviso appena creato utilizzando una proprietà `assetId` e sottoscrive gli utenti agli avvisi per tale query tramite l&#39;utilizzo di `emailIds`.

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
| `alertType` | Tipo di avviso. Sono disponibili cinque stati di avviso per le query pianificate, anche se sono disponibili solo quattro stati di avviso per le query ad hoc. L&#39;avviso `quarantine` è disponibile solo per le query pianificate. Inoltre, è possibile impostare l&#39;avviso `delay` solo dall&#39;interfaccia utente di Platform. Per questo motivo `delay` non è descritto qui. Gli avvisi disponibili sono: <ul><li>`start`: notifica a un utente l&#39;avvio dell&#39;esecuzione della query.</li><li>`success`: invia una notifica all&#39;utente al completamento della query.</li><li>`failure`: invia una notifica all&#39;utente se la query non riesce.</li><li>`quarantine`: si attiva quando una query pianificata viene messa in quarantena.</li></ul> |
| `subscriptions` | Oggetto utilizzato per trasmettere gli ID e-mail registrati dell’Adobe associati agli avvisi e i canali in cui gli utenti riceveranno gli avvisi. |
| `subscriptions.emailIds` | Un array di indirizzi e-mail per identificare gli utenti che devono ricevere gli avvisi. Gli indirizzi e-mail **devono** essere registrati in un account di Adobe. |
| `subscriptions.inContextNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. Un valore `true` conferma che gli avvisi devono essere forniti tramite l&#39;interfaccia utente. Un valore `false` garantisce che gli utenti non ricevano notifiche tramite tale canale. |
| `subscriptions.emailNotifications` | Valore booleano che determina il modo in cui gli utenti ricevono le notifiche di avviso. Un valore `true` conferma che gli avvisi devono essere forniti tramite e-mail. Un valore `false` garantisce che gli utenti non ricevano notifiche tramite tale canale. |

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
| `id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell&#39;avviso è costituito dalla cartella in cui è memorizzato l&#39;avviso, da `alertType` e dall&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella [documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `_links` | Fornisce informazioni sui metodi e gli endpoint disponibili che possono essere utilizzati per recuperare, aggiornare, modificare o eliminare informazioni relative a questo ID avviso. |

## Attivare o disattivare un avviso {#enable-or-disable-alert}

Questa richiesta fa riferimento a un determinato avviso utilizzando un ID di query o pianificazione e un tipo di avviso e aggiorna lo stato dell&#39;avviso a `enable` o `disable`. È possibile aggiornare lo stato di un avviso effettuando una richiesta `PATCH` all&#39;endpoint `/alert-subscriptions/{queryId}/{alertType}` o `/alert-subscriptions/{scheduleId}/{alertType}`.

**Formato API**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Elemento “parameters” | Descrizione |
| -------- | ----------- |
| `ALERT_TYPE` | Tipo di avviso. Sono disponibili cinque stati di avviso per le query pianificate, anche se sono disponibili solo quattro stati di avviso per le query ad hoc. L&#39;avviso `quarantine` è disponibile solo per le query pianificate. Inoltre, è possibile impostare l&#39;avviso `delay` solo dall&#39;interfaccia utente di Platform. Per questo motivo `delay` non è descritto qui. Gli avvisi disponibili sono: <ul><li>`start`: notifica a un utente l&#39;avvio dell&#39;esecuzione della query.</li><li>`success`: invia una notifica all&#39;utente al completamento della query.</li><li>`failure`: invia una notifica all&#39;utente se la query non riesce.</li><li>`quarantine`: si attiva quando una query pianificata viene messa in quarantena.</li></ul>È necessario specificare il tipo di avviso corrente nello spazio dei nomi dell&#39;endpoint per modificarlo. |
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
| `path` | Questo valore si riferisce allo spazio dei nomi nell’endpoint. Attualmente, l&#39;unico valore accettato è `/status`. |
| `value` | In una richiesta PATCH riuscita, viene modificato il valore `status` dell&#39;avviso. Attualmente, i valori accettati sono `enable` o `disable`. |

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
| `id` | Nome dell&#39;avviso. Questo nome viene generato dal servizio Avvisi e utilizzato nel dashboard Avvisi. Il nome dell&#39;avviso è costituito dalla cartella in cui è memorizzato l&#39;avviso, da `alertType` e dall&#39;ID di flusso. Le informazioni sugli avvisi disponibili sono disponibili nella [documentazione del dashboard degli avvisi di Platform](../../observability/alerts/ui.md). |
| `assetId` | L’avviso è associato a questo ID. L’ID può essere un ID query o un ID pianificazione. |
| `alertType` | Ogni avviso può avere tre tipi diversi di avviso. Sono: <ul><li>`start`: notifica a un utente l&#39;avvio dell&#39;esecuzione della query.</li><li>`success`: invia una notifica all&#39;utente al completamento della query.</li><li>`failure`: invia una notifica all&#39;utente se la query non riesce.</li></ul> |
| `status` | L&#39;avviso ha quattro valori di stato: `enabled`, `enabling`, `disabled` e `disabling`. Un avviso è l’ascolto attivo degli eventi, messo in pausa per utilizzi futuri mantenendo tutti gli abbonati e le impostazioni rilevanti, oppure la transizione tra questi stati. |

## Eliminare l&#39;avviso per una query e un tipo di avviso specifici {#delete-alert-info-by-id-and-alert-type}

Eliminare un avviso per un determinato ID di query o pianificazione e tipo di avviso effettuando una richiesta DELETE all&#39;endpoint `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` o `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}`.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Elemento “parameters” | Descrizione |
| -------- | ----------- |
| `ALERT_TYPE` | Tipo di avviso. Sono disponibili cinque stati di avviso per le query pianificate, anche se sono disponibili solo quattro stati di avviso per le query ad hoc. L&#39;avviso `quarantine` è disponibile solo per le query pianificate. Inoltre, è possibile impostare l&#39;avviso `delay` solo dall&#39;interfaccia utente di Platform. Per questo motivo `delay` non è descritto qui. Gli avvisi disponibili sono: <ul><li>`start`: notifica a un utente l&#39;avvio dell&#39;esecuzione della query.</li><li>`success`: invia una notifica all&#39;utente al completamento della query.</li><li>`failure`: invia una notifica all&#39;utente se la query non riesce.</li><li>`quarantine`: si attiva quando una query pianificata viene messa in quarantena.</li></ul> La richiesta DELETE si applica solo al tipo di avviso specifico fornito. |
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

Questa guida descrive l&#39;utilizzo dell&#39;endpoint `/alert-subscriptions` nell&#39;API Query Service. Dopo aver letto questa guida, avrai acquisito maggiori informazioni su come creare un avviso per una query, abbonare gli utenti all’avviso, i tipi di avvisi disponibili e come recuperare, aggiornare ed eliminare le informazioni di abbonamento agli avvisi.

Per ulteriori informazioni su altre funzioni e operazioni disponibili, consulta la [guida API di Query Service](./getting-started.md).
