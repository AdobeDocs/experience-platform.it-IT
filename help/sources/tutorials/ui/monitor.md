---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Monitorare gli account e i flussi di dati
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Monitorare gli account e i flussi di dati

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per visualizzare gli account esistenti e i flussi di dataset dall&#39; *[!UICONTROL Sources]* area di lavoro.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

- [Sistema](../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Monitorare gli account

Accedete a <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse origini con le quali è possibile creare flussi di dati di account. Ciascuna origine mostra il numero di conti e flussi di dati esistenti ad essi associati.

Selezionate *[!UICONTROL Accounts]* dall&#39;intestazione superiore per visualizzare gli account esistenti.

![catalogo](../../images/tutorials/monitor/catalog.png)

Vengono *[!UICONTROL Accounts]* visualizzate le pagine. In questa pagina è presente un elenco di account visualizzabili, con informazioni sulla loro origine, nome utente, numero di flussi di set di dati e data di creazione.

Selezionate l’icona in alto a sinistra per avviare la finestra di ordinamento.

![accounts](../../images/tutorials/monitor/accounts-list.png)

Il pannello di ordinamento consente di accedere agli account da un&#39;origine specifica. Selezionate la fonte con cui desiderate lavorare e selezionate l’account dall’elenco a destra.

![account-select](../../images/tutorials/monitor/accounts-sort.png)

Dalla *[!UICONTROL Accounts]* pagina è possibile visualizzare un elenco dei flussi di dati esistenti associati all&#39;account a cui si è effettuato l&#39;accesso. Selezionare il flusso di set di dati da visualizzare.

![account-page](../../images/tutorials/monitor/dataset-flows.png)

Viene *[!UICONTROL Dataset flow activity]* visualizzata la schermata. In questa pagina viene visualizzata la frequenza dei messaggi utilizzati sotto forma di grafico.

![dataset-flow-activity](../../images/tutorials/monitor/dataset-flows-activity.png)

## Monitorare i flussi di dataset

È possibile accedere ai flussi di set di dati direttamente dalla *[!UICONTROL Catalog]* pagina senza visualizzarli *[!UICONTROL Accounts]*. Selezionate *[!UICONTROL Dataset flows]* dall&#39;intestazione superiore per visualizzare un elenco dei flussi di dati esistenti.

![flussi di dati](../../images/tutorials/monitor/dataset-flows-list.png)

Come per gli account, potete ordinare l&#39;elenco dei flussi di set di dati utilizzando l&#39;icona di ordinamento in alto a sinistra. Selezionare l&#39;origine da visualizzare e selezionare il flusso di set di dati dall&#39;elenco a destra.

![select-dataset-flows](../../images/tutorials/monitor/dataset-flows-sort.png)

Viene *[!UICONTROL Dataset flow activity]* visualizzata la schermata. In questa pagina viene visualizzata la frequenza dei messaggi utilizzati sotto forma di grafico.

![dataset-flow-activity](../../images/tutorials/monitor/dataset-flows-activity.png)

Per ulteriori informazioni sul monitoraggio dei set di dati e sull’assimilazione, fare riferimento all’esercitazione sul [monitoraggio dei flussi di dati](../../../ingestion/quality/monitor-data-flows.md).

## Passaggi successivi

Seguendo questa esercitazione, è stato possibile accedere agli account esistenti e ai flussi di dati dall&#39; *[!UICONTROL Sources]* area di lavoro. I dati in entrata possono ora essere utilizzati dai [!DNL Platform] servizi a valle come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i documenti seguenti:

- [Panoramica del profilo cliente in tempo reale](../../../profile/home.md)
- [Panoramica di Analysis Workspace](../../../data-science-workspace/home.md)