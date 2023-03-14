---
keywords: attivare destinazioni;attivare dati
title: Panoramica di Activation
type: Tutorial
description: Scopri come attivare i dati sul pubblico disponibili in Adobe Experience Platform per vari tipi di destinazioni.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Panoramica di Activation

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Adobe Experience Platform supporta un’ampia gamma di destinazioni. Il flusso di lavoro di attivazione del pubblico varia tra le destinazioni in base al tipo di dati del pubblico supportati e alla frequenza di esportazione dei dati.

## Metodi di attivazione {#activation-methods}

Dopo di te [configurare la destinazione](connect-destination.md), puoi attivare i segmenti di pubblico in diversi modi:

### Attiva i tipi di pubblico dal catalogo delle destinazioni

Per informazioni dettagliate sull’attivazione dei tipi di pubblico nella destinazione dal catalogo delle destinazioni, consulta le seguenti guide:

* [Attiva i dati del pubblico nelle destinazioni di esportazione di segmenti di streaming](activate-segment-streaming-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming](activate-streaming-profile-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](activate-batch-profile-destinations.md)

### Attiva i tipi di pubblico da [!UICONTROL Sfoglia] pagina

Segui i passaggi seguenti per attivare i dati nelle destinazioni da **[!UICONTROL Sfoglia]** pagina.

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, e seleziona la **[!UICONTROL Sfoglia]** scheda.

   ![Scheda Sfoglia](../assets/ui/activation-overview/browse-tab.png)

1. Trova la connessione di destinazione che desideri utilizzare per attivare i segmenti, seleziona i tre punti nella sezione [!UICONTROL Nome] , quindi seleziona **[!UICONTROL Attivare segmenti]**.

   ![Pulsante Attiva segmenti](../assets/ui/activation-overview/activate-segments.png)

1. A seconda della destinazione selezionata, segui i passaggi descritti negli articoli seguenti, iniziando con **[!UICONTROL Seleziona segmenti]** per completare il flusso di lavoro di attivazione:

   * [Attiva i dati del pubblico nelle destinazioni di esportazione di segmenti di streaming](activate-segment-streaming-destinations.md)
   * [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming](activate-streaming-profile-destinations.md)
   * [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](activate-batch-profile-destinations.md)

### Attiva i tipi di pubblico dalla pagina dei dettagli del segmento {#activate-segment-details}

Puoi attivare i segmenti nelle destinazioni dalla pagina dei dettagli dei segmenti. Consulta [Dettagli del segmento](../../segmentation/ui/overview.md#segment-details) per ulteriori informazioni.

A seconda della destinazione selezionata, segui i passaggi descritti negli articoli seguenti per completare il flusso di lavoro di attivazione:

* [Attiva i dati del pubblico nelle destinazioni di esportazione di segmenti di streaming](activate-segment-streaming-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming](activate-streaming-profile-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](activate-batch-profile-destinations.md)
