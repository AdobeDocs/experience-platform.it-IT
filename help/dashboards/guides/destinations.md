---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;interfaccia utente;personalizzazione;dashboard profilo;dashboard dashboard
title: Dashboard delle destinazioni
description: Adobe Experience Platform fornisce un dashboard tramite il quale puoi visualizzare informazioni importanti sulle destinazioni attive della tua organizzazione.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# [!UICONTROL Dashboard delle destinazioni ] 

L’interfaccia utente di Adobe Experience Platform fornisce un dashboard tramite il quale è possibile visualizzare informazioni importanti sulle destinazioni attive dell’organizzazione, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e lavorare con il dashboard delle destinazioni nell’interfaccia utente e fornisce ulteriori informazioni sulle metriche visualizzate nel dashboard.

Per una panoramica delle destinazioni e un catalogo di tutte le destinazioni disponibili all&#39;interno dell&#39;Experience Platform, visita la [documentazione sulle destinazioni](../../destinations/home.md).

##  Destinazioni: dati dashboard  {#destinations-dashboard-data}

Il dashboard [!UICONTROL Destinazioni] visualizza un&#39;istantanea delle destinazioni abilitate dall&#39;organizzazione all&#39;interno di Profilo esperienza. I dati nello snapshot mostrano esattamente come vengono visualizzati nel momento specifico in cui è stata acquisita l&#39;istantanea. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard delle destinazioni non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplorazione del dashboard delle destinazioni

Per passare al dashboard delle destinazioni nell’interfaccia utente di Platform, seleziona **[!UICONTROL Destinazioni]** nella barra a sinistra, quindi seleziona la scheda **[!UICONTROL Panoramica]** per visualizzare il dashboard.

>[!NOTE]
>
>Se la tua organizzazione ha poca esperienza con Experience Platform e non dispone ancora di destinazioni attive, il dashboard [!UICONTROL Destinazioni] e la scheda [!UICONTROL Panoramica] non sono visibili. Invece, selezionando [!UICONTROL Destinazioni] dalla navigazione a sinistra viene visualizzata la scheda [!UICONTROL Catalogo] . Per ulteriori informazioni sulla scheda [!UICONTROL Catalogo], consulta la guida all’area di lavoro [[!UICONTROL Destinazioni]](../../destinations/ui/destinations-workspace.md) .

![](../images/destinations/dashboard-overview.png)

## Widget disponibili

Experience Platform fornisce più widget che puoi utilizzare per visualizzare diverse metriche correlate alle tue destinazioni. Seleziona il nome di un widget qui sotto per ulteriori informazioni:

* [[!UICONTROL Destinazioni più utilizzate]](#most-used-destinations)
* [[!UICONTROL Destinazioni create di recente]](#recently-created-destinations)
* [[!UICONTROL Segmenti attivati di recente]](#recently-activated-segments)

### [!UICONTROL Destinazioni più utilizzate] {#most-used-destinations}

Il widget **[!UICONTROL Destinazioni più utilizzate]** visualizza le destinazioni principali della tua organizzazione per numero di segmenti mappati, a partire dall&#39;ultima istantanea. Questa classificazione fornisce informazioni sulle destinazioni che vengono utilizzate, mostrando al contempo quelle che potrebbero essere sottoutilizzate.

Ad esempio, se hai configurato una destinazione ieri ma non hai mappato alcun segmento su di essa, puoi vedere che la destinazione è attualmente sottoutilizzata.

Il numero di segmenti mappati visualizzati nella colonna del conteggio dei segmenti è preciso a partire dall’ultima istantanea giornaliera. La mappatura di un nuovo segmento alla destinazione non aggiornerà il conteggio fino a quando non viene acquisita la successiva istantanea.

Selezionando il nome di una destinazione dall&#39;elenco visualizzato sul widget, potrai accedere ai dettagli della destinazione come collegati dalla scheda **[!UICONTROL Sfoglia]** . È inoltre possibile selezionare **[!UICONTROL Visualizza tutto]** per passare alla scheda **[!UICONTROL Sfoglia]** e quindi selezionare il nome di una destinazione per visualizzarne i dettagli.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinazioni create di recente] {#recently-created-destinations}

Il widget **[!UICONTROL Destinazioni create di recente]** consente di visualizzare un elenco delle destinazioni configurate più di recente della tua organizzazione.

La data di creazione mostrata corrisponde all’ultima istantanea giornaliera. In altre parole, se crei una nuova destinazione, questa verrà visualizzata nell’elenco solo dopo l’acquisizione dello snapshot successivo.

Selezionando il nome di una destinazione dall&#39;elenco visualizzato sul widget, potrai accedere ai dettagli della destinazione come collegati dalla scheda **[!UICONTROL Sfoglia]** . È inoltre possibile selezionare **[!UICONTROL Visualizza tutto]** per passare alla scheda **[!UICONTROL Sfoglia]** e quindi selezionare il nome di una destinazione per visualizzarne i dettagli.

Per ulteriori informazioni su come configurare tipi specifici di destinazioni, consulta la [documentazione sulle destinazioni](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segmenti attivati di recente] {#recently-activated-segments}

Il widget **[!UICONTROL Segmenti attivati di recente]** fornisce un elenco dei segmenti mappati più di recente a una destinazione. Questo elenco fornisce un’istantanea dei segmenti e delle destinazioni attivamente utilizzati nel sistema e può essere utile per risolvere eventuali mappature errate.

La data aggiornata visualizzata visualizza l’ultima volta che il segmento è stato attivato nella destinazione ed è accurata dell’ultima istantanea giornaliera. In altre parole, se attivi un segmento nella destinazione, la data aggiornata non cambierà fino a quando non viene acquisita la successiva istantanea.

Selezionando il nome di un segmento dall’elenco visualizzato sul widget, passerai ai dettagli del segmento. Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per accedere alla scheda di ricerca dei segmenti e quindi selezionare il nome di un segmento per visualizzarne i dettagli.

Per ulteriori informazioni sull&#39;utilizzo dei segmenti in Experience Platform, inizia leggendo la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard delle destinazioni e comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull&#39;utilizzo delle destinazioni nell&#39;Experience Platform, consulta la [documentazione sulle destinazioni](../../destinations/home.md).
