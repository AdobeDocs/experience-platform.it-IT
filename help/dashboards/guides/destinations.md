---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;interfaccia utente;personalizzazione;dashboard profilo;dashboard dashboard
title: Dashboard delle destinazioni
description: Adobe Experience Platform fornisce un dashboard tramite il quale puoi visualizzare informazioni importanti sulle destinazioni attive della tua organizzazione.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 8571d86e1ce9dc894e54fe72dea75b9f8fe84f0b
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# [!UICONTROL Destinazioni] dashboard

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard attraverso la quale è possibile visualizzare informazioni importanti sulle destinazioni attive dell’organizzazione, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e lavorare con il dashboard delle destinazioni nell’interfaccia utente e fornisce ulteriori informazioni sulle metriche visualizzate nel dashboard.

Per una panoramica delle destinazioni e un catalogo di tutte le destinazioni disponibili all&#39;interno dell&#39;Experience Platform, visita [documentazione sulle destinazioni](../../destinations/home.md).

## [!UICONTROL Destinazioni] dati del dashboard {#destinations-dashboard-data}

La [!UICONTROL Destinazioni] nel dashboard viene visualizzata un’istantanea delle destinazioni abilitate dall’organizzazione in Experience Platform. I dati nello snapshot mostrano esattamente come vengono visualizzati nel momento specifico in cui è stata acquisita l&#39;istantanea. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard delle destinazioni non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplorazione del dashboard delle destinazioni

Per passare al dashboard delle destinazioni nell’interfaccia utente di Platform, seleziona **[!UICONTROL Destinazioni]** nella barra a sinistra, seleziona la **[!UICONTROL Panoramica]** per visualizzare il dashboard.

>[!NOTE]
>
>Se la tua organizzazione ha poca esperienza con Experience Platform e non dispone ancora di destinazioni attive, la [!UICONTROL Destinazioni] dashboard [!UICONTROL Panoramica] non sono visibili. Invece, selezionando [!UICONTROL Destinazioni] nel menu di navigazione a sinistra viene visualizzata la [!UICONTROL Catalogo] scheda . Per ulteriori informazioni sulle [!UICONTROL Catalogo] , fai riferimento alla [[!UICONTROL Destinazioni] guida all’area di lavoro](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Modifica del dashboard delle destinazioni

Puoi modificare l’aspetto del dashboard delle destinazioni selezionando **[!UICONTROL Modifica dashboard]**. Questo consente di spostare, aggiungere e rimuovere i widget dal dashboard e di accedere al **[!UICONTROL Libreria widget]** per esplorare i widget disponibili e creare widget personalizzati per la tua organizzazione.

Fai riferimento alla [modifica delle dashboard](../customize/modify.md) e [panoramica della libreria widget](../customize/widget-library.md) documentazione per ulteriori informazioni.

## Widget standard

Adobe fornisce diversi widget standard che puoi utilizzare per visualizzare diverse metriche correlate alle tue destinazioni. Puoi anche creare widget personalizzati da condividere con la tua organizzazione utilizzando [!UICONTROL Libreria widget]. Per ulteriori informazioni sulla creazione di widget personalizzati, si prega di iniziare leggendo [panoramica della libreria widget](../customize/widget-library.md).

Per ulteriori informazioni su ciascuno dei widget standard disponibili, seleziona il nome di un widget dal seguente elenco:

* [[!UICONTROL Destinazioni più utilizzate]](#most-used-destinations)
* [[!UICONTROL Destinazioni create di recente]](#recently-created-destinations)
* [[!UICONTROL Segmenti attivati di recente]](#recently-activated-segments)

### [!UICONTROL Destinazioni più utilizzate] {#most-used-destinations}

La **[!UICONTROL Destinazioni più utilizzate]** widget visualizza le principali destinazioni della tua organizzazione per numero di segmenti mappati, a partire dall&#39;ultima istantanea. Questa classificazione fornisce informazioni sulle destinazioni che vengono utilizzate, mostrando al contempo quelle che potrebbero essere sottoutilizzate.

Ad esempio, se hai configurato una destinazione ieri ma non hai mappato alcun segmento su di essa, puoi vedere che la destinazione è attualmente sottoutilizzata.

Il numero di segmenti mappati visualizzati nella colonna del conteggio dei segmenti è preciso a partire dall’ultima istantanea giornaliera. La mappatura di un nuovo segmento alla destinazione non aggiornerà il conteggio fino a quando non viene acquisita la successiva istantanea.

Selezionando il nome di una destinazione dall&#39;elenco mostrato sul widget, potrai accedere ai dettagli della destinazione come collegati dal **[!UICONTROL Sfoglia]** scheda . Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per passare al **[!UICONTROL Sfoglia]** , quindi seleziona il nome di una destinazione per visualizzarne i dettagli.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinazioni create di recente] {#recently-created-destinations}

La **[!UICONTROL Destinazioni create di recente]** widget consente di visualizzare un elenco delle destinazioni configurate più di recente della tua organizzazione.

La data di creazione mostrata corrisponde all’ultima istantanea giornaliera. In altre parole, se crei una nuova destinazione, questa verrà visualizzata nell’elenco solo dopo l’acquisizione dello snapshot successivo.

Selezionando il nome di una destinazione dall&#39;elenco mostrato sul widget, potrai accedere ai dettagli della destinazione come collegati dal **[!UICONTROL Sfoglia]** scheda . Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per passare al **[!UICONTROL Sfoglia]** , quindi seleziona il nome di una destinazione per visualizzarne i dettagli.

Per ulteriori informazioni su come configurare tipi specifici di destinazioni, visita il [documentazione sulle destinazioni](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segmenti attivati di recente] {#recently-activated-segments}

La **[!UICONTROL Segmenti attivati di recente]** widget fornisce un elenco dei segmenti mappati più di recente a una destinazione. Questo elenco fornisce un’istantanea dei segmenti e delle destinazioni attivamente utilizzati nel sistema e può essere utile per risolvere eventuali mappature errate.

La data aggiornata visualizzata visualizza l’ultima volta che il segmento è stato attivato nella destinazione ed è accurata dell’ultima istantanea giornaliera. In altre parole, se attivi un segmento nella destinazione, la data aggiornata non cambierà fino a quando non viene acquisita la successiva istantanea.

Selezionando il nome di un segmento dall’elenco visualizzato sul widget, passerai ai dettagli del segmento. Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per passare alla scheda di ricerca dei segmenti, quindi selezionare il nome di un segmento per visualizzarne i dettagli.

Per ulteriori informazioni sull’utilizzo dei segmenti in Experience Platform, inizia leggendo il [Panoramica del servizio di segmentazione](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard delle destinazioni e comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo delle destinazioni nell’Experience Platform, consulta [documentazione sulle destinazioni](../../destinations/home.md).
