---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Monitorare ed eliminare i flussi di dati
topic: overview
translation-type: tm+mt
source-git-commit: f08ad2c9cc48c08bcdc0e278481992e8789000b5
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# Monitorare ed eliminare i flussi di dati

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per visualizzare gli account e i flussi di dati esistenti dall&#39; *[!UICONTROL Sources]* area di lavoro. Questa esercitazione fornisce inoltre i passaggi per eliminare i flussi di dati dall&#39; *[!UICONTROL Sources]* area di lavoro.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

- [Sistema](../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Monitorare gli account

Accedete a [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse origini per le quali è possibile creare account e flussi di dati. Ogni origine mostra il numero di account e di flussi di dati esistenti ad essi associati.

Selezionate *[!UICONTROL Accounts]* dall&#39;intestazione superiore per visualizzare gli account esistenti.

![catalogo](../../images/tutorials/monitor/catalog.png)

Vengono *[!UICONTROL Accounts]* visualizzate le pagine. In questa pagina è presente un elenco di account visualizzabili, con informazioni sull’origine, il nome utente, il numero di flussi di dati e la data di creazione.

Selezionate l’icona funnel in alto a sinistra per avviare la finestra di ordinamento.

![accounts](../../images/tutorials/monitor/accounts-list.png)

Il pannello di ordinamento consente di accedere agli account da un&#39;origine specifica. Selezionate la fonte con cui desiderate lavorare e selezionate l’account dall’elenco a destra.

![account-select](../../images/tutorials/monitor/accounts-sort.png)

Dalla *[!UICONTROL Accounts]* pagina, è possibile visualizzare un elenco dei flussi di dati esistenti associati all&#39;account a cui si è effettuato l&#39;accesso. Selezionate il flusso di dati da visualizzare.

![account-page](../../images/tutorials/monitor/dataflows.png)

Viene *[!UICONTROL Dataflow activity]* visualizzata la schermata. In questa pagina viene visualizzata la frequenza dei messaggi utilizzati sotto forma di grafico.

![dataset-flow-activity](../../images/tutorials/monitor/dataflow-activity.png)

## Monitorare i flussi di dati

È possibile accedere ai flussi di dati direttamente dalla *[!UICONTROL Catalog]* pagina senza visualizzarli *[!UICONTROL Accounts]*. Selezionate *[!UICONTROL Dataflows]* dall’intestazione superiore per visualizzare un elenco dei flussi di dati esistenti.

![catalog-dataflows](../../images/tutorials/monitor/catalog-dataflows.png)

Viene visualizzato un elenco dei flussi di dati esistenti. In questa pagina è presente un elenco di flussi di dati visualizzabili, con informazioni sull’origine, il nome utente, il numero di flussi di dati e lo stato. Selezionate l’icona funnel in alto a sinistra per ordinare i dati.

![elenco dei flussi di dati](../../images/tutorials/monitor/dataflows-list.png)

Viene visualizzato il pannello di ordinamento. Selezionate la sorgente a cui desiderate accedere dal menu di scorrimento e selezionate il flusso di dati dall’elenco a destra.

![sort-dataflows](../../images/tutorials/monitor/dataflows-sort.png)

Viene *[!UICONTROL Dataflow activity]* visualizzata la schermata. In questa pagina viene visualizzata la frequenza dei messaggi utilizzati sotto forma di grafico.

![dataset-flow-activity](../../images/tutorials/monitor/dataflow-activity.png)

Per ulteriori informazioni sul monitoraggio dei flussi di dati e sull’assimilazione, consulta l’esercitazione sul [monitoraggio dei flussi di dati](../../../ingestion/quality/monitor-data-flows.md).

## Eliminare un flusso di dati

È possibile eliminare i flussi di dati creati in modo errato o non più necessari accedendo alla schermata dei flussi di dati. Individuate il flusso di dati da eliminare utilizzando l&#39;icona funnel di ordinamento e selezionate il flusso di dati per aprire il **[!UICONTROL Properties]** pannello.

Per eliminare un flusso di dati, selezionare **[!UICONTROL Delete]** dalle proprietà in alto a destra.

![delete-dataflows](../../images/tutorials/monitor/dataflows-sort-delete.png)

Viene visualizzato un messaggio di conferma finale. Selezionare **[!UICONTROL Delete]** per confermare.

![verify-delete](../../images/tutorials/monitor/confirm-delete.png)

Dopo alcuni istanti, nella parte inferiore dello schermo viene visualizzata una casella di conferma verde per confermare l’avvenuta eliminazione.

![delete-success](../../images/tutorials/monitor/deletion-confirmed.png)

In alternativa, è possibile eliminare un flusso di dati dallo *[!UICONTROL Accounts]* schermo. Individuate l&#39;account a cui desiderate accedere utilizzando l&#39;icona dell&#39;imbuto di ordinamento e selezionate l&#39;account dall&#39;elenco.

![account-select](../../images/tutorials/monitor/accounts-sort.png)

Viene *[!UICONTROL Accounts]* visualizzata la pagina. Selezionate il flusso di dati da eliminare, quindi selezionate **[!UICONTROL Delete]** dal pannello delle proprietà per completare il processo.

![accounts-delete](../../images/tutorials/monitor/accounts-delete.png)

Seguite i passaggi di conferma indicati sopra per completare il processo.

## Passaggi successivi

Seguendo questa esercitazione, è stato possibile accedere agli account e ai flussi di dati esistenti dall&#39; *[!UICONTROL Sources]* area di lavoro. I dati in entrata possono ora essere utilizzati dai [!DNL Platform] servizi a valle come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i documenti seguenti:

- [Panoramica del profilo cliente in tempo reale](../../../profile/home.md)
- [Panoramica di Analysis Workspace](../../../data-science-workspace/home.md)