---
solution: Experience Platform
title: Guida dell’interfaccia utente Segmentazione streaming
description: La segmentazione in streaming su Adobe Experience Platform consente di eseguire la segmentazione quasi in tempo reale concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati arrivano in Platform, riducendo la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità, la maggior parte delle regole del segmento ora possono essere valutate quando i dati vengono passati in Platform, il che significa che l’iscrizione al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: c2f9bcd9aeb0073b8b26413ec29e2dff1ee5c80d
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 0%

---

# Segmentazione in streaming

>[!NOTE]
>
>Il documento seguente illustra come utilizzare la segmentazione in streaming utilizzando l’interfaccia utente. Per informazioni sull&#39;utilizzo della segmentazione in streaming tramite l&#39;API, leggere la [guida dell&#39;API di segmentazione in streaming](../api/streaming-segmentation.md).

La segmentazione in streaming su [!DNL Adobe Experience Platform] consente ai clienti di eseguire la segmentazione quasi in tempo reale concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati in streaming arrivano in [!DNL Platform], riducendo la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità è ora possibile valutare la maggior parte delle regole del segmento quando i dati vengono passati in [!DNL Platform], il che significa che l&#39;appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

>[!NOTE]
>
>La segmentazione in streaming funziona su tutti i dati acquisiti utilizzando un’origine di streaming. I dati acquisiti utilizzando un’origine basata su batch vengono valutati di notte, anche se sono idonei per la segmentazione in streaming.
>
>Inoltre, i segmenti valutati con la segmentazione in streaming possono spostarsi tra l’appartenenza ideale e quella effettiva se la definizione del segmento è basata su un’altra definizione di segmento valutata utilizzando la segmentazione batch. Ad esempio, se il segmento A è basato sul segmento B e il segmento B viene valutato utilizzando la segmentazione batch, poiché il segmento B viene aggiornato solo ogni 24 ore, il segmento A si allontanerà ulteriormente dai dati effettivi fino a sincronizzarsi nuovamente con l’aggiornamento del segmento B.

## Tipi di query di segmentazione in streaming {#query-types}

>[!NOTE]
>
>Affinché la segmentazione in streaming funzioni, devi abilitare la segmentazione pianificata per l’organizzazione. Per informazioni dettagliate sull&#39;abilitazione della segmentazione pianificata, consulta [la panoramica di Audience Portal](./audience-portal.md#scheduled-segmentation).

Una query verrà valutata automaticamente con segmentazione in streaming se soddisfa uno dei seguenti criteri:

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | ![Viene visualizzato un esempio di un singolo evento.](../images/ui/streaming-segmentation/incoming-hit.png) |
| Singolo evento entro una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo. | ![Viene visualizzato un esempio di un singolo evento all&#39;interno di un intervallo di tempo relativo.](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Evento singolo con finestra temporale | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo con una finestra temporale. | ![Viene visualizzato un esempio di un singolo evento con una finestra temporale.](../images/ui/streaming-segmentation/historic-time-window.png) |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. | |
| Singolo evento con un attributo di profilo entro un intervallo di tempo relativo inferiore a 24 ore | Qualsiasi definizione di segmento che si riferisce a un singolo evento in arrivo, con uno o più attributi di profilo, e si verifica entro un intervallo di tempo relativo inferiore a 24 ore. | ![Viene visualizzato un esempio di un singolo evento con un attributo di profilo all&#39;interno di un intervallo di tempo relativo.](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti batch o in streaming. **Nota:** se si utilizza un segmento di segmenti, l&#39;annullamento del profilo avverrà **ogni 24 ore**. | ![Viene visualizzato un esempio di segmento di segmenti.](../images/ui/streaming-segmentation/two-batches.png) |
| Più eventi con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. | ![Viene visualizzato un esempio di più eventi con un attributo di profilo.](../images/ui/streaming-segmentation/event-history-success.png) |

Una definizione di segmento **non** verrà abilitata per la segmentazione in streaming nei seguenti scenari:

- La definizione del segmento include segmenti o caratteristiche di Adobe Audience Manager (AAM).
- La definizione del segmento include più entità (query con più entità).
- La definizione del segmento include una combinazione di un singolo evento e un evento `inSegment`.
   - Tuttavia, se la definizione del segmento contenuta nell&#39;evento `inSegment` è solo di profilo, la definizione del segmento **sarà** abilitata per la segmentazione in streaming.
- La definizione del segmento utilizza &quot;Ignora anno&quot; come parte dei vincoli di tempo.

Tieni presente che le seguenti linee guida sono applicabili quando esegui la segmentazione in streaming:

| Tipo di query | Linea guida |
| ---------- | -------- |
| Query evento singolo | Non ci sono limiti all’intervallo di lookback. |
| Query con cronologia eventi | <ul><li>L&#39;intervallo di lookback è limitato a **un giorno**.</li><li>Tra gli eventi è presente una condizione di ordinamento temporale **must**.</li><li>Sono supportate le query con almeno un evento negato. L&#39;intero evento **non può** essere una negazione.</li></ul> |

Se una definizione di segmento viene modificata in modo da non soddisfare più i criteri per la segmentazione in streaming, la definizione del segmento passerà automaticamente da &quot;Streaming&quot; a &quot;Batch&quot;.

Inoltre, l’annullamento del riconoscimento del segmento, in modo simile alla qualificazione del segmento, avviene in tempo reale. Di conseguenza, se un pubblico non è più idoneo per un segmento, non sarà immediatamente qualificato. Ad esempio, se la definizione del segmento richiede &quot;Tutti gli utenti che hanno acquistato scarpe rosse nelle ultime tre ore&quot;, dopo tre ore tutti i profili che si sono inizialmente qualificati per la definizione del segmento non saranno qualificati.

## Dettagli della definizione del segmento di segmentazione in streaming

Dopo aver creato un segmento abilitato allo streaming, puoi visualizzarne i dettagli.

![Viene visualizzata la pagina dei dettagli di definizione del segmento.](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

In particolare, viene visualizzata la metrica **[!UICONTROL Totale qualificato]** che mostra il numero totale di tipi di pubblico qualificati, in base alle valutazioni in batch e in streaming per questo segmento.

Sotto è riportato un grafico a linee che mostra il numero di nuovi tipi di pubblico aggiornati nelle ultime 24 ore con il metodo di valutazione in streaming. Il menu a discesa può essere modificato per visualizzare le ultime 24 ore, l’ultima settimana o gli ultimi 30 giorni. La metrica **[!UICONTROL Nuovo pubblico aggiornato]** si basa sulla modifica della dimensione del pubblico durante l&#39;intervallo di tempo selezionato, come valutato dalla segmentazione in streaming. Questa metrica non include il pubblico qualificato totale dalla valutazione batch giornaliera dei segmenti.

>[!NOTE]
>
>Una definizione di segmento è considerata qualificata se passa da non avere stato a realizzata o se passa da uscita a realizzata. Una definizione di segmento è considerata non qualificata se passa da realizzata a uscita.
>
>Ulteriori informazioni su questi stati sono disponibili nella tabella di stato in [Panoramica di Audience Portal](./audience-portal.md#customize).

![La scheda Profili nel tempo è evidenziata e mostra un grafico a linee dei profili nel tempo.](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Ulteriori informazioni sull&#39;ultima valutazione del segmento sono disponibili selezionando la bolla delle informazioni accanto a **[!UICONTROL Totale qualificato]**.

![È stata selezionata la bolla di informazioni per il totale dei profili qualificati. Visualizza informazioni sull&#39;ora dell&#39;ultima valutazione del segmento.](../images/ui/streaming-segmentation/info-bubble.png)

Per ulteriori informazioni sulle definizioni dei segmenti, consulta la sezione precedente su [dettagli definizione segmento](#segment-details).

## Passaggi successivi

Questa guida utente spiega come le definizioni dei segmenti abilitati per lo streaming funzionano in Adobe Experience Platform e come monitorare i segmenti abilitati per lo streaming.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente di Adobe Experience Platform, leggere la [Guida utente per la segmentazione](./overview.md).

## Appendice

Nella sezione seguente sono elencate le domande frequenti sulla segmentazione in streaming:

### La segmentazione in streaming &quot;unqualification&quot; (non qualificazione) si verifica anche in tempo reale?

Nella maggior parte dei casi, l’annullamento della qualifica per segmentazione in streaming avviene in tempo reale. Tuttavia, i segmenti di streaming che utilizzano segmenti di segmenti non **** sono idonei in tempo reale, ma vengono annullati dopo 24 ore.

### Su quali dati funziona la segmentazione in streaming?

La segmentazione in streaming funziona su tutti i dati acquisiti utilizzando un’origine di streaming. I segmenti acquisiti utilizzando un’origine basata su batch vengono valutati di notte, anche se è idoneo per la segmentazione in streaming. Gli eventi inviati in streaming al sistema con una marca temporale precedente alle 24 ore verranno elaborati nel processo batch successivo.

### Come vengono definiti i segmenti come segmentazione in batch o in streaming?

Una definizione di segmento è definita come batch, streaming o segmentazione Edge in base a una combinazione di tipo di query e durata della cronologia degli eventi. Nella sezione [tipi di query di segmentazione in streaming](#query-types) è disponibile un elenco dei segmenti che verranno valutati come definizione di segmento in streaming.

Tieni presente che se una definizione di segmento contiene **both** un&#39;espressione `inSegment` e una catena di eventi singola diretta, non può essere qualificata per la segmentazione in streaming. Se desideri che questa definizione di segmento sia idonea per la segmentazione in streaming, devi rendere la catena di eventi singoli diretti un suo segmento.

### Perché il numero di segmenti &quot;qualificati totali&quot; continua a crescere mentre il numero in &quot;Ultimi X giorni&quot; rimane pari a zero nella sezione dei dettagli di definizione del segmento?

Il numero di segmenti qualificati totali viene ricavato dal processo di segmentazione giornaliero, che include tipi di pubblico idonei sia per i segmenti in batch che per quelli in streaming. Questo valore viene visualizzato sia per i segmenti batch che per quelli in streaming.

Il numero in &quot;Ultimi X giorni&quot; **solo** include tipi di pubblico qualificati nella segmentazione in streaming e **solo** aumenta se i dati sono stati inviati in streaming al sistema e conta per tale definizione di streaming. Questo valore è **only** visualizzato per i segmenti di streaming. Di conseguenza, questo valore **maggio** viene visualizzato come 0 per i segmenti batch.

Di conseguenza, se noti che il numero in &quot;Ultimi X giorni&quot; è zero e anche il grafico a linee riporta zero, hai **non** inviato in streaming nel sistema tutti i profili idonei per quel segmento.

### Quanto tempo ci vuole affinché una definizione di segmento sia disponibile?

È necessaria fino a un’ora perché la definizione di un segmento sia disponibile.

### Ci sono limiti ai dati inviati in streaming?

Affinché i dati in streaming possano essere utilizzati nella segmentazione in streaming, **deve** essere presente una spaziatura tra gli eventi in streaming. Se un numero eccessivo di eventi viene inviato in streaming nello stesso secondo, Platform tratterà tali eventi come dati generati da bot, che verranno eliminati. Come best practice, è necessario disporre di **almeno** cinque secondi tra i dati dell&#39;evento per garantire che vengano utilizzati correttamente.
