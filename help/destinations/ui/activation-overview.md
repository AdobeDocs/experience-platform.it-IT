---
keywords: attivare destinazioni;attivare dati
title: Panoramica di Activation
type: Tutorial
description: Scopri come attivare i tipi di pubblico disponibili in Adobe Experience Platform per vari tipi di destinazioni.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# Panoramica di Activation

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Adobe Experience Platform supporta un’ampia gamma di destinazioni. Il flusso di lavoro di attivazione del pubblico varia tra le destinazioni in base al tipo di dati del pubblico supportati e alla frequenza di esportazione dei dati.

## Metodi di attivazione {#activation-methods}

Dopo aver [configurato la destinazione](connect-destination.md), puoi attivare i tipi di pubblico in più modi:

### Attiva i tipi di pubblico dal catalogo delle destinazioni

Per informazioni dettagliate sull’attivazione dei tipi di pubblico nella destinazione dal catalogo delle destinazioni, consulta le seguenti guide:

* [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](activate-segment-streaming-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming](activate-streaming-profile-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](activate-batch-profile-destinations.md)

### Attiva il pubblico dalla pagina [!UICONTROL Sfoglia]

Segui i passaggi seguenti per attivare i dati nelle tue destinazioni dalla pagina **[!UICONTROL Sfoglia]**.

1. Vai a **[!UICONTROL Connessioni > Destinazioni]** e seleziona la scheda **[!UICONTROL Sfoglia]**.

   ![Sfoglia scheda](../assets/ui/activation-overview/browse-tab.png)

1. Trova la connessione di destinazione da utilizzare per attivare i segmenti, seleziona i tre punti nella colonna [!UICONTROL Nome], quindi seleziona **[!UICONTROL Attiva pubblico]**.

   ![Pulsante Attiva pubblico](../assets/ui/activation-overview/activate-segments.png)

1. A seconda della destinazione selezionata, segui i passaggi descritti negli articoli seguenti, a partire dal passaggio **[!UICONTROL Seleziona segmenti]**, per completare il flusso di lavoro di attivazione:

   * [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](activate-segment-streaming-destinations.md)
   * [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming](activate-streaming-profile-destinations.md)
   * [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](activate-batch-profile-destinations.md)

### Attiva i tipi di pubblico dalla pagina dei dettagli del pubblico {#activate-audience-details}

Puoi attivare i tipi di pubblico nelle destinazioni dalla pagina dei dettagli del pubblico. Per ulteriori informazioni, consulta [Dettagli pubblico](../../segmentation/ui/audience-portal.md#audience-details).

A seconda della destinazione selezionata, segui i passaggi descritti negli articoli seguenti per completare il flusso di lavoro di attivazione:

* [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](activate-segment-streaming-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo di streaming](activate-streaming-profile-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](activate-batch-profile-destinations.md)
