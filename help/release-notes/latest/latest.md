---
title: Note sulla versione di Adobe Experience Platform di settembre 2024
description: Note sulla versione di Adobe Experience Platform di settembre 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: eac613434f631cab567ab3fa6e30d33acac79d2f
workflow-type: ht
source-wordcount: '2199'
ht-degree: 100%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 24 settembre 2024**

Aggiornamenti alle funzioni e alla documentazione esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [Dashboard](#dashboards)
- [Preparazione dei dati](#data-prep)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Query Service](#query-service)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Avvisi {#alerts}

Experience Platform consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. Puoi abbonarti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell’interfaccia utente di Platform e scegliere di ricevere messaggi di avviso all’interno dell’interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto sandbox di sviluppo | Ora puoi [abbonarti agli avvisi](../../observability/alerts/ui.md) sia nelle sandbox di produzione che di sviluppo, per consentire un monitoraggio diretto in tutti gli ambienti. |
| Modelli e-mail | [Gli avvisi e-mail](../../observability/alerts/ui.md) ora includono informazioni dettagliate sulla risorsa, garantendo di avere a portata di mano tutti i dettagli chiave. |
| Personalizzazione avanzata | È ora possibile configurare [soglie di avviso](../../observability/alerts/ui.md#alert-threshold) che offrono maggiore flessibilità per adattare gli avvisi alle esigenze specifiche per i seguenti tipi di avviso:<br><ul><li>Ritardo processo segmento</li><li>Ritardo dell’esportazione del segmento</li><li>Ritardo esecuzione flusso destinazione</li><li>Ritardo di esecuzione del flusso di Identity Service</li><li>Ritardo esecuzione flusso profili</li><li>Ritardo esecuzione flusso origini</li><li>Ritardo esecuzione query</li><li>Tasso di attivazione ignorata superato</li><li>Tasso di errori di acquisizione delle origini superato</ul> |
| Avvisi espansi | Gli avvisi sulle informazioni sugli eventi di audit sono ora disponibili per l’abbonamento per le [regole degli avvisi](../../observability/alerts/rules.md) seguenti:<br><ul><li>Creazione pubblico</li><li>Aggiornamento pubblico</li><li>Eliminazione pubblico</li><li>Creazione set di dati</li><li>Aggiornamento set di dati</li><li>Eliminazione set di dati</li><li>Creazione schema</li><li>Aggiornamento schema</li><li>Eliminazione schema. |

{style="table-layout:auto"}

Per ulteriori informazioni sugli avvisi, consulta la [[!DNL Observability Insights] panoramica](../../observability/home.md).

## Dashboard {#dashboards}

Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Tabella dei componenti aggiuntivi per l’utilizzo delle licenze | Ottieni una visibilità granulare sull’utilizzo delle licenze e gestisci le risorse della piattaforma con tabelle dedicate per i prodotti principali e i componenti aggiuntivi. Monitora e analizza le metriche chiave per ciascun prodotto principale con visualizzazioni dettagliate a livello di sandbox. Le metriche dei componenti aggiuntivi si integrano facilmente con le metriche del prodotto principale, offrendo una visione completa dell’utilizzo. La visibilità migliorata consente di ottimizzare la gestione della licenza e di allineare le risorse alle esigenze organizzative. Per ulteriori informazioni, consulta la guida ](../../dashboards/guides/license-usage.md#overview-tab) dashboard per l’[[!UICONTROL Utilizzo licenze]. |
| Modalità query pro - Aggiornamenti del filtro globale | Migliora l’analisi con il nuovo filtro data della Modalità query pro. Perfeziona le informazioni con parametri di data dinamici nelle query SQL e filtra i dati per intervalli di tempo specifici. Scegli intervalli di date predefiniti o personalizzati con un’interfaccia utente intuitiva, mantenendo le dashboard pertinenti per tutti gli utenti. Semplifica i flussi di lavoro, mantieni la precisione e prendi decisioni tempestive. Per ulteriori informazioni, consulta la [guida sulla creazione dei filtri per data](../../dashboards/sql-insights-query-pro-mode/filters/global-filter.md). |
| Modalità query pro - Analisi dettagliate | Approfondisci le informazioni con la funzione Analisi dettagliata della Modalità query pro e passa senza problemi dai grafici di alto livello alle dashboard dettagliate. Utilizza questa funzione per passare facilmente da riepiloghi ad analisi approfondite ed esplorare tendenze, comportamenti della clientela e KPI. I pass-through automatici dei filtri e le analisi dettagliate a più livelli mantengono i dati coerenti, garantendo un’esplorazione fluida. Semplifica i flussi di lavoro, mantieni il contesto e accelera le decisioni. Per ulteriori informazioni, consulta la [guida dettagliata sulla creazione dell’analisi dettagliata](../../dashboards/sql-insights-query-pro-mode/drill-through.md). |
| Modalità query pro - Attributi di tabella avanzati | Utilizza gli attributi di tabella avanzati nella Modalità query pro per semplificare la visualizzazione dei dati, ottimizzare l’efficienza del flusso di lavoro e migliorare la chiarezza dei dati. Puoi aggiungere alle tabelle l’ordinamento, il ridimensionamento e l’impaginazione automatici direttamente dalle dashboard personalizzate. Ordina le colonne per assegnare la priorità ai dati chiave, ridimensionale per garantire una leggibilità ottimale e naviga facilmente in set di dati di grandi dimensioni senza modificare le query SQL. Consulta la guida &#39;[“Ulteriori informazioni](../../dashboards/sql-insights-query-pro-mode/view-more.md)” per scoprire come integrare queste funzioni e migliorare le informazioni sui dati. |
| Volume totale dati | La metrica “Ricchezza media profilo” è stata sostituita dalla metrica “Volume totale dati”. Il volume totale dei dati si riferisce alla quantità totale di dati disponibili che possono essere utilizzati con il profilo cliente in tempo reale per i flussi di lavoro di coinvolgimento e personalizzazione. Ulteriori dettagli su questa modifica sono disponibili nella [Guida al volume totale dati](../../landing/license-usage-and-guardrails/total-data-volume.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Preparazione dei dati {#data-prep}

Usa la preparazione dei dati per mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} nuove funzioni di preparazione dati da utilizzare nelle destinazioni | Ora puoi utilizzare le seguenti funzioni di array per i casi d’uso delle destinazioni:<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Per ulteriori informazioni, consulta la [Guida alle funzioni di preparazione dati](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Per ulteriori informazioni sulla preparazione dati, leggi la [panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Destinazioni {#destinations}

**Aggiornato: 30 settembre 2024**

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) | Con la versione di settembre 2024 è stata aggiunta l’opzione di mappatura per esportare il parametro `countryCode` in Amazon Ads. Utilizza `countryCode` nel [passaggio di mappatura](/help/destinations/catalog/advertising/amazon-ads.md#map) per migliorare le percentuali di corrispondenza delle identità con Amazon. |
| [[!BADGE B2B]{type=Informative} DemandBase](/help/destinations/catalog/advertising/demandbase.md) | Utilizza questa destinazione per attivare i tipi di pubblico del tuo account per i casi d’uso di Account-Based Marketing (ABM). Pubblicizza a persone e ruoli rilevanti negli account target tramite il Demand Side Platform B2B (DSP) di DemandBase. Gli account target possono inoltre essere arricchiti con dati di terze parti di DemandBase, per altri casi d’uso downstream nel marketing e nelle vendite. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti all’[esportazione del set di dati](/help/destinations/ui/export-datasets.md) | La versione di settembre 2024 di Experience Platform include diversi miglioramenti alle funzionalità di esportazione dei set di dati, per supportare meglio vari casi d’uso di uscita dei dati. Questi miglioramenti delle funzioni includono: <ul><li>Nuove opzioni di configurazione della cartella dati, inclusa l’opzione per aggiungere e rimuovere sottocartelle.</li><li>Nuove opzioni di esportazione, inclusa l’esportazione completa dei file (una volta) e la possibilità di specificare le date di fine</li><li>Nota: Adobe sta inoltre introducendo la data di fine predefinita del 1° maggio 2025 per tutti i flussi di dati di esportazione dei set di dati creati prima della versione di settembre. Per uno qualsiasi di questi flussi di dati, la data di fine nel flusso di dati dovrà essere aggiornata manualmente prima della data di fine, altrimenti le esportazioni si interromperanno su tale data.</li></ul> <br> ![Immagine dell’interfaccia utente di Experience Platform in cui è evidenziata l’opzione Modifica pianificazione nel passaggio di pianificazione.](../2024/assets/september/edit-schedule-folders.png "Opzione Modifica pianificazione e cartelle nel passaggio di pianificazione."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti all’Editor di schema | Assumi il controllo delle relazioni tra gli schemi con un flusso di lavoro di relazione aggiornato nell’Editor di schema. Aggiorna o rimuovi facilmente le relazioni esistenti direttamente dall’interfaccia utente di Experience Platform, rendendo la gestione dello schema più semplice e più intuitiva. Regola gli schemi di riferimento e rinomina le relazioni in modo affidabile, garantendo l’integrità dei dati complessiva attraverso la segmentazione e altri processi chiave. Per ulteriori informazioni sulla gestione efficiente delle relazioni tra schemi, consulta le guide sulla [definizione dei campi di relazione nell’interfaccia utente](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) e sulle [relazioni B2B](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM, consulta la [Panoramica sul sistema XDM](../../xdm/home.md).

## Identity Service {#identity-service}

Utilizza Identity Service di Adobe Experience Platform per creare una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità limitata delle regole di collegamento del grafo identità | Le regole di collegamento del grafo identità sono una suite di strumenti in Identity Service che puoi utilizzare per garantire una personalizzazione accurata per i tuoi utenti. <ul><li>È ora possibile utilizzare l’[algoritmo di ottimizzazione delle identità](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) per assicurarsi che un grafo identità sia rappresentativo di una singola persona, evitando così la fusione indesiderata di identità sul profilo cliente in tempo reale.</li><li>Configura le [priorità dello spazio dei nomi](../../identity-service/identity-graph-linking-rules/namespace-priority.md) per definire l’importanza dei rispettivi spazi dei nomi e influenzare il modo in cui i profili vengono formati e segmentati.</li><li>Utilizza lo [strumento di simulazione grafo nell’interfaccia utente](../../identity-service/identity-graph-linking-rules/graph-simulation.md) per simulare grafi identità con configurazioni diverse.</li><li>Utilizza l’[interfaccia delle impostazioni di identità](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) per designare uno spazio dei nomi specifico e stabilire le priorità per tutti gli spazi dei nomi dell’organizzazione.</li><li>Consulta la [dashboard identità](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) per le metriche e le tendenze relative ai dati del grafico.</li></ul> Per provare le regole di collegamento del grafo identità, contatta il team Adobe Account per accedere alle sandbox di sviluppo. |

**Documentazione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Guida alla risoluzione dei problemi per le regole di collegamento del grafo identità | Consulta la nuova [guida alla risoluzione dei problemi per le regole di collegamento del grafo identità](../../identity-service/identity-graph-linking-rules/troubleshooting.md) per gli approcci e le soluzioni di debug che puoi intraprendere per risolvere i problemi comuni che potrebbero verificarsi quando utilizzi le regole di collegamento del grafo identità. |
| Domande frequenti sulle regole di collegamento del grafo identità | Consulta le nuove [domande frequenti sulle regole di collegamento del grafo identità](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) per un elenco di risposte alle domande frequenti sulla priorità dello spazio dei nomi, l’algoritmo di ottimizzazione delle identità e altri aspetti delle regole di collegamento del grafo identità. |

{style="table-layout:auto"}

Per ulteriori informazioni su Identity Service, leggi la [panoramica su Identity Service](../../identity-service/home.md).

## Query Service {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL data lake]. Puoi unire qualsiasi set di dati dal data lake e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire nel profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Tipi di pubblico di Data Distiller | Crea, gestisci e attiva facilmente i tipi di pubblico con l’estensione SQL per tipi di pubblico in Data Distiller di Experience Platform. Definisci i segmenti di pubblico con comandi SQL direttamente dal data lake, evitando la necessità di dati non elaborati nei profili. Ottimizza le strategie di targeting e sincronizza automaticamente i tipi di pubblico con destinazioni basate su file con questo approccio flessibile e basato sui dati. Semplifica i flussi di lavoro, ottimizza la gestione del pubblico e libera tutto il potenziale dei dati. Consulta la [guida sull’utilizzo dell’estensione SQL per tipi di pubblico](../../query-service/data-distiller-audiences/overview.md) per migliorare le strategie per i tipi di pubblico. |
| Statistiche di Data Distiller - Ipercubi | Ottimizza l’analisi dei big data con ipercubi. Gestisci calcoli complessi, come i conteggi distinti e l’analisi multidimensionale, senza rielaborare i dati storici. Aggiorna i dati in modo incrementale, semplifica i flussi di lavoro e riduci i tempi di elaborazione mantenendo al contempo precisione ed efficienza. Ottieni informazioni più veloci, scalabili e convenienti in termini di costi che trasformano il processo decisionale. Esplora la [guida sull’utilizzo di ipercubi](../../query-service/hypercubes/overview.md) per sbloccare l’analisi avanzata. |
| Browser oggetti dell’editor di query | Incrementa l’efficienza delle query con il nuovo browser oggetti dell’editor di query. Cerca, filtra e accedi rapidamente ai set di dati per scrivere e perfezionare le query in modo più rapido. Con gli aggiornamenti in tempo reale degli schemi e i metadati istantanei delle tabelle, puoi semplificare i flussi di lavoro, ridurre i tempi di navigazione e migliorare l’esperienza di query. Sblocca il potenziale dei dati e ottimizza l’analisi. Per ulteriori informazioni, consulta la [guida all’utilizzo del browser oggetti](../../query-service/ui/user-guide.md#object-browser). |
| Calcola ore | Ottieni il controllo sull’utilizzo delle risorse con la metrica Calcola ore da poco visibile per le query pianificate. Visualizza le ore di calcolo a livello di esecuzione della query per monitorare e ottimizzare l’utilizzo delle risorse per le query sui batch CTAS/ITAS. Tieni traccia di orari di inizio, stato di completamento e tempo di calcolo per ogni esecuzione della query. Ottimizza delle prestazioni e riduci i costi senza problemi. Consulta la [guida su Calcola ore](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) per informazioni su come massimizzare l’efficienza delle query. |

{style="table-layout:auto"}

Per ulteriori informazioni su Query Service, consulta la [panoramica su Query Service](../../query-service/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento dei criteri di segmentazione in streaming | A partire dalla versione di settembre 2024, i criteri per i tipi di pubblico idonei per la segmentazione in streaming sono stati aggiornati. Ulteriori informazioni su queste modifiche sono disponibili nell’[aggiornamento dei criteri di idoneità per la segmentazione in streaming](../../segmentation/eligibility-criteria-update.md). |
| Implementazione di Ricerca unificata | Il comportamento di ricerca nel Generatore di segmenti ora utilizza la Ricerca unificata. Ciò consente un’esperienza più solida durante la gestione e la ricerca di tipi di pubblico da riutilizzare per l’appartenenza al segmento. Per ulteriori informazioni su questa modifica, consulta la [guida del Generatore di segmenti](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Supporto di Beta di [!BADGE ]{type=Informative} per l’acquisizione di dati crittografati nell’interfaccia utente | Ora è possibile acquisire dati crittografati da un’origine batch di archiviazione cloud utilizzando l’area di lavoro delle origini nell’interfaccia utente di Experience Platform. Per ulteriori informazioni, consulta il tutorial sull’[acquisizione dei dati crittografati nell’interfaccia utente](../../sources/tutorials/ui/encryped-ingestion.md). |
| Disponibilità generale dell’origine [!DNL Snowflake Streaming] | L’origine [!DNL Snowflake Streaming] è ora in disponibilità generale. Utilizza questa origine per inviare i dati dall’account [!DNL Snowflake] ad Experience Platform. Per ulteriori informazioni, consulta la [[!DNL Snowflake Streaming] panoramica](../../sources/connectors/databases/snowflake-streaming.md). |
| Supporto per l’autenticazione dell’account del servizio in [!DNL Google BigQuery] | È ora possibile connettere l’account [!DNL Google BigQuery] ad Experience Platform utilizzando l’autenticazione dell’account del servizio. Per ulteriori informazioni, consulta la [[!DNL Google BigQuery] panoramica. ](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)<br> ![Immagine dell’interfaccia utente di Experience Platform con l’opzione Modifica pianificazione e cartelle evidenziata nel passaggio di pianificazione.](../2024/assets/september/service_auth.png "Autenticazione del servizio per BigQuery Google."){width="250" align="center" zoomable="yes"} |
| Supporto per ignorare l’anteprima dei dati di esempio | Ora puoi scegliere di saltare l’anteprima dei dati durante la creazione di una connessione di origine con le seguenti origini: <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> Puoi saltare l’anteprima dei dati per evitare un timeout che potrebbe verificarsi durante l’acquisizione di dati in batch di grandi dimensioni. Questa operazione potrebbe impedire la convalida automatica dei campi calcolati e obbligatori. Se scegli di saltare l’anteprima dei dati, potrebbe essere necessario convalidare manualmente i campi calcolati e obbligatori durante la mappatura. |
| Supporto per la disattivazione del blocco in [!DNL SFTP] | È ora possibile configurare un’impostazione che consente di disabilitare il blocco nell’origine [!DNL SFTP]. Per ulteriori informazioni, consulta la [[!DNL SFTP] panoramica](../../sources/connectors/cloud-storage/sftp.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).
