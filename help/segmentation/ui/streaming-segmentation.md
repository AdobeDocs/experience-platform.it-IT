---
keywords: Experience Platform;home;argomenti popolari;streaming segmentation;Segmentation;Segmentation Service;segmentation service;ui guide;
solution: Experience Platform
title: Guida dell’interfaccia utente Segmentazione streaming
description: La segmentazione in streaming su Adobe Experience Platform consente di eseguire la segmentazione quasi in tempo reale concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati arrivano in Platform, riducendo la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità, la maggior parte delle regole del segmento ora possono essere valutate quando i dati vengono passati in Platform, il che significa che l’iscrizione al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 0%

---

# Segmentazione in streaming

>[!NOTE]
>
>Il documento seguente illustra come utilizzare la segmentazione in streaming utilizzando l’interfaccia utente. Per informazioni sull’utilizzo della segmentazione in streaming tramite l’API, leggi la sezione [guida dell’API per la segmentazione in streaming](../api/streaming-segmentation.md).

Segmentazione in streaming su [!DNL Adobe Experience Platform] consente ai clienti di eseguire la segmentazione quasi in tempo reale concentrandosi al contempo sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati in streaming arrivano in [!DNL Platform], riducendo la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità, la maggior parte delle regole del segmento può ora essere valutata mentre i dati vengono trasmessi in [!DNL Platform], il che significa che l’iscrizione al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

>[!NOTE]
>
>La segmentazione in streaming funziona su tutti i dati acquisiti utilizzando un’origine di streaming. I dati acquisiti utilizzando un’origine basata su batch vengono valutati di notte, anche se sono idonei per la segmentazione in streaming.
>
>Inoltre, i segmenti valutati con la segmentazione in streaming possono spostarsi tra l’appartenenza ideale e quella effettiva se il segmento è basato su un altro segmento valutato utilizzando la segmentazione batch. Ad esempio, se il segmento A è basato sul segmento B e il segmento B viene valutato utilizzando la segmentazione batch, poiché il segmento B viene aggiornato solo ogni 24 ore, il segmento A si allontanerà ulteriormente dai dati effettivi fino a sincronizzarsi nuovamente con l’aggiornamento del segmento B.

## Tipi di query di segmentazione in streaming {#query-types}

>[!NOTE]
>
>Affinché la segmentazione in streaming funzioni, devi abilitare la segmentazione pianificata per l’organizzazione. Per informazioni dettagliate sull’abilitazione della segmentazione pianificata, consulta [la sezione segmentazione in streaming nella guida utente Segmentazione](./overview.md#scheduled-segmentation).

Una query verrà valutata automaticamente con segmentazione in streaming se soddisfa uno dei seguenti criteri:

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | ![Viene visualizzato un esempio di un singolo evento.](../images/ui/streaming-segmentation/incoming-hit.png) |
| Singolo evento entro una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo. | ![Viene visualizzato un esempio di un singolo evento all’interno di una finestra temporale relativa.](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Evento singolo con finestra temporale | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo con una finestra temporale. | ![Viene visualizzato un esempio di un singolo evento con una finestra temporale.](../images/ui/streaming-segmentation/historic-time-window.png) |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. |  |
| Evento singolo con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo, senza restrizioni temporali, e a uno o più attributi di profilo. **Nota:** La query viene valutata immediatamente quando si verifica l’evento. Nel caso di un evento profilo, tuttavia, deve attendere 24 ore per essere incorporato. | ![Viene visualizzato un esempio di un singolo evento con un attributo di profilo.](../images/ui/streaming-segmentation/profile-hit.png) |
| Singolo evento con un attributo di profilo all’interno di una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo e a uno o più attributi di profilo. | ![Viene visualizzato un esempio di un singolo evento con un attributo di profilo all’interno di una finestra temporale relativa.](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti batch o in streaming. **Nota:** Se si utilizza un segmento di segmenti, si verifica l’interruzione del profilo **ogni 24 ore**. | ![Viene mostrato un esempio di un segmento di segmenti.](../images/ui/streaming-segmentation/two-batches.png) |
| Più eventi con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. | ![Viene mostrato un esempio di più eventi con un attributo di profilo.](../images/ui/streaming-segmentation/event-history-success.png) |

Una definizione di segmento **non** essere abilitato per la segmentazione in streaming nei seguenti scenari:

- La definizione del segmento include segmenti o caratteristiche di Adobe Audience Manager (AAM).
- La definizione del segmento include più entità (query con più entità).
- La definizione del segmento include una combinazione di un singolo evento e un `inSegment` evento.
   - Tuttavia, se il segmento contenuto in `inSegment` evento è solo profilo, la definizione del segmento **will** per la segmentazione in streaming.

Tieni presente che le seguenti linee guida sono applicabili quando esegui la segmentazione in streaming:

| Tipo di query | Linea guida |
| ---------- | -------- |
| Query evento singolo | Non ci sono limiti all’intervallo di lookback. |
| Query con cronologia eventi | <ul><li>L’intervallo di lookback è limitato a **un giorno**.</li><li>Una rigida condizione di ordinamento temporale **deve** esistono tra gli eventi.</li><li>Sono supportate le query con almeno un evento negato. Tuttavia, l’intero evento **non può** essere una negazione.</li></ul> |

Se una definizione di segmento viene modificata in modo da non soddisfare più i criteri per la segmentazione in streaming, la definizione del segmento passerà automaticamente da &quot;Streaming&quot; a &quot;Batch&quot;.

Inoltre, l’annullamento del riconoscimento del segmento, in modo simile alla qualificazione del segmento, avviene in tempo reale. Di conseguenza, se un pubblico non è più idoneo per un segmento, non sarà immediatamente qualificato. Ad esempio, se la definizione del segmento richiede &quot;Tutti gli utenti che hanno acquistato scarpe rosse nelle ultime tre ore&quot;, dopo tre ore tutti i profili che si sono inizialmente qualificati per la definizione del segmento non saranno qualificati.

## Dettagli del segmento di segmentazione in streaming

Dopo aver creato un segmento abilitato allo streaming, puoi visualizzarne i dettagli.

![Viene visualizzata la pagina dei dettagli del segmento.](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

In particolare, **[!UICONTROL Totale qualificato]** viene visualizzata la metrica, che mostra il numero totale di tipi di pubblico idonei, in base alle valutazioni in batch e in streaming per questo segmento.

Sotto è riportato un grafico a linee che mostra il numero di nuovi tipi di pubblico aggiornati nelle ultime 24 ore con il metodo di valutazione in streaming. Il menu a discesa può essere modificato per visualizzare le ultime 24 ore, l’ultima settimana o gli ultimi 30 giorni. Il **[!UICONTROL Nuovo pubblico aggiornato]** La metrica si basa sulla modifica della dimensione del pubblico durante l’intervallo di tempo selezionato, come valutato dalla segmentazione in streaming. Questa metrica non include il pubblico qualificato totale dalla valutazione batch giornaliera dei segmenti.

>[!NOTE]
>
>Un segmento è considerato qualificato se passa da non avere stato a realizzato o se passa da uscita a realizzato. Un segmento è considerato non qualificato se passa da realizzato a terminato o da esistente a terminato.
>
>Ulteriori informazioni su questi stati sono disponibili nella tabella di stato all&#39;interno di [panoramica sulla segmentazione](./overview.md#browse).

![Viene evidenziata la scheda Profiles over time (Profili nel tempo), che mostra un grafico a linee dei profili nel tempo.](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Per ulteriori informazioni sull’ultima valutazione del segmento, seleziona la bolla di informazioni accanto a **[!UICONTROL Totale qualificato]**.

![È stata selezionata la bolla di informazioni per il totale dei profili qualificati. Visualizza informazioni sull’ora dell’ultima valutazione del segmento.](../images/ui/streaming-segmentation/info-bubble.png)

Per ulteriori informazioni sulle definizioni dei segmenti, consulta la sezione precedente su [dettagli della definizione del segmento](#segment-details).

## Passaggi successivi

Questa guida utente spiega come le definizioni dei segmenti abilitati per lo streaming funzionano in Adobe Experience Platform e come monitorare i segmenti abilitati per lo streaming.

Per ulteriori informazioni sull’utilizzo dell’interfaccia utente di Adobe Experience Platform, consulta [Guida utente alla segmentazione](./overview.md).

## Appendice

Nella sezione seguente sono elencate le domande frequenti sulla segmentazione in streaming:

### La segmentazione in streaming &quot;unqualification&quot; (non qualificazione) si verifica anche in tempo reale?

Nella maggior parte dei casi, l’annullamento della qualifica per segmentazione in streaming avviene in tempo reale. Tuttavia, i segmenti di streaming che utilizzano segmenti di segmenti lo fanno **non** non qualificato in tempo reale, ma non qualificato dopo 24 ore.

### Su quali dati funziona la segmentazione in streaming?

La segmentazione in streaming funziona su tutti i dati acquisiti utilizzando un’origine di streaming. I segmenti acquisiti utilizzando un’origine basata su batch vengono valutati di notte, anche se è idoneo per la segmentazione in streaming. Gli eventi inviati in streaming al sistema con una marca temporale precedente alle 24 ore verranno elaborati nel processo batch successivo.

### Come vengono definiti i segmenti come segmentazione in batch o in streaming?

Un segmento è definito come segmentazione in batch o in streaming basata su una combinazione di tipo di query e durata della cronologia degli eventi. Un elenco dei segmenti che verranno valutati come segmenti di streaming si trova in [sezione tipi di query di segmentazione in streaming](#query-types).

Tieni presente che se un segmento contiene **entrambi** un `inSegment` e una catena di eventi singola diretta, non può qualificarsi per la segmentazione in streaming. Se desideri che questo segmento sia idoneo per la segmentazione in streaming, devi rendere la catena di eventi singoli diretti un suo segmento.

### Perché il numero di segmenti &quot;qualificati totali&quot; continua a crescere mentre il numero in &quot;Ultimi X giorni&quot; rimane pari a zero all’interno della sezione dei dettagli del segmento?

Il numero di segmenti qualificati totali viene ricavato dal processo di segmentazione giornaliero, che include tipi di pubblico idonei sia per i segmenti in batch che per quelli in streaming. Questo valore viene visualizzato sia per i segmenti batch che per quelli in streaming.

Il numero sotto &quot;Ultimi X giorni&quot; **solo** include tipi di pubblico qualificati per la segmentazione in streaming e **solo** aumenta se i dati sono stati inviati in streaming al sistema e vengono conteggiati per tale definizione di streaming. Questo valore è **solo** mostrato per i segmenti di streaming. Di conseguenza questo valore **maggio** visualizza come 0 per i segmenti batch.

Di conseguenza, se noti che il numero in &quot;Ultimi X giorni&quot; è zero e anche il grafico a linee riporta zero, hai **non** ha inviato in streaming nel sistema tutti i profili idonei per quel segmento.

### Quanto tempo ci vuole per rendere disponibile un segmento?

È necessaria fino a un’ora perché un segmento sia disponibile.