---
keywords: Experience Platform;home;argomenti popolari;monitoraggio;monitorare;flussi di dati;monitorare l'acquisizione;inserimento dati;acquisizione dati;visualizzare record;visualizzare batch;
solution: Experience Platform
title: Monitoraggio dell’acquisizione dei dati
description: Questa guida utente descrive come monitorare i dati nell’interfaccia utente di Adobe Experience Platform. Questa guida richiede un Adobe ID e l’accesso a Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: 9399a242b855e151e5822035bc952efa89fe4bf0
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 4%

---

# Monitoraggio dell’acquisizione dei dati

L’acquisizione dei dati consente di acquisire i dati da Adobe Experience Platform. È possibile utilizzare l&#39;acquisizione in batch, che consente di inserire i dati utilizzando vari tipi di file (ad esempio CSV), oppure l&#39;acquisizione in streaming, che consente di acquisire i dati in [!DNL Platform] utilizzando endpoint di streaming in tempo reale.

Questa guida utente descrive come monitorare i dati nell’interfaccia utente di Adobe Experience Platform. Questa guida richiede un Adobe ID e l’accesso a Adobe Experience Platform.

## Monitorare l’acquisizione di dati di streaming end-to-end {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="Tasso di acquisizione"
>abstract="Numero di eventi elaborati correttamente al secondo."
>text="Learn more in the documentation"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-sources.html?lang=it" text="Monitorare i flussi di dati per le origini nell’interfaccia utente"

>[!TIP]
>
>Per calcolare il totale degli eventi in una data specifica, utilizzare l&#39;espressione di: `total events / day = ingestion rate * 60 * 60 * 24`.

Nell&#39;[interfaccia utente di Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Monitoraggio]** nel menu di navigazione a sinistra, seguito da **[!UICONTROL Streaming end-to-end]**.

Viene visualizzata la pagina di monitoraggio **[!UICONTROL Streaming end-to-end]**. In questa area di lavoro è disponibile un grafico che visualizza la frequenza degli eventi in streaming ricevuti da [!DNL Platform], un grafico che visualizza la frequenza degli eventi in streaming elaborati correttamente da [[!DNL Real-Time Customer Profile]](../../profile/home.md) e un elenco dettagliato dei dati in arrivo.

![](../images/quality/monitor-data-flows/list-streams.png)

Per impostazione predefinita, il grafico superiore mostra il tasso di acquisizione negli ultimi sette giorni. Questo intervallo di date può essere regolato per mostrare vari periodi di tempo selezionando il pulsante evidenziato.

![](../images/quality/monitor-data-flows/events-received.png)

Il grafico in basso mostra la frequenza degli eventi in streaming elaborati correttamente da [!DNL Profile] negli ultimi sette giorni. Questo intervallo di date può essere regolato per mostrare vari periodi di tempo selezionando il pulsante evidenziato.

>[!NOTE]
>
>Affinché i dati vengano visualizzati in questo grafico, i dati devono essere **esplicitamente** abilitati per [!DNL Profile]. Per informazioni su come abilitare i dati di streaming per [!DNL Profile], leggere la guida utente dei [set di dati](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

Sotto i grafici c’è un elenco di tutti i record di acquisizione in streaming che corrispondono all’intervallo di date mostrato sopra. Ogni batch elencato visualizza il proprio ID, il nome del set di dati, la data dell’ultimo aggiornamento, il numero di record nel batch e il numero di errori (se presenti). È possibile selezionare qualsiasi record per ottenere informazioni più dettagliate su tale record.

![](../images/quality/monitor-data-flows/streams.png)

### Visualizzazione dei record in streaming

Quando si visualizzano i dettagli di un record trasmesso correttamente, vengono visualizzate informazioni quali il numero di record acquisiti, la dimensione del file e gli orari di inizio e di fine dell’acquisizione.

![](../images/quality/monitor-data-flows/successful-streaming.png)

I dettagli di un record di streaming non riuscito visualizzano le stesse informazioni di un record di successo.

![](../images/quality/monitor-data-flows/failed-batch.png)

Inoltre, i record con errori forniscono dettagli sugli errori che si sono verificati durante l’elaborazione del batch. Nell’esempio seguente si è verificato un errore di analisi durante la conversione o convalida dei dati.

>[!NOTE]
>
>Se nelle righe acquisite sono presenti errori, queste righe **non** verranno eliminate a meno che il messaggio risultante non generi XDM non valido.

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## Monitorare l’acquisizione di dati batch end-to-end

In [[!DNL Experience Platform UI]](https://platform.adobe.com), selezionare **[!UICONTROL Monitoraggio]** nel menu di navigazione sinistro.

Viene visualizzata la pagina di monitoraggio **[!UICONTROL Batch end-to-end]**, in cui viene visualizzato un elenco dei batch precedentemente acquisiti. È possibile selezionare uno qualsiasi dei batch per ottenere informazioni più dettagliate su tale record.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### Visualizzazione dei batch

Quando si visualizzano i dettagli di un batch riuscito, vengono visualizzate informazioni quali il numero di record acquisiti, la dimensione del file e gli orari di inizio e di fine dell’acquisizione.

![](../images/quality/monitor-data-flows/successful-batch.png)

I dettagli di un batch non riuscito visualizzano le stesse informazioni di un batch riuscito, con l&#39;aggiunta del numero di record non riusciti.

![](../images/quality/monitor-data-flows/failed-batch.png)

Inoltre, i batch non riusciti forniscono dettagli sugli errori che si sono verificati durante l’elaborazione del batch. Nell’esempio seguente si è verificato un errore con il batch acquisito perché presenta il numero massimo di identità per la persona.

>[!NOTE]
>
>Se nelle righe acquisite sono presenti errori, queste righe **non** verranno eliminate a meno che il messaggio risultante non generi XDM non valido.

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
