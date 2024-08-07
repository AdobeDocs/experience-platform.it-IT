---
title: Guida alla risoluzione dei problemi dei tag
description: Risposte alle domande più frequenti sui tag in Adobe Experience Platform.
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: 9701a14dc2915e0d6dcc6051c15d5113f305487f
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 78%

---

# Guida alla risoluzione dei problemi dei tag

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](./term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Questo documento contiene le risposte alle domande più frequenti sui tag in Adobe Experience Platform.

## Cosa sono i tag?

I tag sono la nuova generazione di funzionalità di gestione tag fornite da Adobe e sono integrati in Adobe Experience Platform. I tag consentono ai client di:

- distribuire prodotti Web lato client usando integrazioni definite *estensioni*;
- distribuire la configurazione in modo dinamico per aggiornare le implementazioni client nelle applicazioni mobile native;
- acquisire, definire, gestire e condividere in modo coerente i dati tra prodotti marketing e pubblicitari di Adobe e altri fornitori;

I tag costituiscono un sistema avanzato di consegna della configurazione e del codice, in grado di valutare le condizioni ed eseguire azioni per distribuire in modo efficiente ed efficace le librerie e i prodotti lato client. Offrono inoltre un approccio altamente scalabile alla gestione e alla creazione di integrazioni, e dispongono di un solido set di API per l’interazione programmatica.

## Quanto costano i tag?

Non c’è alcun costo aggiuntivo per i tag. Sono disponibili per qualsiasi cliente [!DNL Adobe Experience Cloud].

## Ho saputo che ora sono disponibili plug-in. Cosa significa?

I tag sono incorporati in Adobe Experience Platform e sono completamente estensibili. Clienti, partner di Adobe, agenzie e fornitori di tecnologie marketing e pubblicitarie possono creare un’estensione tag che aggiunge nuove funzionalità o modifica quelle esistenti. Il sistema consente ai partner e ai clienti di creare, gestire e aggiornare le proprie integrazioni. Questo è solo uno dei modi in cui Adobe sta aprendo Adobe Experience Platform per consentire a clienti e partner di creare prodotti e favorire il business. In questo modo tutti hanno la possibilità di collegare con maggiore facilità la tecnologia Adobe alle tecnologie marketing e pubblicitarie di altri fornitori.

## Tutte le estensioni di terze parti saranno immediatamente disponibili?

Le estensioni sono già disponibili per le soluzioni Adobe e per un numero sempre maggiore di fornitori e tecnologie indipendenti di marketing, pubblicità e analisi. Continuiamo a lavorare con i nostri partner per espandere l’ecosistema. Poiché le estensioni possono essere create, gestite e aggiornate dai proprietari di tali tecnologie, i clienti non devono aspettare che vengano sviluppate dagli ingegneri Adobe.

## In che occasioni clienti o partner possono creare estensioni?

I tag sono disponibili tramite un portale self-service, che può essere utilizzato dagli sviluppatori di estensioni per creare le proprie integrazioni con Adobe Cloud Platform.

Anche molti nostri clienti scelgono di creare estensioni private da usare solo all’interno delle proprie aziende utilizzando gli stessi metodi di sviluppo delle estensioni.

Per sviluppare un&#39;estensione, vedi la pagina [Panoramica sullo sviluppo delle estensioni](./extension-dev/overview.md).

## I tag soddisfano gli standard di sicurezza della mia azienda?

I tag sono predisposti per soddisfare SOC-2 e Gramm-Leach-Bliley Act. I tag offrono anche la possibilità di self-hosting. Le librerie JavaScript e le configurazioni mobili possono essere messe a disposizione dai server personali o dal CDN scelto. Per i team di I.T. e di sicurezza, questo offre la possibilità di eseguire test automatizzati, di controllare i file nel sistema di controllo della versione e di rispettare tutti i processi interni di migrazione della produzione, relativamente alla sicurezza o meno.

## Quando posso effettuare il passaggio ai tag?

Ora è il momento migliore per passare ai tag. Il processo di migrazione consente di copiare facilmente le proprietà di DTM nei tag. Abbiamo automatizzato quante più operazioni possibili (non occorre modificare il codice di incorporamento nelle pagine e è stata automatizzata la migrazione di regole ed elementi dati). Tuttavia è consigliabile eseguire test approfonditi.

## I tag supportano le app a pagina singola e il mio framework preferito?

Sì.  I tag offrono funzionalità flessibili che consentono agli utenti e agli sviluppatori di estensioni di raccogliere, gestire e distribuire dati nelle esperienze fornite da applicazioni a pagina singola o da siti o pagine Ajax-heavy. Ciò si applica a prescindere dalle preferenze del framework di sviluppo, Angular, React.js, Ember, Meteor, ecc.

## I tag supportano i livelli di dati dinamici?

Sì.  I tag includono un’estensione specializzata nell’ascolto delle modifiche nei livelli di dati dinamici.

## Quali tipi di evento sono supportati dai tag?

I tipi di evento sono disponibili tramite le estensioni. La quantità di tipi di evento supportati varia in base all’estensione. Ad esempio, l&#39;estensione YouTube include quattro tipi di eventi video: riproduzione, pausa, fine e ora di riproduzione. Mediante le estensioni, i tag possono supportare qualsiasi altro tipo di evento browser o di evento sintetico, ad esempio sequenze specifiche di attività dei visitatori.

## I tag velocizzano (o rallentano) il sito web?

I tag sono progettati per distribuire ed eseguire tecnologie marketing e pubblicitarie sul sito web nel modo più efficiente possibile utilizzando best practice attuali. È stato dimostrato che i tag, utilizzati correttamente, migliorano le prestazioni dei siti web rispetto a metodi alternativi che forniscono funzionalità simili.

## Quali browser supportano i tag?

Vedi i browser supportati [qui](./extension-dev/browsers.md).

La maggior parte dei clienti Adobe sfrutta funzioni di piattaforme web più moderne nei browser attuali e crea esperienze utente migliori, inclusi applicazioni per pagina singola e siti web e pagine interattivi Ajax-heavy. Con sempre più clienti che adottano approcci più moderni per i loro siti, una soluzione come quella offerta dai tag supporta questa tendenza.

## I tag funzionano nelle app mobile native?

Sì! I tag ora supportano proprietà e configurazioni mobili per i nuovi [SDK per dispositivi mobili](https://sdkdocs.com) di Adobe Experience Platform, per implementare la raccolta e la distribuzione dei dati in un ambiente app mobile nativo. Per ulteriori informazioni, consulta la [documentazione](https://sdkdocs.com).

## Perché l’interfaccia utente dice che si è verificato un errore durante il caricamento del mio account?

Se ricevi un messaggio che informa che si è verificato un errore durante il caricamento dell’account, significa che l’account non appartiene ad alcun profilo di prodotto per i tag. Consulta la guida su [gestione delle autorizzazioni](../collection/permissions.md) per scoprire come configurare un profilo di prodotto in Adobe Admin Console per concedere l&#39;accesso alle funzioni di raccolta dati nell&#39;interfaccia utente.

## Perché non posso aggiungere proprietà nell&#39;interfaccia utente?

Se non riesci a creare nuove proprietà quando accedi all’interfaccia utente, significa che il tuo account non appartiene a un profilo di prodotto con l’autorizzazione Gestione proprietà.

Per informazioni su come configurare un profilo di prodotto in Adobe Admin Console per concedere il diritto Manage Properties, consulta la guida su [gestione delle autorizzazioni](../collection/permissions.md). Per ulteriori informazioni sui diversi diritti per i tag, consulta la panoramica sulle [autorizzazioni utente per i tag](./ui/administration/user-permissions.md).

## Cosa succede se ho altre domande?

Se hai altre domande, puoi chiedere nella [pagina della community di Adobe Experience Platform Data Collection](https://adobe.com/go/launchme) su Experience League oppure partecipare all&#39;[area di lavoro di Slack della community](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform) per sviluppatori e argomenti sull&#39;implementazione tecnica.
