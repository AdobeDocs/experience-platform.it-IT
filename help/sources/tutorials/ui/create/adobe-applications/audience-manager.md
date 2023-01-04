---
keywords: Experience Platform;home;argomenti popolari;connettore sorgente di Audience Manager;Audience Manager;connettore di audience manager
title: Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente
description: Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente per Adobe Audience Manager che consenta di inserire i dati relativi all’evento esperienza di consumo in Platform utilizzando l’interfaccia utente di .
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente per Adobe Audience Manager per l’inserimento dei dati relativi all’evento esperienza di consumo in Platform tramite l’interfaccia utente di .

## Creare una connessione sorgente con Adobe Audience Manager

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto [!UICONTROL Applicazione Adobe], seleziona **[!UICONTROL Adobe Audience Manager]** quindi seleziona **[!UICONTROL Configurazione]**.

![catalogo](../../../../images/tutorials/create/aam/catalog.png)

### Selezionare caratteristiche e segmenti

>[!NOTE]
>
>Non è possibile acquisire dati regionali dall’origine Audience Manager all’Experience Platform. Se hai casi d’uso di Analytics che richiedono dati regionali, utilizza la [Connettore sorgente di Analytics](../adobe-applications/analytics.md).

La [!UICONTROL Selezionare caratteristiche e segmenti] viene visualizzato un passaggio che fornisce un’interfaccia interattiva per esplorare e selezionare caratteristiche, segmenti e dati.

* Il pannello a sinistra dell’interfaccia contiene [!UICONTROL Selezionare caratteristiche e segmenti] , nonché una directory gerarchica di tutti i segmenti disponibili.
* La metà destra dell’interfaccia ti consente di interagire con i segmenti selezionati e di selezionare i dati specifici che desideri utilizzare.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Per spostarsi tra i segmenti disponibili, seleziona la cartella a cui desideri accedere dal [!UICONTROL Tutti i segmenti] pannello. La selezione di una cartella consente di scorrere la gerarchia di una cartella e fornisce un elenco di segmenti da filtrare.

![cartella dei segmenti](../../../../images/tutorials/create/aam/segment-folder.png)

Dopo aver identificato e selezionato i segmenti da utilizzare, viene visualizzato un nuovo pannello a destra, che mostra l’elenco degli elementi selezionati. Puoi continuare ad accedere a cartelle diverse e selezionare segmenti diversi per la connessione. Selezionando altri segmenti, il pannello a destra viene aggiornato.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

In alternativa, puoi selezionare la **[!UICONTROL Seleziona tutti i segmenti]** e **[!UICONTROL Seleziona tutte le caratteristiche]** scatole. Selezionando tutti i segmenti, Platform visualizzerà i segmenti di Audience Manager, mentre selezionando tutte le caratteristiche abilita tutte le caratteristiche di prime parti dall’Audience Manager.

>[!WARNING]
>
>L’acquisizione di popolazioni di segmenti di Audience Manager di grandi dimensioni ha un impatto diretto sul conteggio totale dei profili quando invii per la prima volta un segmento di Audience Manager a Platform utilizzando l’origine di Audience Manager. Ciò significa che la selezione di tutti i segmenti può potenzialmente portare a un conteggio di profili superiore all’adesione all’utilizzo della licenza. Controlla la tua [quota di utilizzo della licenza](../../../../../dashboards/guides/license-usage.md) prima di procedere.

Al termine, seleziona **[!UICONTROL Successivo]**

![tutti i segmenti](../../../../images/tutorials/create/aam/all-segments.png)

La [!UICONTROL Revisione] viene visualizzato un passaggio che ti consente di rivedere le caratteristiche e i segmenti selezionati prima che siano collegati a Platform. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: Mostra la piattaforma di origine e lo stato della connessione.
* **[!UICONTROL Dati selezionati]**: Mostra il numero di segmenti selezionati e caratteristiche abilitate.

![revisione](../../../../images/tutorials/create/aam/review.png)

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un certo tempo per la creazione del flusso di dati.

## Passaggi successivi

Mentre un flusso di dati di Audience Manager è attivo, i dati in arrivo vengono automaticamente assimilati in profili cliente in tempo reale. Ora puoi utilizzare questi dati in arrivo e creare segmenti di pubblico utilizzando il servizio di segmentazione della piattaforma. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del profilo cliente in tempo reale](../../../../../profile/home.md)
* [Panoramica del servizio di segmentazione](../../../../../segmentation/home.md)
