---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida alla risoluzione dei problemi e domande frequenti  Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: 9eeddfaf3e704d66b81f983afcdf5ef3c45c6075
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 2%

---


# [!DNL Platform] Domande frequenti e guida alla risoluzione dei problemi

Questo documento contiene le risposte alle domande frequenti sul Adobe Experience Platform , nonché una guida per la risoluzione dei problemi di alto livello per individuare eventuali errori comuni riscontrati in qualsiasi [!DNL Experience Platform] API. Per le guide alla risoluzione dei problemi sui singoli [!DNL Platform] servizi, consulta la directory [per la risoluzione dei problemi del](#service-troubleshooting-directory) servizio di seguito.

## Domande frequenti {#faq}

Di seguito è riportato un elenco di risposte alle domande frequenti sul  Adobe Experience Platform.

## Cosa sono [!DNL Experience Platform] le API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] offre più API RESTful che utilizzano richieste HTTP per accedere alle [!DNL Platform] risorse. Ciascuna di queste API di servizio espone più endpoint e consente di eseguire operazioni per elencare (GET), cercare (GET), modificare (PUT e/o PATCH) e eliminare risorse (DELETE). Per ulteriori informazioni su endpoint e operazioni specifici disponibili per ogni servizio, consulta la documentazione [di riferimento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) API in Adobe I/O.

## Come si formatta una richiesta API? {#how-do-i-format-an-api-request}

I formati delle richieste variano a seconda dell&#39; [!DNL Platform] API utilizzata. Il modo migliore per imparare a strutturare le chiamate API è seguire gli esempi forniti nella documentazione relativa al [!DNL Platform] servizio in uso.

### Lettura di chiamate API di esempio

La documentazione relativa [!DNL Experience Platform] agli esempi di chiamate API avviene in due modi diversi. Innanzitutto, la chiamata viene presentata nel formato **** API, una rappresentazione modello che mostra solo l&#39;operazione (GET, POST, PUT, PATCH, DELETE) e l&#39;endpoint utilizzato (ad esempio, `/global/classes`). Alcuni modelli mostrano anche la posizione delle variabili per illustrare in che modo una chiamata deve essere formulata, ad esempio `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Le chiamate vengono quindi visualizzate come comandi cURL in una **richiesta**, che include le intestazioni necessarie e il &quot;percorso di base&quot; completo necessario per interagire con l&#39;API. Il percorso di base deve essere preceduto da tutti gli endpoint. Ad esempio, l&#39; `/global/classes` endpoint di cui sopra diventa `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Vedrete il formato API/il pattern di richiesta in tutta la documentazione e dovrete utilizzare il percorso completo mostrato nella richiesta di esempio per effettuare chiamate alle API Platform.

### Esempio di richiesta API

Di seguito è riportata una richiesta API di esempio che illustra il formato che verrà trovato nella documentazione.

**Formato API**

Il formato API mostra l&#39;operazione (GET) e l&#39;endpoint in uso. Le variabili sono indicate da parentesi graffe (in questo caso, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Richiesta**

In questa richiesta di esempio, alle variabili del formato API vengono assegnati valori effettivi nel percorso della richiesta. Vengono visualizzate anche tutte le intestazioni richieste, nonché valori di intestazione di esempio o variabili in cui includere informazioni riservate (come token di sicurezza e ID di accesso).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta illustra cosa ci si aspetta di ricevere in seguito a una chiamata all&#39;API, in base alla richiesta inviata. Talvolta la risposta viene troncata per lo spazio, il che significa che potrebbero essere visualizzate ulteriori informazioni o informazioni aggiuntive rispetto a quelle visualizzate nell’esempio.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

Per ulteriori informazioni su endpoint specifici nelle API di Platform, comprese le intestazioni richieste e i corpi di richiesta, consultate la documentazione [di riferimento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API.

## Qual è la mia organizzazione IMS? {#what-is-my-ims-organization}

Un&#39;organizzazione IMS è una rappresentazione Adobe di un cliente. Tutte le soluzioni Adobe su licenza sono integrate con questa organizzazione cliente. Quando un&#39;organizzazione IMS ha diritto a [!DNL Experience Platform], può assegnare l&#39;accesso agli sviluppatori. L&#39;ID organizzazione IMS (`x-gw-ims-org-id`) rappresenta l&#39;organizzazione per la quale deve essere eseguita una chiamata API ed è pertanto richiesto come intestazione in tutte le richieste API. Questo ID si trova tramite [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): nella scheda **Integrazioni** , andate alla sezione **Panoramica** di una particolare integrazione per trovare l&#39;ID in Credenziali **client**. Per una descrizione dettagliata di come autenticarsi, [!DNL Platform]consulta l’esercitazione [sull’](../tutorials/authentication.md)autenticazione.

## Dove posso trovare la mia chiave API? {#where-can-i-find-my-api-key}

Una chiave API è obbligatoria come intestazione in tutte le richieste API. Può essere trovato tramite [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Nella console, nella scheda **Integrazioni** , passare alla sezione **Panoramica** per un&#39;integrazione specifica e la chiave si trova in Credenziali **client**. Per una descrizione dettagliata di come autenticarsi, [!DNL Platform]consulta l’esercitazione [sull’](../tutorials/authentication.md)autenticazione.

## Come posso ottenere un token di accesso? {#how-do-i-get-an-access-token}

I token di accesso sono richiesti nell&#39;intestazione Autorizzazione di tutte le chiamate API. Possono essere generati utilizzando un `curl` comando, a condizione che sia possibile accedere a un&#39;integrazione per un&#39;organizzazione IMS. I token di accesso sono validi solo 24 ore, dopo di che è necessario generare un nuovo token per continuare a utilizzare l&#39;API. Per informazioni dettagliate sulla generazione dei token di accesso, consultate l&#39;esercitazione [sull&#39;](../tutorials/authentication.md)autenticazione.

## Come si utilizzano i parametri di query? {#how-do-i-user-query-parameters}

Alcuni endpoint [!DNL Platform] API accettano parametri di query per individuare informazioni specifiche e filtrare i risultati restituiti nella risposta. I parametri di query vengono aggiunti ai percorsi di richiesta con un simbolo di punto interrogativo (`?`), seguiti da uno o più parametri di query che utilizzano il formato `paramName=paramValue`. Quando si combinano più parametri in una singola chiamata, è necessario utilizzare una e commerciale (`&`) per separare i singoli parametri. L&#39;esempio seguente illustra come una richiesta che utilizza più parametri di query viene rappresentata nella documentazione.

Alcuni esempi di parametri di query comunemente utilizzati:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Per informazioni dettagliate sui parametri di query disponibili per un servizio o un endpoint specifico, consulta la documentazione specifica del servizio.

## Come posso indicare un campo JSON da aggiornare in una richiesta PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Molte operazioni PATCH nelle [!DNL Platform] API utilizzano le stringhe [JSON Pointer](https://tools.ietf.org/html/rfc6901) per indicare le proprietà JSON da aggiornare. Questi sono in genere inclusi nei payload di richiesta utilizzando il formato Patch [](https://tools.ietf.org/html/rfc6902) JSON. Per informazioni dettagliate sulla sintassi richiesta per queste tecnologie, consultate la guida [](api-fundamentals.md) API di base.

## Posso usare Postman per effettuare chiamate alle [!DNL Platform] API? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) è uno strumento utile per visualizzare le chiamate alle API RESTful. Questo post [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) Medium descrive come impostare Postman per eseguire automaticamente l&#39;autenticazione e utilizzarlo per utilizzare [!DNL Experience Platform] le API.

## Quali sono i requisiti di sistema per [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

A seconda se utilizzate l&#39;interfaccia utente o l&#39;API, si applicano i seguenti requisiti di sistema:

**Per le operazioni basate sull’interfaccia utente:**
- Un browser Web standard e moderno. Sebbene [!DNL Chrome] sia consigliata la versione più recente di, sono supportate anche le versioni principali correnti e precedenti di [!DNL Firefox], [!DNL Internet Explorer]e Safari.
   - Ogni volta che viene rilasciata una nuova versione principale, [!DNL Platform] inizia a supportare la versione più recente, mentre viene eliminato il supporto per la terza versione più recente.
- Tutti i browser devono avere cookie e JavaScript abilitati.

**Per le interazioni API e sviluppatore:**
- Un ambiente di sviluppo per le integrazioni REST, streaming e Webhook.

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Di seguito è riportato un elenco di errori che potrebbero verificarsi durante l&#39;utilizzo di un qualsiasi [!DNL Experience Platform] servizio. Per le guide alla risoluzione dei problemi sui singoli [!DNL Platform] servizi, consulta la directory [per la risoluzione dei problemi del](#service-troubleshooting-directory) servizio di seguito.

## Codici di stato API {#api-status-codes}

I seguenti codici di stato possono essere rilevati su qualsiasi [!DNL Experience Platform] API. Ognuno ha una varietà di cause, quindi le spiegazioni fornite in questa sezione sono di natura generale. Per ulteriori informazioni sugli errori specifici dei singoli [!DNL Platform] servizi, consulta la directory [per la risoluzione dei problemi dei](#service-troubleshooting-directory) servizi di seguito.

| Codice di stato | Descrizione | Possibili cause |
--- | --- | ---
| 400 | Richiesta non valida | La richiesta è stata costruita in modo non corretto, le informazioni chiave mancanti e/o conteneva una sintassi non corretta. |
| 401 | Autenticazione non riuscita | La richiesta non ha superato un controllo di autenticazione. Token di accesso mancante o non valido. Per ulteriori informazioni, consulta la sezione Errori [token](#oauth-token-is-missing) OAuth riportata di seguito. |
| 403 | Vietato | La risorsa è stata trovata, ma non si dispone delle credenziali giuste per visualizzarla. |
| 404 | Non trovato | Impossibile trovare la risorsa richiesta sul server. La risorsa potrebbe essere stata eliminata oppure il percorso richiesto non è stato inserito correttamente. |
| 500 | Errore interno del server | Si tratta di un errore lato server. Se state effettuando molte chiamate simultanee, potreste raggiungere il limite API e dover filtrare i risultati. Per ulteriori informazioni, consultate la guida per gli sviluppatori di [!DNL Catalog Service] API nella guida secondaria sul [filtro dei dati](../catalog/api/filter-data.md) . Attendete un momento prima di riprovare a eseguire la richiesta e, se il problema persiste, contattate l&#39;amministratore. |

## Errori di intestazione richiesta {#request-header-errors}

Tutte le chiamate API in [!DNL Platform] richiedono intestazioni di richiesta specifiche. Per vedere quali intestazioni sono necessarie per i singoli servizi, consulta la documentazione [di riferimento](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API. Per trovare i valori per le intestazioni di autenticazione richieste, vedete l&#39;esercitazione [](../tutorials/authentication.md)Autenticazione. Se una di queste intestazioni risulta mancante o non valida durante una chiamata API, si possono verificare i seguenti errori.

### Token OAuth mancante {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39; `Authorization` intestazione da una richiesta API. Prima di riprovare, verificate che l’intestazione Autorizzazione sia inclusa con un token di accesso valido.

### Token OAuth non valido

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso fornito nell&#39; `Authorization` intestazione non è valido. Verifica che il token sia stato immesso correttamente o [genera un nuovo token](../tutorials/authentication.md) nella console Adobe I/O.

### Chiave API obbligatoria

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione di chiave API (`x-api-key`) da una richiesta API. Prima di riprovare, accertatevi che l&#39;intestazione sia inclusa con una chiave API valida.

### Chiave API non valida

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Questo messaggio di errore viene visualizzato quando il valore dell&#39;intestazione della chiave API (`x-api-key`) specificata non è valido. Prima di riprovare, verificate di aver immesso correttamente la chiave. Se non conosci la tua chiave API, puoi trovarlo nella console [I/O di](https://console.adobe.io)Adobe: nella scheda **Integrazioni** , andate alla sezione **Panoramica** di un&#39;integrazione specifica per trovare la chiave API in Credenziali **client**.


### Intestazione mancante

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Questo messaggio di errore viene visualizzato quando un&#39;intestazione organizzazione IMS (`x-gw-ims-org-id`) non è presente in una richiesta API. Prima di riprovare, accertatevi che l’intestazione sia inclusa con l’ID dell’organizzazione IMS.

### Profilo non valido

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Questo messaggio di errore viene visualizzato quando l&#39;utente o l&#39;integrazione di I/O Adobe (identificata dal token [di](#how-do-i-get-an-access-token) accesso nell&#39; `Authorization` intestazione) non è autorizzato a effettuare chiamate alle [!DNL Experience Platform] API per l&#39;organizzazione IMS fornita nell&#39; `x-gw-ims-org-id` intestazione. Prima di riprovare, verificate di aver fornito l’ID corretto per l’organizzazione IMS nell’intestazione. Se non conosci il tuo ID organizzazione, puoi trovarlo nella console [I/O di](https://console.adobe.io)Adobe: nella scheda **Integrazioni** , andate alla sezione **Panoramica** di un&#39;integrazione specifica per trovare l&#39;ID in Credenziali **client**.

### Tipo di contenuto valido non specificato

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Questo messaggio di errore viene visualizzato quando una richiesta POST, PUT o PATCH ha un&#39;intestazione non valida o mancante `Content-Type` . Accertatevi che l’intestazione sia inclusa nella richiesta e che il relativo valore sia `application/json`.


## Directory di risoluzione dei problemi del servizio {#service-troubleshooting-directory}

Di seguito è riportato un elenco di guide per la risoluzione dei problemi e di documentazione di riferimento API per [!DNL Experience Platform] le API. Ogni guida alla risoluzione dei problemi fornisce risposte alle domande frequenti e soluzioni ai problemi specifici dei singoli [!DNL Platform] servizi. I documenti di riferimento API forniscono una guida completa a tutti gli endpoint disponibili per ciascun servizio, e mostrano i corpi delle richieste di esempio, le risposte e i codici di errore che possono essere ricevuti.

| Servizio | Riferimento API | Risoluzione dei problemi |
--- | --- | ---
| Controllo degli accessi | [API di controllo degli accessi](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guida alla risoluzione dei problemi di controllo degli accessi](../access-control/troubleshooting-guide.md) |
| Catalogo | [API Servizio catalogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| Ingestione dati (batch) | [API di inserimento dati](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guida alla risoluzione dei problemi di inserimento batch](../ingestion/batch-ingestion/troubleshooting.md) |
| Ingestione dei dati (streaming) | [API di inserimento dati](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guida alla risoluzione dei problemi di caricamento in streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Area di lavoro Data Science | [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [Guida alla risoluzione dei problemi per l&#39;area di lavoro di analisi dati](../data-science-workspace/troubleshooting-guide.md) |
| Etichettatura ed applicazione dell&#39;uso dei dati (DULE) | [API servizio criteri DULE](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Modello dati esperienza (XDM) | [API del Registro di sistema dello schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [Domande frequenti sul sistema XDM e guida alla risoluzione dei problemi](../xdm/troubleshooting-guide.md) |
| Servizio identità | [API Servizio identità](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [Guida alla risoluzione dei problemi del servizio identità](../identity-service/troubleshooting-guide.md) |
| Servizio query | [API Servizio query](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [Guida alla risoluzione dei problemi del servizio Query](../query-service/troubleshooting-guide.md) |
| Profilo del cliente in tempo reale | [API profilo cliente in tempo reale](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [Guida alla risoluzione dei problemi dei profili](../profile/troubleshooting.md) |
| Sandbox | [API sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guida alla risoluzione dei problemi sandbox](../sandboxes/troubleshooting-guide.md) |
| Segmentazione | [API di segmentazione](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |