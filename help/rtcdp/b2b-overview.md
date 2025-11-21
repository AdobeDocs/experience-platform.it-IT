---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp;Customer AI
title: Panoramica di Real-Time CDP B2B edition
description: Panoramica dell’account Real-time Customer Data Platform B2B Edition
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 4%

---

# Panoramica di Real-Time Customer Data Platform B2B edition

Basato su Adobe Real-Time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B edition è progettato appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono ai marketer di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.

Sono state migliorate diverse funzionalità di Adobe Experience Platform che distinguono Real-Time CDP B2B edition dalla controparte B2C. Includono miglioramenti all&#39;Experience Data Model (XDM) per i casi d&#39;uso B2B, aggiornamenti alla risoluzione delle identità e alla segmentazione del profilo, nonché un connettore e una destinazione personalizzati per [!DNL Marketo Engage]. Il connettore [!DNL Marketo] consente ai brand B2B di collegare i dati di coinvolgimento B2B leader del settore con informazioni comportamentali per sviluppare lead e migliorare le operazioni di marketing basate sull&#39;account.

Con Real-Time CDP B2B edition è possibile:

* Combina dati raccolti da più origini in un’unica vista per creare profili olistici di persone e account.
* Arricchisci, segmenta ed esporta tutti i dati provenienti da più origini da un archivio centralizzato di profili di account unificati.
* Gestisci i tuoi dati utilizzando gli strumenti di governance dei dati disponibili in ogni fase del processo di centralizzazione per garantire la conformità dei tuoi dati alle normative e alle politiche aziendali.

Di seguito sono riportate informazioni più complete sui miglioramenti apportati a Real-Time CDP B2B edition.

## XDM

Real-Time CDP B2B edition fornisce diverse nuove classi di schema XDM, gruppi di campi e tipi di relazione per acquisire e strutturare i dati in modo specifico per scopi B2B. Per informazioni dettagliate su ciascuno di questi miglioramenti, consulta la panoramica su [XDM in Real-Time CDP B2B edition](./schemas/b2b.md).

Utilizzando schemi B2B preconfigurati, puoi inserire i dati in una struttura standardizzata e actionable. Molte delle nuove classi di schema vengono mappate quasi direttamente a quelle incontrate nei sistemi di gestione delle relazioni con i clienti principali come [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] e altre origini dati B2B. Con Real-Time CDP B2B edition, puoi inserire in Experience Platform i dati provenienti da origini B2B in modo semplice e con risultati facili da controllare.

Questi miglioramenti XDM consentono di acquisire e attivare meglio i dati tramite origini e destinazioni incentrate sul B2B, migliorando l’unificazione e la presentazione dei dati per casi d’uso più vari e flessibili.

## Risoluzione identità

Dopo aver definito gli schemi e acquisito i dati in conformità a tali schemi, Real-Time CDP B2B edition identifica i record di origine che rappresentano persone e aziende del mondo reale attraverso un potente sistema di risoluzione delle identità in tempo reale.

Il sistema di risoluzione delle identità offre le seguenti funzionalità:

* Record di persone B2B e B2C combinati
* Gerarchia di account a più livelli
* Connessioni molti-a-molti, persone-account
* Le persone e le identità dell’account vengono risolte in tempo reale

Il sistema di risoluzione delle identità è stato ampliato per supportare una classificazione più sfaccettata delle persone. Il sistema consente di identificare le persone come lead nelle opportunità di business, oltre che nei clienti.

I record account sincronizzati dal sistema CRM di origine e connessi tramite più percorsi all’interno del sistema vengono uniti tra loro da Experience Platform. Il sistema riunisce le persone associate alle opportunità commerciali e quelle registrate come clienti, ma è anche in grado di mantenere la distinzione tra loro come attributo se sono identificabili.

Gli identificativi corrispondenti vengono utilizzati per collegare e unire i record account da più sistemi. Le gerarchie di conti vengono mantenute durante questo processo. I differenziatori vengono utilizzati per verificare se una persona è associata o meno a un account e fornire la possibilità di separarli dall’account, se necessario.

## Profili e segmentazione

Una volta che Real-Time CDP B2B edition ha acquisito i dati e risolto le identità relative a persone, aziende, attributi e comportamenti, tali dati vengono utilizzati per creare i profili. Questi profili possono quindi essere segmentati in tipi di pubblico visualizzabili che possono quindi essere attivati in varie destinazioni.

Se implementato correttamente, il sistema tiene traccia delle persone utilizzando identificatori primari univoci anziché attributi che possono essere modificati, come ad esempio gli indirizzi e-mail. Ciò significa che quando qualcuno cambia lavoro il sistema continua a seguirli. La persona è ancora la stessa entità, ma è collegata a un nuovo account. Questa funzionalità nativa offre un ottimo vettore per l’espansione in nuovi account, in quanto il sistema segue queste persone come individui, inclusi tutti i loro attributi e comportamenti.

## Origini B2B

Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform. L&#39;origine [!DNL Marketo] consente di inviare dati B2B in streaming ad Experience Platform e di tenerli aggiornati utilizzando applicazioni connesse ad Experience Platform. Supporta un numero qualsiasi di istanze di [!DNL Marketo] (a vantaggio delle grandi aziende con più istanze) e si richiama in un&#39;unica organizzazione in cui i dati vengono uniti.

>[!NOTE]
>
>L&#39;origine [!DNL Marketo] è **not** necessaria per utilizzare Real-Time CDP B2B edition.

Per ulteriori informazioni su Marketo e sull&#39;inserimento di dati B2B in Experience Platform, consulta la documentazione sulle [origini in Real-Time CDP B2B edition](./sources/b2b.md).

## Destinazioni B2B

Le destinazioni di Experience Platform, come Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads e Google Ad Manager, sono disponibili e completamente supportate da Real-Time CDP B2B edition. La destinazione Marketo Engage invia anche i dati di iscrizione ai segmenti da Experience Platform e li rende disponibili come elenchi in Marketo.

Per ulteriori informazioni, consulta la panoramica sulla [destinazione Marketo Engage](../destinations/catalog/adobe/marketo-engage.md).

Per le aziende con più CRM, Real-Time CDP B2B edition offre la possibilità di configurare i connettori di destinazione per istanze separate di Marketo o CRM. Se necessario, puoi configurare i connettori di destinazione per ogni istanza e inviare tipi di pubblico a ciascuna istanza di CRM in modo indipendente.

## Passaggi successivi

Ora che conosci meglio i vantaggi offerti da Real-Time CDP B2B edition per gli esperti di marketing e le differenze tra e Real-Time CDP, puoi scoprire come applicare queste funzioni alla tua organizzazione.

Per comprendere in che modo Real-Time CDP B2B edition può trarre vantaggio dal modello di servizio business-to-business, consulta la seguente documentazione per aiutarti a iniziare:

* [Un esempio di caso d’uso per Real-Time CDP B2B edition](./b2b-use-case.md)
* [Un tutorial end-to-end per Real-Time Customer Data Platform B2B edition](./b2b-tutorial.md)
* [Come acquisire i dati](./sources/b2b.md)
* [Come accedere ai profili](./profile/profile-overview.md)
* [Schemi in Real-Time Customer Data Platform B2B edition](./schemas/b2b.md)
* [Come creare tipi di pubblico](./segmentation/b2b.md)
* [Come attivare i tipi di pubblico nelle destinazioni](./destinations/b2b.md)
* [Come definire e applicare i criteri di governance dei dati](./privacy/data-governance-overview.md)
