---
keywords: Experience Platform;home;argomenti popolari;connettore sorgente di Audience Manager;Audience Manager;connettore di audience manager
solution: Experience Platform
title: Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per creare connettori sorgente per Adobe Audience Manager per l’immissione di dati di eventi di esperienza di consumo in Platform tramite l’interfaccia utente di .
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente per Adobe Audience Manager per l’inserimento dei dati relativi all’evento esperienza di consumo in Platform tramite l’interfaccia utente di .

## Creare una connessione sorgente con Adobe Audience Manager

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse origini per le quali è possibile creare un account.

Sotto la categoria [!UICONTROL Adobe applications], selezionare **[!UICONTROL Adobe Audience Manager]**, quindi selezionare **[!UICONTROL Configure]**.

![catalogo](../../../../images/tutorials/create/aam/catalog.png)

Viene visualizzato il passaggio [!UICONTROL Select traits and segments] , che fornisce un’interfaccia interattiva per esplorare e selezionare caratteristiche, segmenti e dati.

* Il pannello a sinistra dell’interfaccia contiene le opzioni [!UICONTROL Select traits and segments] e una directory gerarchica di tutti i segmenti disponibili.
* La metà destra dell’interfaccia ti consente di interagire con i segmenti selezionati e di selezionare i dati specifici che desideri utilizzare.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Per spostarsi tra i segmenti disponibili, seleziona la cartella a cui desideri accedere dal pannello [!UICONTROL All Segments] . La selezione di una cartella consente di scorrere la gerarchia di una cartella e fornisce un elenco di segmenti da filtrare.

![cartella dei segmenti](../../../../images/tutorials/create/aam/segment-folder.png)

Dopo aver identificato e selezionato i segmenti da utilizzare, viene visualizzato un nuovo pannello a destra, che mostra l’elenco degli elementi selezionati. Puoi continuare ad accedere a cartelle diverse e selezionare segmenti diversi per la connessione. Selezionando altri segmenti, il pannello a destra viene aggiornato.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

In alternativa, è possibile selezionare le caselle **[!UICONTROL Select all segments]** e **[!UICONTROL Select all traits]** . Selezionando tutti i segmenti, Platform visualizzerà i segmenti di Audience Manager, mentre selezionando tutte le caratteristiche abilita tutte le caratteristiche di prime parti dall’Audience Manager.

Al termine, seleziona **[!UICONTROL Next]**

![tutti i segmenti](../../../../images/tutorials/create/aam/all-segments.png)

Viene visualizzato il passaggio [!UICONTROL Review] , che consente di rivedere le caratteristiche e i segmenti selezionati prima che siano collegati a Platform. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connection]**: Mostra la piattaforma di origine e lo stato della connessione.
* **[!UICONTROL Selected data]**: Mostra il numero di segmenti selezionati e caratteristiche abilitate.

![revisione](../../../../images/tutorials/create/aam/review.png)

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Finish]** e consenti la creazione del flusso di dati.

## Passaggi successivi

Mentre un flusso di dati di Audience Manager è attivo, i dati in arrivo vengono automaticamente assimilati in profili cliente in tempo reale. Ora puoi utilizzare questi dati in arrivo e creare segmenti di pubblico utilizzando il servizio di segmentazione della piattaforma. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del profilo cliente in tempo reale](../../../../../profile/home.md)
* [Panoramica del servizio di segmentazione](../../../../../segmentation/home.md)
