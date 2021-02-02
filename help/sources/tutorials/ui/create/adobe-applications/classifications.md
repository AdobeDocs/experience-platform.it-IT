---
keywords: ' Experience Platform;casa;argomenti popolari; analytics;classificazioni'
description: Questa esercitazione fornisce i passaggi per creare un connettore dati di classificazione Adobe Analytics  nell'interfaccia utente per trasferire i dati di classificazione in Adobe Experience Platform.
solution: Experience Platform
title: Creare un connettore dati di classificazione Adobe Analytics  nell'interfaccia utente
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Creare un connettore dati di classificazione Adobe Analytics  nell&#39;interfaccia utente

Questa esercitazione fornisce i passaggi per creare un connettore dati di classificazione Adobe Analytics  nell&#39;interfaccia utente per trasferire i dati di classificazione in Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Il Connettore dati classificazione di Analytics richiede che i dati siano stati migrati nella nuova infrastruttura [!DNL Classifications] di  Adobe Analytics prima dell&#39;uso. Per confermare lo stato di migrazione dei tuoi dati, contatta il tuo Customer Success Manager  Adobe.

## Seleziona le classificazioni

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro delle origini. Nella schermata **[!UICONTROL Catalog]** sono visualizzate le sorgenti disponibili con cui creare connessioni in ingresso. Ogni scheda di origine mostra un&#39;opzione per configurare un nuovo account o aggiungere dati a un account esistente.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Nella categoria **[!UICONTROL Adobe applications]**, selezionate la scheda **[!UICONTROL Adobe Analytics]**, quindi selezionate **[!UICONTROL Add data]** per iniziare a lavorare con i dati di classificazione di Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

Viene visualizzato il passaggio **[!UICONTROL Analytics source add data]**. Seleziona **[!UICONTROL Classifications]** dall&#39;intestazione superiore per visualizzare un elenco dei [!DNL Classifications] set di dati, con informazioni sull&#39;ID dimensione, il nome della suite di rapporti e l&#39;ID della suite di rapporti.

Ogni pagina mostra fino a dieci diversi [!DNL Classifications] set di dati tra cui è possibile scegliere. Selezionate **[!UICONTROL Next]** nella parte inferiore della pagina per individuare ulteriori opzioni. Il pannello a destra mostra il numero totale di [!DNL Classifications] set di dati selezionati e i relativi nomi. Questo pannello consente inoltre di rimuovere tutti i set di dati [!DNL Classifications] eventualmente selezionati per errore o di cancellare tutte le selezioni con una sola azione.

È possibile selezionare fino a 30 set di dati [!DNL Classifications] diversi da inserire in [!DNL Platform].

Dopo aver selezionato i set di dati [!DNL Classifications], selezionare **[!UICONTROL Next]** in alto a destra nella pagina.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Verifica le classificazioni

Viene visualizzato il passaggio **[!UICONTROL Review]**, che consente di controllare i set di dati [!DNL Classifications] selezionati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connection]**: Mostra la piattaforma di origine e lo stato della connessione.
* **[!UICONTROL Data type]**: Mostra il numero di persone selezionate  [!DNL Classifications].
* **[!UICONTROL Scheduling]**: Mostra la frequenza della sincronizzazione per  [!DNL Classifications] i dati.

Dopo aver rivisto il flusso di dati, fate clic su **[!UICONTROL Finish]** e lasciate che sia possibile creare il flusso di dati.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorare il flusso di dati delle classificazioni

Una volta creato il flusso di dati, potete monitorare i dati che vengono acquisiti tramite di esso. Dalla schermata **[!UICONTROL Catalog]**, selezionare **[!UICONTROL Dataflows]** per visualizzare un elenco dei flussi definiti associati all&#39;account [!DNL Classifications].

![](../../../../images/tutorials/create/classifications/dataflows.png)

Viene visualizzata la schermata **[!UICONTROL Dataflows]**. In questa pagina è presente un elenco di flussi di dati, con informazioni sul nome, i dati di origine e lo stato di esecuzione del flusso di dati. Sulla destra, c&#39;è il pannello **[!UICONTROL Properties]** che contiene i metadati relativi al flusso di dati [!DNL Classifications].

Selezionare la **[!UICONTROL Target dataset]** a cui si desidera accedere.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

Nella pagina **[!UICONTROL Dataset activity]** sono visualizzate informazioni sul set di dati di destinazione selezionato, inclusi dettagli sullo stato del batch, l&#39;ID del set di dati e lo schema.

>[!IMPORTANT]
>
>Anche se è possibile eliminare i set di dati per altri connettori di origine, al momento non è supportato per il connettore dati di classificazione di Analytics. Se elimini un dataset per errore, contatta  Assistenza clienti di Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore dati di classificazione di Analytics che porta i dati [!DNL Classifications] in [!DNL Platform]. Per ulteriori informazioni sui dati di [!DNL Analytics] e [!DNL Classifications] vedi i documenti seguenti:

* [Panoramica del connettore dati di Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Creare un connettore dati di Analytics nell&#39;interfaccia utente](./analytics.md)
* [Informazioni sulle classificazioni](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)