---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente Adobe Analytics nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Creare un connettore sorgente Adobe Analytics nell’interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente Adobe Analytics nell&#39;interfaccia utente, al fine di inserire i dati di consumo in Adobe Experience Platform.

## Creare una connessione di origine con Adobe Analytics

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro delle origini. Nella schermata *Catalogo* sono visualizzate le sorgenti disponibili con cui creare connessioni in-bound e ciascuna sorgente mostra il numero di connessioni esistenti ad esse associate. Selezionate l&#39;opzione per **Adobe Analytics** , quindi fate clic su **Visualizza origine** per vedere tutte le connessioni in-bound stabilite.

![](../../../../images/tutorials/create/analytics/AA-sources_catalog.png)

Nella schermata Attività *di* origine sono elencate tutte le connessioni precedentemente stabilite ad Adobe Analytics. Per creare una nuova connessione, fai clic su **Seleziona dati**.

>[!NOTE] È possibile creare più connessioni in-bound a un&#39;origine per l&#39;inclusione di dati diversi.

![](../../../..//images/tutorials/create/analytics/AA-source_activity.png)

Nell&#39;elenco delle suite di rapporti disponibili, seleziona quella che desideri portare in Piattaforma e fai clic su **Avanti**.

>[!NOTE] È possibile selezionare una sola suite di rapporti per ogni connessione di origine Analytics. Inoltre, una sola suite di rapporti può esistere solo in una sandbox.

![](../../../../images/tutorials/create/analytics/AA-select_data.png)

Viene visualizzato il passaggio *Rivedi* , che consente di rivedere la nuova connessione in-bound di Analytics prima che venga creata. I dettagli della connessione sono raggruppati per categorie, tra cui:

* *Dettagli* origine: Mostra il tipo di connessione di origine e la suite di rapporti selezionata.
* *Dettagli* di destinazione: Quando si creano altri connettori di origine, questo contenitore mostra in quale set di dati di origine vengono acquisiti i dati, incluso lo schema a cui il dataset aderisce. I dati di Analytics vengono mappati automaticamente e assimilati in profili cliente in tempo reale.

![](../../../../images/tutorials/create/analytics/AA-review.png)

## Passaggi successivi

Una volta creata la connessione, viene automaticamente creato uno schema di destinazione e un dataset che contiene i dati in arrivo. Inoltre, si verifica il recupero dei dati e vengono acquisiti fino a 13 mesi di dati storici. Al termine dell&#39;assimilazione iniziale, i dati di Analytics vengono utilizzati dai servizi della piattaforma a valle, quali Real-time Customer Profile e Segmentation Service. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](../../../../../profile/home.md)
* [Panoramica del servizio di segmentazione](../../../../../segmentation/home.md)
* [Panoramica di Analysis Workspace](../../../../../data-science-workspace/home.md)
* [Panoramica di Servizio query](../../../../../query-service/home.md)

