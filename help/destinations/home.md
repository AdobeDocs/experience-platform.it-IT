---
keywords: destinazioni;adobe experience platform;platform;destinations overview overview overview;activate data;activate;
title: Panoramica delle destinazioni
seo-title: Panoramica delle destinazioni
description: Attiva i dati di Platform nelle destinazioni per campagne di marketing cross-channel, e-mail, pubblicità mirata e altro ancora.
seo-description: Le destinazioni sono integrazioni predefinite con piattaforme di destinazione che consentono l'attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare Destinazioni in Adobe Experience Platform per attivare i dati noti e sconosciuti per campagne di marketing multicanale, campagne e-mail, pubblicità mirata e molti altri casi di utilizzo.
translation-type: tm+mt
source-git-commit: 32eae2ed782e46941bb21e3aca62c6bce68cde1e
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 3%

---


# [!DNL Destinations]panoramica{#overview}

![Banner della panoramica delle destinazioni](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** sono integrazioni preconfigurate con piattaforme di destinazione che consentono l&#39;attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing multicanale, campagne e-mail, pubblicità mirata e molti altri casi di utilizzo.

## Destinazioni e origini {#destinations-and-sources}

Una delle funzionalità principali di Platform è l&#39;acquisizione dei dati di prime parti e l&#39;attivazione per le esigenze aziendali. Utilizzate le origini per assimilare i dati nella piattaforma e nelle destinazioni per esportare i dati dalla piattaforma.

## Passaggi delle destinazioni {#steps}

* Scegliete tra un [catalogo self-service](./catalog/overview.md) di tutte le destinazioni disponibili in Piattaforma.
* Utilizzate **[!UICONTROL Destinations]** per [attivare](./ui/activate-destinations.md) e inviare profili o segmenti alle piattaforme di automazione del marketing, alle piattaforme di pubblicità digitale e altro ancora.
* Programmate le esportazioni di dati nelle destinazioni preferite in orari regolari.

## Controlli {#controls}

I controlli nell&#39;area di lavoro [Destinazioni](./ui/destinations-workspace.md) consentono di:

* Sfoglia il catalogo delle piattaforme di destinazione in cui puoi attivare i tuoi dati;
* Creare, modificare, attivare e disattivare i flussi di dati verso le destinazioni nel catalogo;
* creare un account in una posizione di archiviazione o collegare Piattaforma all&#39;account nella piattaforma di destinazione;
* Selezionare i segmenti da attivare nelle destinazioni;
* Selezionare i campi [Experience Data Model (XDM)](../xdm/home.md) da esportare durante l&#39;attivazione dei segmenti nelle destinazioni di marketing tramite e-mail.

## Tipi di destinazione e categorie {#types-and-categories}

Per informazioni dettagliate, vedere la [panoramica dei tipi di destinazione e delle categorie](./destination-types.md).

## Destinazioni e controlli di accesso {#access-controls}

La funzionalità delle destinazioni in Piattaforma funziona con le autorizzazioni di controllo degli accessi Adobe Experience Platform. A seconda del livello di autorizzazione dell’utente, potete visualizzare, gestire e attivare le destinazioni. Per informazioni sulle singole autorizzazioni, vedere [Controllo degli accessi in Adobe Experience Platform](../access-control/home.md) e scorrere verso il basso fino alla parte inferiore della pagina.

Per ulteriori informazioni sui controlli di accesso, vedere la [Guida utente del controllo di accesso](../access-control/ui/overview.md).

## [!DNL Data Governance] limitazioni all&#39;attivazione dei dati alle destinazioni  {#data-governance}

La governance dei dati è applicata alle destinazioni della piattaforma tramite:

* *Casi di utilizzo del marketing* che potete selezionare nel flusso di lavoro di creazione delle destinazioni;
* *Criteri* di utilizzo dei dati che limitano l&#39;attivazione dei dati contenenti determinate etichette di utilizzo a destinazioni con determinati casi di utilizzo di marketing.

Per ulteriori informazioni su [!DNL Data Governance] casi di utilizzo del marketing[casi di utilizzo del marketing](../data-governance/policies/overview.md) e [risoluzione delle violazioni dei criteri dei dati](../data-governance/enforcement/auto-enforcement.md), consultare la sezione  della documentazione della piattaforma.

Per ulteriori informazioni sulla selezione dei casi di utilizzo del marketing nel flusso di lavoro di creazione della destinazione, consulta le pagine seguenti per i diversi tipi di destinazione in Piattaforma:

* [Destinazioni pubblicitarie - Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [Destinazioni pubblicitarie - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinazioni pubblicitarie - Google Display &amp; Video 360  ](./catalog/advertising/google-dv360.md)
* [Destinazioni di archiviazione cloud](./catalog/cloud-storage/workflow.md)
* [Destinazioni di marketing e-mail](./catalog/email-marketing/overview.md)
* [Destinazioni social network](./catalog/social/workflow.md)

Per ulteriori informazioni sulle violazioni dei criteri dei dati nel flusso di lavoro di attivazione del segmento, vedi il passaggio Review in [Attivare profili e segmenti in una destinazione](./ui/activate-destinations.md#review).