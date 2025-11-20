---
title: Utilizzo licenze e capacità
description: Scopri i limiti di utilizzo delle licenze e di capacità in Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: ae0c626eaad66f663c9d97137087b2cca24d747e
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 6%

---


# Utilizzo delle licenze e capacità

>[!AVAILABILITY]
>
>Per utilizzare questa funzione, è necessario disporre delle seguenti autorizzazioni:
>
>- **Visualizza dashboard utilizzo licenze**
>   - Questa autorizzazione ti consente di **visualizzare** la home di capacità.
>- **Gestione sandbox**
>   - Questa autorizzazione ti consente di **modificare** le allocazioni di capacità.
>   - Inoltre, all&#39;utente **deve** essere assegnato l&#39;accesso a tutte le sandbox per le quali si desidera modificare le allocazioni di capacità.
>
>Ulteriori informazioni sulle autorizzazioni in Experience Platform sono disponibili nella [panoramica sul controllo degli accessi](/help/access-control/home.md#permissions)
>
>Inoltre, se hai acquistato Segmentazione streaming a throughput elevato, **non** potrai allocare le capacità utilizzando la capacità. Per aggiornare le tue capacità, contatta l’Assistenza clienti Adobe.

In Adobe Experience Platform, le funzionalità ti informano se l’organizzazione ha superato uno dei tuoi guardrail e ti forniscono informazioni su come risolvere questi problemi.

Per ulteriori informazioni sui guardrail in Experience Platform, leggere la [panoramica sui guardrail di Real-Time CDP](../../rtcdp/guardrails/overview.md).

## Comportamento della capacità {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Velocità effettiva di streaming"
>abstract="Il valore della velocità effettiva di streaming misura i picchi di eventi in entrata combinati al secondo per l’acquisizione in streaming nel servizio Profilo e nelle sandbox di produzione e sviluppo."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Conteggio del pubblico in streaming"
>abstract="Numero massimo di tipi di pubblico in streaming per sandbox. Questo numero è comprensivo del numero di tipi di pubblico Edge disponibili nella sandbox."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Tipi di pubblico Edge"
>abstract="Numero massimo di tipi di pubblico Edge per sandbox."

Attualmente, Capacity supporta i seguenti servizi:

- Segmentazione in streaming
- Acquisizione in streaming

All’interno di questi servizi, vengono tracciati i seguenti guardrail:

- Il numero massimo di pubblici in streaming è 500
   - Di questi 500 tipi di pubblico in streaming, il numero massimo è 150
- La velocità effettiva combinata iniziale per l’acquisizione in streaming è di 1500 record al secondo (rps)
   - Questo throughput di streaming combinato misura i picchi di eventi in entrata combinati al secondo per l’acquisizione in streaming nel profilo cliente in tempo reale, nelle sandbox di produzione e sviluppo.
   - Puoi acquistare supporto aggiuntivo per la segmentazione in streaming fino a 13.500 record al secondo. Ulteriori informazioni sull&#39;acquisto di diritti aggiuntivi sono disponibili nella [descrizione del prodotto Real-Time CDP](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

La capacità del pubblico è al livello **sandbox**. Ciò significa che, per ogni sandbox presente nell’organizzazione, puoi avere 500 tipi di pubblico in streaming, di cui 150 Edge.

La capacità di trasmissione in streaming si trova a un livello di **organizzazione** e può essere distribuita alle singole sandbox. Ad esempio, con i 1500 rps per la velocità effettiva di acquisizione in streaming, puoi impostare la sandbox di produzione su 1300 rps e la sandbox di sviluppo su 200 rps.

Experience Platform calcola la velocità effettiva della sandbox in intervalli di rotazione di 15 minuti. Questo throughput viene misurato in tempo reale, con i dati aggiornati ogni 60 secondi.

Se l’utilizzo raggiunge l’80% e il 90% della capacità concessa in licenza, Experience Platform invierà un avviso per informarti che stai raggiungendo il massimo della capacità specificata. È possibile modificare le impostazioni per personalizzare la percentuale di capacità in modo da ricevere l&#39;avviso o rimuovere completamente l&#39;avviso.

Se l’utilizzo supera il 100% della capacità concessa in licenza, verrà considerata una violazione della capacità. A questo punto, si verificherà una latenza delle prestazioni e le destinazioni del livello di servizio (SLT) **non** saranno garantite.

## Accesso {#access}

Per accedere alla panoramica della capacità, selezionare **[!UICONTROL License usage]** seguito da **[!UICONTROL Capacity]**.

![Il metodo per accedere alla sezione Capacità è evidenziato.](/help/landing/images/capacity/access-capacity.png)

Viene visualizzata la pagina Panoramica capacità, contenente informazioni quali una cronologia degli avvisi e dettagli sulle capacità dell&#39;organizzazione.

![La pagina di panoramica della capacità viene visualizzata completamente, con le sezioni relative alla cronologia degli avvisi e ai dettagli della capacità.](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

### Cronologia avvisi {#alert-history}

Nella sezione **[!UICONTROL Alert history]** viene visualizzato un elenco delle violazioni di capacità più recenti all&#39;interno dell&#39;organizzazione.

![Viene visualizzata la sezione Cronologia avvisi.](/help/landing/images/capacity/alert-history.png)

| Nome colonna | Descrizione |
| ----------- | ----------- |
| Sandbox | Il nome della sandbox in cui si è verificata la violazione di capacità. |
| Avviso | La capacità che è stata superata nella sandbox. |
| Marca temporale | I dati e l’ora in cui si è verificata la violazione. |

Per visualizzare una cronologia completa degli avvisi per la tua organizzazione, seleziona l&#39;icona ![tre punti](/help/images/icons/more.png), seguita da **[!UICONTROL View all]**.

![Viene visualizzata la cronologia completa degli avvisi per un&#39;organizzazione.](/help/landing/images/capacity/full-alert-history.png)

### Dettagli della capacità {#capacity-details}

La sezione Dettagli capacità contiene informazioni sulle capacità dell&#39;organizzazione. In questa sezione puoi filtrare per sandbox e modificare il periodo di lookback.

![Il selettore sandbox e il selettore data per il periodo di lookback sono evidenziati.](/help/landing/images/capacity/filter-sandbox-and-date.png)

Attualmente, questo mostra informazioni sulla capacità relative alla velocità effettiva dello streaming, ai tipi di pubblico in streaming e ai tipi di pubblico perimetrali.

#### Velocità effettiva di streaming {#streaming-throughput}

La sezione velocità effettiva in streaming visualizza informazioni sulla velocità effettiva in streaming nelle sandbox della tua organizzazione. Il valore della velocità effettiva di streaming misura i picchi di eventi in entrata combinati al secondo per l’acquisizione in streaming nel servizio Profilo.

![Viene visualizzata la sezione della velocità effettiva di streaming all&#39;interno della pagina dei dettagli della capacità.](/help/landing/images/capacity/streaming-throughput-section.png)

| Nome colonna | Descrizione |
| ----------- | ----------- |
| Sandbox | Nome della sandbox. |
| Servizi | Il servizio utilizzato dalla sandbox. Attualmente, l’unico valore supportato è Profilo. |
| Utilizzo (picco) | Il picco di velocità effettiva in streaming dei dati nella sandbox entro il periodo di lookback selezionato. |
| Capacità | Il picco massimo di velocità effettiva di streaming per la sandbox. |
| Violazione | Se si è verificata una violazione, il tipo di violazione per la velocità effettiva di streaming. |
| Azioni consigliate | Colonna che descrive l’azione consigliata per alleviare la violazione. |

Puoi selezionare la singola sandbox per visualizzare una visualizzazione più dettagliata della velocità effettiva di streaming della sandbox.

![Nella sezione della velocità effettiva di streaming è evidenziata una sandbox.](/help/landing/images/capacity/select-sandbox.png)

Viene visualizzata la pagina dei dettagli della velocità effettiva di streaming. Puoi visualizzare un grafico che mostra la velocità effettiva delle richieste rispetto al limite di capacità, un elenco delle sandbox e delle relative velocità effettive, nonché un pulsante per allocare le capacità della tua organizzazione.

![Viene visualizzata la pagina della velocità effettiva di streaming, con informazioni dettagliate sulla velocità effettiva di streaming per la sandbox selezionata.](/help/landing/images/capacity/streaming-capacity-allocation.png)

Per aggiornare le capacità di velocità effettiva di streaming dell&#39;organizzazione, selezionare **[!UICONTROL Allocate capacities]**.

![Il pulsante Alloca capacità è evidenziato nella pagina dei dettagli della velocità effettiva di streaming.](/help/landing/images/capacity/select-allocate.png)

Viene visualizzata la pagina di allocazione. In questa pagina puoi impostare le capacità per le diverse sandbox. La somma di tutte le capacità **deve** corrispondere al totale delle capacità dell&#39;organizzazione.

![Viene visualizzata la pagina allocazione capacità.](/help/landing/images/capacity/allocate-capacity.png)

>[!NOTE]
>
>È possibile impostare la nuova capacità solo in ordini di **100**. Ad esempio, puoi impostare il valore della nuova capacità della sandbox su 300 o 500, ma **non puoi** impostare questo valore su 450.
>
>Se il valore non è nell&#39;ordine di 100, verrà arrotondato per eccesso o per difetto.

Dopo aver aggiornato le allocazioni di capacità, selezionare **[!UICONTROL Save]** per completare gli aggiornamenti. Tieni presente che la riproduzione delle modifiche nell’organizzazione potrebbe richiedere fino a 10 minuti.

#### Conteggio del pubblico {#audience-count}

Le sezioni **[!UICONTROL Streaming audience count]** e **[!UICONTROL Edge audience count]** visualizzano il numero di tipi di pubblico in streaming e edge all&#39;interno della sandbox e il numero massimo di tipi di pubblico in streaming e edge consentiti all&#39;interno della sandbox.

![Vengono visualizzate le sezioni Conteggio pubblico.](/help/landing/images/capacity/audience-count.png)

| Nome colonna | Descrizione |
| ----------- | ----------- |
| Sandbox | Nome della sandbox. |
| Servizi | Servizio utilizzato per la sandbox. |
| Utilizzo | Il numero di tipi di pubblico del tipo elencato presenti nella sandbox. |
| Capacità | Il numero massimo di tipi di pubblico del tipo elencato consentiti nella sandbox. |

## Best practice per la velocità effettiva di streaming {#suggestions}

Puoi risolvere le violazioni della velocità effettiva di streaming adottando una delle seguenti raccomandazioni:

1. Aumenta la capacità allocata per la sandbox.
2. Identifica i flussi di dati a velocità elevata nel [dashboard di monitoraggio](/help/dataflows/ui/monitor-streaming-profile.md) e, se necessario, applica limitazioni o filtri a tali flussi di dati.
3. Ottimizza l’acquisizione utilizzando l’acquisizione in batch per i casi di utilizzo con latenza inferiore.

Inoltre, puoi esaminare i flussi di dati e vedere se è possibile ottimizzare la strategia dei dati.

| Fattore contribuente | Che cos’è | Impatto sui casi d’uso | Best practice |
| --- | --- | --- | --- |
| Conversione da batch a streaming | I carichi di lavoro in batch convertiti in streaming possono aumentare in modo significativo il throughput, influendo sulle prestazioni e sull&#39;allocazione delle risorse. Ad esempio, l’esecuzione di un aggiornamento in blocco del profilo dopo un evento senza limiti di tariffa. | Le strategie di streaming non sono necessarie per i casi di utilizzo in batch in cui non è richiesta l’elaborazione a bassa latenza. | Valuta i requisiti del caso d’uso. Per il marketing in uscita in batch, puoi utilizzare [l&#39;acquisizione in batch](/help/ingestion/batch-ingestion/overview.md) invece dello streaming per gestire l&#39;acquisizione dei dati in modo più efficiente. |
| Acquisizione di dati non necessaria | L’acquisizione di dati non necessari per la personalizzazione aumenta la velocità effettiva senza aggiungere valore e sprecare risorse. Ad esempio, acquisendo in profili tutto il traffico di Analytics, indipendentemente dalla rilevanza. | L’eccesso di dati non rilevanti crea rumore, rendendo più difficile l’identificazione dei punti di dati con impatto. Può anche causare attriti durante la definizione e la gestione di tipi di pubblico e profili. | Acquisisci solo i dati necessari per i tuoi casi d’uso. Assicurati di filtrare i dati non necessari.<ul><li>**Adobe Analytics**: utilizza [filtro a livello di riga](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) per ottimizzare l&#39;immissione di dati.</li><li>**Origini**: utilizza l&#39;API [[!DNL Flow Service] API per filtrare i dati a livello di riga](/help/sources/tutorials/api/filter.md) per le origini supportate come [!DNL Snowflake] e [!DNL Google BigQuery].</li></li>**Stream dati di Edge**: configura [flussi dati dinamici](/help/datastreams/configure-dynamic-datastream.md) per eseguire il filtro a livello di riga del traffico in arrivo da WebSDK.</li></ul> |

## Panoramica video {#video}

Il video seguente offre una panoramica di Capacity.

>[!VIDEO](https://video.tv.adobe.com/v/3475272/?learn=on&enablevpops)

## Domande frequenti {#faq}

La sezione seguente illustra le domande frequenti sulle funzionalità di Capacity.

### Posso avere un limite massimo di velocità effettiva combinata che somma fino a meno del mio massimo target?

+++ Risposta

No. Il limite massimo di velocità effettiva combinata **deve** corrispondere al guardrail della tua organizzazione.

+++

### Cosa succede se supero le capacità massime?

+++ Risposta

Questo dipende dalla capacità superata.

Attualmente, se superi il numero massimo di tipi di pubblico consentiti, i tipi di pubblico in eccesso non verranno interessati. Tuttavia, la possibilità di creare nuovi tipi di pubblico potrebbe essere limitata in futuro.

Se superi la velocità effettiva di streaming, sperimenterai una latenza di prestazioni nell’acquisizione e nella segmentazione.

+++

### Perché devo rispettare le mie capacità massime?

+++ Risposta

Lavorare con le massime capacità garantisce la coerenza dei dati e l&#39;integrità dei dati.

Puoi garantire prestazioni coerenti durante gli eventi di picco, evitando problemi tecnici che potrebbero influire negativamente sulle prestazioni del sistema e influire sulle esperienze dei clienti a valle, migliorando in ultima analisi l’igiene dei dati e le prestazioni complessive del sistema.

+++

### Quali sono le best practice per gestire la velocità effettiva di acquisizione in streaming?

+++ Risposta

Per gestire al meglio la velocità effettiva di acquisizione in streaming, è necessario valutare i set di dati per assicurarsi che assegnino la priorità ai dati necessari per la personalizzazione.


Se non è richiesta l’elaborazione in tempo reale, è necessario utilizzare l’acquisizione in batch invece dell’acquisizione in streaming.

+++
