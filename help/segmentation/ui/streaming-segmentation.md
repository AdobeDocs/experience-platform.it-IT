---
keywords: Experience Platform;home;popular topics;streaming segmentation;Segmentation;Segmentation Service;segmentation service;ui guide;
solution: Experience Platform
title: Segmentazione in streaming
topic: ui guide
description: La segmentazione in streaming su Adobe Experience Platform consente di eseguire la segmentazione in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualifica del segmento ora avviene quando i dati entrano in piattaforma, eliminando la necessità di pianificare ed eseguire processi di segmentazione. Grazie a questa funzionalità, ora è possibile valutare la maggior parte delle regole del segmento quando i dati vengono passati in Piattaforma, il che significa che l'appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.
translation-type: tm+mt
source-git-commit: 578579438ca1d6a7a8c0a023efe2abd616a6dff2
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---


# Segmentazione in streaming

>[!NOTE]
>
>Il seguente documento spiega come utilizzare la segmentazione in streaming utilizzando l&#39;interfaccia utente. Per informazioni sull&#39;utilizzo della segmentazione in streaming mediante l&#39;API, consultate la guida [API per la segmentazione in](../api/streaming-segmentation.md)streaming.

Lo streaming della segmentazione su [!DNL Adobe Experience Platform] consente ai clienti di effettuare la segmentazione in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualifica del segmento ora avviene quando i dati in streaming arrivano [!DNL Platform], eliminando la necessità di pianificare ed eseguire processi di segmentazione. Grazie a questa funzionalità, ora è possibile valutare la maggior parte delle regole del segmento nel momento in cui i dati vengono passati, [!DNL Platform]il che significa che l&#39;appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

>[!NOTE]
>
>La segmentazione in streaming può essere utilizzata solo per valutare i dati in streaming in Piattaforma. In altre parole, i dati acquisiti tramite l’assimilazione batch non verranno valutati tramite la segmentazione in streaming e verranno valutati insieme al processo segmentato pianificato ogni sera.

## Tipi di query di segmentazione in streaming

>[!NOTE]
>
>Per consentire il funzionamento della segmentazione in streaming, è necessario abilitare la segmentazione pianificata per l&#39;organizzazione. Per informazioni dettagliate sull’abilitazione della segmentazione pianificata, consultate [la sezione relativa alla segmentazione in streaming nella guida](./overview.md#scheduled-segmentation)utente alla segmentazione.

Una query verrà valutata automaticamente con segmentazione in streaming se soddisfa uno dei seguenti criteri:

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| hit in ingresso | Definizione di segmento che fa riferimento a un singolo evento in arrivo senza limitazioni temporali. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Hit in arrivo all’interno di una finestra temporale relativa | Definizione di segmento che fa riferimento a un singolo evento in arrivo. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Solo profilo | Definizione di segmento che fa riferimento solo a un attributo di profilo. |  |
| Hit in arrivo che fa riferimento a un profilo | Definizione di segmento che fa riferimento a un singolo evento in arrivo, senza limitazioni temporali, e uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Hit in arrivo che fa riferimento a un profilo all’interno di una finestra temporale relativa | Definizione di segmento che fa riferimento a un singolo evento in arrivo e a uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Più eventi che fanno riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Nella sezione seguente sono elencati alcuni esempi di definizione del segmento che **non** saranno abilitati per la segmentazione in streaming.

| Tipo di query | Dettagli |
| ---------- | ------- |
| Hit in arrivo che fa riferimento a un profilo all’interno di una finestra relativa | Definizione del segmento che include [!DNL Adobe Audience Manager (AAM)] segmenti o caratteristiche. |
| Più eventi che fanno riferimento a un profilo | Definizione di segmento che include segmenti o caratteristiche Adobe Audience Manager (AAM). |
| Query con più entità | Nel complesso, le query con più entità **non** sono supportate dalla segmentazione in streaming. |

Inoltre, durante la segmentazione in streaming si applicano alcune linee guida:

| Tipo di query | Indirizzo |
| ---------- | -------- |
| Query evento singolo | Non ci sono limiti alla finestra di lookback. |
| Query con cronologia eventi | <ul><li>La finestra di look-back è limitata a **un giorno**.</li><li>Tra gli eventi **deve** esistere una condizione di ordine di tempo restrittivo.</li><li>Sono consentiti solo gli ordini temporali semplici (prima e dopo) tra gli eventi.</li><li>I singoli eventi **non possono** essere negati. Tuttavia, l’intera query **può** essere negata.</li></ul> |

Se la definizione di un segmento viene modificata e non soddisfa più i criteri per la segmentazione in streaming, la definizione del segmento passerà automaticamente da &quot;Streaming&quot; a &quot;Batch&quot;.

## Streaming dei dettagli dei segmenti di segmentazione

Dopo aver creato un segmento abilitato per lo streaming, potete visualizzare i dettagli di tale segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Nello specifico, **[!UICONTROL total qualified audience size]** vengono visualizzati i dettagli relativi all&#39;evento. Mostra **[!UICONTROL Total qualified audience size]** il numero totale di audience qualificate dall&#39;ultima esecuzione del processo del segmento completata. Se un processo del segmento non è stato completato entro le ultime 24 ore, il numero di audience verrà preso da una stima.

Sotto c&#39;è un grafico a linee che mostra il numero di segmenti qualificati e non qualificati nelle ultime 24 ore. Il menu a discesa può essere modificato per visualizzare le ultime 24 ore, la settimana scorsa o gli ultimi 30 giorni.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Ulteriori informazioni sulla valutazione dell’ultimo segmento sono reperibili selezionando la bolla delle informazioni.

![](../images/ui/streaming-segmentation/info-bubble.png)

Per ulteriori informazioni sulle definizioni dei segmenti, consulta la sezione precedente sui dettagli [delle definizioni dei](#segment-details)segmenti.

## Video dimostrativo sulla segmentazione in streaming

Il seguente video è pensato per comprendere meglio la segmentazione in streaming. Mostra un esempio di esperienza del cliente seguito da una breve presentazione delle funzioni chiave nell&#39; [!DNL Platform] interfaccia.

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Passaggi successivi

Questa guida utente spiega come funzionano le definizioni dei segmenti abilitate per lo streaming su Adobe Experience Platform e come monitorare i segmenti abilitati per lo streaming.

Per ulteriori informazioni sull’utilizzo dell’interfaccia utente di Adobe Experience Platform, consulta la guida [utente alla](./overview.md)segmentazione.