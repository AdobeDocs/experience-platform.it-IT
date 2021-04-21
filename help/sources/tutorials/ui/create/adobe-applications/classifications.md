---
keywords: Experience Platform;home;argomenti popolari; analytics;classificazioni
description: Scopri come creare un connettore sorgente Adobe Analytics nell’interfaccia utente per inserire i dati delle classificazioni in Adobe Experience Platform.
solution: Experience Platform
title: Creare una connessione sorgente Adobe Analytics per i dati delle classificazioni nell’interfaccia utente
topic-legacy: overview
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# Creare una connessione sorgente Adobe Analytics per i dati di classificazione nell’interfaccia utente

Questa esercitazione fornisce passaggi per creare una connessione all’origine dati Adobe Analytics Classifications nell’interfaccia utente per inserire i dati delle classificazioni in Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Il Connettore dati delle classificazioni di Analytics richiede che i dati siano stati migrati alla nuova infrastruttura [!DNL Classifications] di Adobe Analytics prima dell’utilizzo. Per confermare lo stato di migrazione dei dati, contatta il tuo Adobe Customer Success Manager.

## Seleziona le classificazioni

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro origini. La schermata **[!UICONTROL Catalog]** visualizza le sorgenti disponibili con cui creare connessioni in entrata. Ogni scheda sorgente mostra un&#39;opzione per configurare un nuovo account o aggiungere dati a un account esistente.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Adobe applications]** , seleziona la scheda **[!UICONTROL Adobe Analytics]** e seleziona **[!UICONTROL Add data]** per iniziare a lavorare con i dati delle classificazioni di Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

Viene visualizzato il passaggio **[!UICONTROL Analytics source add data]** . Seleziona **[!UICONTROL Classifications]** dall’intestazione superiore per visualizzare un elenco di [!DNL Classifications] set di dati, con informazioni sull’ID dimensione, il nome della suite di rapporti e l’ID della suite di rapporti.

Ogni pagina mostra fino a dieci diversi set di dati [!DNL Classifications] tra cui puoi scegliere. Seleziona **[!UICONTROL Next]** nella parte inferiore della pagina per cercare altre opzioni. Il pannello a destra mostra il numero totale di set di dati [!DNL Classifications] selezionati e i relativi nomi. Questo pannello consente inoltre di rimuovere eventuali set di dati [!DNL Classifications] selezionati per errore o di cancellare tutte le selezioni con una sola azione.

Puoi selezionare fino a 30 diversi set di dati [!DNL Classifications] da inserire in [!DNL Platform].

Dopo aver selezionato i set di dati [!DNL Classifications], seleziona **[!UICONTROL Next]** in alto a destra nella pagina.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Esamina le classificazioni

Viene visualizzato il passaggio **[!UICONTROL Review]** che consente di rivedere i set di dati [!DNL Classifications] selezionati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connection]**: Mostra la piattaforma di origine e lo stato della connessione.
* **[!UICONTROL Data type]**: Mostra il numero di selezionati  [!DNL Classifications].
* **[!UICONTROL Scheduling]**: Mostra la frequenza di sincronizzazione dei  [!DNL Classifications] dati.

Dopo aver esaminato il flusso di dati, fai clic su **[!UICONTROL Finish]** e consenti la creazione del flusso di dati.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitora il flusso di dati delle classificazioni

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso. Dalla schermata **[!UICONTROL Catalog]** , seleziona **[!UICONTROL Dataflows]** per visualizzare un elenco dei flussi stabiliti associati all’account [!DNL Classifications].

![](../../../../images/tutorials/create/classifications/dataflows.png)

Viene visualizzata la schermata **[!UICONTROL Dataflows]**. In questa pagina è riportato un elenco di flussi di dati, con informazioni sul nome, i dati di origine e lo stato di esecuzione del flusso di dati. A destra c&#39;è il pannello **[!UICONTROL Properties]** che contiene i metadati relativi al flusso di dati [!DNL Classifications].

Seleziona il **[!UICONTROL Target dataset]** a cui desideri accedere.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

La pagina **[!UICONTROL Dataset activity]** visualizza informazioni sul set di dati di destinazione selezionato, inclusi dettagli sullo stato batch, l’ID del set di dati e lo schema.

>[!IMPORTANT]
>
>Mentre l’eliminazione dei set di dati è possibile per altri connettori di origine, al momento non è supportata per il connettore dati di classificazione di Analytics. Se elimini un set di dati per errore, contatta l’Assistenza clienti Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore dati delle classificazioni di Analytics che porta i dati [!DNL Classifications] in [!DNL Platform]. Per ulteriori informazioni sui dati di [!DNL Analytics] e [!DNL Classifications], consulta i seguenti documenti:

* [Panoramica del connettore dati di Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Creare una connessione dati di Analytics nell’interfaccia utente](./analytics.md)
* [Informazioni sulle classificazioni](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
