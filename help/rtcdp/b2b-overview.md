---
keywords: RTCDP;CDP;Edizione B2B;Real-time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp;Customer AI
title: Panoramica dell’edizione B2B di Real-Time CDP
description: Panoramica dell’account Real-time Customer Data Platform B2B Edition
feature: Get Started, B2B
badgeB2B: label="Edizione B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 4%

---

# Panoramica dell’edizione B2B di Real-time Customer Data Platform

Basata su Adobe Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition è progettata appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono ai marketer di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.

Sono stati apportati miglioramenti a diverse funzionalità di Adobe Experience Platform che distinguono Real-Time CDP B2B Edition dalla sua controparte B2C. Includono miglioramenti all’Experience Data Model (XDM) per i casi d’uso B2B, aggiornamenti alla risoluzione delle identità e alla segmentazione dei profili, nonché un connettore e una destinazione personalizzati per [!DNL Marketo Engage]. Il [!DNL Marketo] Il connettore consente ai brand B2B di collegare i dati del coinvolgimento B2B leader del settore con informazioni comportamentali per sviluppare lead e migliorare le operazioni di marketing basate sull’account.

Con Real-Time CDP B2B Edition è possibile:

* Combina dati raccolti da più origini in un’unica vista per creare profili olistici di persone e account.
* Arricchisci, segmenta ed esporta tutti i dati provenienti da più origini da un archivio centralizzato di profili di account unificati.
* Gestisci i tuoi dati utilizzando gli strumenti di governance dei dati disponibili in ogni fase del processo di centralizzazione per garantire la conformità dei tuoi dati alle normative e alle politiche aziendali.

Di seguito sono riportate informazioni più complete sui miglioramenti apportati a Real-Time CDP B2B Edition.

## XDM

Real-Time CDP B2B Edition fornisce diverse nuove classi di schema XDM, gruppi di campi e tipi di relazione per acquisire e strutturare i dati in modo specifico per scopi B2B. Consulta la panoramica su [XDM in Real-Time CDP B2B edition](./schemas/b2b.md) per una suddivisione di ciascuno di questi miglioramenti.

Utilizzando schemi B2B preconfigurati, puoi inserire i dati in una struttura standardizzata e actionable. Molte delle nuove classi di schema vengono mappate quasi direttamente a quelle incontrate nei sistemi CRM tradizionali come [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo]e altre fonti di dati B2B. Con Real-Time CDP B2B Edition, è possibile inserire in Platform i dati provenienti da origini B2B in modo semplice e con risultati facili da controllare.

Questi miglioramenti XDM consentono di acquisire e attivare meglio i dati tramite origini e destinazioni incentrate sul B2B, migliorando l’unificazione e la presentazione dei dati per casi d’uso più vari e flessibili.

## Risoluzione identità

Dopo aver definito gli schemi e acquisito i dati in conformità a tali schemi, Real-Time CDP B2B Edition identifica i record di origine che rappresentano persone e aziende del mondo reale attraverso un potente sistema di risoluzione delle identità in tempo reale.

Il sistema di risoluzione delle identità offre le seguenti funzionalità:

* Record di persone B2B e B2C combinati
* Gerarchia di account a più livelli
* Connessioni molti-a-molti, persone-account
* Le persone e le identità dell’account vengono risolte in tempo reale

Il sistema di risoluzione delle identità è stato ampliato per supportare una classificazione più sfaccettata delle persone. Il sistema consente di identificare le persone come lead nelle opportunità di business, oltre che nei clienti.

I record account sincronizzati dal sistema CRM di origine e connessi tramite più percorsi all’interno del sistema vengono uniti da Platform. Il sistema riunisce le persone associate alle opportunità commerciali e quelle registrate come clienti, ma è anche in grado di mantenere la distinzione tra loro come attributo se sono identificabili.

Gli identificativi corrispondenti vengono utilizzati per collegare e unire i record account da più sistemi. Le gerarchie di conti vengono mantenute durante questo processo. I differenziatori vengono utilizzati per verificare se una persona è associata o meno a un account e fornire la possibilità di separarli dall’account, se necessario.

## Profili e segmentazione

Una volta che Real-Time CDP B2B Edition ha acquisito dati e risolto identità relative a persone, aziende, attributi e comportamenti, tali dati vengono utilizzati per creare profili. Questi profili possono quindi essere segmentati in tipi di pubblico visualizzabili che possono quindi essere attivati in varie destinazioni.

Se implementato correttamente, il sistema tiene traccia delle persone utilizzando identificatori primari univoci anziché attributi che possono essere modificati, come ad esempio gli indirizzi e-mail. Ciò significa che quando qualcuno cambia lavoro il sistema continua a seguirli. La persona è ancora la stessa entità, ma è collegata a un nuovo account. Questa funzionalità nativa offre un ottimo vettore per l’espansione in nuovi account, in quanto il sistema segue queste persone come individui, inclusi tutti i loro attributi e comportamenti.

## Origini B2B

Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. Il [!DNL Marketo] consente di inviare in streaming dati B2B a Platform e di tenerli aggiornati utilizzando applicazioni connesse a Platform. Supporta un numero qualsiasi di istanze di [!DNL Marketo] (a vantaggio delle grandi aziende con più istanze) e si inserisce in un’unica organizzazione in cui i dati vengono uniti.

>[!NOTE]
>
>Il [!DNL Marketo] sorgente è **non** necessario per utilizzare Real-Time CDP B2B Edition.

Consulta la [origini in Real-Time CDP B2B Edition](./sources/b2b.md) per ulteriori informazioni su Marketo e sull’importazione di dati B2B in Platform.

## Destinazioni B2B

Le destinazioni di Experience Platform come Google Customer Match, Facebook, LinkedIn, Marketi Engage, Amazon S3, Google Display &amp; Video 360, Google Ads e Google Ad Manager sono disponibili e completamente supportate da Real-Time CDP B2B Edition. La destinazione del Marketo Engage invia anche i dati di iscrizione ai segmenti fuori da Platform e li rende disponibili come elenchi in Marketo.

Consulta la panoramica su [Destinazione Marketo Engage](../destinations/catalog/adobe/marketo-engage.md) per ulteriori informazioni.

Per le aziende con più CRM, la versione B2B di Real-Time CDP fornisce l’opzione di configurare i connettori di destinazione per istanze separate di Marketo o CRM. Se necessario, puoi configurare i connettori di destinazione per ogni istanza e inviare tipi di pubblico a ciascuna istanza di CRM in modo indipendente.

## Passaggi successivi

Ora che hai compreso meglio i vantaggi per gli esperti di marketing offerti da Real-Time CDP B2B Edition e le differenze tra questa e Real-Time CDP, puoi imparare ad applicare queste funzioni alla tua organizzazione.

Per informazioni sui vantaggi offerti da Real-Time CDP B2B Edition al modello di servizio business-to-business, consulta la documentazione seguente per informazioni introduttive:

* [Esempio di utilizzo per la versione B2B di Real-Time CDP](./b2b-use-case.md)
* [Tutorial completo per la versione B2B di Real-time Customer Data Platform](./b2b-tutorial.md)
* [Come acquisire i dati](./sources/b2b.md)
* [Come accedere ai profili](./profile/profile-overview.md)
* [Schemi in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
* [Come creare tipi di pubblico](./segmentation/b2b.md)
* [Come attivare i tipi di pubblico nelle destinazioni](./destinations/b2b.md)
* [Come definire e applicare i criteri di governance dei dati](./privacy/data-governance-overview.md)
