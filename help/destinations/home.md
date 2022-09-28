---
keywords: destinazioni;adobe experience platform;piattaforma;panoramica destinazioni;attivare dati;attivare;
title: Panoramica sulle destinazioni
description: Le destinazioni sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le Destinazioni in Adobe Experience Platform per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 842aaa7104b277cf415d1ed9ee2744a200c07ce8
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# [!DNL Destinations] panoramica {#overview}

![Banner di panoramica sulle destinazioni](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

## Destinazioni e fonti {#destinations-and-sources}

Una delle funzionalità principali di Platform è l’acquisizione dei dati di prime parti e l’attivazione per le tue esigenze aziendali. Utilizzo [origini](../sources/home.md) per acquisire dati in Platform e destinazioni per esportare dati da Platform.

## Passaggi per le destinazioni {#steps}

* Scegli tra [catalogo self-service](./catalog/overview.md) di tutte le destinazioni disponibili in Platform.
* Utilizza le destinazioni per inviare profili o segmenti alle piattaforme di automazione del marketing, alle piattaforme di pubblicità digitale e altro ancora.
* Pianifica le esportazioni di dati nelle destinazioni preferite in orari regolari.

## Controlli {#controls}

I controlli [Area di lavoro Destinazioni](./ui/destinations-workspace.md) consente di:

* Sfoglia il catalogo delle piattaforme di destinazione in cui puoi attivare i tuoi dati;
* Creare, modificare, attivare e disattivare i flussi di dati verso le destinazioni nel catalogo;
* Crea un account in una posizione di archiviazione o collega Platform all’account nella piattaforma di destinazione;
* Seleziona quali segmenti devono essere attivati nelle destinazioni;
* Seleziona quale [Campi Experience Data Model (XDM)](../xdm/home.md) da esportare quando si attivano i segmenti nelle destinazioni di marketing via e-mail.

## Tipi di destinazione e categorie {#types-and-categories}

Per informazioni dettagliate, consulta la sezione [panoramica dei tipi e delle categorie di destinazione](./destination-types.md).

## Destinazioni e controlli di accesso {#access-controls}

La funzionalità delle destinazioni in Platform funziona con le autorizzazioni di controllo accessi di Adobe Experience Platform. A seconda del livello di autorizzazione dell’utente, puoi visualizzare, gestire e attivare le destinazioni. Per informazioni sulle singole autorizzazioni, consulta [Controllo degli accessi in Adobe Experience Platform](../access-control/home.md) e scorri verso il basso fino alla parte inferiore della pagina.

La tabella seguente illustra le combinazioni di autorizzazioni e autorizzazioni necessarie per eseguire determinate azioni sulle destinazioni:

| Livello di autorizzazione | Descrizione |
| ---- | ----|
| **[!UICONTROL Gestire le destinazioni]** | Per connetterti alle destinazioni, devi disporre delle **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). |
| **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** | Per attivare i segmenti sulle destinazioni, è necessario disporre delle **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sui controlli di accesso, consulta la sezione [Guida utente al controllo degli accessi](../access-control/ui/overview.md).

### Controllo dell&#39;accesso basato su attributi per le destinazioni {#attribute-based-access}

Il controllo dell&#39;accesso basato su attributi in Adobe Experience Platform consente agli amministratori di controllare l&#39;accesso a oggetti e/o funzionalità specifici in base agli attributi.

Con il controllo dell&#39;accesso basato sugli attributi, puoi applicare configurazioni di mappatura ai campi a cui disponi delle autorizzazioni. Inoltre, non puoi esportare i dati in una destinazione se non hai accesso a tutti i campi del set di dati.

Per ulteriori informazioni sul funzionamento delle destinazioni con controlli di accesso basati sugli attributi, consulta la sezione [panoramica sul controllo dell&#39;accesso basato sugli attributi](../access-control/abac/overview.md#destinations).

## Restrizioni sulla governance dei dati sull’attivazione dei dati alle destinazioni {#data-governance}

La governance dei dati viene applicata alle destinazioni Platform tramite:

* *Azioni di marketing* che puoi selezionare nel flusso di lavoro crea destinazioni;
* *Criteri di utilizzo dei dati* che impedisce l’attivazione di dati contenenti determinate etichette di utilizzo a destinazioni con determinate azioni di marketing.

Per ulteriori informazioni, consulta Governance dei dati nella documentazione di Platform . [azioni di marketing](../data-governance/policies/overview.md) e [risoluzione delle violazioni dei criteri dei dati](../data-governance/enforcement/auto-enforcement.md).

Per ulteriori informazioni sulla selezione delle azioni di marketing nel flusso di lavoro di creazione della destinazione, consulta le pagine seguenti per i diversi tipi di destinazione in Platform:

* [Destinazioni pubblicitarie - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Destinazioni pubblicitarie - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinazioni pubblicitarie - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Destinazioni di archiviazione cloud](./catalog/cloud-storage/overview.md)
* [Destinazioni di marketing e-mail](./catalog/email-marketing/overview.md)
* [Destinazioni social](./catalog/social/overview.md)

Per ulteriori informazioni sulle violazioni dei criteri dei dati nel flusso di lavoro di attivazione dei segmenti, consulta la sezione **[!UICONTROL Revisione]** segui le seguenti guide:

* [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](./ui/activate-segment-streaming-destinations.md#review)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](./ui/activate-streaming-profile-destinations.md#review)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](./ui/activate-batch-profile-destinations.md#review)
