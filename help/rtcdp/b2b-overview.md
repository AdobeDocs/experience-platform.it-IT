---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;piattaforma dati cliente in tempo reale;cdp in tempo reale;b2b;cdp;Customer AI
title: Panoramica di Real-time CDP B2B Edition
description: Panoramica dell’account Real-time Customer Data Platform B2B Edition
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# Panoramica di Real-time Customer Data Platform B2B Edition

Basato su Real-time Customer Data Platform (Real-time CDP), Real-time CDP B2B Edition è progettato appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Riunisce i dati provenienti da più sorgenti e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli esperti di marketing di eseguire il targeting preciso di tipi di pubblico specifici e coinvolgerli in tutti i canali disponibili.

Sono stati apportati miglioramenti a una varietà di funzionalità di Adobe Experience Platform che distinguono Real-time CDP B2B Edition dalla sua controparte B2C. Includono miglioramenti a Experience Data Model (XDM) per casi d’uso B2B, aggiornamenti alla risoluzione delle identità e alla segmentazione del profilo, nonché un connettore e una destinazione personalizzati per [!DNL Marketo Engage]. La [!DNL Marketo] connettore consente ai marchi B2B di collegare i dati di coinvolgimento B2B leader del settore con informazioni comportamentali al fine di generare lead e migliorare le operazioni di marketing basate sull’account.

Con Real-time CDP B2B Edition, puoi:

* Combina i dati raccolti da più sorgenti in un’unica visualizzazione per creare persone olistiche e profili di account.
* Arricchisci, segmenta ed esporta tutti i tuoi dati cross-source da un archivio centralizzato di profili account unificati.
* Gestisci i dati utilizzando gli strumenti di governance dei dati disponibili in ogni fase del processo di centralizzazione per garantire la conformità dei dati alle normative legali e alle politiche aziendali.

I dettagli più completi sui miglioramenti apportati per Real-time CDP B2B Edition sono suddivisi nelle sezioni seguenti.

## XDM

Real-time CDP B2B Edition fornisce diverse nuove classi di schema XDM, gruppi di campi e tipi di relazione per acquisire e strutturare i dati in modo specifico per scopi B2B. Vedi la panoramica su [XDM in tempo reale CDP B2B edition](./schemas/b2b.md) per una suddivisione di ciascuno di questi miglioramenti.

Utilizzando schemi B2B preconfigurati, puoi inserire i dati in una struttura standardizzata e fruibile. Molte delle nuove classi di schema sono mappate quasi direttamente a quelle incontrate nelle CRM tradizionali come [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo]e altre fonti di dati B2B. Con Real-time CDP B2B Edition, è possibile portare i dati da fonti B2B in Platform in modo semplice e con risultati di facile controllo.

Questi miglioramenti XDM ti consentono di acquisire e attivare meglio i dati tramite sorgenti e destinazioni incentrate su B2B, migliorando l’unificazione dei dati e la presentazione per casi d’uso più vari e flessibili.

## Risoluzione identità

Una volta definiti gli schemi e acquisiti i dati conformi a tali schemi, Real-time CDP B2B Edition identifica i record sorgente che rappresentano le persone e le aziende del mondo reale attraverso un potente sistema di risoluzione delle identità in tempo reale.

Il sistema di risoluzione delle identità fornisce le seguenti caratteristiche:

* Record di persone combinati B2B e B2C
* Una gerarchia di account a più livelli
* Connessioni molti-a-molti, persone-a-account
* Le persone e le identità dell’account vengono risolte in tempo reale

Il sistema di risoluzione delle identità è stato ampliato per supportare una classificazione più sfaccettata delle persone. Il sistema consente di identificare le persone come i principali responsabili delle opportunità commerciali e dei clienti.

I record account sincronizzati dal CRM di origine e collegati tramite più percorsi all’interno del sistema vengono uniti da Platform. Il sistema riunisce le persone associate a opportunità commerciali e quelle registrate come clienti, ma è anche in grado di preservare la distinzione tra di loro come un attributo se sono identificabili.

Gli identificatori corrispondenti vengono utilizzati per collegare e unire record di account da più sistemi. Le gerarchie di account vengono mantenute in tutto il processo. I differenziatori vengono utilizzati per verificare se una persona è associata o meno a un account e per fornire la possibilità di separarli dal conto, se necessario.

## Profili e segmentazione

Una volta che Real-time CDP B2B Edition ha acquisito i dati e le identità risolte relative a persone, aziende, attributi e comportamenti, tali dati vengono utilizzati per creare profili. Questi profili possono quindi essere segmentati in tipi di pubblico esplorabili che possono essere attivati in varie destinazioni.

Se implementato correttamente, il sistema tiene traccia delle persone utilizzando identificatori primari univoci anziché attributi che possono essere modificati, ad esempio indirizzi e-mail. Ciò significa che quando qualcuno cambia lavoro il sistema continua a seguirli. La persona rimane la stessa entità, ma è collegata a un nuovo conto. Questa funzionalità nativa offre un grande vettore per l&#39;espansione in nuovi account in quanto il sistema segue queste persone come individui, inclusi tutti i loro attributi e comportamenti.

## Fonti B2B

Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. La [!DNL Marketo] source consente di inviare dati B2B in Platform e di tenerli aggiornati utilizzando le applicazioni connesse a Platform. Supporta qualsiasi numero di istanze di [!DNL Marketo] (utile per le grandi aziende con più istanze) e si rivolge a un’unica organizzazione IMS in cui i dati vengono uniti.

>[!NOTE]
>
>La [!DNL Marketo] source **not** richiesto per utilizzare Real-time CDP B2B Edition.

Consulta la sezione [origini in Real-time CDP B2B Edition](./sources/b2b.md) documentazione per ulteriori informazioni su Marketo e sull’inserimento di dati B2B in Platform.

## Destinazioni B2B

Le destinazioni di Experience Platform come Google Customer Match, Facebook, LinkedIn, Marketi Engage, Amazon S3, Google Display &amp; Video 360, Google Ads e Google Ad Manager sono disponibili e completamente supportate da Real-time CDP B2B Edition. La destinazione del Marketo Engage invia anche i dati di appartenenza al segmento da Platform e li rende disponibili come elenchi in Marketo.

Vedi la panoramica sul [Destinazione Marketo Engage](../destinations/catalog/adobe/marketo-engage.md) per ulteriori informazioni.

Per le aziende con più di un sistema di gestione delle relazioni con i clienti, Real-time CDP B2B Edition offre la possibilità di configurare connettori di destinazione per istanze separate di Marketo o CRM. Se necessario, puoi configurare i connettori di destinazione per ogni istanza e inviare i tipi di pubblico a ciascuna istanza CRM in modo indipendente.

## Passaggi successivi

Ora che conosci meglio i vantaggi per gli addetti al marketing offerti da Real-time CDP B2B Edition e le differenze tra esso e Real-time CDP, puoi scoprire come applicare queste funzioni alla tua organizzazione IMS.

Per comprendere in che modo Real-time CDP B2B Edition può trarre vantaggio dal modello di servizio business-to-business, consulta la seguente documentazione per aiutarti a iniziare:

* [Esempio di utilizzo per Real-time CDP B2B Edition](./b2b-use-case.md)
* [Un tutorial end-to-end per Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
* [Come acquisire i dati](./sources/b2b.md)
* [Come accedere ai profili](./profile/profile-overview.md)
* [Schemi in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
* [Come creare segmenti](./segmentation/b2b.md)
* [Come attivare i segmenti sulle destinazioni](./destinations/b2b.md)
* [Come definire e applicare le politiche di governance dei dati](./privacy/data-governance-overview.md)
