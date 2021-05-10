---
keywords: Experience Platform;home;argomenti comuni;connettore origine Analytics;connettore Analytics;origine Analytics;Analytics
solution: Experience Platform
title: Creare una connessione sorgente Adobe Analytics nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Adobe Analytics nell’interfaccia utente per inserire i dati dei consumatori in Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
translation-type: tm+mt
source-git-commit: 32a6d0311169486b1273129c0ee87c242bee1e47
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 2%

---

# Creare una connessione sorgente Adobe Analytics nell’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente Adobe Analytics nell’interfaccia utente per inserire i dati dei clienti in Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md) Experience Data Model (XDM): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
* [Profilo](../../../../../profile/home.md) cliente in tempo reale: Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Creare una connessione sorgente con Adobe Analytics

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro origini. La schermata **Catalogo** visualizza le sorgenti disponibili con cui creare connessioni in entrata e ogni origine mostra il numero di account e flussi di dati esistenti associati.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Adobe applications]**, selezionare **[!UICONTROL Adobe Analytics]** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione dell’origine selezionata e le opzioni per la connessione con l’origine o la visualizzazione della relativa documentazione. Per visualizzare gli account esistenti, selezionare **[!UICONTROL Accounts]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Seleziona dati

Viene visualizzato il passaggio **[!UICONTROL Adobe Analytics]** . I flussi di dati stabiliti in precedenza per Analytics sono elencati in questa schermata. Puoi creare un nuovo flusso di set di dati facendo clic su **[!UICONTROL Select data]**.

>[!NOTE]
>
>È possibile effettuare più connessioni in-bound a un’origine per l’inserimento di dati diversi.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

Dall’elenco delle suite di rapporti disponibili, seleziona quella da importare in Platform e fai clic su **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Denomina il flusso di set di dati

Viene visualizzato il passaggio **[!UICONTROL Dataset flow detail]** , in cui è necessario specificare un nome e una descrizione facoltativa per il flusso di set di dati. Al termine, fai clic su **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### Esamina il flusso dei set di dati

Viene visualizzato il passaggio **[!UICONTROL Review]** , che consente di rivedere il flusso di set di dati in-bound di Analytics prima della creazione. I dettagli della connessione sono raggruppati per categorie, tra cui:

* **[!UICONTROL Connection]**: Mostra il tipo di connessione di origine e la suite di rapporti selezionata.
* **[!UICONTROL Assign dataset & map fields]**: Quando crei altri connettori di origine, questo contenitore mostra in quale set di dati di origine vengono acquisiti, incluso lo schema a cui il set di dati aderisce. Lo schema di output e il set di dati vengono configurati automaticamente per i flussi di dati di Analytics.

![](../../../../images/tutorials/create/analytics/review.png)

### Monitorare il flusso dei set di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso. Dalla schermata **[!UICONTROL Catalog]** , seleziona **[!UICONTROL Dataset flows]** per visualizzare un elenco dei flussi stabiliti associati al tuo account Analytics.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

Viene visualizzata la schermata **Flussi di dati** . In questa pagina è presente una coppia di flussi di set di dati, che include informazioni su nome, dati di origine, tempo di creazione e stato.

Il connettore crea un&#39;istanza di due flussi di set di dati. Un flusso rappresenta i dati di backfill e l’altro è per i dati live. I dati di backfill non sono configurati per il profilo, ma vengono inviati al data lake per casi d’uso analitici e per la scienza dei dati.

Per ulteriori informazioni sul backfill, i dati live e le rispettive latenze, consulta la [panoramica di Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md).

Seleziona il flusso di set di dati da visualizzare dall’elenco.

![](../../../../images/tutorials/create/analytics/backfill.png)

Viene visualizzata la pagina **Attività set di dati** . In questa pagina viene visualizzata la frequenza dei messaggi visualizzati sotto forma di grafico. Seleziona *Data governance* dall&#39;intestazione superiore per accedere ai campi di etichettatura.

![](../../../../images/tutorials/create/analytics/batches.png)

Puoi visualizzare le etichette ereditate di un flusso di dati dalla schermata *governance dei dati* . Per accedere a etichette specifiche, seleziona il pulsante di modifica in alto a destra.

![](../../../../images/tutorials/create/analytics/data-gov.png)

Viene visualizzato il pannello **Modifica etichette di governance** . Questa schermata ti consente di accedere e modificare il contratto, l’identità e le etichette sensibili di un flusso di dati.

Per ulteriori informazioni su come etichettare i dati provenienti da Analytics, visita la [guida alle etichette per l&#39;uso dei dati](../../../../../data-governance/labels/user-guide.md).

![](../../../../images/tutorials/create/analytics/labels.png)

## Passaggi successivi e risorse aggiuntive

Una volta creata la connessione, viene creato automaticamente uno schema di destinazione e un flusso di set di dati per contenere i dati in arrivo. Inoltre, avviene il recupero dei dati e vengono acquisiti fino a 13 mesi di dati storici. Al termine dell’acquisizione iniziale, i dati di Analytics e vengono utilizzati dai servizi della piattaforma a valle, come Profilo cliente in tempo reale e Servizio di segmentazione. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del profilo cliente in tempo reale](../../../../../profile/home.md)
* [Panoramica del servizio di segmentazione](../../../../../segmentation/home.md)
* [Panoramica di Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Panoramica del servizio query](../../../../../query-service/home.md)

Il seguente video è pensato per comprendere come acquisire i dati utilizzando il connettore Adobe Analytics Source:

>[!WARNING]
>
> L’ [!DNL Platform] interfaccia utente mostrata nel video seguente è obsoleta. Fai riferimento alla documentazione precedente per le ultime schermate e funzionalità dell’interfaccia utente.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
