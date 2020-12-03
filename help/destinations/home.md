---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;destinations;destination;rtcdp
title: Panoramica delle destinazioni
seo-title: Panoramica delle destinazioni
description: Attiva i dati di Platform nelle destinazioni per campagne di marketing cross-channel, e-mail, pubblicità mirata e altro ancora.
seo-description: Le destinazioni sono integrazioni preconfigurate con piattaforme di destinazione che consentono l'attivazione senza soluzione di continuità dei dati dalla piattaforma dati cliente in tempo reale. Puoi utilizzare Destinazioni nella piattaforma dati cliente in tempo reale per attivare i dati noti e sconosciuti per campagne di marketing su più canali, campagne e-mail, pubblicità mirata e molti altri casi di utilizzo.
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 3%

---


# [!DNL Destinations]panoramica{#overview}

![Banner della panoramica delle destinazioni](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** sono integrazioni pre-costruite con piattaforme di destinazione che consentono l&#39;attivazione senza soluzione di continuità dei dati dalla piattaforma dati cliente in tempo reale. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing multicanale, campagne e-mail, pubblicità mirata e molti altri casi di utilizzo.

## Destinazioni e origini {#destinations-and-sources}

Una delle funzionalità principali di CDP in tempo reale è l&#39;acquisizione dei dati di prime parti e l&#39;attivazione per le esigenze aziendali. Utilizzare le origini per assimilare i dati in CDP in tempo reale e le destinazioni per esportare i dati da CDP in tempo reale.

## Passaggi delle destinazioni {#steps}

* Scegli da un catalogo [](./catalog/overview.md) self-service di tutte le destinazioni disponibili in CDP in tempo reale.
* Utilizzate **[!UICONTROL Destinations]** per [attivare](./ui/activate-destinations.md) e inviare profili o segmenti alle piattaforme di automazione del marketing, alle piattaforme pubblicitarie digitali e altro ancora.
* Programmate le esportazioni di dati nelle destinazioni preferite in orari regolari.

## Controlli {#controls}

I controlli nell&#39;area di lavoro [](./ui/destinations-workspace.md) Destinazioni consentono di:

* Sfoglia il catalogo delle piattaforme di destinazione in cui puoi attivare i tuoi dati;
* Creare, modificare, attivare e disattivare i flussi di dati verso le destinazioni nel catalogo;
* creare un account in una posizione di archiviazione o collegare CDP in tempo reale all&#39;account nella piattaforma di destinazione;
* Selezionare i segmenti da attivare nelle destinazioni;
* Seleziona i campi [](../xdm/home.md) Experience Data Model (XDM) da esportare quando attivi i segmenti nelle destinazioni di marketing tramite e-mail.

## Destination types and categories {#types-and-categories}

Per informazioni dettagliate, consultate la panoramica [dei tipi di](./destination-types.md)destinazione e delle categorie.

## Destinazioni e controlli di accesso {#access-controls}

La funzionalità delle destinazioni in CDP in tempo reale funziona con le autorizzazioni di controllo degli accessi Adobe Experience Platform. A seconda del livello di autorizzazione dell’utente, potete visualizzare, gestire e attivare le destinazioni. Per informazioni sulle singole autorizzazioni, consultate Controllo [accesso in Adobe Experience Platform](../access-control/home.md) e scorrete verso il basso fino alla parte inferiore della pagina.

Per ulteriori informazioni sui controlli di accesso, vedere la guida [utente relativa al controllo di](../access-control/ui/overview.md)accesso.

## [!DNL Data Governance] limitazioni all&#39;attivazione dei dati alle destinazioni {#data-governance}

La governance dei dati è applicata alle destinazioni CDP in tempo reale tramite:

* *Casi* di utilizzo marketing selezionabili nel flusso di lavoro delle destinazioni di creazione;
* *Criteri* di utilizzo dei dati che limitano l&#39;attivazione dei dati contenenti determinate etichette di utilizzo a destinazioni con determinati casi di utilizzo di marketing.

Per ulteriori informazioni sui casi [!DNL Data Governance] di utilizzo del [marketing e sulla](../rtcdp/privacy/data-governance-overview.md#destinations) risoluzione delle violazioni [dei criteri di protezione dei dati, consulta](../rtcdp/privacy/data-governance-overview.md#enforcement)la documentazione CDP in tempo reale.

Per ulteriori informazioni sulla selezione dei casi di utilizzo del marketing nel flusso di lavoro di creazione della destinazione, consulta le pagine seguenti per i diversi tipi di destinazione in CDP in tempo reale:

* [Destinazioni pubblicitarie - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Destinazioni pubblicitarie - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinazioni pubblicitarie - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Destinazioni di archiviazione cloud](./catalog/cloud-storage/workflow.md)
* [Destinazioni di marketing e-mail](./catalog/email-marketing/overview.md)
* [Destinazioni social network](./catalog/social/workflow.md)

Per ulteriori informazioni sulle violazioni dei criteri dei dati nel flusso di lavoro di attivazione del segmento, consulta il passaggio Revisione in [Attivare profili e segmenti a una destinazione](./ui/activate-destinations.md#review).