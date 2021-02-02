---
keywords: ' Experience Platform;home;argomenti più comuni;codici di errore API;codice di errore API;API codice di errore;API di codici di errore;Errore di richiesta API;Risoluzione dei problemi API;Errore API'
solution: Experience Platform
title: Guida per la risoluzione dei problemi e domande frequenti su Adobe Experience Platform
description: Trova le risposte alle domande frequenti e una guida per la risoluzione dei problemi relativi agli errori più comuni in Experience Platform.
landing-page-description: Trova le risposte alle domande frequenti e una guida per la risoluzione dei problemi relativi agli errori più comuni in Experience Platform.
topic: getting started
type: Documentation
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1994'
ht-degree: 3%

---


# [!DNL Platform] Domande frequenti e guida alla risoluzione dei problemi

Questo documento contiene le risposte alle domande frequenti su Adobe Experience Platform, nonché una guida per la risoluzione dei problemi di alto livello per individuare eventuali errori comuni riscontrati in qualsiasi [!DNL Experience Platform] API. Per le guide alla risoluzione dei problemi relative ai singoli servizi [!DNL Platform], consultare la [directory per la risoluzione dei problemi dei servizi](#service-troubleshooting-directory) di seguito.

## Domande frequenti {#faq}

Segue un elenco di risposte alle domande frequenti su Adobe Experience Platform.

## Cosa sono le [!DNL Experience Platform] API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] offre più API RESTful che utilizzano richieste HTTP per accedere alle  [!DNL Platform] risorse. Ciascuna di queste API di servizio espone più endpoint e consente di eseguire operazioni per elencare (GET), cercare (GET), modificare (PUT e/o PATCH) e eliminare (DELETE) risorse. Per ulteriori informazioni su endpoint e operazioni specifici disponibili per ogni servizio, consultare la [documentazione di riferimento API](http://www.adobe.com/go/platform-api-reference-en)  Adobe I/O.

## Come si formatta una richiesta API? {#how-do-i-format-an-api-request}

I formati delle richieste variano a seconda dell&#39;API [!DNL Platform] in uso. Il modo migliore per imparare a strutturare le chiamate API è seguire gli esempi forniti nella documentazione per il particolare [!DNL Platform] servizio che si sta utilizzando.

### Lettura di chiamate API di esempio

La documentazione relativa a [!DNL Experience Platform] mostra le chiamate API di esempio in due modi diversi. Innanzitutto, la chiamata viene presentata nel suo **formato API**, una rappresentazione modello che mostra solo l&#39;operazione (GET, POST, PUT, PATCH, DELETE) e l&#39;endpoint utilizzato (ad esempio, `/global/classes`). Alcuni modelli mostrano anche la posizione delle variabili per illustrare come formulare una chiamata, ad esempio `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Le chiamate vengono quindi visualizzate come comandi cURL in una **Request**, che include le intestazioni necessarie e il &quot;percorso di base&quot; completo necessari per interagire con l&#39;API. Il percorso di base deve essere preceduto da tutti gli endpoint. Ad esempio, l&#39;endpoint `/global/classes` sopra indicato diventa `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Vedrete il formato API/il pattern di richiesta in tutta la documentazione e dovrete utilizzare il percorso completo mostrato nella richiesta di esempio quando effettuerete chiamate alle API della piattaforma.

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

Per ulteriori informazioni su endpoint specifici nelle API della piattaforma, comprese le intestazioni richieste e i corpi di richiesta, consultate la [documentazione di riferimento API](http://www.adobe.com/go/platform-api-reference-en).

## Qual è la mia organizzazione IMS? {#what-is-my-ims-organization}

Un&#39;organizzazione IMS è una rappresentazione  Adobe di un cliente. Tutte le soluzioni  Adobe con licenza sono integrate con questa organizzazione cliente. Quando un&#39;organizzazione IMS ha diritto a [!DNL Experience Platform], può assegnare l&#39;accesso agli sviluppatori. L&#39;ID organizzazione IMS (`x-gw-ims-org-id`) rappresenta l&#39;organizzazione per la quale deve essere eseguita una chiamata API ed è pertanto richiesto come intestazione in tutte le richieste API. Questo ID si trova tramite la [ console per sviluppatori di Adobi](https://www.adobe.com/go/devs_console_ui): nella scheda **Integrazioni**, andate alla sezione **Panoramica** per qualsiasi integrazione particolare e cercate l&#39;ID in **Credenziali client**. Per una descrizione dettagliata di come autenticarsi in [!DNL Platform], vedere l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Dove posso trovare la mia chiave API? {#where-can-i-find-my-api-key}

Una chiave API è obbligatoria come intestazione in tutte le richieste API. È disponibile tramite la [ Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). All&#39;interno della console, nella scheda **Integrazioni**, passare alla sezione **Panoramica** per una specifica integrazione e individuare la chiave in **Credenziali client**. Per una descrizione dettagliata di come autenticarsi in [!DNL Platform], vedere l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come posso ottenere un token di accesso? {#how-do-i-get-an-access-token}

I token di accesso sono richiesti nell&#39;intestazione Autorizzazione di tutte le chiamate API. Possono essere generati utilizzando un comando `curl`, a condizione che sia possibile accedere a un&#39;integrazione per un&#39;organizzazione IMS. I token di accesso sono validi solo 24 ore, dopo di che è necessario generare un nuovo token per continuare a utilizzare l&#39;API. Per informazioni dettagliate sulla generazione dei token di accesso, vedere l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

## Come si utilizzano i parametri di query? {#how-do-i-user-query-parameters}

Alcuni endpoint [!DNL Platform] API accettano parametri di query per individuare informazioni specifiche e filtrare i risultati restituiti nella risposta. I parametri di query vengono aggiunti ai percorsi di richiesta con un simbolo di punto interrogativo (`?`), seguiti da uno o più parametri di query con il formato `paramName=paramValue`. Quando si combinano più parametri in una singola chiamata, è necessario utilizzare una e commerciale (`&`) per separare i singoli parametri. L&#39;esempio seguente illustra come una richiesta che utilizza più parametri di query viene rappresentata nella documentazione.

Alcuni esempi di parametri di query comunemente utilizzati:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Per informazioni dettagliate sui parametri di query disponibili per un servizio o un endpoint specifico, consulta la documentazione specifica del servizio.

## Come posso indicare un campo JSON da aggiornare in una richiesta di PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Molte operazioni sui PATCH nelle [!DNL Platform] API utilizzano le stringhe [JSON Pointer](https://tools.ietf.org/html/rfc6901) per indicare le proprietà JSON da aggiornare. Questi sono in genere inclusi nei payload di richiesta utilizzando il formato [JSON Patch](https://tools.ietf.org/html/rfc6902). Per informazioni dettagliate sulla sintassi richiesta per queste tecnologie, consultate la [Guida di base delle API](api-fundamentals.md).

## Posso utilizzare Postman per effettuare chiamate alle [!DNL Platform] API? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postmanis è uno strumento utile per visualizzare le chiamate alle API RESTful. ](https://www.postman.com/) Questo [Post medio](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) descrive come impostare Postman per eseguire automaticamente l&#39;autenticazione e utilizzarlo per utilizzare le [!DNL Experience Platform] API.

## Quali sono i requisiti di sistema per [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

A seconda se utilizzate l&#39;interfaccia utente o l&#39;API, si applicano i seguenti requisiti di sistema:

**Per le operazioni basate sull’interfaccia utente:**
- Un browser Web standard e moderno. Sebbene sia consigliata l&#39;ultima versione di [!DNL Chrome], sono supportate anche le versioni principali correnti e precedenti di [!DNL Firefox], [!DNL Internet Explorer] e Safari.
   - Ogni volta che viene rilasciata una nuova versione principale, [!DNL Platform] inizia a supportare la versione più recente, mentre il supporto per la terza versione più recente viene eliminato.
- Tutti i browser devono avere cookie e JavaScript abilitati.

**Per le interazioni API e sviluppatore:**
- Un ambiente di sviluppo per le integrazioni REST, streaming e Webhook.

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Di seguito è riportato un elenco di errori che possono verificarsi durante l&#39;utilizzo di un qualsiasi servizio [!DNL Experience Platform]. Per le guide alla risoluzione dei problemi relative ai singoli servizi [!DNL Platform], consultare la [directory per la risoluzione dei problemi dei servizi](#service-troubleshooting-directory) di seguito.

## Codici di stato API {#api-status-codes}

I seguenti codici di stato possono essere rilevati su qualsiasi API [!DNL Experience Platform]. Ognuno ha una varietà di cause, quindi le spiegazioni fornite in questa sezione sono di natura generale. Per ulteriori informazioni sugli errori specifici relativi ai singoli servizi [!DNL Platform], vedere la [directory per la risoluzione dei problemi del servizio](#service-troubleshooting-directory) di seguito.

| Codice di stato | Descrizione | Possibili cause |
--- | --- | ---
| 400 | Richiesta non valida | La richiesta è stata costruita in modo non corretto, le informazioni chiave mancanti e/o conteneva una sintassi non corretta. |
| 401 | Autenticazione non riuscita | La richiesta non ha superato un controllo di autenticazione. Token di accesso mancante o non valido. Per ulteriori informazioni, vedere la sezione [Errori token OAuth](#oauth-token-is-missing) di seguito. |
| 403 | Vietato | La risorsa è stata trovata, ma non si dispone delle credenziali giuste per visualizzarla. |
| 404 | Non trovato | Impossibile trovare la risorsa richiesta sul server. La risorsa potrebbe essere stata eliminata oppure il percorso richiesto non è stato inserito correttamente. |
| 500 | Errore interno del server | Si tratta di un errore lato server. Se state effettuando molte chiamate simultanee, potreste raggiungere il limite API e dover filtrare i risultati. (Per ulteriori informazioni, consultate la guida per gli sviluppatori [!DNL Catalog Service] API in [filtro dei dati](../catalog/api/filter-data.md).) Attendete un momento prima di riprovare a eseguire la richiesta e, se il problema persiste, contattate l&#39;amministratore. |

## Errori di intestazione richiesta {#request-header-errors}

Tutte le chiamate API in [!DNL Platform] richiedono intestazioni di richiesta specifiche. Per vedere quali intestazioni sono necessarie per i singoli servizi, consultare la [Documentazione di riferimento API](http://www.adobe.com/go/platform-api-reference-en). Per trovare i valori per le intestazioni di autenticazione richieste, vedere l&#39; [Esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Se una di queste intestazioni risulta mancante o non valida durante una chiamata API, si possono verificare i seguenti errori.

### Token OAuth mancante {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione `Authorization` da una richiesta API. Prima di riprovare, verificate che l’intestazione Autorizzazione sia inclusa con un token di accesso valido.

### Token OAuth non valido

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso fornito nell&#39;intestazione `Authorization` non è valido. Assicurarsi che il token sia stato immesso correttamente oppure [generare un nuovo token](https://www.adobe.com/go/platform-api-authentication-en) nella  Adobe I/O Console.

### Chiave API obbligatoria

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Questo messaggio di errore viene visualizzato quando un&#39;intestazione di chiave API (`x-api-key`) manca da una richiesta API. Prima di riprovare, accertatevi che l&#39;intestazione sia inclusa con una chiave API valida.

### Chiave API non valida

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Questo messaggio di errore viene visualizzato quando il valore dell&#39;intestazione della chiave API specificata (`x-api-key`) non è valido. Prima di riprovare, verificate di aver immesso correttamente la chiave. Se non conosci la chiave API, puoi trovarlo nella [ Adobe I/O Console](https://console.adobe.io): nella scheda **Integrazioni**, andate alla sezione **Panoramica** per una specifica integrazione e individuate la chiave API in **Credenziali client**.


### Intestazione mancante

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Questo messaggio di errore viene visualizzato quando un&#39;intestazione organizzazione IMS (`x-gw-ims-org-id`) manca da una richiesta API. Prima di riprovare, accertatevi che l’intestazione sia inclusa con l’ID dell’organizzazione IMS.

### Profilo non valido

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Questo messaggio di errore viene visualizzato quando l&#39;utente o &#39;integrazione Adobe I/O (identificata dal [token di accesso](#how-do-i-get-an-access-token) nell&#39;intestazione `Authorization`) non è autorizzato a effettuare chiamate alle [!DNL Experience Platform] API per l&#39;organizzazione IMS fornite nell&#39;intestazione `x-gw-ims-org-id`. Prima di riprovare, verificate di aver fornito l’ID corretto per l’organizzazione IMS nell’intestazione. Se non conosci il tuo ID organizzazione, puoi trovarlo nella [ Adobe I/O Console](https://console.adobe.io): nella scheda **Integrazioni**, andate alla sezione **Panoramica** per una specifica integrazione e cercate l&#39;ID in **Credenziali client**.

### Tipo di contenuto valido non specificato

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Questo messaggio di errore viene visualizzato quando un&#39;intestazione `Content-Type` POST, PUT o PATCH di una richiesta contiene un&#39;intestazione non valida o mancante. Accertatevi che l’intestazione sia inclusa nella richiesta e che il relativo valore sia `application/json`.


## Directory di risoluzione dei problemi del servizio {#service-troubleshooting-directory}

Di seguito è riportato un elenco delle guide per la risoluzione dei problemi e della documentazione di riferimento API per le [!DNL Experience Platform] API. Ogni guida alla risoluzione dei problemi fornisce risposte alle domande frequenti e soluzioni ai problemi specifici dei singoli [!DNL Platform] servizi. I documenti di riferimento API forniscono una guida completa a tutti gli endpoint disponibili per ciascun servizio, e mostrano i corpi delle richieste di esempio, le risposte e i codici di errore che possono essere ricevuti.

| Servizio | Riferimento API | Risoluzione dei problemi |
| --- | --- | --- |
| Controllo di accesso | [API di controllo degli accessi](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guida alla risoluzione dei problemi di controllo degli accessi](../access-control/troubleshooting-guide.md) |
| Ingestione dati Adobe Experience Platform | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guida ](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[alla risoluzione dei problemi di acquisizione batchGuida alla risoluzione dei problemi di assimilazione dello streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guida alla risoluzione dei problemi](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform Data Governance | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Servizio Adobe Experience Platform Identity | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] guida alla risoluzione dei problemi](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] guida alla risoluzione dei problemi](../query-service/troubleshooting-guide.md) |
| Segmentazione Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] Domande frequenti e guida alla risoluzione dei problemi](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] ed [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] guida alla risoluzione dei problemi](../profile/troubleshooting.md) |
| Sandbox | [API sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guida alla risoluzione dei problemi sandbox](../sandboxes/troubleshooting-guide.md) |

