---
keywords: Experience Platform;home;argomenti comuni;monitoraggio;monitorare;flussi di dati;monitorare l’acquisizione;inserimento dati;inserimento dati;visualizzare record;visualizzare batch;
solution: Experience Platform
title: Monitoraggio dell’acquisizione dei dati
topic: ' - Panoramica'
description: Questa guida utente descrive come monitorare i dati all’interno dell’interfaccia utente di Adobe Experience Platform. Questa guida richiede un Adobe ID e l’accesso ad Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---


# Monitoraggio dell’acquisizione di dati

L’acquisizione dei dati ti consente di acquisire i dati in Adobe Experience Platform. Puoi utilizzare l’acquisizione batch, che ti consente di inserire i dati utilizzando vari tipi di file (come CSV), o l’acquisizione in streaming, che ti consente di acquisire i dati in [!DNL Platform] utilizzando gli endpoint di streaming in tempo reale.

Questa guida utente descrive come monitorare i dati all’interno dell’interfaccia utente di Adobe Experience Platform. Questa guida richiede un Adobe ID e l’accesso ad Adobe Experience Platform.

## Monitorare l’acquisizione di dati end-to-end in streaming

Nel [Interfaccia utente di Experience Platform](https://platform.adobe.com), fai clic su **[!UICONTROL Monitoring]** nel menu di navigazione a sinistra, quindi fai clic su **[!UICONTROL Streaming end-to-end]**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

Viene visualizzata la pagina di monitoraggio **[!UICONTROL Streaming end-to-end]**. Questa area di lavoro fornisce un grafico che mostra la frequenza degli eventi in streaming ricevuti da [!DNL Platform], un grafico che mostra la frequenza degli eventi in streaming elaborati correttamente da [[!DNL Real-time Customer Profile]](../../profile/home.md) e un elenco dettagliato dei dati in arrivo.

![](../images/quality/monitor-data-flows/list-streams.png)

Per impostazione predefinita, il grafico superiore mostra il tasso di acquisizione degli ultimi sette giorni. Per modificare questo intervallo di date e visualizzare vari periodi di tempo, fai clic sul pulsante evidenziato.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

Il grafico in basso mostra la frequenza degli eventi in streaming elaborati correttamente da [!DNL Profile] negli ultimi sette giorni. Per modificare questo intervallo di date e visualizzare vari periodi di tempo, fai clic sul pulsante evidenziato.

>[!NOTE]
>
>Affinché i dati vengano visualizzati su questo grafico, i dati devono essere abilitati **esplicitamente** per [!DNL Profile]. Per informazioni su come abilitare i dati in streaming per [!DNL Profile], consulta la [guida utente per i set di dati](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Sotto i grafici è riportato un elenco di tutti i record di acquisizione in streaming corrispondenti all’intervallo di date visualizzato sopra. Ogni batch elencato visualizza il proprio ID, il nome del set di dati, al momento dell’ultimo aggiornamento, il numero di record nel batch e il numero di errori (se presenti). Puoi fare clic su uno qualsiasi dei record per ottenere informazioni più dettagliate su quel record.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Visualizzazione dei record in streaming

Quando si visualizzano i dettagli di un record con streaming riuscito, vengono visualizzate informazioni quali il numero di record acquisiti, le dimensioni del file e gli orari di inizio e fine dell’acquisizione.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

I dettagli di un record di streaming non riuscito visualizzano le stesse informazioni di un record riuscito.

![](../images/quality/monitor-data-flows/failed-batch.png)

Inoltre, i record non riusciti forniscono dettagli sugli errori che si sono verificati durante l&#39;elaborazione del batch. Nell&#39;esempio seguente si è verificato un errore di sistema durante la convalida del set di datiId dal catalogo.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Monitorare l’acquisizione di dati in batch end-to-end

Nel [[!DNL Experience Platform UI]](https://platform.adobe.com), fai clic su **[!UICONTROL Monitoring]** nel menu di navigazione a sinistra.

![](../images/quality/monitor-data-flows/click-monitoring.png)

Viene visualizzata la pagina di monitoraggio **[!UICONTROL Batch end-to-end]**, che presenta un elenco dei batch precedentemente acquisiti. Puoi fare clic su uno dei batch per ottenere informazioni più dettagliate su tale record.

![](../images/quality/monitor-data-flows/list-batches.png)

### Visualizzazione dei batch

Quando si visualizzano i dettagli di un batch di successo, vengono visualizzate informazioni quali il numero di record acquisiti, le dimensioni del file e gli orari di inizio e fine dell’acquisizione.

![](../images/quality/monitor-data-flows/successful-batch.png)

I dettagli di un batch non riuscito visualizzano le stesse informazioni di un batch riuscito, con l&#39;aggiunta del numero di record non riusciti.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

Inoltre, i batch con errori forniscono dettagli sugli errori che si sono verificati durante l&#39;elaborazione del batch. Nell’esempio seguente, si è verificato un errore con il batch acquisito perché utilizzava un campo sconosciuto di `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)