---
title: Panoramica sulle destinazioni
description: Le destinazioni sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione fluida dei dati da Adobe Experience Platform. Puoi utilizzare le Destinazioni in Adobe Experience Platform per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 4%

---

# Panoramica di [!DNL Destinations] {#overview}

![Banner panoramica sulle destinazioni](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Destinazioni e origini {#destinations-and-sources}

Una delle funzionalità principali di Platform è l’acquisizione dei dati di prime parti e l’attivazione per le esigenze aziendali. Utilizzare [sorgenti](../sources/home.md) per acquisire dati in Platform e nelle destinazioni per esportare dati da Platform.

## Passaggi delle destinazioni {#steps}

* Scegli da un [catalogo self-service](./catalog/overview.md) di tutte le destinazioni disponibili in Platform.
* Utilizza le destinazioni per inviare profili o tipi di pubblico a piattaforme di automazione marketing, piattaforme di pubblicità digitale e altro ancora.
* Pianifica le esportazioni di dati nelle destinazioni preferite a intervalli regolari.

## Controlli {#controls}

I controlli in [area di lavoro destinazioni](./ui/destinations-workspace.md) consente di:

* Sfoglia il catalogo delle piattaforme di destinazione in cui puoi attivare i tuoi dati;
* Creare, modificare, attivare e disattivare flussi di dati per le destinazioni nel catalogo;
* Creare un account in un percorso di archiviazione o collegare Platform all’account nella piattaforma di destinazione;
* Seleziona i tipi di pubblico da attivare sulle destinazioni;
* Seleziona quale [Campi Experience Data Model (XDM)](../xdm/home.md) da esportare quando si attivano tipi di pubblico su destinazioni di e-mail marketing.

## Tipi e categorie di destinazione {#types-and-categories}

Ad Experience Platform, puoi attivare i dati per vari tipi di destinazioni, per soddisfare i casi d’uso di attivazione. Le destinazioni variano da integrazioni basate su API a integrazioni con sistemi di ricezione di file, destinazioni di ricerca dei profili e altro ancora. Per informazioni dettagliate su tutte le destinazioni disponibili, vedi [panoramica sui tipi e sulle categorie di destinazione](./destination-types.md).

## Destinazioni create da Adobi e da partner {#adobe-and-partner-built-destinations}

Alcuni dei connettori nel catalogo delle destinazioni Experienci Platform sono generati e gestiti da Adobe, mentre altri sono generati e gestiti da aziende partner che utilizzano [Destination SDK](/help/destinations/destination-sdk/overview.md). Una nota nella parte superiore della pagina della documentazione per ciascun connettore creato dal partner richiama se una destinazione è stata creata e gestita dal partner. Ad esempio, il [Connettore Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) viene creato da Adobe, mentre [Connettore TikTok](/help/destinations/catalog/social/tiktok.md) viene creato e gestito dal team TikTok.

Per i connettori creati e gestiti dal partner, ciò significa che potrebbe essere necessario risolvere i problemi con il connettore dal team partner (metodo di contatto fornito nella nota nella pagina della documentazione). Per i problemi relativi ai connettori creati e gestiti da Adobe, contatta il rappresentante dell’Adobe o l’Assistenza clienti.

## Destinazioni e controlli di accesso {#access-controls}

La funzionalità delle destinazioni in Platform funziona con le autorizzazioni di controllo degli accessi di Adobe Experience Platform. A seconda del livello di autorizzazione dell’utente, è possibile visualizzare, gestire e attivare le destinazioni. Per informazioni sulle singole autorizzazioni, consulta [Controllo degli accessi in Adobe Experience Platform](../access-control/home.md) e scorri verso il basso fino alla parte inferiore della pagina.

La tabella seguente illustra le autorizzazioni e le combinazioni di autorizzazioni necessarie per eseguire determinate azioni sulle destinazioni:

| Livello di autorizzazione | Descrizione |
| ---- | ---- |
| **[!UICONTROL Gestire le destinazioni]** | Per connettersi alle destinazioni, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). |
| **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** | Per attivare i tipi di pubblico nelle destinazioni e abilitare [passaggio di mappatura](ui/activate-batch-profile-destinations.md#mapping) del flusso di lavoro, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). |
| **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare i segmenti senza mappatura]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** | Per attivare il pubblico nelle destinazioni e nascondere [passaggio di mappatura](ui/activate-batch-profile-destinations.md#mapping) del flusso di lavoro, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare i segmenti senza mappatura]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). |
| **[!UICONTROL Visualizza grafico delle identità]** | Per esportare *identità* nelle destinazioni, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

Per ulteriori informazioni sui controlli di accesso, vedere [Guida utente al controllo degli accessi](../access-control/ui/overview.md).

### Controllo degli accessi basato su attributi per le destinazioni {#attribute-based-access}

Il controllo dell’accesso basato su attributi in Adobe Experience Platform consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi.

Con il controllo degli accessi basato su attributi, puoi applicare configurazioni di mappatura ai campi per i quali disponi delle autorizzazioni di. Inoltre, non è possibile esportare i dati in una destinazione se non si dispone dell’accesso a tutti i campi del set di dati.

Per ulteriori informazioni sul funzionamento delle destinazioni con i controlli di accesso basati su attributi, vedi [panoramica sul controllo degli accessi basato su attributi](../access-control/abac/overview.md#destinations).

## Controllo delle destinazioni {#destinations-monitoring}

Dopo aver stabilito una connessione a una destinazione e aver completato il flusso di lavoro di attivazione, puoi monitorare le esportazioni di dati nel sistema di ricezione. Leggi le [guida sul monitoraggio dei flussi di dati per le destinazioni nell’interfaccia utente](/help/dataflows/ui/monitor-destinations.md) per ulteriori informazioni.

Puoi anche verificare se i dati arrivano correttamente alla destinazione. La maggior parte delle pagine della documentazione di destinazione nel catalogo presenta un *Convalida sezione esportazione dati*, che indica come verificare nella piattaforma di destinazione che i dati siano stati correttamente importati da Experienci Platform.

## Restrizioni alla governance dei dati per l’attivazione dei dati nelle destinazioni {#data-governance}

La governance dei dati viene applicata alle destinazioni Platform tramite:

* *Azioni di marketing* che puoi selezionare nel flusso di lavoro crea destinazioni;
* *Criteri di utilizzo dati* che impediscono l’attivazione di dati contenenti determinate etichette di utilizzo in destinazioni con determinate azioni di marketing.

Per ulteriori informazioni su, consulta Governance dei dati nella documentazione di Platform. [azioni di marketing](../data-governance/policies/overview.md) e [risoluzione delle violazioni dei criteri per i dati](../data-governance/enforcement/auto-enforcement.md).

Per ulteriori informazioni sulla selezione delle azioni di marketing nel flusso di lavoro di creazione della destinazione, consulta le pagine seguenti per i diversi tipi di destinazione in Platform:

* [Destinazioni pubblicitarie - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Destinazioni pubblicitarie - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinazioni pubblicitarie - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Destinazioni di archiviazione cloud](./catalog/cloud-storage/overview.md)
* [Destinazioni di e-mail marketing](./catalog/email-marketing/overview.md)
* [Destinazioni social](./catalog/social/overview.md)

Per ulteriori informazioni sulle violazioni dei criteri per i dati nel flusso di lavoro di attivazione del pubblico, vedi **[!UICONTROL Revisione]** nelle seguenti guide:

* [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](./ui/activate-segment-streaming-destinations.md#review)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming](./ui/activate-streaming-profile-destinations.md#review)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](./ui/activate-batch-profile-destinations.md#review)
