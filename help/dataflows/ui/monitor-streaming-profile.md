---
title: Monitorare l’acquisizione del profilo di streaming
description: Scopri come utilizzare la dashboard di monitoraggio per monitorare l’acquisizione del profilo di streaming
exl-id: da7bb08d-2684-45a1-b666-7580f2383748
source-git-commit: 75e0231aa9a040226584aeb05f10756b6db8bb62
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 20%

---

# Monitorare l’acquisizione del profilo di streaming

Puoi utilizzare la dashboard di monitoraggio nell’interfaccia utente di Adobe Experience Platform per eseguire il monitoraggio in tempo reale dell’acquisizione del profilo di streaming all’interno della tua organizzazione. Utilizza questa funzione per accedere in modo più trasparente alle metriche di velocità effettiva, latenza e qualità dei dati correlate ai dati in streaming. Inoltre, utilizza questa funzione per gli avvisi proattivi e il recupero di informazioni fruibili per identificare potenziali violazioni della capacità e problemi di acquisizione dei dati.

Leggi la guida seguente per scoprire come utilizzare la dashboard di monitoraggio per tracciare tassi e metriche per i processi di acquisizione dei profili di streaming nella tua organizzazione.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Flussi dati](../home.md): i flussi dati rappresentano processi di dati che trasferiscono informazioni in Experience Platform. Sono configurati in vari servizi per facilitare lo spostamento di dati dai connettori di origine ai set di dati di destinazione, nonché al servizio Identity, al profilo cliente in tempo reale e alle destinazioni.
* [Profilo cliente in tempo reale](../../profile/home.md): Profilo cliente in tempo reale combina dati provenienti da più origini, online, offline, CRM e di terze parti, in un&#39;unica vista actionable di ciascun cliente, consentendo esperienze coerenti e personalizzate in tutti i punti di contatto.
* [Acquisizione in streaming](../../ingestion/streaming-ingestion/overview.md): l&#39;acquisizione in streaming per Experience Platform offre agli utenti un metodo per inviare in tempo reale dati da dispositivi lato client e lato server ad Experience Platform.Experience Platform consente di gestire esperienze coordinate, coerenti e rilevanti generando un profilo cliente in tempo reale per ciascuno dei singoli clienti. &#x200B;L’acquisizione in streaming svolge un ruolo chiave nella creazione di questi profili con la minore latenza possibile.
* [Capacità](../../landing/license-usage-and-guardrails/capacity.md): in Experience Platform, le capacità ti informano se la tua organizzazione ha superato uno dei tuoi guardrail e ti forniscono informazioni su come risolvere questi problemi.

>[!NOTE]
>
>La capacità di trasmissione in streaming supporta fino a 1500 eventi in entrata al secondo. Puoi acquistare ulteriore segmentazione streaming per supportare fino a un massimo di 13.500 eventi in entrata al secondo&#x200B;. Real-Time CDP Per ulteriori informazioni, consultare le descrizioni del prodotto [Pacchetti B2C Edition - Prime e Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

## Metriche di monitoraggio per l’acquisizione del profilo di streaming {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="Monitorare l’acquisizione del profilo di streaming"
>abstract="La dashboard di monitoraggio per i profili di streaming mostra informazioni su velocità effettiva, tassi di acquisizione e latenza. Utilizza questa dashboard per visualizzare, comprendere e analizzare le metriche di elaborazione dei dati. dei profili di streaming in Experience Platform."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="Velocità effettiva della richiesta"
>abstract="Questa metrica rappresenta il numero di eventi che entrano nel sistema di acquisizione al secondo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="Velocità effettiva di elaborazione"
>abstract="Questa metrica rappresenta il numero di eventi correttamente acquisiti dal sistema ogni secondo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="Latenza di acquisizione P95"
>abstract="Questa metrica misura la latenza del 95° percentile dal momento in cui un evento arriva in Experience Platform al momento in cui viene correttamente acquisito nell’archivio Profili."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="Velocità effettiva massima"
>abstract="Questa metrica rappresenta il numero massimo di richieste in entrata al secondo che entrano nell’acquisizione del profilo di streaming."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="Record acquisiti"
>abstract="Questa metrica rappresenta il numero totale di record acquisiti nell’archivio profili all’interno di un intervallo di tempo configurato."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="Record con errori"
>abstract="Questa metrica rappresenta il numero totale di record che, a causa di errori, non sono stati acquisiti nell’archivio profili entro un intervallo di tempo configurato."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="Record ignorati"
>abstract="Questa metrica rappresenta il numero totale di record eliminati in un intervallo di tempo configurato a causa di violazioni della configurazione o della capacità."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="Dettagli errore"
>abstract="Questa metrica rappresenta il numero di eventi non riusciti a causa di errori."
>text="Learn more in documentation"

Utilizza la tabella delle metriche per informazioni specifiche sui flussi di dati. Per informazioni dettagliate su ciascuna colonna, consulta la tabella seguente.

| Metrica | Descrizione | Dimensioni | Frequenza di misurazione |
| --- | --- | --- | --- |
| Velocità effettiva della richiesta | Questa metrica rappresenta il numero di eventi che entrano nel sistema di acquisizione al secondo. | Sandbox/Flusso di dati | Monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi. |
| Velocità effettiva di elaborazione | Questa metrica rappresenta il numero di eventi correttamente acquisiti dal sistema ogni secondo. | Sandbox/Flusso di dati | Monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi. |
| Latenza di acquisizione P95 | Questa metrica misura la latenza del 95° percentile dal momento in cui un evento arriva in Experience Platform al momento in cui viene correttamente acquisito nell’archivio Profili. | Sandbox/Flusso di dati | Monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi. |
| Velocità effettiva massima | Questa metrica rappresenta il numero massimo di richieste in entrata al secondo che entrano nell’acquisizione del profilo di streaming | <ul><li>Sandbox/Flusso di dati</li><li>Esecuzione flusso di dati</li></ul> |
| Record acquisiti | Questa metrica rappresenta il numero totale di record acquisiti nell’archivio profili all’interno di un intervallo di tempo configurato. | <ul><li>Sandbox/Flusso di dati</li><li>Esecuzione flusso di dati</li></ul> | <ul><li>Sandbox/Flusso di dati: monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi.</li><li>Esecuzione del flusso di dati: raggruppato in 15 minuti.</li></ul> |
| Record con errori | Questa metrica rappresenta il numero totale di record che, a causa di errori, non sono stati acquisiti nell’archivio profili entro un intervallo di tempo configurato. | <ul><li>Sandbox/Flusso di dati</li><li>Esecuzione flusso di dati</li></ul> | <ul><li>Sandbox/Flusso di dati: monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi.</li><li>Esecuzione del flusso di dati: raggruppato in 15 minuti.</li></ul> |
| Record ignorati | Questa metrica rappresenta il numero totale di record eliminati in un intervallo di tempo configurato a causa di violazioni della configurazione o della capacità. | <ul><li>Sandbox/Flusso di dati</li><li>Esecuzione flusso di dati</li></ul> | <ul><li>Sandbox/Flusso di dati: monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi.</li><li>Esecuzione del flusso di dati: raggruppato in 15 minuti.</li></ul> |
| Dettagli errore | Questa metrica rappresenta il numero di eventi non riusciti a causa di errori. | Esecuzione flusso di dati | Raggruppati in una finestra oraria. |

{style="table-layout:auto"}

## Utilizza il dashboard di monitoraggio per l’acquisizione del profilo di streaming

Per accedere al dashboard di monitoraggio per l&#39;acquisizione del profilo di streaming, passa all&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Monitoraggio]** dal menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Streaming end-to-end]**.

![Dashboard di monitoraggio per l&#39;acquisizione del profilo di streaming.](../assets/ui/streaming-profiles/monitoring-dashboard.png)

Fai riferimento all&#39;intestazione superiore del dashboard per la scheda delle metriche *[!UICONTROL Profilo]*. Utilizza questa visualizzazione per visualizzare informazioni sui record acquisiti, non riusciti e saltati, nonché sullo stato corrente della velocità effettiva e della latenza della richiesta.

![Scheda del profilo.](../assets/ui/streaming-profiles/profile-card.png)

Quindi, utilizza l’interfaccia per visualizzare informazioni dettagliate sulle metriche di acquisizione del profilo di streaming. Utilizza la funzione calendario per passare da un intervallo di tempo all’altro. Puoi scegliere tra le seguenti finestre temporali preconfigurate:

* [!UICONTROL Ultime 6 ore]
* [!UICONTROL Ultime 12 ore]
* [!UICONTROL Ultime 24 ore]
* [!UICONTROL Ultimi 7 giorni]
* [!UICONTROL Ultimi 30 giorni]

In alternativa, puoi configurare manualmente il tuo intervallo temporale utilizzando il calendario.

Puoi utilizzare tre diverse categorie di metriche nel dashboard di monitoraggio per l&#39;acquisizione del profilo di streaming: [!UICONTROL Throughput], [!UICONTROL Acquisizione] e [!UICONTROL Latenza].

>[!BEGINTABS]

>[!TAB Velocità effettiva]

Seleziona **[!UICONTROL Throughput]** per visualizzare informazioni sulla quantità di dati che Experience Platform sta elaborando in un periodo di tempo configurato. Fai riferimento a questa metrica per valutare l’efficienza e la capacità del sistema.

![Dashboard con visualizzazione impostata su &quot;throughput&quot;.](../assets/ui/streaming-profiles/throughput.png)

* **[Capacità](../../landing/license-usage-and-guardrails/capacity.md)**: la quantità massima di dati che la sandbox può elaborare in condizioni definite.
* **Throughput richieste**: frequenza con cui gli eventi vengono ricevuti dal sistema di acquisizione, misurata in eventi al secondo.
* **Velocità effettiva di elaborazione**: velocità alla quale il sistema acquisisce ed elabora correttamente i payload degli eventi in ingresso, misurata in eventi al secondo.

>[!TAB Acquisizione]

**Acquisizione**: seleziona **[!UICONTROL Acquisizione]** per visualizzare informazioni sui processi di acquisizione nella sandbox. Questi processi di acquisizione vengono misurati in tre metriche diverse.

![Dashboard con visualizzazione impostata su &quot;Ingestion&quot;.](../assets/ui/streaming-profiles/ingestion.png)

* **Record acquisiti**: la quantità totale di record creati in un determinato periodo di tempo. Questa metrica rappresenta i processi di acquisizione dei dati corretti nella sandbox.
* **Record ignorati**: numero totale di record che non sono stati acquisiti a causa di errori.
* **Record ignorati**: numero totale di record ignorati a causa della violazione dei limiti di capacità.

>[!TAB Latenza]

Seleziona **[!UICONTROL Latenza]** per visualizzare informazioni sul tempo necessario ad Experience Platform per rispondere a una richiesta o completare un&#39;operazione entro un determinato periodo di tempo.

![Dashboard con visualizzazione impostata su &quot;latency&quot;.](../assets/ui/streaming-profiles/latency.png)

>[!ENDTABS]

### Utilizzare la tabella delle metriche del flusso di dati

La tabella del flusso di dati elenca tutte le attività di acquisizione in streaming con il corrispondente set di metriche per Real-Time Customer Profile. Ogni flusso di dati viene elencato con il relativo set di dati corrispondente.

Se ti stai avvicinando ai limiti della capacità a livello di sandbox, puoi fare riferimento alla colonna [!UICONTROL Velocità effettiva massima] per identificare tutti i flussi di dati esistenti che contribuiscono ai tassi di consumo. Leggi la [sezione sulle best practice](#best-practices) per ulteriori informazioni sulle best practice per la gestione dei flussi di dati.

Per monitorare i dati che vengono acquisiti in un flusso di dati specifico, seleziona l&#39;icona del filtro ![filter](/help/images/icons/filter-add.png) accanto al nome del flusso di dati.

![Pagina delle metriche](../assets/ui/streaming-profiles/metrics.png)

Quindi, utilizza l’interfaccia delle metriche del flusso di dati per selezionare l’esecuzione di flusso specifica che desideri verificare. Selezionare l&#39;icona filtro ![filter](/help/images/icons/filter-add.png) accanto a un&#39;iterazione di esecuzione del flusso per visualizzare le metriche specifiche dell&#39;esecuzione del flusso selezionata.

![Interfaccia delle metriche del flusso di dati.](../assets/ui/streaming-profiles/flows.png)

Le esecuzioni del flusso di dati rappresentano un’istanza dell’esecuzione del flusso di dati. Ad esempio, se un flusso di dati è pianificato per essere eseguito ogni ora alle 9:00, alle 10:00 e alle 11:00, avrai tre istanze di un flusso eseguito. Le esecuzioni del flusso sono specifiche per la tua particolare organizzazione.

Utilizza la pagina dei dettagli dell’esecuzione del flusso di dati per visualizzare le metriche e le informazioni dell’iterazione di esecuzione selezionata.

![L&#39;interfaccia delle attività di esecuzione del flusso di dati.](../assets/ui/streaming-profiles/flow-runs.png)

## Best practice per la gestione dei flussi di dati {#best-practices}

Leggi la sezione seguente per informazioni su come gestire al meglio i flussi di dati e ottimizzare il consumo di dati su Experience Platform.

### Valutare e ottimizzare i flussi di dati di acquisizione in streaming

Per garantire un’acquisizione efficiente dello streaming, rivedi e regola i flussi di dati e la strategia di elaborazione:

* **Valuta l&#39;utilizzo corrente**: identifica quali flussi di dati e set di dati contribuiscono maggiormente alla velocità effettiva.
* **Assegna priorità ai dati importanti**: è possibile che non tutti i dati siano necessari. Escludi i dati che non supportano casi d’uso per ridurre lo storage e migliorare l’efficienza.
* **Ottimizza modalità di elaborazione**: determina se alcuni dati possono essere spostati dallo streaming all&#39;acquisizione batch. Riserva lo streaming per i casi d’uso che richiedono una latenza bassa, ad esempio la segmentazione in tempo reale.

### Piano per capacità e traffico stagionale

Se il limite corrente di **1.500 eventi al secondo** non è sufficiente, è consigliabile ottimizzare la strategia dei dati o aumentare la capacità di licenza:

* **Analisi dell&#39;utilizzo del set di dati e della sandbox**: rivedi i dati correnti e storici per comprendere in che modo il traffico e il coinvolgimento influiscono sulla velocità effettiva di segmentazione in streaming.
* **Account per la stagionalità**: identifica i periodi di traffico di picco guidati da campagne di marketing ricorrenti o cicli specifici del settore.
* **Previsione della domanda futura**: stima dei volumi di traffico e coinvolgimento futuri in base alle tendenze stagionali passate, alle campagne pianificate o agli eventi principali.

| Fattore contribuente | Che cos’è | Impatto sui casi d’uso | Best practice |
| --- | --- | --- | --- |
| Conversione da batch a streaming | I carichi di lavoro in batch convertiti in streaming possono aumentare in modo significativo il throughput, influendo sulle prestazioni e sull&#39;allocazione delle risorse. Ad esempio, l’esecuzione di un aggiornamento in blocco del profilo dopo un evento senza limiti di tariffa. | Le strategie di streaming non sono necessarie per i casi di utilizzo in batch in cui non è richiesta l’elaborazione a bassa latenza. | Valuta i requisiti del caso d’uso. Per il marketing in uscita in batch, puoi utilizzare [l&#39;acquisizione in batch](../../ingestion/batch-ingestion/overview.md) invece dello streaming per gestire l&#39;acquisizione dei dati in modo più efficiente. |
| Acquisizione di dati non necessaria | L’acquisizione di dati non necessari per la personalizzazione aumenta la velocità effettiva senza aggiungere valore e sprecare risorse. Ad esempio, acquisendo in profili tutto il traffico di Analytics, indipendentemente dalla rilevanza. | L’eccesso di dati non rilevanti crea rumore, rendendo più difficile l’identificazione dei punti di dati con impatto. Può anche causare attriti durante la definizione e la gestione di tipi di pubblico e profili. | Acquisisci solo i dati necessari per i tuoi casi d’uso. Assicurati di filtrare i dati non necessari.<ul><li>**Adobe Analytics**: utilizza [filtro a livello di riga](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) per ottimizzare l&#39;immissione di dati.</li><li>**Origini**: utilizza l&#39;API [[!DNL Flow Service] API per filtrare i dati a livello di riga](../../sources/tutorials/api/filter.md) per le origini supportate come [!DNL Snowflake] e [!DNL Google BigQuery].</li></li>**Stream dati di Edge**: configura [flussi dati dinamici](../../datastreams/configure-dynamic-datastream.md) per eseguire il filtro a livello di riga del traffico in arrivo da WebSDK.</li></ul> |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai imparato a monitorare i processi di acquisizione dei profili di streaming all’interno della tua organizzazione. Leggi i seguenti documenti per ulteriori informazioni sul monitoraggio dei dati per Real-Time Customer Profile.

* [Utilizzare il dashboard di monitoraggio](./monitor.md).
* [Monitorare i dati del profilo](./monitor-profiles.md).
