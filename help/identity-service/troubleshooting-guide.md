---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida alla risoluzione dei problemi per  Adobe Experience Platform Identity Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2225'
ht-degree: 1%

---


# Guida alla risoluzione dei problemi del servizio identità

Questo documento contiene le risposte alle domande frequenti sul  Adobe Experience Platform [!DNL Identity Service], nonché una guida per la risoluzione dei problemi relativi agli errori più comuni. Per domande e risoluzione dei problemi relativi alle [!DNL Platform] API in generale, consultate la guida alla risoluzione dei problemi delle API di [Adobe Experience Platform](../landing/troubleshooting.md).

I dati che identificano un singolo cliente sono spesso frammentati tra i vari dispositivi e sistemi utilizzati per interagire con il tuo marchio. [!DNL Identity Service] riunisce queste identità frammentate, facilitando la comprensione completa del comportamento dei clienti e offrendo esperienze digitali di grande impatto in tempo reale. Per ulteriori informazioni, consultate la panoramica [del servizio](./home.md)identità.

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande frequenti su [!DNL Identity Service].

## Che cosa sono i dati di identità?

I dati di identità sono tutti i dati che possono essere utilizzati per identificare una singola persona. A seconda del contesto di utilizzo dei dati all&#39;interno dell&#39;organizzazione, i dati di identità possono includere nomi utente, indirizzi e-mail e ID dai sistemi CRM. I dati di identità non sono limitati agli utenti registrati del sito Web o del servizio, in quanto anche gli utenti anonimi possono essere identificati dal loro dispositivo o ID di cookie.

## Qual è il vantaggio di etichettare i campi di dati come identità?

Etichettare alcuni campi dati come identità nei dati dei record e delle serie temporali consente di mappare le relazioni di identità all&#39;interno della struttura naturale dei dati e di riconciliare i dati duplicati tra canali. Per ulteriori informazioni, consulta la panoramica [del servizio](./home.md) identità.

## Cosa sono le identità conosciute e anonime?

Un&#39;identità nota si riferisce a un valore di identità che può essere utilizzato autonomamente o con altre informazioni per identificare, contattare o individuare una singola persona. Esempi di identità note possono includere indirizzi e-mail, numeri di telefono e ID CRM.

Un&#39;identità anonima si riferisce a un valore di identità che non può essere utilizzato da sola o con altre informazioni per identificare, contattare o individuare una singola persona (ad esempio un ID di cookie).

## Cos&#39;è un grafico di identità privata?

Un grafico di identità privata è una mappa privata delle relazioni tra identità collegate e unite, visibile solo all’organizzazione.

Quando più identità sono incluse in tutti i dati acquisiti da un endpoint di streaming o inviati a un set di dati abilitato per [!DNL Identity Service], tali identità sono collegate in Private Identity Graph. [!DNL Identity Service] sfrutta questo grafico per cogliere le identità di un determinato consumatore o entità, consentendo l&#39;unione di identità e profilo.

## Come si creano più campi di identità all&#39;interno di uno schema XDM?

[Gli schemi XDM (Experience Data Model)](../xdm/home.md) supportano più campi di identità. Qualsiasi campo di dati di tipo `string` all&#39;interno di uno schema che implementa la classe XDM Singolo profilo o XDM ExperienceEvent può essere etichettato come campo di identità. Una volta etichettati, tutti i dati contenuti in questi campi vengono aggiunti alla mappa di identità del profilo.

Per i passaggi su come etichettare un campo XDM come campo di identità utilizzando l&#39;interfaccia utente, vedere la sezione [](../xdm/tutorials/create-schema-ui.md) Identità nell&#39;esercitazione Editor di schema. Se utilizzate l&#39;API, consultate la sezione [descrittore di](../xdm/tutorials/create-schema-api.md) identità nell&#39;esercitazione API del Registro di sistema dello schema.

## Esistono contesti in cui alcuni campi non devono essere etichettati come identità?

I campi di identità devono essere riservati ai valori univoci per ogni singolo utente. Ad esempio, prendere in considerazione un dataset per un programma di fidelizzazione dei clienti. Il campo &quot;livello di fedeltà&quot; (oro, argento, bronzo) non sarebbe un campo di identità utile, mentre l&#39;ID fedeltà, un valore unico, sarebbe.

Campi come codici ZIP e indirizzi IP non devono essere etichettati come identità per singoli utenti, in quanto questi valori possono essere applicati a più persone. Questi tipi di campi devono essere etichettati solo come identità per le strategie di marketing a livello domestico.

## Perché i miei campi di identità non collegano come mi aspetto?

Utilizzando l&#39; [`/cluster/members` endpoint](./api/list-cluster-identites.md) nell&#39;API del servizio identità, potete visualizzare le identità associate per uno o più campi di identità. Se la risposta non restituisce le identità collegate attese, assicurarsi di fornire le informazioni di identità appropriate nei dati XDM. Per ulteriori informazioni, vedere la sezione relativa alla [fornitura di dati XDM al servizio](./home.md) identità nella panoramica del servizio identità.

## Che cos&#39;è uno spazio nomi identità?

Uno spazio dei nomi di identità fornisce un contesto in cui i campi di identità si riferiscono all&#39;identità di un cliente. Ad esempio, i campi di identità nello spazio dei nomi &quot;E-mail&quot; devono essere conformi a un formato e-mail standard (nome<span>@emailprovider.com), mentre i campi che utilizzano lo spazio dei nomi &quot;Phone&quot; devono essere conformi a un numero di telefono standard (ad esempio 987-555-1234 in Nord America).

Gli spazi dei nomi distinguono valori di identità simili tra i diversi sistemi CRM. Ad esempio, prendete in considerazione un profilo che contiene un ID fedeltà numerico associato al programma di premi della società. Uno spazio dei nomi di &quot;Fedeltà&quot; separerebbe questo valore da un ID numerico simile per il sistema eCommerce che appare anche nello stesso profilo.

Per ulteriori informazioni, vedere la panoramica [dello spazio dei nomi](./home.md) identità.

## Come si collega un&#39;identità a uno spazio nomi identità?

I campi identità devono essere associati a uno spazio nomi identità esistente al momento della creazione. Eventuali nuovi spazi dei nomi devono essere [creati mediante l&#39;API](#how-do-i-create-a-custom-namespace-for-my-organization) prima di associarli ai campi di identità.

Per istruzioni dettagliate sulla definizione di uno spazio nomi durante la creazione di un descrittore di identità tramite l&#39;API, vedere la sezione sulla [creazione di un descrittore](../xdm/tutorials/create-schema-ui.md) nella guida per gli sviluppatori del Registro di sistema dello schema. Per contrassegnare un campo di schema come identità nell&#39;interfaccia utente, seguire i passaggi dell&#39;esercitazione [Editor di](../xdm/tutorials/create-schema-api.md)schema.

## Quali sono gli spazi dei nomi di identità standard forniti dal Experience Platform ?

I seguenti spazi dei nomi standard sono forniti per l&#39;uso da parte di tutte le organizzazioni all&#39;interno  Experience Platform:

| Nome visualizzato | ID | Codice | Descrizione |
| ------------ | --- | --- | ----------- |
| CORE | 0 | CORE | nome legacy: &quot; Adobe AudienceManager&quot; |
| ECID | 4 | ECID | alias: &quot; ID Adobe Marketing Cloud&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot; ID Adobe Experience Platform&quot; |
| E-mail | 6 | E-mail |  |
| E-mail (SHA256, minuscola) | 11 | E-mail | Spazio dei nomi standard per le e-mail con hash precedente. I valori forniti in questo spazio nomi vengono convertiti in lettere minuscole prima di eseguire l&#39;hash con SHA-256. |
| Telefono | 7 | Telefono |  |
| Windows AID | 8 | WAID |  |
| AdCloud | 411 | AdCloud | alias:  Ad Cloud |
| Adobe Target | 9 | TNTID | ID Target |
| Google Ad ID | 20914 | GAID | GAID |
| Apple IDFA | 20915 | IDFA | ID per inserzionisti |

## Dove è possibile trovare l&#39;elenco di spazi dei nomi identità disponibili per la mia organizzazione?

Utilizzando l&#39;API [Servizio](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)identità potete elencare tutti gli spazi dei nomi identità disponibili per la vostra organizzazione effettuando una richiesta di GET all&#39; `/idnamespace/identities` endpoint. Per ulteriori informazioni, consulta la sezione sull’ [elenco degli spazi dei nomi](./api/list-namespaces.md) disponibili nella panoramica API del servizio identità.

## Come si crea uno spazio nomi personalizzato per la propria organizzazione?

Utilizzando l&#39;API [Servizio](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)identità potete creare uno spazio nomi identità personalizzato per la vostra organizzazione effettuando una richiesta di POST all&#39; `/idnamespace/identities` endpoint. Per ulteriori informazioni, consulta la sezione sulla [creazione di uno spazio dei nomi](./api/create-custom-namespace.md) personalizzato nella panoramica API del servizio identità.

## Cosa sono le identità composite e gli XID?

Alle identità viene fatto riferimento nelle chiamate API tramite la loro identità composita o XID. Un&#39;identità **** composita è una rappresentazione di un&#39;identità che contiene un valore ID e uno spazio dei nomi. Un **XID** è un identificatore a valore singolo che rappresenta lo stesso costrutto di un&#39;identità composita (un ID e uno spazio dei nomi) e viene automaticamente assegnato alle nuove identità se persistente da Identity Service. Per ulteriori informazioni, consulta la panoramica [API del servizio](./home.md) identità.

## In che modo Identity Service gestisce le informazioni personali (PII)?

Il servizio identità crea un hash di crittografia univoca dei dati PII prima dei valori persistenti. I dati di identità negli spazi dei nomi &quot;Phone&quot; e &quot;Email&quot; vengono automaticamente crittografati con SHA-256, con i valori &quot;Email&quot; automaticamente convertiti in lettere minuscole prima dell&#39;hashing.

## Devo crittografare tutti i dati PII prima di inviarli ad Platform?

Non è necessario crittografare manualmente i dati PII prima di assimilarli in Platform. Applicando l&#39;etichetta di utilizzo dei `I1` dati a tutti i campi di dati applicabili, Platform converte automaticamente questi campi in valori ID con hash al momento dell&#39;assimilazione.

Per i passaggi relativi all&#39;applicazione e alla gestione delle etichette di utilizzo dei dati, vedere l&#39;esercitazione [sulle etichette di uso](../data-governance/labels/user-guide.md)dei dati.

## Ci sono delle considerazioni quando si hashing delle identità basate su PII?

Se si inviano valori PII con hash a Servizio identità, è necessario utilizzare lo stesso metodo di crittografia per tutti i set di dati. In questo modo lo stesso valore di identità nei set di dati genera gli stessi valori con hash e può essere confrontato e collegato correttamente nel grafico dell&#39;identità.

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

La sezione seguente contiene suggerimenti per la risoluzione dei problemi relativi a codici di errore specifici e a comportamenti imprevisti che potrebbero verificarsi durante l&#39;utilizzo dell&#39; [!DNL Identity Service] API.

## [!DNL Identity Service] messaggi di errore

Di seguito è riportato un elenco di messaggi di errore che potrebbero verificarsi durante l&#39;utilizzo dell&#39; [!DNL Identity Service] API.

### Parametro di query obbligatorio mancante

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Questo errore viene visualizzato quando un parametro di query richiesto non è stato incluso nel percorso della richiesta. Il nome `detail` del messaggio di errore fornisce il nome del parametro mancante. Le varianti di questo messaggio di errore includono:

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

Questo messaggio di errore viene visualizzato quando tentate di recuperare informazioni di identità per un numero superiore al massimo di [XID](#what-are-composite-identities-and-xids) consentiti in una singola chiamata API. Ridurre il numero di XID nella richiesta al di sotto del limite visualizzato per risolvere il problema.


### Esiste un limite per 1000 compositeXids in una singola chiamata

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Questo messaggio di errore viene visualizzato quando tentate di recuperare informazioni di identità per più del numero massimo di identità [](#what-are-composite-identities-and-xids) composite consentito in una singola chiamata API. Riducete il numero di identità composite nella richiesta al di sotto del limite visualizzato per risolvere il problema.

### Il tipo di grafico specificato non è valido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Questo messaggio di errore viene visualizzato quando a un parametro di `graph-type` query viene assegnato un valore non valido nel percorso della richiesta. Consultate la sezione sui grafici [di](./home.md) identità nella [!DNL Identity Service] panoramica per scoprire quali tipi di grafico sono supportati.

### Il token di servizio non dispone di un ambito valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Questo messaggio di errore viene visualizzato quando non è stato eseguito il provisioning dell&#39;organizzazione IMS con le autorizzazioni appropriate per [!DNL Identity Service]. Per risolvere il problema, contattate l’amministratore di sistema.

### Token del servizio gateway non valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

In caso di errore, il token di accesso non è valido. I token di accesso scadono ogni 24 ore e devono essere rigenerati per continuare a utilizzare [!DNL Platform] le API. Per istruzioni sulla generazione di nuovi token di accesso, consulta l’esercitazione [](../tutorials/authentication.md) sull’autenticazione.

### Token del servizio di autorizzazione non valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

In caso di errore, il token di accesso non è valido. I token di accesso scadono ogni 24 ore e devono essere rigenerati per continuare a utilizzare [!DNL Platform] le API. Per istruzioni sulla generazione di nuovi token di accesso, consulta l’esercitazione [](../tutorials/authentication.md) sull’autenticazione.

### Il token utente non dispone di contesto prodotto valido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Questo messaggio di errore viene visualizzato quando il token di accesso non è stato generato da un&#39; [!DNL Experience Platform] integrazione. Per istruzioni su come generare nuovi token di accesso per un’ [integrazione, consultate l’esercitazione](../tutorials/authentication.md) sull’ [!DNL Experience Platform] autenticazione.

### Errore interno durante il recupero di XID nativo dal codice identità e spazio dei nomi

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Quando [!DNL Identity Service] persiste un&#39;identità, all&#39;ID dell&#39;identità e all&#39;ID dello spazio nomi associato viene assegnato un identificatore univoco denominato XID. Questo messaggio viene visualizzato quando si verifica un errore durante il processo di ricerca dell&#39;XID per un determinato valore ID e spazio dei nomi.

### Organizzazione IMS non fornita per [!DNL Identity Service] l&#39;utilizzo

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Questo messaggio di errore viene visualizzato quando non è stato eseguito il provisioning dell&#39;organizzazione IMS con le autorizzazioni appropriate per [!DNL Identity Service]. Per risolvere il problema, contattate l’amministratore di sistema.

### Errore interno del server

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Questo errore viene visualizzato quando si verifica un&#39;eccezione imprevista nell&#39;esecuzione di una chiamata di [!DNL Platform] servizio. La procedura consigliata consiste nel programmare le chiamate automatizzate in modo che ritentino le richieste alcune volte a un intervallo di tempo al momento della ricezione dell&#39;errore. Se il problema persiste, contattare l&#39;amministratore di sistema.

## Codici di errore di inserimento batch

[!DNL Identity Service] acquisisce i dati di identità dai dati di record e serie temporali caricati [!DNL Platform] utilizzando l&#39;inserimento batch. Poiché l’assimilazione batch è un processo asincrono, è necessario visualizzare i dettagli di un batch per visualizzare gli errori. Gli errori si accumulano man mano che il batch avanza fino al completamento del batch.

Di seguito è riportato un elenco di messaggi di errore correlati ai [!DNL Identity Service] quali potresti trovarti quando utilizzi l&#39;API [di](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)inserimento dati.

### Schema XDM sconosciuto

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] utilizza solo le identità per i dati di record o serie temporali conformi rispettivamente alle [!DNL Profile] classi o alle [!DNL ExperienceEvent] classi. Se si tenta di acquisire dati per [!DNL Identity Service] le quali non è conforme a una delle due classi, l&#39;errore viene generato.

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
