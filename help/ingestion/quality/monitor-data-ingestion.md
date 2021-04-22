---
keywords: Experience Platform;home;argomenti popolari;monitoraggio;monitorare;flussi di dati;monitorare l’acquisizione;inserimento dati;inserimento dati;visualizzare record;visualizzare batch;
solution: Experience Platform
title: Monitoraggio dell’acquisizione dei dati
topic-legacy: overview
description: Questa guida utente descrive come monitorare i dati all’interno dell’interfaccia utente di Adobe Experience Platform. Questa guida richiede un Adobe ID e l’accesso a Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
translation-type: tm+mt
source-git-commit: 6bedd5ec0865e858a337155deb80309a54e30892
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# Monitoraggio dell’acquisizione di dati

L’inserimento dei dati consente di acquisire i dati in Adobe Experience Platform. Puoi utilizzare l’acquisizione batch, che ti consente di inserire i dati utilizzando vari tipi di file (come CSV), o l’acquisizione in streaming, che ti consente di acquisire i dati in [!DNL Platform] utilizzando gli endpoint di streaming in tempo reale.

Questa guida utente descrive come monitorare i dati all’interno dell’interfaccia utente di Adobe Experience Platform. Questa guida richiede un Adobe ID e l’accesso a Adobe Experience Platform.

## Monitorare l’acquisizione di dati end-to-end in streaming

Nell&#39; [Interfaccia Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Monitoring]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Streaming end-to-end]**.

Viene visualizzata la pagina di monitoraggio **[!UICONTROL Streaming end-to-end]**. Questa area di lavoro fornisce un grafico che mostra la frequenza degli eventi in streaming ricevuti da [!DNL Platform], un grafico che mostra la frequenza degli eventi in streaming elaborati correttamente da [[!DNL Real-time Customer Profile]](../../profile/home.md) e un elenco dettagliato dei dati in arrivo.

![](../images/quality/monitor-data-flows/list-streams.png)

Per impostazione predefinita, il grafico superiore mostra il tasso di acquisizione degli ultimi sette giorni. Questo intervallo di date può essere regolato per mostrare vari periodi di tempo selezionando il pulsante evidenziato.

![](../images/quality/monitor-data-flows/events-received.png)

Il grafico in basso mostra la frequenza degli eventi in streaming elaborati correttamente da [!DNL Profile] negli ultimi sette giorni. Questo intervallo di date può essere regolato per mostrare vari periodi di tempo selezionando il pulsante evidenziato.

>[!NOTE]
>
>Affinché i dati vengano visualizzati su questo grafico, i dati devono essere abilitati **esplicitamente** per [!DNL Profile]. Per informazioni su come abilitare i dati in streaming per [!DNL Profile], consulta la [guida utente per i set di dati](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

Sotto i grafici è riportato un elenco di tutti i record di acquisizione in streaming corrispondenti all’intervallo di date visualizzato sopra. Ogni batch elencato visualizza il proprio ID, il nome del set di dati, al momento dell’ultimo aggiornamento, il numero di record nel batch e il numero di errori (se presenti). È possibile selezionare uno qualsiasi dei record per informazioni più dettagliate su quel record.

![](../images/quality/monitor-data-flows/streams.png)

### Visualizzazione dei record in streaming

Quando si visualizzano i dettagli di un record con streaming riuscito, vengono visualizzate informazioni quali il numero di record acquisiti, le dimensioni del file e gli orari di inizio e fine dell’acquisizione.

![](../images/quality/monitor-data-flows/successful-streaming.png)

I dettagli di un record di streaming non riuscito visualizzano le stesse informazioni di un record riuscito.

![](../images/quality/monitor-data-flows/failed-batch.png)

Inoltre, i record non riusciti forniscono dettagli sugli errori che si sono verificati durante l&#39;elaborazione del batch. Nell’esempio seguente si è verificato un errore di analisi durante la conversione o la convalida dei dati.

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## Monitorare l’acquisizione di dati in batch end-to-end

Nel [[!DNL Experience Platform UI]](https://platform.adobe.com), seleziona **[!UICONTROL Monitoring]** dal menu di navigazione a sinistra.

Viene visualizzata la pagina di monitoraggio **[!UICONTROL Batch end-to-end]**, che presenta un elenco dei batch precedentemente acquisiti. Puoi selezionare uno dei batch per informazioni più dettagliate su tale record.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### Visualizzazione dei batch

Quando si visualizzano i dettagli di un batch di successo, vengono visualizzate informazioni quali il numero di record acquisiti, le dimensioni del file e gli orari di inizio e fine dell’acquisizione.

![](../images/quality/monitor-data-flows/successful-batch.png)

I dettagli di un batch non riuscito visualizzano le stesse informazioni di un batch riuscito, con l&#39;aggiunta del numero di record non riusciti.

![](../images/quality/monitor-data-flows/failed-batch.png)

Inoltre, i batch con errori forniscono dettagli sugli errori che si sono verificati durante l&#39;elaborazione del batch. Nell’esempio seguente, si è verificato un errore con il batch acquisito perché contiene il numero massimo di identità per la persona.

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
