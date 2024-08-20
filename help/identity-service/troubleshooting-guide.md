---
keywords: Experience Platform;home;argomenti popolari;spazio dei nomi identità;spazio dei nomi identità
solution: Experience Platform
title: Guida alla risoluzione dei problemi del servizio Identity
description: Questo documento contiene le risposte alle domande più frequenti sul servizio Adobe Experience Platform Identity e una guida alla risoluzione dei problemi relativi agli errori più comuni.
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '2165'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di Identity Service

Questo documento contiene le risposte alle domande frequenti su Adobe Experience Platform [!DNL Identity Service] e una guida alla risoluzione dei problemi relativi agli errori più comuni. Per domande e risoluzione dei problemi relativi alle API [!DNL Platform] in generale, consulta la [guida alla risoluzione dei problemi API di Adobe Experience Platform](../landing/troubleshooting.md).

I dati che identificano un singolo cliente sono spesso frammentati tra i vari dispositivi e sistemi utilizzati per interagire con il tuo marchio. [!DNL Identity Service] riunisce queste identità frammentate, facilitando una comprensione completa del comportamento del cliente in modo da poter fornire esperienze digitali di impatto in tempo reale. Per ulteriori informazioni, consulta [Panoramica del servizio Identity](./home.md).

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande più frequenti su [!DNL Identity Service].

## Cosa sono i dati di identità?

I dati di identità sono tutti i dati che possono essere utilizzati per identificare una singola persona. A seconda del contesto in cui i dati vengono utilizzati all’interno dell’organizzazione, i dati di identità possono includere nomi utente, indirizzi e-mail e ID dai sistemi di gestione delle relazioni con i clienti. I dati di identità non sono limitati agli utenti registrati del sito web o del servizio, in quanto gli utenti anonimi possono essere identificati anche dal loro ID dispositivo o cookie.

## Qual è il vantaggio di etichettare i campi di dati come identità?

Etichettare alcuni campi di dati come identità nei dati di record e serie temporali consente di mappare le relazioni di identità all’interno della struttura naturale dei dati e riconciliare i dati duplicati tra canali diversi. Per ulteriori informazioni, consulta [Panoramica del servizio Identity](./home.md).

## Cosa sono le identità note e anonime?

Un’identità nota si riferisce a un valore di identità che può essere utilizzato da solo o con altre informazioni per identificare, contattare o individuare una singola persona. Esempi di identità note possono includere indirizzi e-mail, numeri di telefono e CRMID.

Un’identità anonima si riferisce a un valore di identità che non può essere utilizzato da solo o con altre informazioni per identificare, contattare o individuare una singola persona (ad esempio un ID cookie).

## Cos’è un grafico dell’identità privata?

Un grafo di identità privata è una mappa privata delle relazioni tra identità collegate e unite, visibile solo all’organizzazione.

Quando più identità sono incluse in qualsiasi dato acquisito da un endpoint di streaming o inviato a un set di dati abilitato per [!DNL Identity Service], tali identità sono collegate nel grafo delle identità private. [!DNL Identity Service] sfrutta questo grafico per ottenere le identità per un determinato consumatore o entità, consentendo l&#39;unione di identità e profili.

## Come si creano più campi di identità in uno schema XDM?

Gli schemi [Experience Data Model (XDM)](../xdm/home.md) supportano più campi di identità. Qualsiasi campo dati di tipo `string` all&#39;interno di uno schema che implementa la classe XDM Individual Profile o XDM ExperienceEvent può essere etichettato come campo di identità. Una volta etichettati, tutti i dati contenuti in questi campi vengono aggiunti alla mappa di identità del profilo.

Per i passaggi su come etichettare un campo XDM come campo di identità tramite l&#39;interfaccia utente, vedi la [sezione Identità](../xdm/tutorials/create-schema-ui.md) nell&#39;esercitazione dell&#39;Editor di schema. Se utilizzi l&#39;API, consulta la [sezione del descrittore di identità](../xdm/tutorials/create-schema-api.md) nell&#39;esercitazione sull&#39;API del registro degli schemi.

## Esistono contesti in cui alcuni campi non devono essere etichettati come identità?

I campi di identità devono essere riservati a valori univoci per ogni singolo utente. Ad esempio, considera un set di dati per un programma fedeltà dei clienti. Il campo &quot;livello di fedeltà&quot; (oro, argento, bronzo) non sarebbe un campo di identità utile, mentre l’ID di fedeltà (un valore univoco) sarebbe.

Campi come i codici postali e gli indirizzi IP non devono essere etichettati come identità per singoli utenti, in quanto questi valori possono essere applicati a più di una singola persona. Questi tipi di campi dovrebbero essere etichettati solo come identità per le strategie di marketing a livello familiare.

## Perché i campi di identità non collegano come previsto?

Utilizzando l&#39;endpoint [`/cluster/members`](./api/list-cluster-identites.md) nell&#39;API del servizio Identity, è possibile visualizzare le identità associate per uno o più campi di identità. Se la risposta non restituisce le identità collegate previste, assicurati di fornire le informazioni di identità appropriate nei dati XDM. Per ulteriori informazioni, consulta la sezione relativa alla [fornitura di dati XDM al servizio Identity](./home.md) nella panoramica del servizio Identity.

## Che cos’è uno spazio dei nomi delle identità?

Uno spazio dei nomi delle identità fornisce contesto per il modo in cui i campi di identità si relazionano all’identità di un cliente. Ad esempio, i campi di identità nello spazio dei nomi &quot;E-mail&quot; devono essere conformi a un formato e-mail standard (nome<span>@emailprovider.com), mentre i campi che utilizzano lo spazio dei nomi &quot;Telefono&quot; devono essere conformi a un numero di telefono standard (ad esempio 987-555-1234 in Nord America).

Gli spazi dei nomi distinguono valori di identità simili tra sistemi di gestione delle relazioni con i clienti diversi. Ad esempio, considera un profilo che contiene un ID fedeltà numerico associato al programma di premi della tua azienda. Uno spazio dei nomi di &quot;Fedeltà&quot; separerebbe questo valore da un ID numerico simile per il sistema di eCommerce che appare anche nello stesso profilo.

Per ulteriori informazioni, consulta la [panoramica dello spazio dei nomi delle identità](./home.md).

## Come si associa un’identità a uno spazio dei nomi delle identità?

I campi di identità devono essere associati a uno spazio dei nomi di identità esistente al momento della creazione. Qualsiasi nuovo spazio dei nomi deve essere [creato utilizzando l&#39;API](#how-do-i-create-a-custom-namespace-for-my-organization) prima di associarlo ai campi di identità.

Per istruzioni dettagliate sulla definizione di uno spazio dei nomi durante la creazione di un descrittore di identità tramite l&#39;API, consulta la sezione [creazione di un descrittore](../xdm/tutorials/create-schema-ui.md) nella guida per gli sviluppatori del registro dello schema. Per contrassegnare un campo schema come identità nell&#39;interfaccia utente, seguire i passaggi descritti nell&#39;esercitazione [Editor schema](../xdm/tutorials/create-schema-api.md).

## Quali sono gli spazi dei nomi di identità standard forniti da Experience Platform? {#standard-namespaces}

Gli spazi dei nomi di identità standard sono spazi dei nomi disponibili per tutte le organizzazioni. Per un elenco completo degli spazi dei nomi standard disponibili, consulta la [Panoramica sugli spazi dei nomi delle identità](./features/namespaces.md).

## Dove posso trovare l’elenco degli spazi dei nomi di identità disponibili per la mia organizzazione?

Utilizzando l&#39;API [Identity Service](https://www.adobe.io/experience-platform-apis/references/identity-service), puoi elencare tutti gli spazi dei nomi di identità disponibili per la tua organizzazione effettuando una richiesta di GET all&#39;endpoint `/idnamespace/identities`. Per ulteriori informazioni, consulta la sezione su [elenco degli spazi dei nomi disponibili](./api/list-namespaces.md) nella panoramica dell&#39;API del servizio Identity.

## Come si crea uno spazio dei nomi personalizzato per l’organizzazione?

Utilizzando l&#39;API [Identity Service](https://www.adobe.io/experience-platform-apis/references/identity-service), puoi creare uno spazio dei nomi di identità personalizzato per la tua organizzazione effettuando una richiesta POST all&#39;endpoint `/idnamespace/identities`. Per ulteriori informazioni, consulta la sezione sulla [creazione di uno spazio dei nomi personalizzato](./api/create-custom-namespace.md) nella panoramica dell&#39;API del servizio Identity.

## Cosa sono le identità composite e gli XID?

Nelle chiamate API viene fatto riferimento alle identità tramite l’identità composita o XID. Un’identità composita è una rappresentazione di un’identità che contiene un valore ID e uno spazio dei nomi. Un XID è un identificatore a valore singolo che rappresenta lo stesso costrutto di un’identità composita (un ID e uno spazio dei nomi) e viene assegnato automaticamente alle nuove identità quando viene mantenuto da Identity Service. Per ulteriori informazioni, consulta la [Panoramica API del servizio Identity](./home.md).

## In che modo il servizio Identity gestisce le informazioni personali (PII, personally identifiable information)?

Identity Service dispone di spazi dei nomi standard per supportare l’acquisizione di valori di identità con hash per numeri di telefono e e-mail. Tuttavia, sei responsabile dell’hashing dei valori. Per ulteriori informazioni sull&#39;hashing dei dati acquisiti in Platform, consulta la [[!DNL Data Prep] guida alle funzioni di mappatura](../data-prep/functions.md#hashing).

## Ci sono considerazioni quando si esegue l’hashing di identità basate su PII?

Se invii valori PII con hash a Identity Service, devi utilizzare lo stesso metodo di crittografia nei set di dati. In questo modo lo stesso valore di identità in tutti i set di dati genera gli stessi valori con hash e può essere correttamente associato e collegato nel grafico delle identità.

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

## Perché non posso accedere alla pagina o alle API del grafo delle identità?

L&#39;amministratore di Platform deve fornire l&#39;autorizzazione `view-identity-graph` per poter visualizzare i dati del grafico delle identità. Senza questa autorizzazione, riceverai un messaggio di autorizzazione negata nella pagina del visualizzatore del grafico delle identità e quando chiami le API di Platform. Per ulteriori informazioni sulle autorizzazioni, vedere la [panoramica sul controllo degli accessi](../access-control/home.md).

## Risoluzione dei problemi

Nella sezione seguente vengono forniti suggerimenti per la risoluzione dei problemi relativi a codici di errore specifici e a possibili comportamenti imprevisti durante l&#39;utilizzo dell&#39;API [!DNL Identity Service].

## [!DNL Identity Service] messaggi di errore

Di seguito è riportato un elenco di messaggi di errore che è possibile visualizzare quando si utilizza l&#39;API [!DNL Identity Service].

### Parametro di query richiesto mancante

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Questo errore viene visualizzato quando un parametro di query richiesto non è stato incluso nel percorso della richiesta. Il `detail` del messaggio di errore fornisce il nome del parametro mancante. Le varianti di questo messaggio di errore includono:

- Parametro query richiesto mancante - nsId
- Parametro query richiesto mancante - ID
- Parametro query richiesto mancante: xid o (nsid,id)
- Parametro query richiesto mancante - targetNs
- Parametro query richiesto mancante: xids o compositeXids

Prima di riprovare, verifica di includere correttamente il parametro indicato nel percorso della richiesta.

### Il timestamp deve rientrare negli ultimi 180 giorni

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] elimina i dati più vecchi di 180 giorni. Questo messaggio di errore viene visualizzato quando si tenta di accedere a dati precedenti a questo.

### Una singola chiamata ha un limite di 1000 XID

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Questo messaggio di errore viene visualizzato quando si tenta di recuperare informazioni di identità per un numero di [XIDs](#what-are-composite-identities-and-xids) superiore al numero massimo consentito in una singola chiamata API. Per risolvere il problema, riduci il numero di XID nella richiesta a meno del limite visualizzato.


### Una singola chiamata ha un limite di 1000 compositeXids

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Questo messaggio di errore viene visualizzato quando si tenta di recuperare informazioni di identità per un numero di identità composite superiore al numero massimo di [identità composite](#what-are-composite-identities-and-xids) consentito in una singola chiamata API. Per risolvere il problema, riduci il numero di identità composite nella richiesta a meno del limite visualizzato.

### Il tipo di grafico specificato non è valido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Questo messaggio di errore viene visualizzato quando a un parametro di query `graph-type` viene assegnato un valore non valido nel percorso della richiesta. Per informazioni sui tipi di grafo supportati, consulta la sezione sui [grafi di identità](./home.md) nella panoramica di [!DNL Identity Service].

### Il token di servizio non dispone di un ambito valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Questo messaggio di errore viene visualizzato quando all&#39;organizzazione non sono state assegnate le autorizzazioni appropriate per [!DNL Identity Service]. Per risolvere il problema, contatta l’amministratore di sistema.

### Token del servizio gateway non valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

In caso di errore, il token di accesso non è valido. I token di accesso scadono ogni 24 ore e devono essere rigenerati per continuare a utilizzare le API [!DNL Platform]. Per istruzioni sulla generazione di nuovi token di accesso, consulta l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

### Token del servizio di autorizzazione non valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

In caso di errore, il token di accesso non è valido. I token di accesso scadono ogni 24 ore e devono essere rigenerati per continuare a utilizzare le API [!DNL Platform]. Per istruzioni sulla generazione di nuovi token di accesso, consulta l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

### Il token utente non dispone di un contesto di prodotto valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso non è stato generato da un&#39;integrazione [!DNL Experience Platform]. Per istruzioni sulla generazione di nuovi token di accesso per un&#39;integrazione [!DNL Experience Platform], vedere il [tutorial di autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

### Errore interno nell’ottenere XID nativo dal codice di identità e spazio dei nomi

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Quando [!DNL Identity Service] persiste un&#39;identità, all&#39;ID dell&#39;identità e all&#39;ID dello spazio dei nomi associato viene assegnato un identificatore univoco denominato XID. Questo messaggio viene visualizzato quando si verifica un errore durante il processo di ricerca dell’XID per un determinato valore ID e spazio dei nomi.

### Non è stato eseguito il provisioning per l’organizzazione IMS per l’utilizzo [!DNL Identity Service]

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Questo messaggio di errore viene visualizzato quando all&#39;organizzazione non sono state assegnate le autorizzazioni appropriate per [!DNL Identity Service]. Per risolvere il problema, contatta l’amministratore di sistema.

### Errore interno del server

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Questo errore viene visualizzato quando si verifica un&#39;eccezione imprevista nell&#39;esecuzione di una chiamata del servizio [!DNL Platform]. Si consiglia di programmare le chiamate automatizzate in modo da ritentare le richieste più volte a intervalli temporizzati quando si riceve questo errore. Se il problema persiste, contattare l&#39;amministratore di sistema.

## Codici di errore di acquisizione batch

[!DNL Identity Service] acquisisce i dati di identità dai dati di record e serie temporali caricati in [!DNL Platform] mediante acquisizione in batch. Poiché l’acquisizione batch è un processo asincrono, è necessario visualizzare i dettagli di un batch per visualizzare gli errori. Gli errori si accumulano con l’avanzamento del batch fino al suo completamento.

Di seguito è riportato un elenco di messaggi di errore relativi a [!DNL Identity Service] che è possibile incontrare quando si utilizza l&#39;[API di acquisizione batch](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).

### Schema XDM sconosciuto

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] utilizza le identità solo per i dati di record o serie temporali conformi rispettivamente alle classi [!DNL Profile] o [!DNL ExperienceEvent]. Il tentativo di acquisire i dati per [!DNL Identity Service] che non aderisce a nessuna delle due classi attiverà questo errore.

### Nelle prime 100 righe del batch elaborato erano presenti 0 identità valide

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Questo errore viene visualizzato quando le prime 100 righe di un batch non presentano identità. Questo errore non indica in modo conclusivo che non sono state trovate identità nei record successivi, tuttavia.

### Record ignorati perché avevano una sola identità per record XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] collega le identità solo quando singoli record presentano due o più valori di identità. Questo messaggio di errore si verifica una volta per ogni batch acquisito e visualizza il numero di record in cui è stata trovata una sola identità e non ha prodotto alcuna modifica al grafico delle identità.

### Codice dello spazio dei nomi non registrato per questa organizzazione IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Questo errore viene visualizzato quando un record acquisito presenta un’identità il cui spazio dei nomi associato non esiste o è inaccessibile per la tua organizzazione.

### L’acquisizione batch verrà ignorata perché non è stato eseguito il provisioning dell’organizzazione IMS per il grafo delle identità private

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Durante l&#39;acquisizione dei dati batch, questo messaggio di errore viene visualizzato quando all&#39;organizzazione non sono state assegnate le autorizzazioni appropriate per [!DNL Identity Service]. Per risolvere il problema, contatta l’amministratore di sistema.

### Errore interno

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Questo errore viene visualizzato quando si verifica un’eccezione imprevista durante l’acquisizione di un batch. Si consiglia di programmare le chiamate automatizzate in modo da ritentare le richieste più volte a intervalli temporizzati quando si riceve questo errore. Se il problema persiste, contattare l&#39;amministratore di sistema.
