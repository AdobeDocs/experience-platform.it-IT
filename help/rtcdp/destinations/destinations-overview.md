---
title: Panoramica delle destinazioni
seo-title: Panoramica delle destinazioni
description: Le destinazioni sono integrazioni predefinite con piattaforme di destinazione che consentono l'attivazione senza soluzione di continuità dei dati dall'Platform di dati del cliente in tempo reale. Puoi utilizzare Destinazioni nell'Platform dati cliente in tempo reale di Adobe per attivare i dati noti e sconosciuti per campagne di marketing multicanale, campagne e-mail, campagne pubblicitarie mirate e molti altri casi di utilizzo.
seo-description: Le destinazioni sono integrazioni predefinite con piattaforme di destinazione che consentono l'attivazione senza soluzione di continuità dei dati dall'Platform di dati del cliente in tempo reale. Puoi utilizzare Destinazioni nell'Platform dati cliente in tempo reale di Adobe per attivare i dati noti e sconosciuti per campagne di marketing multicanale, campagne e-mail, campagne pubblicitarie mirate e molti altri casi di utilizzo.
translation-type: tm+mt
source-git-commit: a61a2a4d9d51c402bb50153c06a93d255a3613cb
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---


# Destinations Overview {#overview}

![Banner della panoramica delle destinazioni](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**Le destinazioni** sono integrazioni preconfigurate con piattaforme di destinazione che consentono l&#39;attivazione senza soluzione di continuità dei dati dall&#39;Platform di dati del cliente in tempo reale. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing multicanale, campagne e-mail, pubblicità mirata e molti altri casi di utilizzo.

## Destinazioni e origini {#destinations-and-sources}

Una delle funzionalità principali di CDP in tempo reale è l&#39;acquisizione dei dati di prime parti e l&#39;attivazione per le esigenze aziendali. Utilizzare le origini per assimilare i dati in CDP in tempo reale e le destinazioni per esportare i dati da CDP in tempo reale.

## Passaggi delle destinazioni {#steps}

* Scegli da un catalogo [](/help/rtcdp/destinations/destinations-catalog.md) self-service di tutte le destinazioni disponibili in CDP in tempo reale.
* Utilizzate **[!UICONTROL Destinations]** per [attivare](/help/rtcdp/destinations/activate-destinations.md) e inviare profili o segmenti alle piattaforme di automazione del marketing, alle piattaforme pubblicitarie digitali e altro ancora.
* Programmate le esportazioni di dati nelle destinazioni preferite in orari regolari.

## Controlli {#controls}

I controlli nell&#39;area di lavoro [](/help/rtcdp/destinations/destinations-workspace.md) Destinazioni consentono di:

* Sfoglia il catalogo delle piattaforme di destinazione in cui puoi attivare i tuoi dati;
* Creare, modificare, attivare e disattivare i flussi di dati verso le destinazioni nel catalogo;
* creare un account in una posizione di archiviazione o collegare CDP in tempo reale all&#39;account nella piattaforma di destinazione;
* Selezionare i segmenti da attivare nelle destinazioni;
* Seleziona i campi [](../../xdm/home.md) Experience Data Model (XDM) da esportare quando attivi i segmenti nelle destinazioni di marketing tramite e-mail.

## Destination types and categories {#types-and-categories}

Per informazioni dettagliate, consultate la panoramica [dei tipi di](/help/rtcdp/destinations/destination-types.md)destinazione e delle categorie.

## Destinazioni e controlli di accesso {#access-controls}

La funzionalità delle destinazioni in CDP in tempo reale funziona con  autorizzazioni di controllo dell&#39;accesso al Adobe Experience Platform. A seconda del livello di autorizzazione dell’utente, potete visualizzare, gestire e attivare le destinazioni. Per informazioni sulle singole autorizzazioni, consultate Controllo [Accesso in  Adobe Experience Platform](../../access-control/home.md) e scorrete verso il basso fino alla parte inferiore della pagina.

Per ulteriori informazioni sui controlli di accesso, vedere la guida [utente relativa al controllo di](../../access-control/ui/overview.md)accesso.

## Limitazioni per la governance dei dati sull&#39;attivazione dei dati sulle destinazioni {#data-governance}

La governance dei dati è applicata alle destinazioni CDP in tempo reale tramite:

* *Casi* di utilizzo marketing selezionabili nel flusso di lavoro delle destinazioni di creazione;
* *Criteri* di utilizzo dei dati che limitano l&#39;attivazione dei dati contenenti determinate etichette di utilizzo a destinazioni con determinati casi di utilizzo di marketing.

Per ulteriori informazioni sui casi [di utilizzo del](/help/rtcdp/privacy/data-governance-overview.md#destinations) marketing e sulla [risoluzione delle violazioni](/help/rtcdp/privacy/data-governance-overview.md#enforcement)dei criteri per i dati, consulta la sezione Gestione dei dati in tempo reale.

Per ulteriori informazioni sulla selezione dei casi di utilizzo del marketing nel flusso di lavoro di creazione della destinazione, consulta le pagine seguenti per i diversi tipi di destinazione in CDP in tempo reale:

* [Destinazioni pubblicitarie - Google Ad Manager ](/help/rtcdp/destinations/google-ad-manager-destination.md)
* [Destinazioni pubblicitarie - Google Ads](/help/rtcdp/destinations/google-ads-destination.md)
* [Destinazioni pubblicitarie - Google Display &amp; Video 360 ](/help/rtcdp/destinations/google-dv360-destination.md)
* [Destinazioni di archiviazione cloud](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)
* [Destinazioni di marketing e-mail](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Destinazioni social network](/help/rtcdp/destinations/social-network-destinations-workflow.md)

Per ulteriori informazioni sulle violazioni dei criteri dei dati nel flusso di lavoro di attivazione del segmento, vedi il passaggio 7 in [Attivare profili e segmenti su una destinazione](/help/rtcdp/destinations/activate-destinations.md).