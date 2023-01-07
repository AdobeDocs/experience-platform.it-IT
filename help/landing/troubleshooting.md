---
keywords: Experience Platform;home;argomenti popolari;codici di errore API;codice di errore API;codice di errore API;codici di errore API;errore di richiesta API;risoluzione dei problemi API;errore API
solution: Experience Platform
title: Domande frequenti e guida alla risoluzione dei problemi di Adobe Experience Platform
description: Trova le risposte alle domande frequenti e una guida per la risoluzione dei problemi relativi agli errori più comuni in Experience Platform.
landing-page-description: Trova le risposte alle domande frequenti e una guida per la risoluzione dei problemi relativi agli errori più comuni in Experience Platform.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 4%

---

# [!DNL Platform] Domande frequenti e guida alla risoluzione dei problemi

Questo documento fornisce le risposte alle domande più frequenti su Adobe Experience Platform, nonché una guida alla risoluzione dei problemi di alto livello per gli errori comuni che possono verificarsi in qualsiasi [!DNL Experience Platform] API. Per guide sulla risoluzione dei problemi individuali [!DNL Platform] servizi, vedi [directory di risoluzione dei problemi del servizio](#service-troubleshooting-directory) sotto.

## Domande frequenti {#faq}

Di seguito è riportato un elenco di risposte alle domande frequenti su Adobe Experience Platform.

## Cosa sono [!DNL Experience Platform] API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] offre più API RESTful che utilizzano richieste HTTP per accedere [!DNL Platform] risorse. Ciascuna API di servizio espone più endpoint e consente di eseguire operazioni per elencare (GET), cercare (GET), modificare (PUT e/o PATCH) ed eliminare risorse (DELETE). Per ulteriori informazioni su endpoint e operazioni specifici disponibili per ogni servizio, consulta la sezione [Documentazione di riferimento API](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O.

## Come si formatta una richiesta API? {#how-do-i-format-an-api-request}

I formati di richiesta variano a seconda del [!DNL Platform] API utilizzata. Il modo migliore per strutturare le chiamate API è seguire gli esempi forniti nella documentazione per [!DNL Platform] servizio in uso.

Per ulteriori informazioni sulla formattazione delle richieste API, visita la guida introduttiva all’API Platform [lettura di chiamate API di esempio](./api-guide.md#sample-api) sezione .

## Qual è la mia organizzazione IMS? {#what-is-my-ims-organization}

Un’organizzazione IMS è un Adobe di rappresentazione di un cliente. Tutte le soluzioni di Adobe con licenza sono integrate con questa organizzazione clienti. Quando un&#39;organizzazione IMS ha diritto a [!DNL Experience Platform], può assegnare l’accesso agli sviluppatori. ID organizzazione IMS (`x-gw-ims-org-id`) rappresenta l’organizzazione per la quale deve essere eseguita una chiamata API ed è pertanto obbligatoria come intestazione in tutte le richieste API. Questo ID può essere trovato attraverso [Console Adobe Developer](https://www.adobe.com/go/devs_console_ui): in **Integrazioni** , passa alla **Panoramica** sezione per qualsiasi integrazione particolare per trovare l’ID in **Credenziali client**. Per informazioni dettagliate su come eseguire l&#39;autenticazione in [!DNL Platform], vedi [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Dove posso trovare la mia chiave API? {#where-can-i-find-my-api-key}

Una chiave API è necessaria come intestazione in tutte le richieste API. Può essere trovato attraverso [Console Adobe Developer](https://www.adobe.com/go/devs_console_ui). Nella console, nella **Integrazioni** , passa alla **Panoramica** per un’integrazione specifica e troverai la chiave in **Credenziali client**. Per informazioni dettagliate su come eseguire l&#39;autenticazione in [!DNL Platform], vedi [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come posso ottenere un token di accesso? {#how-do-i-get-an-access-token}

I token di accesso sono necessari nell’intestazione Autorizzazione di tutte le chiamate API. Possono essere generati utilizzando un `curl` , purché sia possibile accedere a un’integrazione per un’organizzazione IMS. I token di accesso sono validi solo per 24 ore, dopodiché è necessario generare un nuovo token per continuare a utilizzare l’API. Per informazioni dettagliate sulla generazione dei token di accesso, consulta la sezione [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come si utilizzano i parametri di query? {#how-do-i-user-query-parameters}

Alcuni [!DNL Platform] Gli endpoint API accettano parametri di query per individuare informazioni specifiche e filtrare i risultati restituiti nella risposta. I parametri di query vengono aggiunti ai percorsi di richiesta con un punto interrogativo (`?`), seguita da uno o più parametri di query che utilizzano il formato `paramName=paramValue`. Quando combini più parametri in una singola chiamata, devi utilizzare una e commerciale (`&`) per separare i singoli parametri. L’esempio seguente illustra come una richiesta che utilizza più parametri di query viene rappresentata nella documentazione.

Alcuni esempi di parametri di query comunemente utilizzati:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Per informazioni dettagliate sui parametri di query disponibili per un servizio o un endpoint specifico, consulta la documentazione specifica del servizio.

## Come si indica un campo JSON da aggiornare in una richiesta PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Molte operazioni di PATCH in [!DNL Platform] Utilizzo delle API [Puntatore JSON](https://tools.ietf.org/html/rfc6901) stringhe per indicare le proprietà JSON da aggiornare. In genere sono inclusi nei payload di richiesta utilizzando [Patch JSON](https://tools.ietf.org/html/rfc6902) formato. Consulta la sezione [Guida di base sulle API](api-fundamentals.md) per informazioni dettagliate sulla sintassi richiesta per queste tecnologie.

## Posso utilizzare Postman per effettuare chiamate a [!DNL Platform] API? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) è uno strumento utile per visualizzare le chiamate alle API RESTful. La [Guida introduttiva all’API di Platform](api-guide.md) contiene un video e istruzioni per l’importazione di raccolte Postman. Inoltre, viene fornito un elenco di raccolte Postman per ogni servizio.

## Quali sono i requisiti di sistema per [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

A seconda dell’interfaccia utente o dell’API, si applicano i seguenti requisiti di sistema:

**Per le operazioni basate sull’interfaccia utente:**
- Un browser web moderno e standard. Mentre l&#39;ultima versione di [!DNL Chrome] è consigliato, versioni principali attuali e precedenti di [!DNL Firefox], [!DNL Internet Explorer]Sono supportati anche Safari e .
   - Ogni volta che viene rilasciata una nuova versione principale, [!DNL Platform] inizia a supportare la versione più recente, mentre viene eliminato il supporto per la terza versione più recente.
- Tutti i browser devono avere i cookie e JavaScript abilitati.

**Per le interazioni con API e sviluppatori:**
- Un ambiente di sviluppo per le integrazioni REST, streaming e Webhook.

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Di seguito è riportato un elenco di errori che si possono verificare quando si utilizzano [!DNL Experience Platform] servizio. Per guide sulla risoluzione dei problemi individuali [!DNL Platform] servizi, vedi [directory di risoluzione dei problemi del servizio](#service-troubleshooting-directory) sotto.

## Codici di stato API {#api-status-codes}

È possibile rilevare i seguenti codici di stato su qualsiasi [!DNL Experience Platform] API. Ognuno ha una varietà di cause, quindi le spiegazioni fornite in questa sezione sono di natura generale. Per maggiori dettagli sugli errori specifici in singoli [!DNL Platform] i servizi [directory di risoluzione dei problemi del servizio](#service-troubleshooting-directory) sotto.

| Codice di stato | Descrizione | Possibili cause |
|--- | --- | ---|
| 400 | Richiesta errata | La richiesta è stata costruita in modo errato, contiene informazioni chiave mancanti e/o contiene una sintassi non corretta. |
| 401 | Autenticazione non riuscita | La richiesta non ha superato un controllo di autenticazione. Token di accesso mancante o non valido. Consulta la sezione [Errori del token OAuth](#oauth-token-is-missing) per ulteriori informazioni, consulta la sezione seguente. |
| 403 | Proibito | La risorsa è stata trovata, ma non si dispone delle credenziali necessarie per visualizzarla. |
| 404 | Non trovato | Impossibile trovare la risorsa richiesta sul server. È possibile che la risorsa sia stata eliminata o che il percorso richiesto non sia stato inserito correttamente. |
| 500 | Errore interno del server | Errore lato server. Se effettui molte chiamate simultanee, potresti raggiungere il limite API e dover filtrare i risultati. (Vedi [!DNL Catalog Service] Guida secondaria per sviluppatori API su [filtraggio dei dati](../catalog/api/filter-data.md) per saperne di più). Attendi un attimo prima di riprovare la richiesta e, se il problema persiste, contatta l’amministratore. |

## Errori di intestazione della richiesta {#request-header-errors}

Tutte le chiamate API in [!DNL Platform] richiede intestazioni di richiesta specifiche. Per vedere quali intestazioni sono necessarie per i singoli servizi, consulta la sezione [Documentazione di riferimento API](https://www.adobe.com/go/platform-api-reference-en). Per trovare i valori per le intestazioni di autenticazione richieste, vedi [Esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Se una di queste intestazioni è mancante o non è valida durante una chiamata API, potrebbero verificarsi i seguenti errori.

### Token OAuth mancante {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Questo messaggio di errore viene visualizzato quando viene visualizzata una `Authorization` intestazione mancante da una richiesta API. Assicurati che l’intestazione Autorizzazione sia inclusa con un token di accesso valido prima di riprovare.

### Il token OAuth non è valido {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso fornito nel `Authorization` intestazione non valida. Assicurati che il token sia stato immesso correttamente oppure [genera un nuovo token](https://www.adobe.com/go/platform-api-authentication-en) nella console Adobe I/O.

### Chiave API obbligatoria {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Questo messaggio di errore viene visualizzato quando viene visualizzata un&#39;intestazione di chiave API (`x-api-key`) manca da una richiesta API. Assicurati che l’intestazione sia inclusa con una chiave API valida prima di riprovare.

### Chiave API non valida {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Questo messaggio di errore viene visualizzato quando viene visualizzato il valore dell&#39;intestazione della chiave API fornita (`x-api-key`) non è valida. Assicurati di aver immesso correttamente la chiave prima di riprovare. Se non conosci la tua chiave API, puoi trovarlo nella [Console Adobe I/O](https://console.adobe.io): in **Integrazioni** , passa alla **Panoramica** per un’integrazione specifica per trovare la chiave API in **Credenziali client**.

### Intestazione mancante {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Questo messaggio di errore viene visualizzato quando un&#39;intestazione org IMS (`x-gw-ims-org-id`) manca da una richiesta API. Assicurati che l’intestazione sia inclusa con l’ID della tua organizzazione IMS prima di riprovare.

### Profilo non valido {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Questo messaggio di errore viene visualizzato quando l&#39;utente o l&#39;integrazione di Adobe I/O (identificata da [token di accesso](#how-do-i-get-an-access-token) in `Authorization` header) non è autorizzato a effettuare chiamate a [!DNL Experience Platform] API per l’organizzazione IMS fornita nella `x-gw-ims-org-id` intestazione. Assicurati di aver fornito l’ID corretto per la tua organizzazione IMS nell’intestazione prima di riprovare. Se non conosci il tuo ID organizzazione, puoi trovarlo nella [Console Adobe I/O](https://console.adobe.io): in **Integrazioni** , passa alla **Panoramica** per un’integrazione specifica per trovare l’ID in **Credenziali client**.

### Errore di aggiornamento del tag {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Puoi ricevere un errore di tag se un’altra chiamata API ha apportato una modifica a un’entità di origine o di destinazione come flusso, connessione, connettore di origine o connessione di destinazione. A causa di una mancata corrispondenza della versione, la modifica che stai tentando di apportare non verrà applicata all’ultima versione dell’entità.

Per risolvere questo problema, devi recuperare nuovamente l’entità, accertarti che le modifiche siano compatibili con la nuova versione dell’entità, quindi inserisci il nuovo tag nella `If-Match` e infine effettua la chiamata API .

### Tipo di contenuto valido non specificato {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Questo messaggio di errore viene visualizzato quando una richiesta di POST, PUT o PATCH presenta una richiesta non valida o mancante `Content-Type` intestazione. Verifica che l’intestazione sia inclusa nella richiesta e che il relativo valore sia `application/json`.

### Area utente mancante {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Questo messaggio di errore viene visualizzato in uno dei due casi seguenti:
- Quando un&#39;intestazione dell&#39;organizzazione IMS non è corretta o non è corretta (`x-gw-ims-org-id`) viene passato in una richiesta API. Assicurati di includere l’ID corretto della tua organizzazione IMS prima di riprovare.
- Quando l’account (rappresentato dalle credenziali di autenticazione fornite) non è associato, ad Experience Platform, a un profilo di prodotto. Segui i passaggi seguenti [generazione delle credenziali di accesso](./api-authentication.md#authentication-for-each-session) nell’esercitazione sull’autenticazione dell’API Platform per aggiungere Platform al tuo account e aggiornare di conseguenza le credenziali di autenticazione.

## Directory di risoluzione dei problemi del servizio {#service-troubleshooting-directory}

Di seguito è riportato un elenco delle guide per la risoluzione dei problemi e la documentazione di riferimento API per [!DNL Experience Platform] API. Ogni guida alla risoluzione dei problemi fornisce le risposte alle domande frequenti e le soluzioni ai problemi specifici delle singole persone [!DNL Platform] servizi. I documenti di riferimento API forniscono una guida completa a tutti gli endpoint disponibili per ogni servizio e mostrano corpi di richiesta di esempio, risposte e codici di errore che possono essere ricevuti.

| Servizio | Documentazione di riferimento API | Risoluzione dei problemi |
| --- | --- | --- |
| Controllo degli accessi | [API di controllo accessi](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Guida alla risoluzione dei problemi di controllo degli accessi](../access-control/troubleshooting-guide.md) |
| Acquisizione dei dati Adobe Experience Platform | [[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) | [Guida alla risoluzione dei problemi di inserimento in batch](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[Guida alla risoluzione dei problemi di acquisizione in streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guida alla risoluzione dei problemi](../data-science-workspace/troubleshooting-guide.md) |
| Governance dei dati di Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Servizio Adobe Experience Platform Identity | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] guida alla risoluzione dei problemi](../identity-service/troubleshooting-guide.md) |
| Servizio query Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] guida alla risoluzione dei problemi](../query-service/troubleshooting-guide.md) |
| Segmentazione Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Domande frequenti e guida alla risoluzione dei problemi](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] e [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] guida alla risoluzione dei problemi](../profile/troubleshooting.md) |
| Sandbox | [API sandbox](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Guida alla risoluzione dei problemi delle sandbox](../sandboxes/troubleshooting-guide.md) |
