---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Monitoraggio dell’assimilazione dei dati
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Monitoraggio dell’assimilazione dei dati

L&#39;assimilazione dei dati consente di assimilare i dati  Adobe Experience Platform. È possibile utilizzare l’assimilazione batch, che consente di inserire i dati utilizzando vari tipi di file (come i CSV), oppure l’assimilazione in streaming, per trasferire i dati ad Platform utilizzando gli endpoint in streaming in tempo reale.

Questa guida utente descrive come monitorare i dati all&#39;interno &#39;interfaccia utente del Adobe Experience Platform. Questa guida richiede un Adobe ID  e l&#39;accesso al Adobe Experience Platform .

## Monitorare l’inserimento di dati end-to-end

Nell’interfaccia utente [di](https://platform.adobe.com)Experience Platform, fai clic su **Monitoraggio** nel menu di navigazione a sinistra, quindi fai clic su **Streaming end-to-end**(Streaming end-to-end).

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

Viene visualizzata la pagina *Streaming end-to-end* monitoring (Monitoraggio end-to-end dello streaming). Questa area di lavoro fornisce un grafico che mostra la frequenza degli eventi in streaming ricevuti da Platform, un grafico che mostra la frequenza degli eventi in streaming elaborati correttamente dal profilo [cliente](../../profile/home.md)in tempo reale, nonché un elenco dettagliato dei dati in arrivo.

![](../images/quality/monitor-data-flows/list-streams.png)

Per impostazione predefinita, il grafico superiore mostra il tasso di assimilazione degli ultimi sette giorni. È possibile modificare questo intervallo di date per visualizzare diversi periodi di tempo facendo clic sul pulsante evidenziato.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

Il grafico inferiore mostra la frequenza degli eventi in streaming elaborati correttamente da Profile negli ultimi sette giorni. È possibile modificare questo intervallo di date per visualizzare diversi periodi di tempo facendo clic sul pulsante evidenziato.

>[!NOTE]
>
>Affinché i dati vengano visualizzati su questo grafico, i dati devono essere **esplicitamente** attivati per il profilo. Per informazioni su come abilitare i dati di streaming per il profilo, consulta la guida [utente](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)per i set di dati.

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Sotto i grafici è riportato un elenco di tutti i record di assimilazione in streaming corrispondenti all’intervallo di date visualizzato sopra. Ciascun batch elencato visualizza il proprio ID, il nome del set di dati, al momento dell&#39;ultimo aggiornamento, il numero di record nel batch, nonché il numero di eventuali errori (se presenti). È possibile fare clic su uno dei record per ottenere informazioni più dettagliate su tale record.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Visualizzazione dei record in streaming

Quando si visualizzano i dettagli di un record trasmesso con successo, vengono visualizzate informazioni quali il numero di record acquisiti, la dimensione del file e l&#39;ora di inizio e fine dell&#39;assimilazione.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

I dettagli di un record di streaming non riuscito visualizzano le stesse informazioni di un record riuscito.

![](../images/quality/monitor-data-flows/failed-batch.png)

Inoltre, i record con errore forniscono dettagli sugli errori che si sono verificati durante l&#39;elaborazione del batch. Nell&#39;esempio seguente si è verificato un errore di sistema durante la convalida dell&#39;datasetId dal catalogo.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Monitorare l’inserimento di dati end-to-end in batch

Nell’interfaccia [Experience Platform](https://platform.adobe.com), fate clic su **Monitoraggio** nel menu di navigazione a sinistra.

![](../images/quality/monitor-data-flows/click-monitoring.png)

Viene visualizzata la pagina **Batch di monitoraggio end-to-end** , con un elenco dei batch precedentemente assimilati. Potete fare clic su uno dei batch per ottenere informazioni più dettagliate su tale record.

![](../images/quality/monitor-data-flows/list-batches.png)

### Visualizzazione dei batch

Quando si visualizzano i dettagli di un batch di successo, vengono visualizzate informazioni quali il numero di record acquisiti, la dimensione del file e l’ora di inizio e fine dell’assimilazione.

![](../images/quality/monitor-data-flows/successful-batch.png)

Nei dettagli di un batch con errore vengono visualizzate le stesse informazioni di un batch con esito positivo, con l&#39;aggiunta del numero di record con esito negativo.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

Inoltre, i batch con errore forniscono dettagli sugli errori che si sono verificati durante l&#39;elaborazione del batch. Nell&#39;esempio seguente si è verificato un errore con il batch assimilato perché utilizzava un campo sconosciuto di `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)