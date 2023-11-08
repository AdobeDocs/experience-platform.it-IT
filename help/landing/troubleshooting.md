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
source-wordcount: '1906'
ht-degree: 3%

---

# [!DNL Platform] Domande frequenti e guida alla risoluzione dei problemi

Questo documento contiene le risposte alle domande più frequenti su Adobe Experience Platform, nonché una guida di alto livello per la risoluzione dei problemi relativi agli errori più comuni che possono verificarsi in qualsiasi [!DNL Experience Platform] API. Per guide alla risoluzione dei problemi su singoli [!DNL Platform] servizi, consulta [directory di risoluzione dei problemi del servizio](#service-troubleshooting-directory) di seguito.

## Domande frequenti {#faq}

Di seguito è riportato un elenco di risposte alle domande più frequenti su Adobe Experience Platform.

## Cosa sono [!DNL Experience Platform] API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] offre più API RESTful che utilizzano richieste HTTP per accedere [!DNL Platform] risorse. Queste API di servizio espongono ciascuna più endpoint e consentono di eseguire operazioni per elencare (GET), cercare (GET), modificare (PUT e/o PATCH) ed eliminare (DELETE) le risorse. Per ulteriori informazioni su endpoint e operazioni specifici disponibili per ciascun servizio, vedere [Documentazione di riferimento API](https://www.adobe.com/go/platform-api-reference-en) su Adobe I/O.

## Come si formatta una richiesta API? {#how-do-i-format-an-api-request}

I formati delle richieste variano a seconda della [!DNL Platform] API in uso. Il modo migliore per imparare a strutturare le chiamate API è seguire insieme agli esempi forniti nella documentazione per le specifiche [!DNL Platform] servizio in uso.

Per ulteriori informazioni sulla formazione delle richieste API, consulta la guida introduttiva all’API della piattaforma [lettura di chiamate API di esempio](./api-guide.md#sample-api) sezione.

## Qual è la mia organizzazione? {#what-is-my-ims-organization}

Un’organizzazione è una rappresentazione di Adobe di un cliente. Tutte le soluzioni di Adobe concesse in licenza sono integrate con questa organizzazione del cliente. Quando un’organizzazione ha il diritto di [!DNL Experience Platform], può assegnare l’accesso agli sviluppatori. ID organizzazione (`x-gw-ims-org-id`) rappresenta l’organizzazione per la quale deve essere eseguita una chiamata API ed è pertanto richiesto come intestazione in tutte le richieste API. Questo ID si trova tramite il [Console Adobe Developer](https://www.adobe.com/go/devs_console_ui): nel **Integrazioni** , passare alla scheda **Panoramica** per una particolare integrazione per trovare l’ID in **Credenziali client**. Per informazioni dettagliate su come eseguire l’autenticazione in [!DNL Platform], vedere [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Dove posso trovare la mia chiave API? {#where-can-i-find-my-api-key}

È necessaria una chiave API come intestazione in tutte le richieste API. È disponibile tramite il [Console Adobe Developer](https://www.adobe.com/go/devs_console_ui). Nella console, sul **Integrazioni** , passare alla scheda **Panoramica** per un’integrazione specifica e troverai la chiave in **Credenziali client**. Per informazioni dettagliate su come eseguire l’autenticazione in [!DNL Platform], vedere [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come si ottiene un token di accesso? {#how-do-i-get-an-access-token}

I token di accesso sono necessari nell’intestazione Autorizzazione di tutte le chiamate API. Possono essere generati utilizzando un comando CURL, a condizione che tu abbia accesso a un’integrazione per un’organizzazione. I token di accesso sono validi solo per 24 ore, dopo di che è necessario generare un nuovo token per continuare a utilizzare l’API. Per informazioni dettagliate sulla generazione dei token di accesso, vedi [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come si utilizzano i parametri di query? {#how-do-i-user-query-parameters}

Alcuni [!DNL Platform] Gli endpoint API accettano parametri di query per individuare informazioni specifiche e filtrare i risultati restituiti nella risposta. I parametri di query vengono aggiunti ai percorsi di richiesta con un punto interrogativo (`?`), seguito da uno o più parametri di query utilizzando il formato `paramName=paramValue`. Quando si combinano più parametri in una singola chiamata, è necessario utilizzare una e commerciale (`&`) per separare i singoli parametri. L’esempio seguente illustra come viene rappresentata nella documentazione una richiesta che utilizza più parametri di query.

Esempi di parametri di query comunemente utilizzati includono:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Per informazioni dettagliate sui parametri di query disponibili per un servizio o un endpoint specifico, consulta la documentazione relativa al servizio.

## Come si indica un campo JSON da aggiornare in una richiesta PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Molte operazioni PATCH in [!DNL Platform] Le API utilizzano [Puntatore JSON](https://tools.ietf.org/html/rfc6901) stringhe per indicare le proprietà JSON da aggiornare. In genere sono inclusi nei payload di richiesta tramite [Patch JSON](https://tools.ietf.org/html/rfc6902) formato. Consulta la [Guida di base sulle API](api-fundamentals.md) per informazioni dettagliate sulla sintassi richiesta per queste tecnologie.

## Posso utilizzare Postman per effettuare chiamate a [!DNL Platform] API? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) è uno strumento utile per visualizzare le chiamate alle API RESTful. Il [Guida introduttiva all’API di Platform](api-guide.md) contiene un video e le istruzioni per l’importazione delle raccolte Postman. Inoltre, viene fornito un elenco di raccolte Postman per ciascun servizio.

## Requisiti di sistema per [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

A seconda che si utilizzi l’interfaccia o l’API, si applicano i seguenti requisiti di sistema:

**Per le operazioni basate sull’interfaccia utente:**
- Un browser web moderno e standard. Mentre l’ultima versione di [!DNL Chrome] è consigliato, le versioni principali attuali e precedenti di [!DNL Firefox], [!DNL Internet Explorer], e Safari.
   - Ogni volta che viene rilasciata una nuova versione principale, [!DNL Platform] inizia a supportare la versione più recente, mentre il supporto per la terza versione più recente viene rimosso.
- Tutti i browser devono avere cookie e JavaScript abilitati.

**Per interazioni con API e sviluppatori:**
- Un ambiente di sviluppo da sviluppare per le integrazioni REST, streaming e Webhook.

## Errori e risoluzione problemi {#errors-and-troubleshooting}

Di seguito è riportato un elenco di errori che è possibile riscontrare durante l’utilizzo di [!DNL Experience Platform] servizio. Per guide alla risoluzione dei problemi su singoli [!DNL Platform] servizi, consulta [directory di risoluzione dei problemi del servizio](#service-troubleshooting-directory) di seguito.

## Codici di stato API {#api-status-codes}

I seguenti codici di stato possono essere rilevati in qualsiasi [!DNL Experience Platform] API. Ognuno di essi ha una varietà di cause, pertanto le spiegazioni fornite in questa sezione sono di natura generale. Per ulteriori dettagli sugli errori specifici in singoli [!DNL Platform] servizi, consultare il [directory di risoluzione dei problemi del servizio](#service-troubleshooting-directory) di seguito.

| Codice di stato | Descrizione | Possibili cause |
|--- | --- | ---|
| 400 | Richiesta non valida | La richiesta non è stata costruita correttamente, mancano informazioni sulla chiave e/o contiene una sintassi errata. |
| 401 | Autenticazione non riuscita | La richiesta non ha superato un controllo di autenticazione. Il token di accesso potrebbe essere mancante o non valido. Consulta la [Errori token OAuth](#oauth-token-is-missing) per ulteriori dettagli. |
| 403 | Non consentito | La risorsa è stata trovata, ma non si dispone delle credenziali corrette per visualizzarla. <br> È probabile che l&#39;errore sia dovuto al fatto che non si dispone del necessario [autorizzazioni di controllo degli accessi](/help/access-control/home.md) per accedere o modificare la risorsa. Scopri come [ottenere le autorizzazioni di controllo dell&#39;accesso basate su attributi necessarie](/help/landing/api-authentication.md#get-abac-permissions) per utilizzare le API di Platform. </p> |
| 404 | Non trovato | Impossibile trovare la risorsa richiesta nel server. È possibile che la risorsa sia stata eliminata o che il percorso richiesto non sia stato immesso correttamente. |
| 500 | Errore interno del server | Si tratta di un errore lato server. Se effettui molte chiamate simultanee, potresti raggiungere il limite API e dover filtrare i risultati. (consultare la [!DNL Catalog Service] Guida secondaria per gli sviluppatori API su [filtraggio dei dati](../catalog/api/filter-data.md) per ulteriori informazioni.) Attendi un attimo prima di riprovare a eseguire la richiesta e, se il problema persiste, contatta l’amministratore. |

## Errori di intestazione della richiesta {#request-header-errors}

Tutte le chiamate API in [!DNL Platform] richiedere intestazioni di richiesta specifiche. Per informazioni sulle intestazioni necessarie per i singoli servizi, vedere [Documentazione di riferimento API](https://www.adobe.com/go/platform-api-reference-en). Per trovare i valori per le intestazioni di autenticazione richieste, vedi [Tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Se una di queste intestazioni risulta mancante o non valida durante una chiamata API, possono verificarsi gli errori seguenti.

### Token OAuth mancante {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Questo messaggio di errore viene visualizzato quando `Authorization` Intestazione mancante in una richiesta API. Prima di riprovare, assicurati che l’intestazione Autorizzazione sia inclusa con un token di accesso valido.

### Token OAuth non valido {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso fornito in `Authorization` intestazione non valida. Verifica che il token sia stato immesso correttamente, oppure [genera un nuovo token](https://www.adobe.com/go/platform-api-authentication-en) nella console Adobe I/O.

### È richiesta una chiave API {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Questo messaggio di errore viene visualizzato quando un’intestazione di chiave API (`x-api-key`) non è presente in una richiesta API. Prima di riprovare, assicurati che l’intestazione sia inclusa con una chiave API valida.

### Chiave API non valida {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Questo messaggio di errore viene visualizzato quando il valore dell’intestazione della chiave API fornita (`x-api-key`) non è valido. Prima di riprovare, assicurati di aver immesso correttamente la chiave. Se non conosci la tua chiave API, puoi trovarla in [Console Adobi I/O](https://console.adobe.io): nel **Integrazioni** , passare alla scheda **Panoramica** per un’integrazione specifica per trovare la chiave API in **Credenziali client**.

### Intestazione mancante {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Questo messaggio di errore viene visualizzato quando un&#39;intestazione organizzazione (`x-gw-ims-org-id`) non è presente in una richiesta API. Prima di riprovare, assicurati che l’intestazione sia inclusa nell’ID dell’organizzazione.

### Profilo non valido {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Questo messaggio di errore viene visualizzato quando l’utente o l’integrazione Adobe I/O (identificata da [token di accesso](#how-do-i-get-an-access-token) nel `Authorization` non è autorizzato ad effettuare chiamate a [!DNL Experience Platform] API per l’organizzazione fornite nella `x-gw-ims-org-id` intestazione. Prima di riprovare, assicurati di aver fornito l’ID corretto per la tua organizzazione nell’intestazione. Se non conosci il tuo ID organizzazione, puoi trovarlo nella sezione [Console Adobi I/O](https://console.adobe.io): nel **Integrazioni** , passare alla scheda **Panoramica** per un’integrazione specifica per trovare l’ID in **Credenziali client**.

### Errore di aggiornamento tag {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Se è stata apportata una modifica a un’entità di origine o di destinazione come flusso, connessione, connettore di origine o connessione di destinazione da parte di un altro chiamante API, è possibile che venga visualizzato un errore e-mail. A causa della mancata corrispondenza delle versioni, la modifica che stai tentando di apportare non verrà applicata all’ultima versione dell’entità.

Per risolvere questo problema, è necessario recuperare nuovamente l’entità, assicurarsi che le modifiche siano compatibili con la nuova versione dell’entità, quindi inserire la nuova e-mail nel `If-Match` e infine effettua la chiamata API.

### Tipo di contenuto valido non specificato {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Questo messaggio di errore viene visualizzato quando una richiesta di POST, PUT o PATCH contiene un valore non valido o mancante `Content-Type` intestazione. Assicurati che l’intestazione sia inclusa nella richiesta e che il suo valore sia `application/json`.

### Area geografica utente mancante {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Questo messaggio di errore viene visualizzato in uno dei due casi seguenti:
- Se l’intestazione dell’ID organizzazione (`x-gw-ims-org-id`) viene passato in una richiesta API. Prima di riprovare, assicurati di includere l’ID corretto della tua organizzazione.
- Quando il tuo account (rappresentato dalle credenziali di autenticazione fornite) non è associato a un profilo di prodotto, ad Experience Platform. Segui i passaggi per [generazione delle credenziali di accesso](./api-authentication.md#authentication-for-each-session) nel tutorial sull’autenticazione API di Platform per aggiungere Platform al tuo account e aggiornare di conseguenza le credenziali di autenticazione.

## Directory di risoluzione dei problemi del servizio {#service-troubleshooting-directory}

Di seguito è riportato un elenco di guide alla risoluzione dei problemi e documentazione di riferimento API per [!DNL Experience Platform] API. Ogni guida alla risoluzione dei problemi fornisce le risposte alle domande frequenti e alle soluzioni ai problemi specifici dei singoli utenti [!DNL Platform] servizi. I documenti di riferimento API forniscono una guida completa a tutti gli endpoint disponibili per ciascun servizio e mostrano esempi di corpo della richiesta, risposte e codici di errore che potresti ricevere.

| Servizio | Documentazione di riferimento API | Risoluzione dei problemi |
| --- | --- | --- |
| Controllo degli accessi | [API di controllo degli accessi](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Guida alla risoluzione dei problemi del controllo degli accessi](../access-control/troubleshooting-guide.md) |
| Acquisizione dei dati Adobe Experience Platform | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [Guida alla risoluzione dei problemi di acquisizione in batch](../ingestion/batch-ingestion/troubleshooting.md) |
| Acquisizione dei dati Adobe Experience Platform | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [Guida alla risoluzione dei problemi di acquisizione in streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guida alla risoluzione dei problemi](../data-science-workspace/troubleshooting-guide.md) |
| Governance dei dati Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Servizio Adobe Experience Platform Identity | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] guida alla risoluzione dei problemi](../identity-service/troubleshooting-guide.md) |
| Servizio query Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] guida alla risoluzione dei problemi](../query-service/troubleshooting-guide.md) |
| Segmentazione di Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Domande frequenti e guida alla risoluzione dei problemi](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] e [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] guida alla risoluzione dei problemi](../profile/troubleshooting.md) |
| Sandbox | [API sandbox](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Guida alla risoluzione dei problemi relativi alle sandbox](../sandboxes/troubleshooting-guide.md) |
