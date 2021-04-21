---
keywords: Experience Platform;home;argomenti popolari;codici di errore API;codice di errore API;codice di errore API;codici di errore API;errore di richiesta API;risoluzione dei problemi API;errore API
solution: Experience Platform
title: Domande frequenti e guida alla risoluzione dei problemi di Adobe Experience Platform
description: Trova le risposte alle domande frequenti e una guida per la risoluzione dei problemi relativi agli errori più comuni in Experience Platform.
landing-page-description: Trova le risposte alle domande frequenti e una guida per la risoluzione dei problemi relativi agli errori più comuni in Experience Platform.
topic-legacy: getting started
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 4%

---

# [!DNL Platform] Domande frequenti e guida alla risoluzione dei problemi

Questo documento fornisce le risposte alle domande frequenti su Adobe Experience Platform e una guida per la risoluzione dei problemi di alto livello per gli errori comuni che possono verificarsi in qualsiasi API [!DNL Experience Platform]. Per le guide alla risoluzione dei problemi sui singoli servizi [!DNL Platform], consulta la [directory per la risoluzione dei problemi dei servizi](#service-troubleshooting-directory) di seguito.

## Domande frequenti {#faq}

Di seguito è riportato un elenco di risposte alle domande frequenti su Adobe Experience Platform.

## Cosa sono le API [!DNL Experience Platform]? {#what-are-experience-platform-apis}

[!DNL Experience Platform] offre più API RESTful che utilizzano richieste HTTP per accedere alle  [!DNL Platform] risorse. Ciascuna API di servizio espone più endpoint e consente di eseguire operazioni per elencare (GET), cercare (GET), modificare (PUT e/o PATCH) ed eliminare risorse (DELETE). Per ulteriori informazioni su endpoint e operazioni specifici disponibili per ogni servizio, consulta la [documentazione di riferimento API](http://www.adobe.com/go/platform-api-reference-en) sull&#39;Adobe I/O.

## Come si formatta una richiesta API? {#how-do-i-format-an-api-request}

I formati di richiesta variano a seconda dell’ [!DNL Platform] API utilizzata. Il modo migliore per imparare a strutturare le chiamate API è seguire gli esempi forniti nella documentazione del particolare servizio [!DNL Platform] che utilizzi.

Per ulteriori informazioni sulla formattazione delle richieste API, visita la sezione Guida introduttiva all’API Platform [lettura di chiamate API di esempio](./api-guide.md#sample-api) .

## Qual è la mia organizzazione IMS? {#what-is-my-ims-organization}

Un’organizzazione IMS è un Adobe di rappresentazione di un cliente. Tutte le soluzioni di Adobe con licenza sono integrate con questa organizzazione clienti. Quando un’organizzazione IMS ha diritto a [!DNL Experience Platform], può assegnare l’accesso agli sviluppatori. L’ID organizzazione IMS (`x-gw-ims-org-id`) rappresenta l’organizzazione per la quale deve essere eseguita una chiamata API ed è pertanto richiesto come intestazione in tutte le richieste API. Questo ID si trova tramite [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): nella scheda **Integrazioni** , passa alla sezione **Panoramica** per qualsiasi integrazione particolare e trova l&#39;ID in **Credenziali client**. Per informazioni dettagliate su come eseguire l&#39;autenticazione in [!DNL Platform], consulta l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Dove posso trovare la mia chiave API? {#where-can-i-find-my-api-key}

Una chiave API è necessaria come intestazione in tutte le richieste API. È disponibile tramite la [Console per sviluppatori di Adobe](https://www.adobe.com/go/devs_console_ui). Nella console, nella scheda **Integrazioni** , passa alla sezione **Panoramica** per una specifica integrazione e troverai la chiave in **Credenziali client**. Per informazioni dettagliate su come eseguire l&#39;autenticazione in [!DNL Platform], consulta l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come posso ottenere un token di accesso? {#how-do-i-get-an-access-token}

I token di accesso sono necessari nell’intestazione Autorizzazione di tutte le chiamate API. Possono essere generati utilizzando un comando `curl`, purché sia possibile accedere a un’integrazione per un’organizzazione IMS. I token di accesso sono validi solo per 24 ore, dopodiché è necessario generare un nuovo token per continuare a utilizzare l’API. Per informazioni dettagliate sulla generazione dei token di accesso, consulta l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come si utilizzano i parametri di query? {#how-do-i-user-query-parameters}

Alcuni endpoint [!DNL Platform] API accettano parametri di query per individuare informazioni specifiche e filtrare i risultati restituiti nella risposta. I parametri di query vengono aggiunti ai percorsi di richiesta con un simbolo di punto interrogativo (`?`) seguito da uno o più parametri di query che utilizzano il formato `paramName=paramValue`. Quando combini più parametri in una singola chiamata, devi utilizzare una e commerciale (`&`) per separare i singoli parametri. L’esempio seguente illustra come una richiesta che utilizza più parametri di query viene rappresentata nella documentazione.

Alcuni esempi di parametri di query comunemente utilizzati:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Per informazioni dettagliate sui parametri di query disponibili per un servizio o un endpoint specifico, consulta la documentazione specifica del servizio.

## Come si indica un campo JSON da aggiornare in una richiesta PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Molte operazioni PATCH nelle API [!DNL Platform] utilizzano le stringhe [JSON Pointer](https://tools.ietf.org/html/rfc6901) per indicare le proprietà JSON da aggiornare. Questi sono in genere inclusi nei payload della richiesta utilizzando il formato [Patch JSON](https://tools.ietf.org/html/rfc6902) . Per informazioni dettagliate sulla sintassi richiesta per queste tecnologie, consulta la [Guida di base API](api-fundamentals.md) .

## Posso utilizzare Postman per effettuare chiamate alle API [!DNL Platform]? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[](https://www.postman.com/) Postmanis uno strumento utile per visualizzare le chiamate alle API RESTful. La [guida introduttiva all’API Platform](api-guide.md) contiene un video e istruzioni per l’importazione di raccolte Postman. Inoltre, viene fornito un elenco di raccolte Postman per ogni servizio.

## Quali sono i requisiti di sistema per [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

A seconda dell’interfaccia utente o dell’API, si applicano i seguenti requisiti di sistema:

**Per le operazioni basate sull’interfaccia utente:**
- Un browser web moderno e standard. È consigliata anche l’ultima versione di [!DNL Chrome] , ma sono supportate anche le versioni principali correnti e precedenti di [!DNL Firefox], [!DNL Internet Explorer] e Safari.
   - Ogni volta che viene rilasciata una nuova versione principale, [!DNL Platform] inizia a supportare la versione più recente, mentre viene eliminato il supporto per la terza versione più recente.
- Tutti i browser devono avere i cookie e JavaScript abilitati.

**Per le interazioni con API e sviluppatori:**
- Un ambiente di sviluppo per le integrazioni REST, streaming e Webhook.

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Di seguito è riportato un elenco di errori che si possono verificare durante l&#39;utilizzo di un servizio [!DNL Experience Platform]. Per le guide alla risoluzione dei problemi sui singoli servizi [!DNL Platform], consulta la [directory per la risoluzione dei problemi dei servizi](#service-troubleshooting-directory) di seguito.

## Codici di stato API {#api-status-codes}

I seguenti codici di stato possono essere rilevati su qualsiasi API [!DNL Experience Platform]. Ognuno ha una varietà di cause, quindi le spiegazioni fornite in questa sezione sono di natura generale. Per ulteriori dettagli sugli errori specifici nei singoli servizi [!DNL Platform], consulta la [directory per la risoluzione dei problemi dei servizi](#service-troubleshooting-directory) di seguito.

| Codice di stato | Descrizione | Possibili cause |
|--- | --- | ---|
| 400 | Richiesta errata | La richiesta è stata costruita in modo errato, contiene informazioni chiave mancanti e/o contiene una sintassi non corretta. |
| 401 | Autenticazione non riuscita | La richiesta non ha superato un controllo di autenticazione. Token di accesso mancante o non valido. Per ulteriori informazioni, consulta la sezione [Errori token OAuth](#oauth-token-is-missing) di seguito. |
| 403 | Proibito | La risorsa è stata trovata, ma non si dispone delle credenziali necessarie per visualizzarla. |
| 404 | Non trovato | Impossibile trovare la risorsa richiesta sul server. È possibile che la risorsa sia stata eliminata o che il percorso richiesto non sia stato inserito correttamente. |
| 500 | Errore interno del server | Errore lato server. Se effettui molte chiamate simultanee, potresti raggiungere il limite API e dover filtrare i risultati. (Per ulteriori informazioni, consulta la guida per gli sviluppatori [!DNL Catalog Service] API nella sezione [filtro dei dati](../catalog/api/filter-data.md) .) Attendi un attimo prima di riprovare la richiesta e, se il problema persiste, contatta l’amministratore. |

## Errori di intestazione della richiesta {#request-header-errors}

Tutte le chiamate API in [!DNL Platform] richiedono intestazioni di richiesta specifiche. Per vedere quali intestazioni sono necessarie per i singoli servizi, consulta la [documentazione di riferimento API](http://www.adobe.com/go/platform-api-reference-en). Per trovare i valori per le intestazioni di autenticazione richieste, consulta l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Se una di queste intestazioni è mancante o non è valida durante una chiamata API, potrebbero verificarsi i seguenti errori.

### Token OAuth mancante {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione `Authorization` da una richiesta API. Assicurati che l’intestazione Autorizzazione sia inclusa con un token di accesso valido prima di riprovare.

### Il token OAuth non è valido

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso fornito nell&#39;intestazione `Authorization` non è valido. Assicurati che il token sia stato immesso correttamente oppure [genera un nuovo token](https://www.adobe.com/go/platform-api-authentication-en) nella console Adobe I/O.

### Chiave API obbligatoria

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione di chiave API (`x-api-key`) da una richiesta API. Assicurati che l’intestazione sia inclusa con una chiave API valida prima di riprovare.

### Chiave API non valida

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Questo messaggio di errore viene visualizzato quando il valore dell&#39;intestazione della chiave API fornita (`x-api-key`) non è valido. Assicurati di aver immesso correttamente la chiave prima di riprovare. Se non conosci la tua chiave API, puoi trovarlo nella [Console Adobe I/O](https://console.adobe.io): nella scheda **Integrazioni** , passa alla sezione **Panoramica** per una specifica integrazione per trovare la chiave API in **Credenziali client**.


### Intestazione mancante

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione organizzazione IMS (`x-gw-ims-org-id`) da una richiesta API. Assicurati che l’intestazione sia inclusa con l’ID della tua organizzazione IMS prima di riprovare.

### Profilo non valido

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Questo messaggio di errore viene visualizzato quando l’utente o l’integrazione di Adobe I/O (identificata dal [token di accesso](#how-do-i-get-an-access-token) nell’ intestazione `Authorization` ) non è autorizzata a effettuare chiamate alle API [!DNL Experience Platform] per l’organizzazione IMS fornita nell’intestazione `x-gw-ims-org-id` . Assicurati di aver fornito l’ID corretto per la tua organizzazione IMS nell’intestazione prima di riprovare. Se non conosci il tuo ID organizzazione, puoi trovarlo nella [Console di Adobe I/O](https://console.adobe.io): nella scheda **Integrazioni** , passa alla sezione **Panoramica** per una specifica integrazione e trova l&#39;ID in **Credenziali client**.

### Tipo di contenuto valido non specificato

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Questo messaggio di errore viene visualizzato quando una richiesta di POST, PUT o PATCH presenta un&#39;intestazione `Content-Type` non valida o mancante. Verifica che l’intestazione sia inclusa nella richiesta e che il relativo valore sia `application/json`.


## Directory dei servizi per la risoluzione dei problemi {#service-troubleshooting-directory}

Di seguito è riportato un elenco delle guide per la risoluzione dei problemi e della documentazione di riferimento API per [!DNL Experience Platform] API. Ogni guida alla risoluzione dei problemi fornisce le risposte alle domande frequenti e le soluzioni ai problemi specifici dei singoli servizi [!DNL Platform]. I documenti di riferimento API forniscono una guida completa a tutti gli endpoint disponibili per ogni servizio e mostrano corpi di richiesta di esempio, risposte e codici di errore che possono essere ricevuti.

| Servizio | Documentazione di riferimento API | Risoluzione dei problemi |
| --- | --- | --- |
| Controllo dell&#39;accesso | [API di controllo accessi](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guida alla risoluzione dei problemi di controllo degli accessi](../access-control/troubleshooting-guide.md) |
| Acquisizione dei dati Adobe Experience Platform | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guida ](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[alla risoluzione dei problemi di inserimento in batchGuida alla risoluzione dei problemi di acquisizione in streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guida alla risoluzione dei problemi](../data-science-workspace/troubleshooting-guide.md) |
| Governance dei dati di Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Servizio Adobe Experience Platform Identity | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] guida alla risoluzione dei problemi](../identity-service/troubleshooting-guide.md) |
| Servizio query Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] guida alla risoluzione dei problemi](../query-service/troubleshooting-guide.md) |
| Segmentazione Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] Domande frequenti e guida alla risoluzione dei problemi](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] e [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] guida alla risoluzione dei problemi](../profile/troubleshooting.md) |
| Sandbox | [API sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guida alla risoluzione dei problemi delle sandbox](../sandboxes/troubleshooting-guide.md) |
