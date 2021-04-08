---
keywords: Experience Platform;home;argomenti popolari;segmentazione in streaming;Segmentazione;Servizio di segmentazione;servizio di segmentazione;guida interfaccia utente;
solution: Experience Platform
title: Guida all’interfaccia utente per la segmentazione in streaming
topic: guida all'interfaccia utente
description: La segmentazione in streaming su Adobe Experience Platform consente di eseguire la segmentazione in tempo quasi reale concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati arrivano in Platform, alleviando la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità, la maggior parte delle regole del segmento può ora essere valutata quando i dati vengono trasmessi in Platform, il che significa che l’appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
translation-type: tm+mt
source-git-commit: e1ae20412f449c991f53fdd0f095d0c3a6de262c
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# Segmentazione streaming

>[!NOTE]
>
>Il seguente documento spiega come utilizzare la segmentazione in streaming utilizzando l’interfaccia utente. Per informazioni sull&#39;utilizzo della segmentazione in streaming tramite API, consulta la [guida API per la segmentazione in streaming](../api/streaming-segmentation.md).

La segmentazione in streaming su [!DNL Adobe Experience Platform] consente ai clienti di eseguire la segmentazione in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati in streaming arrivano in [!DNL Platform], alleviando la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità, la maggior parte delle regole del segmento può ora essere valutata in quanto i dati vengono trasmessi in [!DNL Platform], il che significa che l’appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

>[!NOTE]
>
>La segmentazione in streaming può essere utilizzata solo per valutare i dati trasmessi in streaming in Platform. In altre parole, i dati acquisiti tramite l’acquisizione batch non verranno valutati tramite la segmentazione in streaming e verranno valutati insieme al lavoro del segmento pianificato ogni notte.
>
>Inoltre, i segmenti valutati con la segmentazione in streaming possono variare tra l’appartenenza ideale e l’appartenenza effettiva se il segmento è basato su un altro segmento valutato utilizzando la segmentazione in batch. Ad esempio, se il segmento A è basato sul segmento B e il segmento B viene valutato utilizzando la segmentazione batch, poiché il segmento B viene aggiornato solo ogni 24 ore, il segmento A si allontanerà ulteriormente dai dati effettivi fino a quando non viene sincronizzato nuovamente con l’aggiornamento del segmento B.

## Tipi di query per segmentazione in streaming

>[!NOTE]
>
>Affinché la segmentazione in streaming funzioni, è necessario abilitare la segmentazione pianificata per l’organizzazione. Per informazioni dettagliate sull&#39;abilitazione della segmentazione pianificata, fai riferimento alla sezione [segmentazione in streaming nella guida utente Segmentazione](./overview.md#scheduled-segmentation).

Una query viene valutata automaticamente con la segmentazione in streaming se soddisfa uno dei seguenti criteri:

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| Hit in entrata | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Hit in arrivo in una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Hit in arrivo con una finestra temporale | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo con una finestra temporale. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. |  |
| Hit in entrata che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo, senza restrizioni di tempo, e a uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Hit in arrivo che fa riferimento a un profilo all’interno di una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo e a uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti in batch o in streaming. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Eventi multipli che fanno riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

La definizione di un segmento **non** sarà abilitata per la segmentazione in streaming nei seguenti scenari:

- La definizione del segmento include segmenti o caratteristiche Adobe Audience Manager (AAM).
- La definizione del segmento include più entità (query con più entità).

Inoltre, durante la segmentazione in streaming si applicano alcune linee guida:

| Tipo di query | Indirizzo |
| ---------- | -------- |
| Query a evento singolo | Non ci sono limiti all’intervallo di lookback. |
| Query con cronologia eventi | <ul><li>L&#39;intervallo di lookback è limitato a **un giorno**.</li><li>Tra gli eventi è presente una condizione di ordine temporale rigida **deve** .</li><li>Sono supportate le query con almeno un evento negato. Tuttavia, l&#39;intero evento **non può** essere una negazione.</li></ul> |

Se la definizione di un segmento viene modificata in modo da non soddisfare più i criteri per la segmentazione in streaming, la definizione del segmento passa automaticamente da &quot;Streaming&quot; a &quot;Batch&quot;.

## Dettagli dei segmenti di segmentazione in streaming

Dopo aver creato un segmento abilitato per lo streaming, puoi visualizzare i dettagli di tale segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Nello specifico, vengono visualizzati i dettagli relativi a **[!UICONTROL total qualified audience size]**. Il **[!UICONTROL Total qualified audience size]** mostra il numero totale di tipi di pubblico qualificati dall’ultima esecuzione di processi di segmento completata. Se un lavoro di segmento non è stato completato nelle ultime 24 ore, il numero di tipi di pubblico verrà invece calcolato in base a una stima.

Sotto c’è un grafico a linee che mostra il numero di segmenti qualificati e non qualificati nelle ultime 24 ore. Il menu a discesa può essere regolato in modo da visualizzare le ultime 24 ore, la settimana scorsa o gli ultimi 30 giorni.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Per ulteriori informazioni sulla valutazione dell’ultimo segmento, seleziona la bolla di informazioni.

![](../images/ui/streaming-segmentation/info-bubble.png)

Per ulteriori informazioni sulle definizioni dei segmenti, consulta la sezione precedente su [dettagli delle definizioni dei segmenti](#segment-details).

## Passaggi successivi

Questa guida utente spiega come funzionano le definizioni dei segmenti abilitate per lo streaming su Adobe Experience Platform e come monitorare i segmenti abilitati per lo streaming.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente di Adobe Experience Platform, consulta la [Guida utente alla segmentazione](./overview.md).
