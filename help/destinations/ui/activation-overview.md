---
keywords: attivare destinazioni;attivare dati
title: Panoramica di Activation
type: Tutorial
description: Scopri come attivare i dati del pubblico in Adobe Experience Platform a vari tipi di destinazioni.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Panoramica di Activation

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Adobe Experience Platform supporta un’ampia gamma di destinazioni. Il flusso di lavoro di attivazione del pubblico varia a seconda delle destinazioni, in base al tipo di dati del pubblico che supportano e alla frequenza dell’esportazione dei dati.

## Metodi di attivazione {#activation-methods}

Dopo [configurare la destinazione](connect-destination.md), puoi attivare i segmenti di pubblico in diversi modi:

### Attivare i tipi di pubblico dal catalogo delle destinazioni

Consulta le seguenti guide per informazioni dettagliate sull’attivazione dei tipi di pubblico nella destinazione dal catalogo delle destinazioni:

* [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](activate-segment-streaming-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](activate-streaming-profile-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](activate-batch-profile-destinations.md)

### Attiva i tipi di pubblico dalla [!UICONTROL Sfoglia] page

Segui i passaggi riportati di seguito per attivare i dati sulle destinazioni dal **[!UICONTROL Sfoglia]** pagina.

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, quindi seleziona la **[!UICONTROL Sfoglia]** scheda .

   ![Scheda Sfoglia](../assets/ui/activation-overview/browse-tab.png)

1. Trova la connessione di destinazione che desideri utilizzare per attivare i segmenti, seleziona i tre punti nella [!UICONTROL Nome] , quindi seleziona **[!UICONTROL Attivare i segmenti]**.

   ![Pulsante Attiva segmenti](../assets/ui/activation-overview/activate-segments.png)

1. A seconda della destinazione selezionata, segui i passaggi descritti negli articoli seguenti, iniziando con **[!UICONTROL Selezionare segmenti]** per completare il flusso di lavoro di attivazione:

   * [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](activate-segment-streaming-destinations.md)
   * [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](activate-streaming-profile-destinations.md)
   * [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](activate-batch-profile-destinations.md)

### Attivare i tipi di pubblico dalla pagina dei dettagli del segmento {#activate-segment-details}

Puoi attivare i segmenti nelle destinazioni dalla pagina dei dettagli del segmento. Vedi [Dettagli del segmento](../../segmentation/ui/overview.md#segment-details) per ulteriori informazioni.

A seconda della destinazione selezionata, segui i passaggi descritti negli articoli seguenti per completare il flusso di lavoro di attivazione:

* [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](activate-segment-streaming-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](activate-streaming-profile-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](activate-batch-profile-destinations.md)
