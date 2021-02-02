---
keywords: ' Experience Platform;home;argomenti popolari;Audience Manager connettore origine; Audience Manager;Audience Manager connettore'
solution: Experience Platform
title: Creare un connettore sorgente Adobe Audience Manager nell’interfaccia utente
topic: overview
type: Tutorial
description: Questa esercitazione illustra i passaggi necessari per creare un connettore sorgente che consenta ad Adobe Audience Manager di inserire i dati dell'evento Consumer Experience Event nella piattaforma utilizzando l'interfaccia utente.
translation-type: tm+mt
source-git-commit: bdf95d75bf8db9f3438011f298d17c4259d2c63c
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# Creare un connettore sorgente Adobe Audience Manager nell’interfaccia utente

Questa esercitazione illustra i passaggi necessari per creare un connettore di origine per Adobe Audience Manager che consenta di inserire i dati dell&#39;evento di esperienza del consumatore nella piattaforma utilizzando l&#39;interfaccia utente.

## Creare una connessione di origine con Adobe Audience Manager

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Sotto la categoria [!UICONTROL Adobe applications], selezionare **[!UICONTROL Adobe Audience Manager]**, quindi selezionare **[!UICONTROL Configure]**.

![catalogo](../../../../images/tutorials/create/aam/catalog.png)

Viene visualizzato il passaggio [!UICONTROL Select traits and segments], che fornisce un&#39;interfaccia interattiva per esplorare e selezionare le caratteristiche, i segmenti e i dati.

* Il pannello sinistro dell&#39;interfaccia contiene le opzioni [!UICONTROL Select traits and segments], nonché una directory gerarchica di tutti i segmenti disponibili.
* La metà destra dell&#39;interfaccia consente di interagire con i segmenti selezionati e di selezionare i dati specifici che si desidera utilizzare.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Per spostarsi tra i segmenti disponibili, selezionate la cartella a cui desiderate accedere dal pannello [!UICONTROL All Segments]. La selezione di una cartella consente di scorrere la gerarchia di una cartella e fornisce un elenco di segmenti da filtrare.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Dopo aver identificato e selezionato i segmenti da utilizzare, viene visualizzato un nuovo pannello a destra con l’elenco degli elementi selezionati. Puoi continuare ad accedere a cartelle diverse e selezionare diversi segmenti per la connessione. Selezionando altri segmenti, il pannello si aggiorna a destra.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

In alternativa, è possibile selezionare le caselle **[!UICONTROL Select all segments]** e **[!UICONTROL Select all traits]**. Selezionando tutti i segmenti,  segmenti di Audience Manager verrà portato su Piattaforma, mentre selezionando tutte le caratteristiche, tutte le caratteristiche di prime parti verranno abilitate da  Audience Manager.

Al termine, selezionare **[!UICONTROL Next]**

![tutti i segmenti](../../../../images/tutorials/create/aam/all-segments.png)

Viene visualizzato il passaggio [!UICONTROL Review], che consente di esaminare le caratteristiche e i segmenti selezionati prima che siano collegati alla piattaforma. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connection]**: Mostra la piattaforma di origine e lo stato della connessione.
* **[!UICONTROL Selected data]**: Mostra il numero di segmenti selezionati e caratteristiche abilitate.

![review](../../../../images/tutorials/create/aam/review.png)

Dopo aver controllato il flusso di dati, selezionare **[!UICONTROL Finish]** e concedere un po&#39; di tempo per la creazione del flusso di dati.

## Passaggi successivi

Mentre è attivo un flusso di dati  Audience Manager, i dati in arrivo vengono automaticamente assimilati nei profili cliente in tempo reale. Ora puoi utilizzare questi dati in arrivo e creare segmenti di pubblico tramite il servizio di segmentazione della piattaforma. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](../../../../../profile/home.md)
* [Panoramica del servizio di segmentazione](../../../../../segmentation/home.md)