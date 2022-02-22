---
keywords: Experience Platform;home;argomenti comuni;spazio dei nomi identità;spazio dei nomi identità
solution: Experience Platform
title: Guida alla risoluzione dei problemi del servizio Identity
topic-legacy: troubleshooting
description: Questo documento fornisce le risposte alle domande frequenti sul servizio Adobe Experience Platform Identity e una guida alla risoluzione dei problemi relativi agli errori comuni.
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 80530705f5f8d30294ad31e00d8956257ee2c085
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi del servizio Identity

Questo documento fornisce le risposte alle domande frequenti su Adobe Experience Platform [!DNL Identity Service], nonché una guida alla risoluzione dei problemi relativi agli errori comuni. Per domande e risoluzione dei problemi relativi [!DNL Platform] API in generale, consulta la sezione [Guida alla risoluzione dei problemi dell’API Adobe Experience Platform](../landing/troubleshooting.md).

I dati che identificano un singolo cliente sono spesso frammentati tra i vari dispositivi e sistemi utilizzati per interagire con il tuo marchio. [!DNL Identity Service] riunisce queste identità frammentate, facilitando una comprensione completa del comportamento dei clienti in modo da poter offrire esperienze digitali di impatto in tempo reale. Per ulteriori informazioni, consulta la sezione [Panoramica del servizio Identity](./home.md).

## Domande frequenti

Di seguito è riportato un elenco delle risposte alle domande frequenti su [!DNL Identity Service].

## Cosa sono i dati di identità?

I dati di identità sono tutti i dati che possono essere utilizzati per identificare una singola persona. A seconda del contesto in cui i dati vengono utilizzati all’interno della tua organizzazione, i dati di identità possono includere nomi utente, indirizzi e-mail e ID dai sistemi CRM. I dati di identità non sono limitati agli utenti registrati del tuo sito web o servizio, in quanto gli utenti anonimi possono essere identificati anche dal loro ID dispositivo o cookie.

## Qual è il vantaggio dell&#39;etichettatura dei campi di dati come identità?

L’etichettatura di alcuni campi di dati come identità nei dati dei record e delle serie temporali consente di mappare le relazioni di identità all’interno della struttura naturale dei dati e di riconciliare i dati duplicati tra canali. Consulta la sezione [Panoramica del servizio Identity](./home.md) per ulteriori informazioni.

## Quali sono le identità conosciute e anonime?

Un&#39;identità nota si riferisce a un valore di identità che può essere utilizzato da solo o con altre informazioni per identificare, contattare o individuare una singola persona. Esempi di identità note possono includere indirizzi e-mail, numeri di telefono e ID CRM.

Un&#39;identità anonima si riferisce a un valore di identità che non può essere utilizzato da solo o con altre informazioni per identificare, contattare o individuare una persona singola (ad esempio un ID cookie).

## Cos’è un grafico di identità privata?

Un grafico di identità privata è una mappa privata delle relazioni tra identità unite e collegate, visibile solo all’organizzazione.

Quando più identità sono incluse in tutti i dati acquisiti da un endpoint di streaming o inviati a un set di dati abilitato per [!DNL Identity Service], queste identità sono collegate nel grafico Private Identity. [!DNL Identity Service] sfrutta questo grafico per ottenere identità globali per un determinato consumatore o entità, consentendo l’unione delle identità e dei profili.

## Come si creano più campi di identità all&#39;interno di uno schema XDM?

[Experience Data Model (XDM)](../xdm/home.md) Gli schemi supportano più campi di identità. Qualsiasi campo di dati di tipo `string` all&#39;interno di uno schema che implementa la classe Profilo individuale XDM o ExperienceEvent XDM può essere etichettata come campo di identità. Una volta etichettati, tutti i dati contenuti in questi campi vengono aggiunti alla mappa di identità del profilo.

Per i passaggi su come etichettare un campo XDM come campo di identità utilizzando l’interfaccia utente, vedi [Sezione identità](../xdm/tutorials/create-schema-ui.md) nell’esercitazione Editor di schema. Se utilizzi l’API, consulta la sezione [Sezione descrittore di identità](../xdm/tutorials/create-schema-api.md) nell’esercitazione sull’API del Registro di sistema dello schema.

## Esistono contesti in cui alcuni campi non devono essere etichettati come identità?

I campi di identità devono essere riservati ai valori univoci per ogni singolo utente. Ad esempio, considera un set di dati per un programma fedeltà clienti. Il campo &quot;livello fedeltà&quot; (oro, argento, bronzo) non sarebbe un campo di identità utile, mentre l&#39;ID fedeltà, un valore unico, sarebbe.

I campi come i codici ZIP e gli indirizzi IP non devono essere etichettati come identità per singoli utenti, in quanto questi valori possono essere applicati a più di una singola persona. Questi tipi di campi devono essere etichettati solo come identità per le strategie di marketing a livello di famiglia.

## Perché i campi di identità non collegano il modo in cui mi aspetto?

Utilizzo della [`/cluster/members` endpoint](./api/list-cluster-identites.md) nell’API del servizio Identity, puoi visualizzare le identità associate per uno o più campi di identità. Se la risposta non restituisce le identità collegate desiderate, assicurati di fornire le informazioni di identità appropriate nei dati XDM. Vedi la sezione su [fornitura di dati XDM al servizio Identity](./home.md) nella panoramica del servizio Identity per ulteriori informazioni.

## Che cos’è uno spazio dei nomi di identità?

Uno spazio dei nomi di identità fornisce il contesto in cui i campi di identità si relazionano all’identità di un cliente. Ad esempio, i campi di identità nello spazio dei nomi &quot;E-mail&quot; devono essere conformi a un formato e-mail standard (nome<span>@emailprovider.com) mentre i campi che utilizzano lo spazio dei nomi &quot;Phone&quot; devono essere conformi a un numero di telefono standard (come 987-555-1234 in Nord America).

I namespace distinguono valori di identità simili tra diversi sistemi CRM. Ad esempio, considera un profilo che contiene un ID fedeltà numerico associato al programma di ricompense della tua azienda. Uno spazio dei nomi di &quot;Fedeltà&quot; separerebbe questo valore da un ID numerico simile per il sistema eCommerce che viene visualizzato anche nello stesso profilo.

Consulta la sezione [panoramica dello spazio dei nomi identità](./home.md) per ulteriori informazioni.

## Come si associa un&#39;identità a uno spazio dei nomi di identità?

I campi di identità devono essere associati a uno spazio dei nomi di identità esistente al momento della loro creazione. Eventuali nuovi spazi dei nomi devono essere [creato utilizzando l’API](#how-do-i-create-a-custom-namespace-for-my-organization) prima di associarli ai campi di identità.

Per istruzioni dettagliate sulla definizione di uno spazio dei nomi durante la creazione di un descrittore di identità utilizzando l’API, consulta la sezione su [creazione di un descrittore](../xdm/tutorials/create-schema-ui.md) nella guida per gli sviluppatori del Registro di schema. Per contrassegnare un campo di schema come identità nell’interfaccia utente, segui i passaggi descritti nella sezione [Esercitazione sull’Editor di schema](../xdm/tutorials/create-schema-api.md).

## Quali sono i namespace di identità standard forniti da Experience Platform? {#standard-namespaces}

I namespace di identità standard sono spazi dei nomi disponibili per tutte le organizzazioni. Consulta la sezione [Panoramica sugli spazi dei nomi delle identità](./namespaces.md) per un elenco completo dei namespace standard disponibili.

## Dove posso trovare l’elenco dei namespace identità disponibili per la mia organizzazione?

Utilizzo della [API del servizio Identity](https://www.adobe.io/experience-platform-apis/references/identity-service), puoi elencare tutti i namespace di identità disponibili per la tua organizzazione effettuando una richiesta GET al `/idnamespace/identities` punto finale. Vedi la sezione su [elenco dei namespace disponibili](./api/list-namespaces.md) per ulteriori informazioni, consulta la panoramica dell’API del servizio Identity .

## Come si crea uno spazio dei nomi personalizzato per la mia organizzazione?

Utilizzo della [API del servizio Identity](https://www.adobe.io/experience-platform-apis/references/identity-service), puoi creare uno spazio dei nomi di identità personalizzato per la tua organizzazione effettuando una richiesta di POST al `/idnamespace/identities` punto finale. Vedi la sezione su [creazione di uno spazio dei nomi personalizzato](./api/create-custom-namespace.md) per ulteriori informazioni, consulta la panoramica dell’API del servizio Identity .

## Cosa sono le identità composite e gli XID?

Le identità sono referenziate nelle chiamate API dalla loro identità composita o XID. Un&#39;identità composita è una rappresentazione di un&#39;identità che contiene un valore ID e uno spazio dei nomi. Un XID è un identificatore a valore singolo che rappresenta lo stesso costrutto di un’identità composita (un ID e uno spazio dei nomi) e viene assegnato automaticamente a nuove identità quando viene mantenuto dal servizio Identity. Consulta la sezione [Panoramica API del servizio Identity](./home.md) per ulteriori informazioni.

## In che modo il servizio Identity gestisce le informazioni personali identificabili (PII)?

Il servizio Identity crea un hash di crittografia potente e unidirezionale di PII prima di valori persistenti. I dati di identità negli spazi dei nomi &quot;Telefono&quot; e &quot;E-mail&quot; vengono automaticamente crittografati con SHA-256, con i valori &quot;E-mail&quot; automaticamente convertiti in minuscole prima dell’hashing.

## È necessario crittografare tutti i dati PII prima di inviarli a Platform?

Non è necessario crittografare manualmente i dati PII prima di acquisirli in Platform. Applicando la `I1` l’etichetta di utilizzo dei dati in tutti i campi di dati applicabili, Platform converte automaticamente questi campi in valori ID con hash al momento dell’acquisizione.

Per i passaggi su come applicare e gestire le etichette di utilizzo dei dati, consulta la [esercitazione sulle etichette per l&#39;utilizzo dei dati](../data-governance/labels/user-guide.md).

## Ci sono delle considerazioni quando si usano gli hashing delle identità basate su PII?

Se invii valori PII con hash al servizio Identity, devi utilizzare lo stesso metodo di crittografia nei set di dati. In questo modo lo stesso valore di identità nei set di dati genera gli stessi valori con hash e può essere abbinato e collegato correttamente nel grafico delle identità.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## Perché non posso accedere alla pagina o alle API del grafico delle identità?

L’amministratore di Platform deve effettuare il provisioning con `view-identity-graph` per poter visualizzare i dati del grafico delle identità. Senza questa autorizzazione, riceverai un messaggio di autorizzazione negata sulla pagina del visualizzatore del grafico dell’identità e durante la chiamata alle API di Platform. Consulta la sezione [panoramica del controllo degli accessi](../access-control/home.md) per ulteriori informazioni sulle autorizzazioni.

## Risoluzione dei problemi

La sezione seguente fornisce suggerimenti per la risoluzione dei problemi relativi a codici di errore specifici e a comportamenti imprevisti che potresti riscontrare durante l&#39;utilizzo di [!DNL Identity Service] API.

## [!DNL Identity Service] messaggi di errore

Di seguito è riportato un elenco di messaggi di errore che potresti riscontrare durante l’utilizzo del [!DNL Identity Service] API.

### Parametro di query obbligatorio mancante

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Questo errore viene visualizzato quando un parametro di query obbligatorio non è stato incluso nel percorso della richiesta. La `detail` del messaggio di errore fornisce il nome del parametro mancante. Le varianti di questo messaggio di errore includono:

- Parametro di query obbligatorio mancante - nsId
- Parametro di query obbligatorio mancante - id
- Parametro di query obbligatorio mancante - xid o (nsid,id)
- Parametro di query obbligatorio mancante - targetNs
- Parametro di query obbligatorio mancante - xids o compositoXids

Verifica di includere correttamente il parametro indicato nel percorso della richiesta prima di riprovare.

### La marca temporale deve essere compresa negli ultimi 180 giorni

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] elimina i dati più vecchi di 180 giorni. Questo messaggio di errore viene visualizzato quando si tenta di accedere a dati più vecchi di questo.

### Esiste un limite di 1000 XID in una singola chiamata

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Questo messaggio di errore viene visualizzato quando si tenta di recuperare informazioni di identità per un numero superiore al massimo di [XID](#what-are-composite-identities-and-xids) consentito in una singola chiamata API. Per risolvere il problema, riduci il numero di XID nella richiesta al di sotto del limite visualizzato.


### Esiste un limite per 1000 compositeXids in una singola chiamata

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Questo messaggio di errore viene visualizzato quando si tenta di recuperare informazioni di identità per un numero superiore al massimo di [identità composite](#what-are-composite-identities-and-xids) consentito in una singola chiamata API. Riduci il numero di identità composite nella richiesta al di sotto del limite visualizzato per risolvere il problema.

### Il tipo di grafico specificato non è valido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Questo messaggio di errore viene visualizzato quando viene visualizzata una `graph-type` al parametro query viene assegnato un valore non valido nel percorso della richiesta. Vedi la sezione su [grafici di identità](./home.md) in [!DNL Identity Service] panoramica per scoprire quali tipi di grafico sono supportati.

### Il token del servizio non ha un ambito valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Questo messaggio di errore viene visualizzato quando non è stato eseguito il provisioning dell’organizzazione IMS con le autorizzazioni appropriate per [!DNL Identity Service]. Per risolvere il problema, contatta l’amministratore di sistema.

### Il token del servizio gateway non è valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

In caso di errore, il token di accesso non è valido. I token di accesso scadono ogni 24 ore e devono essere rigenerati per continuare a utilizzare [!DNL Platform] API. Consulta la sezione [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per istruzioni su come generare nuovi token di accesso.

### Token del servizio di autorizzazione non valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

In caso di errore, il token di accesso non è valido. I token di accesso scadono ogni 24 ore e devono essere rigenerati per continuare a utilizzare [!DNL Platform] API. Consulta la sezione [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per istruzioni su come generare nuovi token di accesso.

### Il token utente non ha un contesto di prodotto valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso non è stato generato da un [!DNL Experience Platform] integrazione. Consulta la sezione [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per istruzioni su come generare nuovi token di accesso per un [!DNL Experience Platform] integrazione.

### Errore interno durante la ricezione di XID nativo dal codice di identità e spazio dei nomi

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Quando [!DNL Identity Service] persiste un&#39;identità. All&#39;ID dell&#39;identità e all&#39;ID dello spazio dei nomi associato viene assegnato un identificatore univoco denominato XID. Questo messaggio viene visualizzato quando si verifica un errore durante il processo di ricerca dell&#39;XID per un valore ID e uno spazio dei nomi specificati.

### Per l’organizzazione IMS non è disponibile il provisioning per [!DNL Identity Service] usage

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Questo messaggio di errore viene visualizzato quando non è stato eseguito il provisioning dell’organizzazione IMS con le autorizzazioni appropriate per [!DNL Identity Service]. Per risolvere il problema, contatta l’amministratore di sistema.

### Errore interno del server

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Questo errore viene visualizzato quando si verifica un&#39;eccezione imprevista nell&#39;esecuzione di un [!DNL Platform] chiamata di servizio. Si consiglia di programmare le chiamate automatizzate in modo da ripetere le richieste alcune volte a un intervallo di tempo quando viene ricevuto questo errore. Se il problema persiste, contattare l&#39;amministratore di sistema.

## Codici di errore di inserimento batch

[!DNL Identity Service] acquisisce i dati di identità dai record e dai dati delle serie temporali caricati in [!DNL Platform] mediante l’acquisizione in batch. Poiché l’acquisizione in batch è un processo asincrono, è necessario visualizzare i dettagli di un batch per visualizzare gli errori. Gli errori si accumulano mentre il batch progredisce fino al completamento del batch.

Di seguito è riportato un elenco dei messaggi di errore relativi a [!DNL Identity Service] è possibile che si verifichi quando si utilizza il [API di acquisizione dati](https://www.adobe.io/experience-platform-apis/references/data-ingestion/).

### Schema XDM sconosciuto

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] utilizza solo identità per i dati di record o serie temporali conformi alla [!DNL Profile] o [!DNL ExperienceEvent] classi, rispettivamente. Tentativo di acquisizione di dati per [!DNL Identity Service] che non aderisce a nessuna delle due classi attiverà questo errore.

### C&#39;erano 0 identità valide nelle prime 100 righe del batch elaborato

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Questo errore viene visualizzato quando le prime 100 righe di un batch non presentavano identità. Questo errore non indica in modo conclusivo che non sono state trovate identità nei record successivi, tuttavia.

### Record ignorati in quanto avevano solo 1 identità per record XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] collega le identità solo quando i singoli record presentano due o più valori di identità. Questo messaggio di errore si verifica una volta per ogni batch acquisito e visualizza il numero di record in cui è stato possibile trovare una sola identità e non sono state apportate modifiche al grafico dell’identità.

### Codice dello spazio dei nomi non registrato per questa organizzazione IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Questo errore viene visualizzato quando un record acquisito presenta un’identità il cui namespace associato non esiste o è inaccessibile dall’organizzazione IMS.

### L’inserimento batch non viene eseguito perché IMS Org non è disponibile per Private Identity Graph

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Quando si acquisiscono dati batch, questo messaggio di errore viene visualizzato quando non è stato eseguito il provisioning dell’organizzazione IMS con le autorizzazioni appropriate per [!DNL Identity Service]. Per risolvere il problema, contatta l’amministratore di sistema.

### Errore interno

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Questo errore viene visualizzato quando si verifica un&#39;eccezione imprevista durante un&#39;acquisizione batch. Si consiglia di programmare le chiamate automatizzate in modo da ripetere le richieste alcune volte a un intervallo di tempo quando viene ricevuto questo errore. Se il problema persiste, contattare l&#39;amministratore di sistema.
