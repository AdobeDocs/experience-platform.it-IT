---
title: Endpoint API contenuto
description: Scopri come recuperare i dati di accesso utilizzando l’API Privacy Service.
role: Developer
badgePrivateBeta: label="Versione beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 8bd4bd293b68d01e072c1c0a776080379692c5ee
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Endpoint di contenuto

>[!IMPORTANT]
>
>Il `/content` l’endpoint è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. La funzionalità e la documentazione sono soggette a modifiche.

<!-- Q) Should this be called 'access information' or 'customer content'? -->

Maggiore sicurezza per il recupero di &quot;informazioni di accesso&quot; (informazioni a cui un soggetto con privacy può legittimamente richiedere l’accesso). L’URL di download fornito nella risposta a un `/jobs/{JOB_ID}` La richiesta GET ora punta a un endpoint del servizio Adobe. Puoi quindi effettuare una richiesta GET a `/jobs/:JOB_ID/content` per restituire i dati dei clienti in formato JSON. Questo metodo di accesso implementa più livelli di autenticazione e controllo degli accessi per migliorare la sicurezza.

Prima di utilizzare questa guida, consultare [guida introduttiva](./getting-started.md) per informazioni sulle intestazioni di autenticazione richieste presentate nella chiamata API di esempio di seguito.

>[!TIP]
>
>Se al momento non conosci l’ID processo per le informazioni di accesso necessarie, chiama il `/jobs`e utilizzare parametri di query aggiuntivi per filtrare i risultati. Un elenco completo dei parametri di query disponibili è disponibile nella sezione [guida dell’endpoint &quot;privacy jobs&quot;](./privacy-jobs.md).

## Recuperare le informazioni sul processo di privacy

Per recuperare informazioni su un job specifico, ad esempio lo stato di elaborazione corrente, includere il relativo `jobId` nel percorso di una richiesta GET al `/jobs` endpoint.

**Formato API**

```http
GET /jobs/{JOB_ID}
```

**Richiesta**

La richiesta seguente recupera i dettagli del processo il cui `jobId` viene fornito nel percorso della richiesta.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del processo specificato.

>[!NOTE]
>
>I processi relativi alla privacy devono avere `complete` stato per contenere il `downloadUrl`.

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform-stage.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Proprietà | Descrizione |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | Un identificatore univoco per il processo di privacy. |
| `requestId` | Identificatore univoco della richiesta specifica effettuata al Privacy Service. |
| `userKey` | `userKey` è il `key` valore fornito quando hai inviato la richiesta di accesso a dati personali. Il `key` value è l’opportunità di fornire all’interessato un identificatore appropriato. In genere si tratta di un identificatore univoco creato dal sistema per tenere traccia dell’interessato. SUGGERIMENTO: è possibile elencare tutti i processi di privacy attivi e confrontare `key` a ogni processo. |
| `action` | Tipo di azione richiesta. I valori accettati sono `access` e `delete`. |
| `status` | Lo stato corrente del processo di privacy. |
| `submittedBy` | L’indirizzo e-mail della persona che ha inviato il processo di privacy. |
| `createdDate` | La data e l’ora in cui è stato creato il processo di privacy. |
| `lastModifiedDate` | La data e l’ora dell’ultima modifica apportata al processo di privacy. |
| `userIds` | Array contenente gli identificatori utente e le informazioni correlate. |
| `userIds.namespace` | Lo spazio dei nomi utilizzato per l’identificatore utente. |
| `userIds.value` | Valore effettivo dell&#39;identificatore utente. |
| `userIds.type` | Tipo di identificatore (ad esempio `standard` o `custom`). |
| `userIds.namespaceId` | Identificatore dello spazio dei nomi utilizzato per categorizzare e gestire le identità utente. |
| `userIds.isDeletedClientSide` | Valore booleano che indica se l’identificatore è stato eliminato sul lato client. |
| `productResponses` | Array contenente le risposte di diversi prodotti o servizi correlati al processo sulla privacy. |
| `productResponses.product` | Il nome del prodotto o del servizio utilizzato per acquisire informazioni sulla persona interessata. |
| `productResponses.retryCount` | Il numero di tentativi della richiesta. |
| `productResponses.processedDate` | La data e l’ora in cui è stata elaborata la risposta del prodotto. |
| `productResponses.productStatusResponse` | Oggetto contenente lo stato della risposta del prodotto. |
| `productResponses.productStatusResponse.status` | Stato della risposta del prodotto. |
| `downloadURL` | Questo attributo fornisce un endpoint che è disponibile per la chiamata per 60 giorni dopo il completamento del processo. Lo stato del processo deve essere `complete` e `action` deve essere `access`. In caso contrario, questo campo è assente. |
| `regulation` | Il quadro normativo in base al quale viene elaborata la richiesta di accesso a dati personali, ad esempio `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha`e così via. |

{style="table-layout:auto"}

## Recuperare le informazioni di accesso del cliente {#retrieve-access-data}

Per ottenere le &quot;informazioni di accesso&quot; prodotte in risposta alla richiesta dell’interessato, invia una richiesta di GET al `/jobs/{JOB_ID}/content` endpoint. La risposta è un file zip (*.zip) contenente una cartella con sottocartelle per ciascun prodotto che contiene dati sulla persona interessata.

>[!TIP]
>
>Per effettuare questa richiesta è necessario un ID processo specifico. Se devi recuperare l’ID processo specifico, effettua prima una richiesta GET al `/jobs` e utilizzare parametri di query aggiuntivi per filtrare i risultati. Informazioni dettagliate, inclusi i parametri di query consentiti, sono disponibili nella sezione [guida dell’endpoint &quot;privacy jobs&quot;](./privacy-jobs.md).

**Formato API**

```http
GET /jobs/{JOB_ID}/content
```

**Richiesta**

La seguente richiesta restituisce &quot;informazioni di accesso&quot; per l’ID processo fornito nella richiesta.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**Risposta**

La risposta è un file zip (*.zip). Le informazioni vengono generalmente restituite in formato JSON, anche se questo non può essere garantito. I dati estratti possono essere restituiti in qualsiasi formato.

