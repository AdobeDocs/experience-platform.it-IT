---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione in streaming;segmentazione in streaming;Segmentation Service;segmentation service;ui guide;'
solution: Experience Platform
title: Guida all’interfaccia utente per la segmentazione in streaming
topic: ui guide
description: La segmentazione in streaming su Adobe Experience Platform consente di eseguire la segmentazione in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualifica del segmento ora avviene quando i dati entrano in piattaforma, eliminando la necessità di pianificare ed eseguire processi di segmentazione. Grazie a questa funzionalità, ora è possibile valutare la maggior parte delle regole del segmento quando i dati vengono passati in Piattaforma, il che significa che l'appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.
translation-type: tm+mt
source-git-commit: c0c42f872666323bfb3bdbdf5fb02475d3b5bc79
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---


# Segmentazione in streaming

>[!NOTE]
>
>Il seguente documento spiega come utilizzare la segmentazione in streaming utilizzando l&#39;interfaccia utente. Per informazioni sull&#39;utilizzo della segmentazione in streaming mediante l&#39;API, consultate la guida [streaming API guide](../api/streaming-segmentation.md).

La segmentazione in streaming su [!DNL Adobe Experience Platform] consente ai clienti di eseguire la segmentazione in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualifica del segmento ora avviene quando i dati in streaming arrivano in [!DNL Platform], riducendo la necessità di pianificare ed eseguire processi di segmentazione. Grazie a questa funzionalità, ora è possibile valutare la maggior parte delle regole del segmento in quanto i dati vengono passati in [!DNL Platform], il che significa che l&#39;appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

>[!NOTE]
>
>La segmentazione in streaming può essere utilizzata solo per valutare i dati in streaming in Piattaforma. In altre parole, i dati acquisiti tramite l’assimilazione batch non saranno valutati tramite la segmentazione in streaming e verranno valutati insieme al processo di segmento pianificato ogni sera.
>
>Inoltre, i segmenti valutati con la segmentazione in streaming possono variare tra l’appartenenza ideale e quella effettiva se il segmento è basato su un altro segmento valutato utilizzando la segmentazione batch. Ad esempio, se il segmento A è basato sul segmento B, e il segmento B viene valutato utilizzando la segmentazione batch, poiché il segmento B si aggiorna solo ogni 24 ore, il segmento A si allontanerà ulteriormente dai dati effettivi fino a quando non viene nuovamente sincronizzato con l&#39;aggiornamento del segmento B.

## Tipi di query di segmentazione in streaming

>[!NOTE]
>
>Per consentire il funzionamento della segmentazione in streaming, è necessario abilitare la segmentazione pianificata per l&#39;organizzazione. Per informazioni dettagliate sull&#39;abilitazione della segmentazione pianificata, fare riferimento alla sezione [segmentazione in streaming nella guida utente della segmentazione](./overview.md#scheduled-segmentation).

Una query verrà valutata automaticamente con segmentazione in streaming se soddisfa uno dei seguenti criteri:

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| hit in ingresso | Definizione di segmento che fa riferimento a un singolo evento in arrivo senza limitazioni temporali. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Hit in arrivo all’interno di una finestra temporale relativa | Definizione di segmento che fa riferimento a un singolo evento in arrivo. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Solo profilo | Definizione di segmento che fa riferimento solo a un attributo di profilo. |  |
| Hit in arrivo che fa riferimento a un profilo | Definizione di segmento che fa riferimento a un singolo evento in arrivo, senza limitazioni temporali, e uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Hit in arrivo che fa riferimento a un profilo all’interno di una finestra temporale relativa | Definizione di segmento che fa riferimento a un singolo evento in arrivo e a uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Più eventi che fanno riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Una definizione di segmento **non** sarà abilitata per la segmentazione in streaming nei seguenti scenari:

- La definizione del segmento include segmenti o caratteristiche Adobe Audience Manager (AAM).
- La definizione del segmento include più entità (query con più entità).

Inoltre, durante la segmentazione in streaming si applicano alcune linee guida:

| Tipo di query | Indirizzo |
| ---------- | -------- |
| Query evento singolo | Non ci sono limiti alla finestra di lookback. |
| Query con cronologia eventi | <ul><li>La finestra di lookback è limitata a **un giorno**.</li><li>Tra gli eventi è presente una condizione di ordine di tempo rigoroso **must**.</li><li>Sono supportate le query con almeno un evento negativo. Tuttavia, l&#39;intero evento **non può essere una negazione**.</li></ul> |

Se la definizione di un segmento viene modificata e non soddisfa più i criteri per la segmentazione in streaming, la definizione del segmento passerà automaticamente da &quot;Streaming&quot; a &quot;Batch&quot;.

## Streaming dei dettagli dei segmenti di segmentazione

Dopo aver creato un segmento abilitato per lo streaming, potete visualizzare i dettagli di tale segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

In modo specifico, vengono visualizzati i dettagli relativi alla **[!UICONTROL total qualified audience size]**. Il **[!UICONTROL Total qualified audience size]** mostra il numero totale di audience qualificate dall&#39;ultima esecuzione del processo del segmento completata. Se un processo del segmento non è stato completato entro le ultime 24 ore, il numero di audience verrà preso da una stima.

Sotto c&#39;è un grafico a linee che mostra il numero di segmenti qualificati e non qualificati nelle ultime 24 ore. Il menu a discesa può essere modificato per visualizzare le ultime 24 ore, la settimana scorsa o gli ultimi 30 giorni.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Ulteriori informazioni sulla valutazione dell’ultimo segmento sono reperibili selezionando la bolla delle informazioni.

![](../images/ui/streaming-segmentation/info-bubble.png)

Per ulteriori informazioni sulle definizioni dei segmenti, consulta la sezione precedente su [dettagli di definizione dei segmenti](#segment-details).

## Video dimostrativo sulla segmentazione in streaming

Il seguente video è pensato per comprendere meglio la segmentazione in streaming. Mostra un esempio di esperienza del cliente seguito da una breve presentazione delle funzioni chiave nell&#39;interfaccia [!DNL Platform].

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Passaggi successivi

Questa guida utente spiega come funzionano le definizioni dei segmenti abilitate per lo streaming su Adobe Experience Platform e come monitorare i segmenti abilitati per lo streaming.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente di Adobe Experience Platform, consultare la [Guida utente alla segmentazione](./overview.md).