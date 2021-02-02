---
keywords: ' Experience Platform;home;argomenti popolari;spazio dei nomi identità;spazio dei nomi identità'
solution: Experience Platform
title: Guida alla risoluzione dei problemi di Adobe Experience Platform Identity Service
topic: troubleshooting
description: Questo documento contiene le risposte alle domande frequenti su Adobe Experience Platform Identity Service e una guida alla risoluzione dei problemi per individuare gli errori più comuni.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '2191'
ht-degree: 0%

---


# Guida alla risoluzione dei problemi del servizio identità

Questo documento contiene le risposte alle domande frequenti su Adobe Experience Platform [!DNL Identity Service] e una guida alla risoluzione dei problemi per individuare gli errori più comuni. Per domande e risoluzione dei problemi relativi alle [!DNL Platform] API in generale, consultare la [Guida alla risoluzione dei problemi delle API di Adobe Experience Platform](../landing/troubleshooting.md).

I dati che identificano un singolo cliente sono spesso frammentati tra i vari dispositivi e sistemi utilizzati per interagire con il tuo marchio. [!DNL Identity Service] riunisce queste identità frammentate, facilitando la comprensione completa del comportamento dei clienti e offrendo esperienze digitali di grande impatto in tempo reale. Per ulteriori informazioni, vedere [Panoramica del servizio identità](./home.md).

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande frequenti su [!DNL Identity Service].

## Che cosa sono i dati di identità?

I dati di identità sono tutti i dati che possono essere utilizzati per identificare una singola persona. A seconda del contesto di utilizzo dei dati all&#39;interno dell&#39;organizzazione, i dati di identità possono includere nomi utente, indirizzi e-mail e ID dai sistemi CRM. I dati di identità non sono limitati agli utenti registrati del sito Web o del servizio, in quanto anche gli utenti anonimi possono essere identificati dal loro dispositivo o ID di cookie.

## Qual è il vantaggio di etichettare i campi di dati come identità?

Etichettare alcuni campi dati come identità nei dati dei record e delle serie temporali consente di mappare le relazioni di identità all&#39;interno della struttura naturale dei dati e di riconciliare i dati duplicati tra canali. Per ulteriori informazioni, vedere [Panoramica del servizio identità](./home.md).

## Cosa sono le identità conosciute e anonime?

Un&#39;identità nota si riferisce a un valore di identità che può essere utilizzato autonomamente o con altre informazioni per identificare, contattare o individuare una singola persona. Esempi di identità note possono includere indirizzi e-mail, numeri di telefono e ID CRM.

Un&#39;identità anonima si riferisce a un valore di identità che non può essere utilizzato da sola o con altre informazioni per identificare, contattare o individuare una singola persona (ad esempio un ID di cookie).

## Cos&#39;è un grafico di identità privata?

Un grafico di identità privata è una mappa privata delle relazioni tra identità collegate e unite, visibile solo all’organizzazione.

Quando più identità sono incluse in tutti i dati acquisiti da un endpoint di streaming o inviati a un set di dati abilitato per [!DNL Identity Service], tali identità sono collegate in Private Identity Graph. [!DNL Identity Service] sfrutta questo grafico per cogliere le identità di un determinato consumatore o entità, consentendo l&#39;unione di identità e profilo.

## Come si creano più campi di identità all&#39;interno di uno schema XDM?

[Gli ](../xdm/home.md) schemi XDM (Experience Data Model) supportano più campi di identità. Qualsiasi campo di dati di tipo `string` all&#39;interno di uno schema che implementa la classe XDM Singolo profilo o XDM ExperienceEvent può essere etichettato come campo di identità. Una volta etichettati, tutti i dati contenuti in questi campi vengono aggiunti alla mappa di identità del profilo.

Per i passaggi su come etichettare un campo XDM come campo di identità utilizzando l&#39;interfaccia utente, vedere la sezione [Identità](../xdm/tutorials/create-schema-ui.md) nell&#39;esercitazione dell&#39;Editor di schema. Se si utilizza l&#39;API, vedere la sezione [descrittore di identità](../xdm/tutorials/create-schema-api.md) nell&#39;esercitazione API del Registro di sistema dello schema.

## Esistono contesti in cui alcuni campi non devono essere etichettati come identità?

I campi di identità devono essere riservati ai valori univoci per ogni singolo utente. Ad esempio, prendere in considerazione un dataset per un programma di fidelizzazione dei clienti. Il campo &quot;livello di fedeltà&quot; (oro, argento, bronzo) non sarebbe un campo di identità utile, mentre l&#39;ID fedeltà, un valore unico, sarebbe.

Campi come codici ZIP e indirizzi IP non devono essere etichettati come identità per singoli utenti, in quanto questi valori possono essere applicati a più persone. Questi tipi di campi devono essere etichettati solo come identità per le strategie di marketing a livello domestico.

## Perché i miei campi di identità non collegano come mi aspetto?

Utilizzando l&#39;endpoint [`/cluster/members`](./api/list-cluster-identites.md) nell&#39;API del servizio identità, potete visualizzare le identità associate per uno o più campi di identità. Se la risposta non restituisce le identità collegate attese, assicurarsi di fornire le informazioni di identità appropriate nei dati XDM. Per ulteriori informazioni, vedere la sezione relativa alla [fornitura di dati XDM a Servizio identità](./home.md) nella panoramica del servizio identità.

## Che cos&#39;è uno spazio nomi identità?

Uno spazio dei nomi di identità fornisce un contesto in cui i campi di identità si riferiscono all&#39;identità di un cliente. Ad esempio, i campi di identità nello spazio dei nomi &quot;E-mail&quot; devono essere conformi a un formato e-mail standard (nome<span>@emailprovider.com), mentre i campi che utilizzano lo spazio dei nomi &quot;Phone&quot; devono essere conformi a un numero di telefono standard (ad esempio 987-555-1234 in Nord America).

Gli spazi dei nomi distinguono valori di identità simili tra i diversi sistemi CRM. Ad esempio, prendete in considerazione un profilo che contiene un ID fedeltà numerico associato al programma di premi della società. Uno spazio dei nomi di &quot;Fedeltà&quot; separerebbe questo valore da un ID numerico simile per il sistema eCommerce che appare anche nello stesso profilo.

Per ulteriori informazioni, vedere [panoramica dello spazio dei nomi identità](./home.md).

## Come si collega un&#39;identità a uno spazio nomi identità?

I campi identità devono essere associati a uno spazio nomi identità esistente al momento della creazione. Eventuali nuovi spazi dei nomi devono essere [creati utilizzando l&#39;API](#how-do-i-create-a-custom-namespace-for-my-organization) prima di associarli ai campi di identità.

Per istruzioni dettagliate sulla definizione di uno spazio nomi durante la creazione di un descrittore di identità tramite l&#39;API, consultare la sezione relativa alla creazione di un descrittore](../xdm/tutorials/create-schema-ui.md) nella guida per gli sviluppatori del Registro di sistema dello schema. [ Per contrassegnare un campo di schema come identità nell&#39;interfaccia utente, seguire i passaggi descritti nell&#39;esercitazione [Editor di schema](../xdm/tutorials/create-schema-api.md).

## Quali sono gli spazi dei nomi di identità standard forniti dal Experience Platform ? {#standard-namespaces}

Gli spazi dei nomi delle identità standard sono spazi dei nomi disponibili per tutte le organizzazioni. Per un elenco completo degli spazi dei nomi standard disponibili, vedere la [Panoramica sugli spazi dei nomi delle identità](./namespaces.md).

## Dove è possibile trovare l&#39;elenco di spazi dei nomi identità disponibili per la mia organizzazione?

Utilizzando l&#39; [API del servizio identità](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml), puoi elencare tutti gli spazi dei nomi identità disponibili per la tua organizzazione effettuando una richiesta di GET all&#39;endpoint `/idnamespace/identities`. Per ulteriori informazioni, vedere la sezione sull&#39; [elencazione di namespace disponibili](./api/list-namespaces.md) nella panoramica API del servizio identità.

## Come si crea uno spazio nomi personalizzato per la propria organizzazione?

Utilizzando l&#39; [API del servizio identità](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml), è possibile creare uno spazio nomi identità personalizzato per la propria organizzazione effettuando una richiesta di POST all&#39;endpoint `/idnamespace/identities`. Per ulteriori informazioni, vedere la sezione relativa alla creazione di uno spazio dei nomi personalizzato](./api/create-custom-namespace.md) nella panoramica API del servizio identità.[

## Cosa sono le identità composite e gli XID?

Alle identità viene fatto riferimento nelle chiamate API tramite la loro identità composita o XID. Un&#39;identità composita è una rappresentazione di un&#39;identità che contiene un valore ID e uno spazio dei nomi. Un XID è un identificatore a valore singolo che rappresenta lo stesso costrutto di un&#39;identità composita (un ID e uno spazio dei nomi) e viene assegnato automaticamente alle nuove identità se persistente da Servizio identità. Per ulteriori informazioni, consultare la [panoramica API Servizio identità](./home.md).

## In che modo Identity Service gestisce le informazioni personali (PII)?

Il servizio identità crea un hash di crittografia univoca dei dati PII prima dei valori persistenti. I dati di identità negli spazi dei nomi &quot;Phone&quot; e &quot;Email&quot; vengono automaticamente crittografati con SHA-256, con i valori &quot;Email&quot; automaticamente convertiti in lettere minuscole prima dell&#39;hashing.

## Devo crittografare tutti i dati PII prima di inviarli alla piattaforma?

Non è necessario crittografare manualmente i dati PII prima di assimilarli nella piattaforma. Applicando l&#39;etichetta di utilizzo dei dati `I1` a tutti i campi di dati applicabili, Platform converte automaticamente questi campi in valori ID con hash al momento dell&#39;inserimento.

Per istruzioni su come applicare e gestire le etichette di utilizzo dei dati, vedere l&#39;esercitazione sulle etichette di utilizzo dei dati [tutorial](../data-governance/labels/user-guide.md).

## Ci sono delle considerazioni quando si hashing delle identità basate su PII?

Se si inviano valori PII con hash al servizio identità, è necessario utilizzare lo stesso metodo di crittografia per tutti i set di dati. In questo modo lo stesso valore di identità nei set di dati genera gli stessi valori con hash e può essere confrontato e collegato correttamente nel grafico dell&#39;identità.

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

## Risoluzione dei problemi

La sezione seguente contiene suggerimenti per la risoluzione dei problemi relativi a codici di errore specifici e a comportamenti imprevisti che potrebbero verificarsi durante l&#39;utilizzo dell&#39;API [!DNL Identity Service].

## [!DNL Identity Service] messaggi di errore

Di seguito è riportato un elenco di messaggi di errore che potrebbero verificarsi durante l&#39;utilizzo dell&#39;API [!DNL Identity Service].

### Parametro di query obbligatorio mancante

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Questo errore viene visualizzato quando un parametro di query richiesto non è stato incluso nel percorso della richiesta. Il `detail` del messaggio di errore fornisce il nome del parametro mancante. Le varianti di questo messaggio di errore includono:

- Parametro query obbligatorio mancante - nsId
- Parametro query richiesto mancante - id
- Parametro query richiesto mancante - xid o (nsid,id)
- Parametro query obbligatorio mancante - targetNs
- Parametro query obbligatorio mancante - xids o compositeXids

Prima di riprovare, verificate di aver incluso correttamente il parametro indicato nel percorso della richiesta.

### La marca temporale deve essere compresa negli ultimi 180 giorni

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] elimina i dati di età superiore a 180 giorni. Questo messaggio di errore viene visualizzato quando si tenta di accedere a dati più vecchi di questo.

### Esiste un limite di 1000 XIDs in una singola chiamata

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Questo messaggio di errore viene visualizzato quando tentate di recuperare informazioni di identità per un numero superiore al massimo di [XIDs](#what-are-composite-identities-and-xids) consentiti in una singola chiamata API. Ridurre il numero di XID nella richiesta al di sotto del limite visualizzato per risolvere il problema.


### Esiste un limite per 1000 compositeXids in una singola chiamata

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Questo messaggio di errore viene visualizzato quando tentate di recuperare informazioni di identità per un numero superiore al massimo di [identità composite](#what-are-composite-identities-and-xids) consentiti in una singola chiamata API. Riducete il numero di identità composite nella richiesta al di sotto del limite visualizzato per risolvere il problema.

### Il tipo di grafico specificato non è valido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Questo messaggio di errore viene visualizzato quando a un parametro di query `graph-type` viene assegnato un valore non valido nel percorso della richiesta. Per informazioni sui tipi di grafico supportati, vedere la sezione relativa ai [grafici identità](./home.md) nella [!DNL Identity Service] panoramica.

### Il token di servizio non dispone di un ambito valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Questo messaggio di errore viene visualizzato quando l&#39;organizzazione IMS non dispone delle autorizzazioni necessarie per [!DNL Identity Service]. Per risolvere il problema, contattate l’amministratore di sistema.

### Token del servizio gateway non valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

In caso di errore, il token di accesso non è valido. I token di accesso scadono ogni 24 ore e devono essere rigenerati per continuare a utilizzare le [!DNL Platform] API. Per istruzioni su come generare nuovi token di accesso, vedere l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

### Token del servizio di autorizzazione non valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

In caso di errore, il token di accesso non è valido. I token di accesso scadono ogni 24 ore e devono essere rigenerati per continuare a utilizzare le [!DNL Platform] API. Per istruzioni su come generare nuovi token di accesso, vedere l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

### Il token utente non dispone di contesto prodotto valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso non è stato generato da un&#39;integrazione [!DNL Experience Platform]. Per istruzioni su come generare nuovi token di accesso per un&#39;integrazione [!DNL Experience Platform], vedere l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

### Errore interno durante il recupero di XID nativo dal codice identità e spazio dei nomi

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Quando [!DNL Identity Service] persiste un&#39;identità, all&#39;ID dell&#39;identità e all&#39;ID dello spazio dei nomi associato viene assegnato un identificatore univoco denominato XID. Questo messaggio viene visualizzato quando si verifica un errore durante il processo di ricerca dell&#39;XID per un determinato valore ID e spazio dei nomi.

### L&#39;organizzazione IMS non è predisposta per l&#39;utilizzo di [!DNL Identity Service]

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Questo messaggio di errore viene visualizzato quando l&#39;organizzazione IMS non dispone delle autorizzazioni necessarie per [!DNL Identity Service]. Per risolvere il problema, contattate l’amministratore di sistema.

### Errore interno del server

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Questo errore viene visualizzato quando si verifica un&#39;eccezione imprevista nell&#39;esecuzione di una chiamata di servizio [!DNL Platform]. La procedura consigliata consiste nel programmare le chiamate automatizzate in modo che ritentino le richieste alcune volte a un intervallo di tempo al momento della ricezione dell&#39;errore. Se il problema persiste, contattare l&#39;amministratore di sistema.

## Codici di errore di inserimento batch

[!DNL Identity Service] acquisisce i dati di identità dai dati di record e serie temporali caricati  [!DNL Platform] utilizzando l&#39;inserimento batch. Poiché l’assimilazione batch è un processo asincrono, è necessario visualizzare i dettagli di un batch per visualizzare gli errori. Gli errori si accumulano man mano che il batch avanza fino al completamento del batch.

Di seguito è riportato un elenco di messaggi di errore relativi a [!DNL Identity Service] che si possono incontrare quando si utilizza l&#39;API [Data Ingestion](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

### Schema XDM sconosciuto

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] utilizza solo le identità per i dati di record o serie temporali conformi rispettivamente alle  [!DNL Profile] classi o alle  [!DNL ExperienceEvent] classi. Il tentativo di assimilare i dati per [!DNL Identity Service] che non aderiscono a nessuna delle due classi causerà l&#39;errore.

### 0 identità valide nelle prime 100 righe del batch elaborato

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Questo errore viene visualizzato quando le prime 100 righe di un batch non presentavano identità. Questo errore non indica in modo conclusivo che non sono state trovate identità nei record successivi.

### Record ignorati poiché avevano solo 1 identità per record XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] collega solo le identità quando i singoli record presentano due o più valori di identità. Questo messaggio di errore si verifica una volta per ciascun batch acquisito e visualizza il numero di record in cui è stata trovata una sola identità e non sono state apportate modifiche al grafico dell&#39;identità.

### Il codice dello spazio dei nomi non è registrato per questa organizzazione IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Questo errore viene visualizzato quando un record acquisito presenta un&#39;identità il cui spazio nomi associato non esiste o non è accessibile dall&#39;organizzazione IMS.

### L&#39;assimilazione batch come organizzazione IMS non è stata fornita per il grafico dell&#39;identità privata

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Durante l&#39;assimilazione dei dati batch, questo messaggio di errore viene visualizzato quando l&#39;organizzazione IMS non dispone delle autorizzazioni necessarie per [!DNL Identity Service]. Per risolvere il problema, contattate l’amministratore di sistema.

### Errore interno

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Questo errore viene visualizzato quando si verifica un&#39;eccezione imprevista durante l&#39;assimilazione di un batch. La procedura consigliata consiste nel programmare le chiamate automatizzate in modo che ritentino le richieste alcune volte a un intervallo di tempo al momento della ricezione dell&#39;errore. Se il problema persiste, contattare l&#39;amministratore di sistema.
