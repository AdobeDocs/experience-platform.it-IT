---
title: Endpoint API contenuto
description: Scopri come recuperare i dati di accesso utilizzando l’API Privacy Service.
role: Developer
badgePrivateBeta: label="Private Beta" type="Informative"
exl-id: b3b7ea0f-957d-4e51-bf92-121e9ae795f5
source-git-commit: e3a453ad166fe244b82bd1f90e669579fcf09d17
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# Endpoint di contenuto

>[!IMPORTANT]
>
>L&#39;endpoint `/content` è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. La funzionalità e la documentazione sono soggette a modifiche.

Utilizza l&#39;endpoint `/content` per recuperare in modo sicuro *le informazioni di accesso* (le informazioni a cui un soggetto che si occupa di privacy può legittimamente richiedere di accedere) per i tuoi clienti. L&#39;URL di download fornito nella risposta a una richiesta di `/jobs/{JOB_ID}` GET punta a un endpoint del servizio Adobe. È quindi possibile effettuare una richiesta GET a `/jobs/:JOB_ID/content` per restituire i dati dei clienti in formato JSON. Questo metodo di accesso implementa più livelli di autenticazione e controllo degli accessi per migliorare la sicurezza.

Prima di utilizzare questa guida, consulta la [guida introduttiva](./getting-started.md) per informazioni sulle intestazioni di autenticazione richieste presentate nella chiamata API di esempio seguente.

>[!TIP]
>
>Se al momento non si conosce l&#39;ID processo per le informazioni di accesso necessarie, effettuare una chiamata all&#39;endpoint `/jobs` e utilizzare parametri di query aggiuntivi per filtrare i risultati. Un elenco completo dei parametri di query disponibili è disponibile nella [guida dell&#39;endpoint dei processi di privacy](./privacy-jobs.md).

## Recuperare le informazioni sul processo di privacy

Per recuperare informazioni su un processo specifico, ad esempio il relativo stato di elaborazione corrente, includere il processo `jobId` nel percorso di una richiesta GET all&#39;endpoint `/jobs`.

**Formato API**

```http
GET /jobs/{JOB_ID}
```

**Richiesta**

La richiesta seguente recupera i dettagli del processo di cui viene fornito `jobId` nel percorso della richiesta.

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
>I processi per la privacy devono avere lo stato `complete` per contenere `downloadUrl`.

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
    "downloadUrl":"https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Proprietà | Descrizione |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | Un identificatore univoco per il processo di privacy. |
| `requestId` | Identificatore univoco della richiesta specifica effettuata al Privacy Service. |
| `userKey` | `userKey` è il valore `key` fornito quando hai inviato la richiesta di privacy. Il valore `key` è l&#39;opportunità di fornire un identificatore appropriato per la persona interessata. In genere si tratta di un identificatore univoco creato dal sistema per tenere traccia dell’interessato. SUGGERIMENTO: è possibile elencare tutti i processi di privacy attivi e confrontare `key` con ogni processo. |
| `action` | Tipo di azione richiesta. I valori accettati sono `access` e `delete`. |
| `status` | Lo stato corrente del processo di privacy. |
| `submittedBy` | L’indirizzo e-mail della persona che ha inviato il processo di privacy. |
| `createdDate` | La data e l’ora in cui è stato creato il processo di privacy. |
| `lastModifiedDate` | La data e l’ora dell’ultima modifica apportata al processo di privacy. |
| `userIds` | Array contenente gli identificatori utente e le informazioni correlate. |
| `userIds.namespace` | Lo spazio dei nomi utilizzato per l’identificatore utente. |
| `userIds.value` | Valore effettivo dell&#39;identificatore utente. |
| `userIds.type` | Il tipo di identificatore (ad esempio `standard` o `custom`). |
| `userIds.namespaceId` | Identificatore dello spazio dei nomi utilizzato per categorizzare e gestire le identità utente. |
| `userIds.isDeletedClientSide` | Valore booleano che indica se l’identificatore è stato eliminato sul lato client. |
| `productResponses` | Array contenente le risposte di diversi prodotti o servizi correlati al processo sulla privacy. |
| `productResponses.product` | Il nome del prodotto o del servizio utilizzato per acquisire informazioni sulla persona interessata. |
| `productResponses.retryCount` | Il numero di tentativi della richiesta. |
| `productResponses.processedDate` | La data e l’ora in cui è stata elaborata la risposta del prodotto. |
| `productResponses.productStatusResponse` | Oggetto contenente lo stato della risposta del prodotto. |
| `productResponses.productStatusResponse.status` | Stato della risposta del prodotto. |
| `downloadURL` | Questo attributo fornisce un endpoint che è disponibile per la chiamata per 60 giorni dopo il completamento del processo. Lo stato del processo deve essere `complete` e il `action` deve essere `access`. In caso contrario, questo campo è assente. |
| `regulation` | Framework normativo in cui viene elaborata la richiesta di accesso a dati personali, ad esempio `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha` e così via. |

{style="table-layout:auto"}

## Recuperare le informazioni di accesso del cliente {#retrieve-access-data}

Per ottenere le informazioni di accesso prodotte in risposta alla query dell&#39;interessato, effettuare una richiesta di GET all&#39;endpoint `/jobs/{JOB_ID}/content`. La risposta è un file zip (*.zip) contenente una cartella con sottocartelle per ciascun prodotto che contiene dati sulla persona interessata.

>[!TIP]
>
>Per effettuare questa richiesta è necessario un ID processo specifico. Se devi recuperare l&#39;ID del processo specifico, devi prima effettuare una richiesta di GET all&#39;endpoint `/jobs` e utilizzare parametri di query aggiuntivi per filtrare i risultati. Informazioni dettagliate, inclusi i parametri di query consentiti, sono disponibili nella [guida dell&#39;endpoint per i processi di privacy](./privacy-jobs.md).

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

