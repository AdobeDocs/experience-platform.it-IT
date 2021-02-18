---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;interfaccia utente;interfaccia utente;personalizzazione;dashboard profilo;dashboard
title: Pannello Destinazioni
description: Adobe Experience Platform fornisce una dashboard attraverso la quale potete visualizzare informazioni importanti sulle destinazioni attive della vostra organizzazione.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---


# (Beta) [!UICONTROL Destinations] dashboard

>[!IMPORTANT]
>
>La funzionalità del dashboard descritta in questo documento è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

L&#39;interfaccia utente di Adobe Experience Platform (interfaccia utente) fornisce una dashboard attraverso la quale è possibile visualizzare informazioni importanti sulle destinazioni attive dell&#39;organizzazione, come acquisito durante uno snapshot giornaliero. Questa guida descrive come accedere e utilizzare il dashboard delle destinazioni nell&#39;interfaccia utente e fornisce ulteriori informazioni sulle metriche visualizzate nel dashboard.

Per una panoramica delle destinazioni, oltre a un catalogo di tutte le destinazioni disponibili all&#39;interno  Experience Platform, visitare la [panoramica delle destinazioni](../../destinations/home.md).

## [!UICONTROL Destinations] dati del dashboard  {#destinations-dashboard-data}

Il dashboard [!UICONTROL Destinations] visualizza un&#39;istantanea delle destinazioni abilitate dall&#39;organizzazione all&#39;interno del profilo esperienza. I dati nello snapshot mostrano esattamente come appaiono nel momento in cui è stata scattata l&#39;istantanea. In altre parole, l&#39;istantanea non è un&#39;approssimazione o un esempio dei dati e il dashboard delle destinazioni non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dopo l&#39;acquisizione dell&#39;istantanea non verranno visualizzati nel dashboard fino all&#39;acquisizione dell&#39;istantanea successiva.

## Esplorazione del dashboard delle destinazioni

Per passare al dashboard delle destinazioni nell&#39;interfaccia utente della piattaforma, seleziona **[!UICONTROL Destinations]** nella barra a sinistra, quindi seleziona la scheda **[!UICONTROL Overview]** per visualizzare il dashboard.

![](../images/destinations/dashboard-overview.png)

## widget disponibili

 Experience Platform fornisce più widget che potete utilizzare per visualizzare diverse metriche correlate alle vostre destinazioni. Seleziona il nome di un widget qui sotto per saperne di più:

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated segments]](#recently-activated-segments)

### [!UICONTROL Most used destinations] {#most-used-destinations}

Il widget **[!UICONTROL Most used destinations]** visualizza le principali destinazioni dell&#39;organizzazione per numero di segmenti mappati, a partire dall&#39;ultima istantanea. Questa classifica fornisce informazioni sulle destinazioni utilizzate, mostrando anche quelle che potrebbero essere sottoutilizzate.

Ad esempio, se hai configurato una destinazione ieri ma non hai mappato alcun segmento su di essa, potresti vedere che la destinazione è attualmente sottoutilizzata.

Il numero di segmenti mappati visualizzati nella colonna del conteggio dei segmenti è preciso a partire dall&#39;ultima istantanea giornaliera. La mappatura di un nuovo segmento alla destinazione non aggiornerà il conteggio fino a quando non viene scattata l&#39;istantanea successiva.

Selezionando il nome di una destinazione dall&#39;elenco visualizzato nel widget, potrete accedere ai dettagli di destinazione come collegati dalla scheda **[!UICONTROL Browse]**. È inoltre possibile selezionare **[!UICONTROL View All]** per passare alla scheda **[!UICONTROL Browse]**, quindi selezionare il nome di una destinazione per visualizzarne i dettagli.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

Il widget **[!UICONTROL Recently created destinations]** consente di visualizzare un elenco delle destinazioni configurate più di recente dall&#39;organizzazione.

La data di creazione mostrata è accurata rispetto all&#39;ultima istantanea giornaliera. In altre parole, se create una nuova destinazione, questa non verrà visualizzata nell&#39;elenco finché non viene scattata l&#39;istantanea successiva.

Selezionando il nome di una destinazione dall&#39;elenco visualizzato nel widget, potrete accedere ai dettagli di destinazione come collegati dalla scheda **[!UICONTROL Browse]**. È inoltre possibile selezionare **[!UICONTROL View All]** per passare alla scheda **[!UICONTROL Browse]**, quindi selezionare il nome di una destinazione per visualizzarne i dettagli.

Per ulteriori informazioni su come configurare tipi specifici di destinazioni, consultare la [documentazione delle destinazioni](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated segments] {#recently-activated-segments}

Il widget **[!UICONTROL Recently activated segments]** fornisce un elenco dei segmenti mappati più di recente a una destinazione. Questo elenco fornisce un&#39;istantanea dei segmenti e delle destinazioni attivamente utilizzati nel sistema e può aiutare a risolvere eventuali mappature errate.

La data aggiornata mostrata mostra l’ultima volta che il segmento è stato attivato nella destinazione ed è preciso rispetto all’ultima istantanea giornaliera. In altre parole, se si attiva un segmento nella destinazione, la data aggiornata non cambierà fino a quando non viene scattata l&#39;istantanea successiva.

Selezionando il nome di un segmento dall&#39;elenco visualizzato nel widget, potrai visualizzare i dettagli del segmento. Potete anche selezionare **[!UICONTROL View All]** per passare alla scheda di ricerca del segmento, quindi selezionare il nome di un segmento per visualizzarne i dettagli.

Per ulteriori informazioni sull&#39;utilizzo dei segmenti in  Experience Platform, leggere la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard delle destinazioni e comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull&#39;utilizzo delle destinazioni in  Experience Platform, fare riferimento alla [documentazione delle destinazioni](../../destinations/home.md).