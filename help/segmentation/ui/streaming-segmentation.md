---
keywords: Experience Platform;home;argomenti popolari;segmentazione in streaming;Segmentazione;Servizio di segmentazione;servizio di segmentazione;guida interfaccia utente;
solution: Experience Platform
title: Guida all’interfaccia utente per la segmentazione in streaming
topic-legacy: ui guide
description: La segmentazione in streaming su Adobe Experience Platform consente di eseguire la segmentazione in tempo quasi reale concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati arrivano in Platform, alleviando la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità, la maggior parte delle regole del segmento può ora essere valutata quando i dati vengono trasmessi in Platform, il che significa che l’appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 58b546ea83774672dd36ca6cd952e229410aa645
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# Segmentazione streaming

>[!NOTE]
>
>Il seguente documento spiega come utilizzare la segmentazione in streaming utilizzando l’interfaccia utente. Per informazioni sull’utilizzo della segmentazione in streaming tramite API, consulta la [guida API per la segmentazione in streaming](../api/streaming-segmentation.md).

Segmentazione streaming su [!DNL Adobe Experience Platform] consente ai clienti di effettuare segmentazione in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati in streaming arrivano in [!DNL Platform], per ridurre la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità, ora è possibile valutare la maggior parte delle regole di segmento quando i dati vengono trasmessi in [!DNL Platform], il che significa che l’appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

>[!NOTE]
>
>
>I segmenti valutati con la segmentazione in streaming possono variare tra l’appartenenza ideale e quella effettiva se il segmento è basato su un altro segmento valutato utilizzando la segmentazione in batch. Ad esempio, se il segmento A è basato sul segmento B e il segmento B viene valutato utilizzando la segmentazione batch, poiché il segmento B viene aggiornato solo ogni 24 ore, il segmento A si allontanerà ulteriormente dai dati effettivi fino a quando non viene sincronizzato nuovamente con l’aggiornamento del segmento B.

## Tipi di query per segmentazione in streaming {#query-types}

>[!NOTE]
>
>Affinché la segmentazione in streaming funzioni, è necessario abilitare la segmentazione pianificata per l’organizzazione. Per informazioni dettagliate sull’abilitazione della segmentazione pianificata, consulta [la sezione segmentazione in streaming nella guida utente Segmentazione](./overview.md#scheduled-segmentation).

Una query viene valutata automaticamente con la segmentazione in streaming se soddisfa uno dei seguenti criteri:

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Singolo evento all’interno di una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Singolo evento con una finestra temporale | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo con una finestra temporale. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. |  |
| Singolo evento con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo, senza restrizioni di tempo, e a uno o più attributi di profilo. **Nota:** La query viene valutata immediatamente quando viene generato l’evento. Nel caso di un evento di profilo, tuttavia, deve attendere 24 ore per essere incorporato. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Singolo evento con un attributo di profilo in una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo e a uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti in batch o in streaming. **Nota:** Se utilizzi un segmento, si verificherà l’annullamento della qualifica del profilo **ogni 24 ore**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Eventi multipli con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Una definizione di segmento **not** è abilitata per la segmentazione in streaming nei seguenti scenari:

- La definizione del segmento include segmenti o caratteristiche Adobe Audience Manager (AAM).
- La definizione del segmento include più entità (query con più entità).

Durante la segmentazione in streaming si applicano le seguenti linee guida:

| Tipo di query | Indirizzo |
| ---------- | -------- |
| Query a evento singolo | Non ci sono limiti all’intervallo di lookback. |
| Query con cronologia eventi | <ul><li>L’intervallo di lookback è limitato a **un giorno**.</li><li>Una rigorosa condizione di ordinamento dei tempi **deve** esistono tra gli eventi.</li><li>Sono supportate le query con almeno un evento negato. Tuttavia, l&#39;intero evento **impossibile** sia una negazione.</li></ul> |

Se la definizione di un segmento viene modificata in modo da non soddisfare più i criteri per la segmentazione in streaming, la definizione del segmento passa automaticamente da &quot;Streaming&quot; a &quot;Batch&quot;.

Inoltre, l’annullamento della qualificazione dei segmenti, analogamente alla qualificazione dei segmenti, avviene in tempo reale. Di conseguenza, se un pubblico non è più idoneo per un segmento, verrà immediatamente non qualificato. Ad esempio, se la definizione del segmento richiede &quot;Tutti gli utenti che hanno acquistato scarpe rosse nelle ultime tre ore&quot;, dopo tre ore, tutti i profili inizialmente qualificati per la definizione del segmento non saranno qualificati.

## Dettagli dei segmenti di segmentazione in streaming

Dopo aver creato un segmento abilitato per lo streaming, puoi visualizzare i dettagli di tale segmento.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

In particolare, i dettagli **[!UICONTROL dimensione totale del pubblico qualificato]** vengono visualizzati. La **[!UICONTROL Dimensione totale del pubblico qualificato]** mostra il numero totale di tipi di pubblico qualificati dall’ultima esecuzione di processi del segmento completata. Se un lavoro di segmento non è stato completato nelle ultime 24 ore, il numero di tipi di pubblico verrà invece calcolato in base a una stima.

Sotto c’è un grafico a linee che mostra il numero di segmenti qualificati e non qualificati nelle ultime 24 ore. Il menu a discesa può essere regolato in modo da visualizzare le ultime 24 ore, la settimana scorsa o gli ultimi 30 giorni.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Per ulteriori informazioni sulla valutazione dell’ultimo segmento, seleziona la bolla di informazioni.

![](../images/ui/streaming-segmentation/info-bubble.png)

Per ulteriori informazioni sulle definizioni dei segmenti, consulta la sezione precedente su [dettagli di definizione del segmento](#segment-details).

## Passaggi successivi

Questa guida utente spiega come funzionano le definizioni dei segmenti abilitate per lo streaming su Adobe Experience Platform e come monitorare i segmenti abilitati per lo streaming.

Per ulteriori informazioni sull’utilizzo dell’interfaccia utente di Adobe Experience Platform, consulta la sezione [Guida utente alla segmentazione](./overview.md).

## Appendice

Nella sezione seguente sono elencate le domande frequenti sulla segmentazione in streaming:

Nella sezione seguente sono elencate le domande frequenti sulla segmentazione in streaming:

### La segmentazione in streaming avviene anche in tempo reale?

Per la maggior parte delle istanze, l’annullamento della segmentazione in streaming avviene in tempo reale. Tuttavia, i segmenti in streaming che utilizzano segmenti **not** non sono qualificati in tempo reale, ma non possono essere qualificati dopo 24 ore.

### Su quali dati funziona la segmentazione in streaming?

La segmentazione in streaming funziona su tutti i dati acquisiti tramite un’origine streaming. I segmenti acquisiti utilizzando un’origine basata su batch verranno valutati ogni notte, anche se idonei per la segmentazione in streaming.

### Come vengono definiti i segmenti come segmentazione in batch o in streaming?

Un segmento è definito come segmentazione in batch o in streaming in base a una combinazione di tipo di query e durata della cronologia degli eventi. Un elenco dei segmenti che verranno valutati come segmento in streaming si trova nella sezione [sezione tipi di query per segmentazione in streaming](#query-types).

### Un utente può definire un segmento come segmentazione in batch o in streaming?

Al momento, l’utente non può definire se un segmento viene valutato utilizzando l’acquisizione in batch o in streaming, in quanto il sistema determinerà automaticamente con quale metodo verrà valutato il segmento.

### Perché il numero di segmenti &quot;qualificati totali&quot; continua ad aumentare mentre il numero sotto &quot;Ultimi X giorni&quot; rimane a zero all’interno della sezione dei dettagli del segmento?

Il numero di segmenti qualificati totali viene ricavato dal processo di segmentazione giornaliera, che include i tipi di pubblico idonei per i segmenti batch e in streaming. Questo valore viene visualizzato sia per i segmenti batch che per quelli in streaming.

Il numero sotto &quot;Ultimi X giorni&quot; **only** include i tipi di pubblico qualificati nella segmentazione in streaming, e **only** aumenta se hai inviato dati in streaming nel sistema e conta verso tale definizione di streaming. Questo valore è **only** mostrata per i segmenti in streaming. Di conseguenza, questo valore **possono** viene visualizzato come 0 per i segmenti batch.

Di conseguenza, se vedi che il numero sotto &quot;Ultimi X giorni&quot; è zero, e il grafico a linee è anche pari a zero, hai **not** ha inviato in streaming nel sistema tutti i profili idonei per quel segmento.