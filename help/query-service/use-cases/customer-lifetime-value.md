---
title: Tracciamento dei segnali di dati per generare il valore del ciclo di vita del cliente
description: Questa guida fornisce una dimostrazione end-to-end su come utilizzare Data Distiller e dashboard definiti dall’utente con Real-time Customer Data Platform per misurare e visualizzare il valore del ciclo di vita del cliente.
exl-id: c74b5bff-feb2-4e21-9ee4-1e0973192570
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---

# Tracciare i segnali di dati per generare valore nel ciclo di vita del cliente

Puoi utilizzare Real-time Customer Data Platform per tenere traccia del valore del ciclo di vita del cliente (CLV, Customer Lifetime Value) e visualizzare tale metrica con dashboard definite dall’utente. Utilizzando Data Distiller e dashboard definiti dall’utente, puoi misurare il valore di un cliente per la tua azienda in tutta la relazione. La conoscenza di CLV consente di sviluppare strategie aziendali per acquisire nuovi clienti mantenendo quelli esistenti e mantenendo i margini di profitto.

L’infografica seguente illustra il ciclo di raccolta, manipolazione, analisi e attuazione dei dati che genera dati ad alte prestazioni per migliorare le campagne di marketing.

![L&#39;infografica di andata e ritorno dei dati dall&#39;osservazione all&#39;analisi all&#39;azione.](../images/use-cases/infographic-use-case-cycle.png)

Questo caso d’uso end-to-end illustra come acquisire e modificare i segnali di dati per calcolare l’attributo derivato del valore del ciclo di vita del cliente. Questi set di dati derivati possono quindi essere applicati ai dati del profilo di Real-Time CDP e sono disponibili per l’utilizzo con dashboard definiti dall’utente per creare una dashboard per l’analisi approfondita. Tramite Data Distiller, puoi estendere il modello dati di Real-Time CDP Insights e utilizzare i set di dati derivati da CLV e le informazioni della dashboard per creare un nuovo pubblico e attivarlo nella destinazione desiderata. Questi tipi di pubblico ad alte prestazioni possono quindi essere utilizzati per sviluppare la tua prossima campagna di marketing.

Questa guida è stata progettata per aiutarti a comprendere meglio la customer experience misurando i segnali di dati tra i punti di contatto chiave che guidano CLV e implementando un caso d’uso simile nell’ambiente. L’intero processo è riassunto nell’immagine seguente.

![Infografica dei passaggi generali necessari per utilizzare il valore del ciclo di vita del cliente.](../images/use-cases/implementation-steps.png)

## Introduzione {#getting-started}

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Query Service](../home.md): fornisce un&#39;interfaccia utente e un&#39;API RESTful in cui è possibile utilizzare query SQL per analizzare e arricchire i dati.
* [Servizio di segmentazione](../../segmentation/home.md): consente di generare tipi di pubblico dai dati del profilo cliente in tempo reale.

## Prerequisiti

Questa guida richiede che lo SKU di [Data Distiller](../data-distiller/overview.md) sia incluso nell&#39;offerta del pacchetto. In caso di dubbi, contatta il rappresentante del servizio Adobe.

## Creare un set di dati derivato {#create-derived-dataset}

Il primo passo per stabilire il proprio CLV consiste nel creare un set di dati derivato dai segnali di dati acquisiti dalle azioni dell&#39;utente. Questo caso d’uso particolare è trattato in un documento separato relativo a uno schema di fidelizzazione di una compagnia aerea. Consulta la guida per scoprire come [utilizzare Query Service per creare set di dati derivati basati su decile da utilizzare con i dati del profilo](./deciles-use-case.md). Il documento contiene esempi e spiegazioni completi che illustrano i seguenti passaggi:

* Crea uno schema per consentire il bucket decile.
* Utilizza Query Service per creare decili.
* Genera set di dati decili.
* Abilita lo schema per l’utilizzo in Real-Time Customer Profile.
* Crea uno spazio dei nomi delle identità e contrassegnalo come identificatore primario.
* Crea una query per calcolare i decili in un periodo di lookback.

## Estendere il modello dati di insights e pianificare gli aggiornamenti {#extend-data-model-and-set-refresh-schedule}

Successivamente, devi creare un modello dati personalizzato o estendere un modello dati Adobe Real-Time CDP esistente per interagire con le informazioni di reporting di CLV. Consulta la documentazione per scoprire come [creare un modello di dati Reporting Insights tramite Query Service da utilizzare con dati di archivio accelerati e dashboard definiti dall&#39;utente](../data-distiller/sql-insights/reporting-insights-data-model.md#build-a-reporting-insights-data-model). Il tutorial illustra i seguenti passaggi:

* Crea un modello per la generazione di rapporti di approfondimenti con Data Distiller.
* Crea tabelle, relazioni e popola i dati.
* Eseguire una query sul modello dati di reporting insight.
* Estendi il modello dati con il modello dati di Real-Time CDP Insights.
* Crea tabelle dimensione per estendere il modello di reporting insights.
* Eseguire una query sul modello dati Exaccelerated Store Reporting Insights

Per informazioni su come [personalizzare i modelli di query SQL per creare rapporti Real-Time CDP per i casi d&#39;uso di indicatori di prestazioni chiave (KPI) e marketing, consulta la documentazione del modello dati di Real-time Customer Data Platform Insights](../../dashboards/data-models/cdp-insights-data-model-b2c.md).

Assicurati di impostare una pianificazione per aggiornare il modello dati personalizzato a intervalli regolari. In questo modo i dati vengono reinseriti come parte della pipeline di acquisizione in base alle esigenze e popolano le dashboard definite dall’utente. Per informazioni su come impostare la pianificazione, consulta la [guida alla pianificazione delle query](../ui/query-schedules.md#create-schedule).

## Creare un dashboard per acquisire informazioni {#build-a-custom-dashboard}

Dopo aver creato il modello dati personalizzato, puoi visualizzare i dati con query personalizzate e dashboard definiti dall’utente. Per istruzioni complete su come [creare un dashboard personalizzato](../../dashboards/standard-dashboards.md), consulta la panoramica dei dashboard definiti dall&#39;utente. La guida dell’interfaccia utente include informazioni su:

* Come creare un widget.
* Come utilizzare il compositore widget.

Di seguito sono riportati alcuni esempi di widget CLV personalizzati che utilizzano contenitori decile.

![Insieme di widget CLTV personalizzati basati su decile.](../images/use-cases/deciles-user-defined-dashboard.png)

## Creare e attivare tipi di pubblico ad alte prestazioni {#create-and-activate-audiences}

Il passaggio successivo consiste nel creare una definizione di segmento e generare tipi di pubblico dai dati dei profili cliente in tempo reale. Per informazioni su come [creare e attivare tipi di pubblico in Platform](../../segmentation/ui/segment-builder.md), consulta la guida dell&#39;interfaccia utente di Segment Builder. La guida fornisce sezioni su come:

* Crea definizioni di segmenti utilizzando una combinazione di attributi, eventi e tipi di pubblico esistenti come blocchi predefiniti.
* Utilizza l’area di lavoro e i contenitori del generatore di regole per controllare l’ordine in cui vengono eseguite le regole di segmentazione.
* Visualizza le stime del tuo pubblico potenziale, consentendoti di regolare le definizioni dei segmenti in base alle esigenze.
* Abilita tutte le definizioni dei segmenti per la segmentazione pianificata.
* Abilita le definizioni di segmenti specificate per la segmentazione in streaming.

In alternativa, è disponibile anche un&#39;esercitazione video [per la generazione di segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-segments.html) per ulteriori informazioni.

## Attivare il pubblico per una campagna e-mail {#activate-audience-for-campaign}

Una volta creato il pubblico, puoi attivarlo in una destinazione. Platform supporta diversi provider di servizi e-mail (ESP) che consentono di gestire le attività di marketing e-mail, ad esempio l’invio di campagne e-mail promozionali.

Controlla la [panoramica delle destinazioni di e-mail marketing](../../destinations/catalog/email-marketing/overview.md#connect-destination) per ottenere un elenco delle destinazioni supportate in cui desideri esportare i dati (ad esempio la pagina [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)).

## Visualizzare i dati di analisi restituiti dalla campagna {#post-campaign-data-analysis}

I dati delle origini ora possono essere [elaborati in modo incrementale](../key-concepts/incremental-load.md) come parte di un aggiornamento pianificato del modello dati nell&#39;archivio dati accelerato. Eventuali eventi di risposta dai clienti possono essere acquisiti in Adobe Experience Platform così come si verificano o in batch. Il modello dati può essere aggiornato una o più volte al giorno, a seconda delle impostazioni o dei connettori di origine. Per ulteriori informazioni, consulta la [panoramica dell&#39;API di acquisizione batch](../../ingestion/batch-ingestion/api-overview.md) o la [panoramica dell&#39;acquisizione streaming](../../ingestion/streaming-ingestion/overview.md).

Una volta aggiornato il modello dati, i widget del dashboard personalizzati forniscono segnali significativi che consentono di misurare e visualizzare il valore del ciclo di vita del cliente.

![Un widget personalizzato per mostrare il numero di e-mail aperte in base al pubblico e alla campagna e-mail.](../images/use-cases/post-activation-and-email-response-kpis.png)

Sono disponibili diverse opzioni di visualizzazione per l’analisi personalizzata.

![Indirizzo e-mail aperto dal widget dei bucket della campagna.](../images/use-cases/email-opened-by-campaign-buckets.png)

Queste informazioni possono a loro volta aiutarti a sviluppare le tue strategie aziendali per le campagne successive.

![Raccolta di quattro widget personalizzati che descrivono i risultati della campagna e-mail.](../images/use-cases/example-widgets.png)

## Passaggi successivi

La lettura di questo documento consente di comprendere meglio come utilizzare Real-time Customer Data Platform per monitorare e visualizzare la metrica CLV (Customer Lifetime Value). Per ulteriori informazioni sui molti casi d’uso aziendali risolti tramite Query Service e l’Experience Platform, si consiglia di leggere i seguenti documenti:

* [Un esempio end-to-end di un caso d’uso di navigazione abbandonato che dimostra la versatilità e i vantaggi di Query Service.](./abandoned-browse.md)
* [Come utilizzare Query Service e l’apprendimento automatico per determinare e filtrare l’attività bot dal traffico autentico dei visitatori del sito web online](./bot-filtering.md)
* [Come eseguire una corrispondenza sui dati di Platform che combini i risultati di più set di dati facendo corrispondere approssimativamente una stringa scelta.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
