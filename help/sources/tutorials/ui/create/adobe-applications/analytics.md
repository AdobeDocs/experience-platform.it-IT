---
keywords: Experience Platform;home;popular topics;Analytics source connector;Analytics connector;Analytics source;analytics
solution: Experience Platform
title: Creare un connettore sorgente Adobe Analytics  nell’interfaccia utente
topic: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente Adobe Analytics  nell’interfaccia utente per trasferire i dati di consumo in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 1%

---


# Creare un connettore sorgente Adobe Analytics  nell’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente Adobe Analytics  nell’interfaccia utente per trasferire i dati di consumo in Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Creare una connessione di origine con  Adobe Analytics

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro delle origini. Nella schermata **Catalogo** sono visualizzate le origini disponibili con cui creare connessioni in ingresso e ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la **[!UICONTROL Adobe applications]** categoria, selezionate **[!UICONTROL Adobe Analytics]** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per visualizzare gli account esistenti, selezionare **[!UICONTROL Accounts]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Seleziona dati

Viene **[!UICONTROL Adobe Analytics]** visualizzato il passaggio. I flussi di dati precedentemente stabiliti per Analytics sono elencati in questa schermata. Puoi creare un nuovo flusso di dati facendo clic su **[!UICONTROL Select data]**.

>[!NOTE]
>
>È possibile creare più connessioni in-bound a un&#39;origine per l&#39;inclusione di dati diversi.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

Nell&#39;elenco delle suite di rapporti disponibili, seleziona quella che desideri portare in Piattaforma e fai clic su **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Denominate il flusso di dati

Viene visualizzato il **[!UICONTROL Dataset flow detail]** passaggio in cui è necessario specificare un nome e una descrizione facoltativa per il flusso di dati. Selezionate **[!UICONTROL Next]** al termine.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### Controlla il flusso dei dataset

Viene visualizzato il **[!UICONTROL Review]** passaggio che consente di rivedere il flusso di dati in-bound di Analytics prima della creazione. I dettagli della connessione sono raggruppati per categorie, tra cui:

* **[!UICONTROL Connection]**: Mostra il tipo di connessione di origine e la suite di rapporti selezionata.
* **[!UICONTROL Assign dataset & map fields]**: Quando si creano altri connettori di origine, questo contenitore mostra in quale set di dati di origine vengono acquisiti i dati, incluso lo schema a cui il dataset aderisce. Lo schema di output e il dataset vengono configurati automaticamente per i flussi di dati di Analytics.

![](../../../../images/tutorials/create/analytics/review.png)

### Monitorare il flusso dei dataset

Una volta creato il flusso di set di dati, è possibile monitorare i dati che vengono acquisiti attraverso di esso. Dalla **[!UICONTROL Catalog]** schermata, seleziona **[!UICONTROL Dataset flows]** per visualizzare un elenco dei flussi stabiliti associati al tuo account Analytics.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

Viene visualizzata la schermata **Flussi** di dati. In questa pagina sono presenti una coppia di flussi di dati, con informazioni su nome, dati di origine, ora di creazione e stato.

Il connettore crea un&#39;istanza di due flussi di dati. Un flusso rappresenta i dati di backfill e l&#39;altro è per i dati live. I dati di backfill non sono configurati per il profilo, ma vengono inviati al lago di dati per casi d’uso analitici e scientifici.

Per ulteriori informazioni sul backfill, i dati dal vivo e le rispettive latenze, consulta la panoramica [del Connettore dati di](../../../../connectors/adobe-applications/analytics.md)Analytics.

Selezionare dall&#39;elenco il flusso di dati che si desidera visualizzare.

![](../../../../images/tutorials/create/analytics/backfill.png)

Viene visualizzata la pagina **Attività** DataSet. In questa pagina viene visualizzata la frequenza dei messaggi utilizzati sotto forma di grafico. Seleziona *Gestione* dati dall&#39;intestazione superiore per accedere ai campi di etichettatura.

![](../../../../images/tutorials/create/analytics/batches.png)

È possibile visualizzare le etichette ereditate di un flusso di dati dalla schermata *Gestione* dati. Per accedere a etichette specifiche, fare clic sul pulsante Modifica in alto a destra.

![](../../../../images/tutorials/create/analytics/data-gov.png)

Viene visualizzato il pannello **Modifica etichette** governance. Questa schermata consente di accedere e modificare il contratto, l&#39;identità e le etichette sensibili di un flusso di dati.

Per ulteriori informazioni su come etichettare i dati provenienti da Analytics, consulta la guida [alle etichette di utilizzo dei](../../../../../data-governance/labels/user-guide.md)dati.

![](../../../../images/tutorials/create/analytics/labels.png)

## Passaggi successivi e risorse aggiuntive

Una volta creata la connessione, viene automaticamente creato uno schema di destinazione e un flusso di dati per contenere i dati in arrivo. Inoltre, avviene il recupero dei dati e vengono acquisiti fino a 13 mesi di dati storici. Al termine dell&#39;assimilazione iniziale, i dati di Analytics vengono utilizzati dai servizi della piattaforma a valle, quali Real-time Customer Profile e Segmentation Service. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](../../../../../profile/home.md)
* [Panoramica del servizio di segmentazione](../../../../../segmentation/home.md)
* [Panoramica di Analysis Workspace](../../../../../data-science-workspace/home.md)
* [Panoramica di Servizio query](../../../../../query-service/home.md)

Il seguente video è stato realizzato per consentire agli utenti di acquisire i dati utilizzando il connettore sorgente Adobe Analytics :

>[!WARNING]
>
> L’ [!DNL Platform] interfaccia utente mostrata nel video seguente è obsoleta. Per informazioni sulle ultime funzionalità e videate dell’interfaccia, consulta la documentazione precedente.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

