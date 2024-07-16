---
keywords: Experience Platform;home;argomenti popolari;codici di errore API;codice di errore API;codice di errore API;codici di errore API;errore richiesta API;risoluzione dei problemi API;errore API
solution: Experience Platform
title: Domande frequenti e guida alla risoluzione dei problemi di Adobe Experience Platform
description: Trova le risposte alle domande frequenti e una guida per la risoluzione dei problemi relativi agli errori più comuni in Adobe Experience Platform.
landing-page-description: Trova le risposte alle domande frequenti e una guida per la risoluzione dei problemi relativi agli errori più comuni in Adobe Experience Platform.
short-description: Trova le risposte alle domande frequenti e una guida per la risoluzione dei problemi relativi agli errori più comuni in Experience Platform.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: 81f570f8e5401624ccac74696b2323252a4de0a9
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 4%

---

# [!DNL Platform] Domande frequenti e guida alla risoluzione dei problemi

Questo documento contiene le risposte alle domande più frequenti su Adobe Experience Platform e una guida di alto livello per la risoluzione dei problemi relativi agli errori più comuni che possono verificarsi in qualsiasi API [!DNL Experience Platform]. Per le guide alla risoluzione dei problemi dei singoli servizi [!DNL Platform], vedere la [directory per la risoluzione dei problemi dei servizi](#service-troubleshooting-directory) di seguito.

## Domande frequenti {#faq}

Di seguito è riportato un elenco di risposte alle domande più frequenti su Adobe Experience Platform.

## Cosa sono le API [!DNL Experience Platform]? {#what-are-experience-platform-apis}

[!DNL Experience Platform] offre più API RESTful che utilizzano richieste HTTP per accedere alle risorse [!DNL Platform]. Queste API di servizio espongono ciascuna più endpoint e consentono di eseguire operazioni per elencare (GET), cercare (GET), modificare (PUT e/o PATCH) ed eliminare (DELETE) le risorse. Per ulteriori informazioni su endpoint e operazioni specifici disponibili per ciascun servizio, consulta la [documentazione di riferimento API](https://www.adobe.com/go/platform-api-reference-en) sull&#39;Adobe I/O.

## Come si formatta una richiesta API? {#how-do-i-format-an-api-request}

I formati di richiesta variano a seconda dell&#39;API [!DNL Platform] utilizzata. Il modo migliore per scoprire come strutturare le chiamate API è seguire gli esempi forniti nella documentazione del servizio [!DNL Platform] specifico che si sta utilizzando.

Per ulteriori informazioni sulla formattazione delle richieste API, consulta la guida introduttiva all&#39;API Platform [lettura di chiamate API di esempio](./api-guide.md#sample-api).

## Qual è la mia organizzazione? {#what-is-my-ims-organization}

Un’organizzazione è una rappresentazione di Adobe di un cliente. Tutte le soluzioni di Adobe concesse in licenza sono integrate con questa organizzazione del cliente. Quando un&#39;organizzazione ha diritto a [!DNL Experience Platform], può assegnare l&#39;accesso agli sviluppatori. L&#39;ID organizzazione (`x-gw-ims-org-id`) rappresenta l&#39;organizzazione per la quale deve essere eseguita una chiamata API ed è pertanto richiesto come intestazione in tutte le richieste API. Questo ID si trova tramite [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): nella scheda **Integrazioni**, accedi alla sezione **Panoramica** per trovare una particolare integrazione per l&#39;ID in **Credenziali client**. Per informazioni dettagliate su come eseguire l&#39;autenticazione in [!DNL Platform], vedere [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Dove posso trovare la mia chiave API? {#where-can-i-find-my-api-key}

È necessaria una chiave API come intestazione in tutte le richieste API. È disponibile tramite [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Nella console, nella scheda **Integrazioni**, passa alla sezione **Panoramica** per un&#39;integrazione specifica e troverai la chiave in **Credenziali client**. Per informazioni dettagliate su come eseguire l&#39;autenticazione in [!DNL Platform], vedere [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come si ottiene un token di accesso? {#how-do-i-get-an-access-token}

I token di accesso sono necessari nell’intestazione Autorizzazione di tutte le chiamate API. Possono essere generati utilizzando un comando CURL, a condizione che tu abbia accesso a un’integrazione per un’organizzazione. I token di accesso sono validi solo per 24 ore, dopo di che è necessario generare un nuovo token per continuare a utilizzare l’API. Per informazioni dettagliate sulla generazione dei token di accesso, consulta l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come si utilizzano i parametri di query? {#how-do-i-user-query-parameters}

Alcuni endpoint API [!DNL Platform] accettano parametri di query per individuare informazioni specifiche e filtrare i risultati restituiti nella risposta. I parametri di query vengono aggiunti ai percorsi di richiesta con il simbolo del punto interrogativo (`?`) seguito da uno o più parametri di query nel formato `paramName=paramValue`. Quando si combinano più parametri in una singola chiamata, è necessario utilizzare una e commerciale (`&`) per separare i singoli parametri. L’esempio seguente illustra come viene rappresentata nella documentazione una richiesta che utilizza più parametri di query.

Esempi di parametri di query comunemente utilizzati includono:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Per informazioni dettagliate sui parametri di query disponibili per un servizio o un endpoint specifico, consulta la documentazione relativa al servizio.

## Come si indica un campo JSON da aggiornare in una richiesta PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Molte operazioni PATCH nelle API [!DNL Platform] utilizzano [stringhe JSON Pointer](https://tools.ietf.org/html/rfc6901) per indicare le proprietà JSON da aggiornare. Questi sono in genere inclusi nei payload di richiesta utilizzando il formato [Patch JSON](https://tools.ietf.org/html/rfc6902). Per informazioni dettagliate sulla sintassi richiesta per queste tecnologie, consulta la [guida sui concetti fondamentali dell&#39;API](api-fundamentals.md).

## Posso usare Postman per effettuare chiamate alle API [!DNL Platform]? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) è uno strumento utile per visualizzare le chiamate alle API RESTful. La guida introduttiva all&#39;API di [Platform](api-guide.md) contiene un video e le istruzioni per l&#39;importazione di raccolte Postman. Inoltre, viene fornito un elenco di raccolte Postman per ciascun servizio.

## Requisiti di sistema per [!DNL Platform] {#what-are-the-system-requirements-for-platform}

A seconda che si utilizzi l’interfaccia o l’API, si applicano i seguenti requisiti di sistema:

**Per operazioni basate sull&#39;interfaccia utente:**
- Un browser web moderno e standard. Sebbene sia consigliata l&#39;ultima versione di [!DNL Chrome], sono supportate anche le versioni principali corrente e precedenti di [!DNL Firefox], [!DNL Internet Explorer] e Safari.
   - Ogni volta che viene rilasciata una nuova versione principale, [!DNL Platform] inizia a supportare la versione più recente, mentre il supporto per la terza versione più recente viene rimosso.
- Tutti i browser devono avere cookie e JavaScript abilitati.

**Per interazioni con API e sviluppatori:**
- Un ambiente di sviluppo da sviluppare per le integrazioni REST, streaming e Webhook.

## Errori e risoluzione problemi {#errors-and-troubleshooting}

Di seguito è riportato un elenco di errori che possono verificarsi quando si utilizza un servizio [!DNL Experience Platform]. Per le guide alla risoluzione dei problemi dei singoli servizi [!DNL Platform], vedere la [directory per la risoluzione dei problemi dei servizi](#service-troubleshooting-directory) di seguito.

## Codici di stato API {#api-status-codes}

I seguenti codici di stato possono essere rilevati in qualsiasi API [!DNL Experience Platform]. Ognuno di essi ha una varietà di cause, pertanto le spiegazioni fornite in questa sezione sono di natura generale. Per ulteriori dettagli sugli errori specifici nei singoli servizi [!DNL Platform], vedere la [directory di risoluzione dei problemi dei servizi](#service-troubleshooting-directory) di seguito.

| Codice di stato | Descrizione | Possibili cause |
|--- | --- | ---|
| 400 | Richiesta non valida | La richiesta non è stata costruita correttamente, mancano informazioni sulla chiave e/o contiene una sintassi errata. |
| 401 | Autenticazione non riuscita | La richiesta non ha superato un controllo di autenticazione. Il token di accesso potrebbe essere mancante o non valido. Per ulteriori dettagli, consulta la sezione [Errori token OAuth](#oauth-token-is-missing) di seguito. |
| 403 | Non consentito | La risorsa è stata trovata, ma non si dispone delle credenziali corrette per visualizzarla. <br> È probabile che l&#39;errore sia dovuto al fatto che non si dispone delle [autorizzazioni di controllo di accesso](/help/access-control/home.md) necessarie per accedere o modificare la risorsa. Scopri come [ottenere le autorizzazioni di controllo dell&#39;accesso basate su attributi](/help/landing/api-authentication.md#get-abac-permissions) necessarie per utilizzare le API di Platform. </p> |
| 404 | Non trovato | Impossibile trovare la risorsa richiesta nel server. È possibile che la risorsa sia stata eliminata o che il percorso richiesto non sia stato immesso correttamente. |
| 500 | Errore interno del server | Si tratta di un errore lato server. Se effettui molte chiamate simultanee, potresti raggiungere il limite API e dover filtrare i risultati. Per ulteriori informazioni, consulta la guida per gli sviluppatori API [!DNL Catalog Service] nella sezione [filtraggio dei dati](../catalog/api/filter-data.md). Attendi un attimo prima di riprovare a eseguire la richiesta e, se il problema persiste, contatta l’amministratore. |

## Errori di intestazione della richiesta {#request-header-errors}

Tutte le chiamate API in [!DNL Platform] richiedono intestazioni di richiesta specifiche. Per vedere quali intestazioni sono necessarie per i singoli servizi, consulta la [documentazione di riferimento API](https://www.adobe.com/go/platform-api-reference-en). Per trovare i valori per le intestazioni di autenticazione richieste, vedere l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Se una di queste intestazioni risulta mancante o non valida durante una chiamata API, possono verificarsi gli errori seguenti.

### Token OAuth mancante {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione `Authorization` da una richiesta API. Prima di riprovare, assicurati che l’intestazione Autorizzazione sia inclusa con un token di accesso valido.

### Token OAuth non valido {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso fornito nell&#39;intestazione `Authorization` non è valido. Verificare che il token sia stato immesso correttamente oppure [generare un nuovo token](https://www.adobe.com/go/platform-api-authentication-en) nella console Adobe I/O.

### È richiesta una chiave API {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione di chiave API (`x-api-key`) in una richiesta API. Prima di riprovare, assicurati che l’intestazione sia inclusa con una chiave API valida.

### Chiave API non valida {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Questo messaggio di errore viene visualizzato quando il valore dell&#39;intestazione della chiave API (`x-api-key`) fornita non è valido. Prima di riprovare, assicurati di aver immesso correttamente la chiave. Se non conosci la tua chiave API, puoi trovarla nella [Console Adobe I/O](https://console.adobe.io): nella scheda **Integrazioni**, passa alla sezione **Panoramica** per una specifica integrazione per trovare la chiave API in **Credenziali client**.

### Intestazione mancante {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione organizzazione (`x-gw-ims-org-id`) in una richiesta API. Prima di riprovare, assicurati che l’intestazione sia inclusa nell’ID dell’organizzazione.

### Profilo non valido {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Questo messaggio di errore viene visualizzato quando l&#39;integrazione utente o Adobe I/O (identificata dal [token di accesso](#how-do-i-get-an-access-token) nell&#39;intestazione `Authorization`) non è autorizzata ad effettuare chiamate alle API [!DNL Experience Platform] per l&#39;organizzazione fornita nell&#39;intestazione `x-gw-ims-org-id`. Prima di riprovare, assicurati di aver fornito l’ID corretto per la tua organizzazione nell’intestazione. Se non conosci il tuo ID organizzazione, puoi trovarlo nella [Console Adobe I/O](https://console.adobe.io): nella scheda **Integrazioni**, passa alla sezione **Panoramica** per una specifica integrazione per trovare l&#39;ID in **Credenziali client**.

### Errore di aggiornamento tag {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Se è stata apportata una modifica a un’entità di origine o di destinazione come flusso, connessione, connettore di origine o connessione di destinazione da parte di un altro chiamante API, è possibile che venga visualizzato un errore e-mail. A causa della mancata corrispondenza delle versioni, la modifica che stai tentando di apportare non verrà applicata all’ultima versione dell’entità.

Per risolvere questo problema, è necessario recuperare nuovamente l&#39;entità, assicurarsi che le modifiche siano compatibili con la nuova versione dell&#39;entità, quindi inserire il nuovo etag nell&#39;intestazione `If-Match` e infine eseguire la chiamata API.

### Tipo di contenuto valido non specificato {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Questo messaggio di errore viene visualizzato quando una richiesta POST, PUT o PATCH contiene un&#39;intestazione `Content-Type` non valida o mancante. Verificare che l&#39;intestazione sia inclusa nella richiesta e che il relativo valore sia `application/json`.

### Area geografica utente mancante {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Questo messaggio di errore viene visualizzato in uno dei due casi seguenti:
- Quando un&#39;intestazione dell&#39;ID organizzazione (`x-gw-ims-org-id`) errata o non valida viene passata in una richiesta API. Prima di riprovare, assicurati di includere l’ID corretto della tua organizzazione.
- Quando il tuo account (rappresentato dalle credenziali di autenticazione fornite) non è associato a un profilo di prodotto, ad Experience Platform. Segui i passaggi su [generazione delle credenziali di accesso](./api-authentication.md#authentication-for-each-session) nell&#39;esercitazione sull&#39;autenticazione API di Platform per aggiungere Platform al tuo account e aggiornare di conseguenza le credenziali di autenticazione.

## Directory di risoluzione dei problemi del servizio {#service-troubleshooting-directory}

Di seguito è riportato un elenco di guide per la risoluzione dei problemi e documentazione di riferimento API per le API [!DNL Experience Platform]. Ogni guida alla risoluzione dei problemi fornisce le risposte alle domande frequenti e alle soluzioni ai problemi specifici dei singoli servizi [!DNL Platform]. I documenti di riferimento API forniscono una guida completa a tutti gli endpoint disponibili per ciascun servizio e mostrano esempi di corpo della richiesta, risposte e codici di errore che potresti ricevere.

| Servizio | Riferimento API | Risoluzione dei problemi |
| --- | --- | --- |
| Controllo degli accessi | [API di controllo degli accessi](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Guida alla risoluzione dei problemi relativi al controllo degli accessi](../access-control/troubleshooting-guide.md) |
| Acquisizione dei dati Adobe Experience Platform | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [Guida alla risoluzione dei problemi di acquisizione in batch](../ingestion/batch-ingestion/troubleshooting.md) |
| Acquisizione dei dati Adobe Experience Platform | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [Guida alla risoluzione dei problemi di acquisizione in streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guida alla risoluzione dei problemi](../data-science-workspace/troubleshooting-guide.md) |
| Governance dei dati Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] guida alla risoluzione dei problemi](../identity-service/troubleshooting-guide.md) |
| Servizio query Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] guida alla risoluzione dei problemi](../query-service/troubleshooting-guide.md) |
| Segmentazione di Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Domande frequenti e guida alla risoluzione dei problemi](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] e [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] guida alla risoluzione dei problemi](../profile/troubleshooting.md) |
| Sandbox | [API Sandbox](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Guida alla risoluzione dei problemi relativi alle sandbox](../sandboxes/troubleshooting-guide.md) |
