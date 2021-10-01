---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;piattaforma dati cliente in tempo reale;cdp in tempo reale;b2b;cdp;Customer AI
title: Panoramica di Real-time CDP B2B Edition
seo-title: Real-time Customer Data Platform B2B Edition overview
description: Panoramica dell’account Real-time Customer Data Platform B2B Edition
seo-description: Overview of Real-time Customer Data Platform B2B Edition Account
hide: true
hidefromtoc: true
source-git-commit: 193e709ccf6d4cec0a1ce2182f0106cc20c155ab
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 1%

---

# Panoramica su Real-time Customer Data Platform B2B Edition

>[!IMPORTANT]
>
>Real-time CDP B2B Edition è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Basato su Real-time Customer Data Platform (Real-time CDP), Real-time CDP B2B Edition è progettato appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Riunisce i dati provenienti da più sorgenti e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli esperti di marketing di eseguire il targeting preciso di tipi di pubblico specifici e coinvolgerli in tutti i canali disponibili.

Sono stati apportati miglioramenti a una varietà di funzionalità di Adobe Experience Platform che distinguono Real-time CDP B2B Edition dalla sua controparte B2C. Includono miglioramenti a Experience Data Model (XDM) per casi d’uso B2B, aggiornamenti alla risoluzione delle identità e alla segmentazione del profilo, nonché un connettore e una destinazione personalizzati per [!DNL Marketo Engage]. Il connettore [!DNL Marketo] consente ai marchi B2B di collegare i dati di coinvolgimento B2B leader del settore con informazioni comportamentali al fine di generare lead e migliorare le operazioni di marketing basate sull’account.

Con Real-time CDP B2B Edition, puoi:

* Combina i dati raccolti da più sorgenti in un’unica visualizzazione per creare persone olistiche e profili di account.
* Arricchisci, segmenta ed esporta tutti i tuoi dati cross-source da un archivio centralizzato di profili account unificati.
* Gestisci i dati utilizzando gli strumenti di governance dei dati disponibili in ogni fase del processo di centralizzazione, per garantire la conformità dei dati alle normative legali e alle politiche aziendali.

I dettagli più completi sui miglioramenti apportati per Real-time CDP B2B Edition sono suddivisi nelle sezioni seguenti.

## XDM

Real-time CDP B2B Edition fornisce diverse nuove classi di schema XDM, gruppi di campi e tipi di relazione per acquisire e strutturare i dati in modo specifico per scopi B2B. Per informazioni dettagliate su ciascuno di questi miglioramenti, consulta la panoramica su [XDM in Real-time CDP B2B edition](./schemas/b2b.md) .

Utilizzando schemi B2B preconfigurati, puoi inserire i dati in una struttura standardizzata e fruibile. Molte delle nuove classi di schema sono mappate quasi direttamente a quelle incontrate nelle CRM tradizionali come [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] e altre origini dati B2B. Con Real-time CDP B2B Edition, è possibile portare i dati da fonti B2B in Platform in modo semplice e con risultati di facile controllo.

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

Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. La sorgente [!DNL Marketo] consente di inviare dati B2B in Platform e di tenerli aggiornati utilizzando le applicazioni connesse a Platform. Supporta un numero qualsiasi di istanze di [!DNL Marketo] (utile per le grandi aziende con più istanze) e richiama in un&#39;unica organizzazione IMS in cui i dati vengono uniti.

>[!NOTE]
>
>La [!DNL Marketo] sorgente è **non** necessaria per utilizzare Real-time CDP B2B Edition.

Per ulteriori informazioni su Marketo e sull’inserimento di dati B2B in Platform, consulta le fonti nella documentazione di Real-time CDP B2B Edition .

<!-- PLACEHOLDER [sources in Real-time CDP B2B Edition](./sources/b2b) -->

## Destinazioni B2B

Tutte le destinazioni di Experience Platform come [!DNL Google], [!DNL Linkedin] o [!DNL Facebook] sono disponibili e supportate completamente da Real-time CDP B2B Edition. Esiste anche una destinazione [!DNL Marketo Engage] che esegue lo streaming dei dati da [!DNL Marketo] o fuori dalla piattaforma e li rende disponibili come tipi di pubblico.

La destinazione [!DNL Marketo] offre un modo semplice e rapido per estrarre informazioni dall&#39;Experience Platform in [!DNL Marketo]. La destinazione consente agli addetti al marketing di inviare in push i segmenti creati in Adobe Experience Platform a [!DNL Marketo]. In [!DNL Marketo] questi tipi di pubblico sono quindi disponibili come elenchi statici.

Per le aziende con più di un sistema di gestione delle relazioni con i clienti, Real-time CDP B2B Edition offre la possibilità di configurare connettori di destinazione per istanze separate di [!DNL Marketo] o CRM. Se necessario, puoi configurare i connettori di destinazione per ogni istanza e inviare i tipi di pubblico a ciascuna istanza CRM in modo indipendente.

## Passaggi successivi

Ora che conosci meglio i vantaggi per gli addetti al marketing offerti da Real-time CDP B2B Edition e le differenze tra esso e Real-time CDP, puoi imparare ad applicare queste funzioni alla tua organizzazione IMS.

<!-- PLACEHOLDER [example use case for Real-time CDP B2B Edition]() -->

Per comprendere in che modo Real-time CDP B2B Edition può trarre vantaggio dal modello di servizio business-to-business, vedi l&#39;esempio di caso d&#39;uso per Real-time CDP B2B Edition. In alternativa, puoi fare riferimento agli schemi [nella documentazione di Real-time Customer Data Platform B2B Edition](./schemas/b2b.md) per indicazioni più specifiche sulla creazione di schemi e sulla definizione di relazioni per le entità dati B2B essenziali.
