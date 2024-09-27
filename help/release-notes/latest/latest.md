---
title: Note sulla versione di Adobe Experience Platform di settembre 2024
description: Note sulla versione di settembre 2024 per Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 059ed53ace6d54a0c0fb406c2f0379588fea2c44
workflow-type: tm+mt
source-wordcount: '2149'
ht-degree: 24%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 24 settembre 2024**

Aggiornamenti alle funzioni e alla documentazione esistenti in Adobe Experience Platform:

- [Note sulla versione di Adobe Experience Platform](#adobe-experience-platform-release-notes)
   - [Avvisi {#alerts}](#alerts-alerts)
   - [Dashboard {#dashboards}](#dashboards-dashboards)
   - [Preparazione dati {#data-prep}](#data-prep-data-prep)
   - [Destinazioni {#destinations}](#destinations-destinations)
   - [Experience Data Model (XDM) {#xdm}](#experience-data-model-xdm-xdm)
   - [Servizio identità {#identity-service}](#identity-service-identity-service)
   - [Servizio query {#query-service}](#query-service-query-service)
   - [Servizio di segmentazione {#segmentation-service}](#segmentation-service-segmentation-service)
   - [Origini {#sources}](#sources-sources)

## Avvisi {#alerts}

Experience Platform consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. Puoi abbonarti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell’interfaccia utente di Platform e scegliere di ricevere messaggi di avviso all’interno dell’interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto sandbox di sviluppo | Ora puoi [abbonarti agli avvisi](../../observability/alerts/ui.md) sia nelle sandbox di produzione che di sviluppo, per consentire un monitoraggio senza soluzione di continuità in tutti gli ambienti. |
| Modelli e-mail | [Gli avvisi e-mail](../../observability/alerts/ui.md) ora includono informazioni dettagliate sulla risorsa, garantendo di avere a portata di mano tutti i dettagli chiave. |
| Personalizzazione avanzata | È ora possibile configurare [soglie di avviso](../../observability/alerts/ui.md#alert-threshold) che offrono maggiore flessibilità per adattare gli avvisi alle esigenze specifiche per i seguenti tipi di avviso:<br><ul><li>Ritardo processo segmento</li><li>Ritardo esportazione segmento</li><li>Ritardo esecuzione flusso di destinazione</li><li>Ritardo esecuzione flusso servizio identità</li><li>Ritardo esecuzione flusso profilo</li><li>Ritardo esecuzione flusso origini</li><li>Ritardo esecuzione query</li><li>Frequenza di salto attivazione superata</li><li>Frequenza errori di acquisizione origini superata</ul> |
| Avvisi espansi | Gli avvisi sulle informazioni sugli eventi di controllo sono ora disponibili per la sottoscrizione per le [regole di avviso](../../observability/alerts/rules.md) seguenti:<br><ul><li>Creazione di pubblico</li><li>Aggiornamento del pubblico</li><li>Eliminazione del pubblico</li><li>Creazione set di dati</li><li>Aggiornamento set di dati</li><li>Eliminazione set di dati</li><li>Creazione schema</li><li>Aggiornamento schema</li><li>Eliminazione schema. |

{style="table-layout:auto"}

Per ulteriori informazioni sugli avvisi, leggere la [[!DNL Observability Insights] panoramica](../../observability/home.md).

## Dashboard {#dashboards}

Experience Platform fornisce più dashboard attraverso i quali è possibile visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Tabella dei componenti aggiuntivi per l’utilizzo della licenza | Ottieni una visibilità granulare sull’utilizzo delle licenze e gestisci le risorse Platform con tabelle dedicate per i prodotti di base e i componenti aggiuntivi. Monitora e analizza le metriche chiave per ogni prodotto di base con viste drill-through a livello di sandbox. Le metriche dei componenti aggiuntivi si integrano perfettamente con le metriche dei prodotti di base, offrendo una visione completa dell’utilizzo. La visibilità migliorata consente di ottimizzare la gestione delle licenze e di allineare le risorse alle esigenze organizzative. Per ulteriori dettagli, consulta la [[!UICONTROL guida del dashboard Utilizzo licenze]](../../dashboards/guides/license-usage.md#overview-tab). |
| Modalità Query Pro - Aggiornamenti filtri globali | Migliora l’analisi con il nuovo filtro date della modalità Query Pro. Perfeziona le informazioni con parametri di data dinamici nelle query SQL e filtra i dati per intervalli di tempo specifici. Scegli intervalli di date predefiniti o personalizzati con un’interfaccia utente intuitiva, mantenendo le dashboard pertinenti per tutti gli utenti. Semplificare i flussi di lavoro, mantenere la precisione e prendere decisioni tempestive. Per ulteriori informazioni, consulta la [guida sulla creazione di filtri per date](../../dashboards/data-distiller/query-pro-mode/filters/global-filter.md). |
| Modalità Query Pro: drill-through | Approfondisci le informazioni con la funzione Drill Through della modalità Query Pro e passa senza problemi dai grafici di alto livello alle dashboard dettagliate. Utilizza questa funzione per passare facilmente da riepiloghi ad analisi approfondite ed esplorare tendenze, comportamenti dei clienti e KPI. I pass-through automatici dei filtri e i drill-through a più livelli mantengono i dati coerenti, garantendo un&#39;esplorazione fluida. Semplificare i flussi di lavoro, mantenere il contesto e accelerare le decisioni. Per ulteriori informazioni, leggere la [guida dettagliata sulla creazione di drill-through](../../dashboards/data-distiller/query-pro-mode/drill-through.md). |
| Modalità Query Pro - Attributi di tabella avanzati | Utilizza gli attributi di tabella avanzati in modalità Query Pro per semplificare la visualizzazione dei dati, migliorare l’efficienza del flusso di lavoro e migliorare la chiarezza dei dati. Puoi aggiungere alle tabelle l’ordinamento, il ridimensionamento e l’impaginazione automatici direttamente dai dashboard personalizzati. Ordina le colonne per assegnare la priorità ai dati chiave, ridimensionarle per garantire una leggibilità ottimale e navigare facilmente in set di dati di grandi dimensioni senza modificare le query SQL. Leggi la guida &#39;[Visualizza altro](../../dashboards/data-distiller/query-pro-mode/view-more.md)&#39; per scoprire come integrare queste funzionalità e migliorare le informazioni sui dati. |
| Volume dati totale | La metrica &quot;Ricchezza media del profilo&quot; è stata sostituita dalla metrica &quot;Volume totale di dati&quot;. Il volume di dati totale si riferisce alla quantità totale di dati disponibili che possono essere utilizzati con Real-Time Customer Profile per flussi di lavoro di coinvolgimento e personalizzazione. Ulteriori dettagli su questa modifica sono disponibili nella [Guida del volume totale dei dati](../../landing/license-usage-and-guardrails/total-data-volume.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Preparazione dei dati {#data-prep}

Usa la preparazione dei dati per mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} nuove funzioni di preparazione dati da utilizzare nelle destinazioni | Ora puoi utilizzare le seguenti funzioni di array per i casi di utilizzo delle destinazioni:<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Per ulteriori informazioni, consulta la [Guida alle funzioni di preparazione dati](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Per ulteriori informazioni sulla preparazione dati, leggi la [panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) | Con la versione di settembre 2024 è stata aggiunta l&#39;opzione di mappatura per esportare il parametro `countryCode` in Amazon Ads. Utilizza `countryCode` nel [passaggio di mappatura](/help/destinations/catalog/advertising/amazon-ads.md#map) per migliorare le percentuali di corrispondenza delle identità con Amazon. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| [Miglioramenti all&#39;esportazione del set di dati](/help/destinations/ui/export-datasets.md) | La versione di settembre 2024 di Experience Platform include diversi miglioramenti alle funzionalità di esportazione dei set di dati, per supportare meglio vari casi di utilizzo di uscita dei dati. Questi miglioramenti includono: <ul><li>Nuove opzioni di configurazione della cartella dati, inclusa l’opzione per aggiungere e rimuovere sottocartelle.</li><li>Nuove opzioni di esportazione, inclusa l’esportazione completa dei file (una volta) e la possibilità di specificare le date di fine</li><li>Nota: Adobe sta inoltre introducendo una data di fine predefinita del 1° maggio 2025 per tutti i flussi di dati di esportazione dei set di dati creati prima della versione di settembre. Per uno qualsiasi di questi flussi di dati, i clienti dovranno aggiornare manualmente la data di fine nel flusso di dati prima della data di fine, altrimenti le esportazioni si fermeranno in tale data.</li></ul> <br> ![Immagine dell&#39;interfaccia utente di Experience Platform che evidenzia l&#39;opzione Modifica pianificazione e cartelle nel passaggio di pianificazione.](../2024/assets/september/edit-schedule-folders.png "Opzione Modifica pianificazione e cartelle nel passaggio di pianificazione."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti all’Editor di schema | Assumi il controllo delle relazioni tra schemi con un flusso di lavoro di relazione aggiornato nell’Editor di schema. Aggiorna o rimuovi facilmente le relazioni esistenti direttamente dall’interfaccia utente di Experience Platform, rendendo la gestione dello schema più semplice e intuitiva. Regola gli schemi di riferimento e rinomina le relazioni in modo affidabile, garantendo l’integrità dei dati attraverso la segmentazione e altri processi chiave. Per ulteriori informazioni sulla gestione efficiente delle relazioni tra schemi, consulta le guide su [definizione dei campi di relazione nell&#39;interfaccia utente](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) e per [relazioni B2B](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM, leggere la [Panoramica del sistema XDM](../../xdm/home.md).

## Identity Service {#identity-service}

Utilizza Identity Service di Adobe Experience Platform per creare una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità limitata delle regole di collegamento del grafico delle identità | Le regole di collegamento del grafo di identità sono una suite di strumenti in Identity Service che puoi utilizzare per garantire una personalizzazione accurata per i tuoi utenti. <ul><li>È ora possibile utilizzare l&#39;algoritmo di ottimizzazione delle identità [](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) per assicurarsi che un grafo delle identità sia rappresentativo di una singola persona e, pertanto, impedisca l&#39;unione indesiderata di identità sul Profilo cliente in tempo reale.</li><li>Configura le [priorità dello spazio dei nomi](../../identity-service/identity-graph-linking-rules/namespace-priority.md) per definire l&#39;importanza dei rispettivi spazi dei nomi e influenzare il modo in cui i profili vengono formati e segmentati.</li><li>Utilizza lo strumento di simulazione del grafico [ nell&#39;interfaccia utente](../../identity-service/identity-graph-linking-rules/graph-simulation.md) per simulare grafici di identità con configurazioni diverse.</li><li>Utilizza l&#39;[interfaccia delle impostazioni di identità](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) per designare lo spazio dei nomi univoco e stabilire le priorità per tutti gli spazi dei nomi dell&#39;organizzazione.</li><li>Consulta la [dashboard delle identità](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) per le metriche e le tendenze relative ai dati del grafico.</li></ul> Per provare le regole di collegamento del grafo delle identità, contatta il team degli account Adobi per accedere alle sandbox di sviluppo. |

**Documentazione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Guida alla risoluzione dei problemi per le regole di collegamento del grafico delle identità | Leggi la nuova [guida alla risoluzione dei problemi per le regole di collegamento del grafo delle identità](../../identity-service/identity-graph-linking-rules/troubleshooting.md) per gli approcci e le soluzioni di debug per risolvere i problemi comuni che potrebbero verificarsi quando utilizzi le regole di collegamento del grafo delle identità. |
| Domande frequenti per le regole di collegamento del grafico delle identità | Leggi le nuove [domande frequenti sulle regole di collegamento del grafo delle identità](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) per un elenco di risposte alle domande frequenti sulla priorità dello spazio dei nomi, l&#39;algoritmo di ottimizzazione delle identità e altri aspetti delle regole di collegamento del grafo delle identità. |

{style="table-layout:auto"}

Per ulteriori informazioni su Identity Service, leggi la [panoramica s Identity Service](../../identity-service/home.md).

## Servizio query {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform.[!DNL data lake] Puoi unire qualsiasi set di dati dal data lake e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire nel profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Tipi di pubblico di Data Distiller | Crea, gestisci e attiva facilmente i tipi di pubblico con l’estensione SQL audience in Experience Platform Data Distiller. Definisci i segmenti di pubblico con comandi SQL direttamente dal data lake, evitando la necessità di dati non elaborati nei profili. Ottimizza le strategie di targeting e sincronizza automaticamente i tipi di pubblico con destinazioni basate su file con questo approccio flessibile e basato sui dati. Semplifica i flussi di lavoro, ottimizza la gestione dell&#39;audience e sfrutta appieno il potenziale dei dati. Leggi la [guida sull&#39;utilizzo dell&#39;estensione del pubblico SQL](../../query-service/data-distiller-audiences/overview.md) per migliorare le strategie per i tipi di pubblico. |
| Statistiche di Data Distiller - Ipercubi | Ottimizza l’analisi dei big data con Hypercubes. Gestisci calcoli complessi, come i conteggi distinti e l’analisi multidimensionale, senza rielaborare i dati storici. Aggiorna i dati in modo incrementale, semplifica i flussi di lavoro e riduce i tempi di elaborazione mantenendo al contempo precisione ed efficienza. Ottieni informazioni più veloci, scalabili e convenienti che trasformano il processo decisionale. Esplora la [guida sull&#39;utilizzo di Hypercubes](../../query-service/hypercubes/overview.md) per sbloccare l&#39;analisi avanzata. |
| Browser oggetti editor query | Incrementa l’efficienza delle query con il nuovo Visualizzatore oggetti nell’Editor query. Cerca, filtra e accedi rapidamente ai set di dati per scrivere e perfezionare le query in modo più rapido. Con gli aggiornamenti in tempo reale degli schemi e i metadati istantanei delle tabelle, puoi semplificare i flussi di lavoro, ridurre i tempi di navigazione e migliorare l’esperienza di query. Sblocca il potenziale dei dati e ottimizza l’analisi. Per ulteriori informazioni, leggere la [guida all&#39;utilizzo del Visualizzatore oggetti](../../query-service/ui/user-guide.md#object-browser). |
| Calcola ore | Ottieni il controllo sull’utilizzo delle risorse con la metrica Calcola ore appena visibile per le query pianificate. Visualizzare le ore di calcolo a livello di esecuzione della query per monitorare e ottimizzare l&#39;utilizzo delle risorse per le query batch CTAS/ITAS. Tenere traccia di orari di inizio, stato di completamento e tempo di calcolo per ogni esecuzione della query. Ottimizzazione delle prestazioni e riduzione dei costi senza problemi. Leggi la [guida su Calcola ore](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) per informazioni su come massimizzare l&#39;efficienza delle query. |

{style="table-layout:auto"}

Per ulteriori informazioni su Query Service, leggere la [Panoramica di Query Service](../../query-service/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento dei criteri di segmentazione in streaming | A partire dalla versione di settembre 2024, i criteri per i tipi di pubblico per essere idonei alla segmentazione in streaming sono stati aggiornati. Ulteriori informazioni su queste modifiche sono disponibili nell&#39;aggiornamento dei criteri di idoneità alla segmentazione in streaming [](../../segmentation/eligibility-criteria-update.md). |
| Implementazione di Unified Search | Il comportamento di ricerca nel Generatore di segmenti ora utilizza la Ricerca unificata. Ciò consente un’esperienza più solida durante la gestione e la ricerca di tipi di pubblico da riutilizzare per l’iscrizione ai segmenti. Per ulteriori informazioni su questa modifica, consulta la [guida del Generatore di segmenti](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], leggere la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Supporto di [!BADGE Beta]{type=Informative} per l&#39;acquisizione di dati crittografati nell&#39;interfaccia utente | Ora è possibile acquisire dati crittografati da un’origine batch di archiviazione cloud utilizzando l’area di lavoro origini nell’interfaccia utente di Experience Platform. Per ulteriori informazioni, leggi l&#39;esercitazione sull&#39;acquisizione di dati crittografati nell&#39;interfaccia utente](../../sources/tutorials/ui/encryped-ingestion.md).[ |
| Disponibilità generale dell&#39;origine [!DNL Snowflake Streaming] | L&#39;origine [!DNL Snowflake Streaming] è ora in GA. Utilizzare questa origine per eseguire lo streaming dei dati dall&#39;account [!DNL Snowflake] all&#39;Experience Platform. Per ulteriori informazioni, leggere la [[!DNL Snowflake Streaming] panoramica](../../sources/connectors/databases/snowflake-streaming.md). |
| Supporto per l&#39;autenticazione dell&#39;account del servizio in [!DNL Google BigQuery] | È ora possibile connettere l&#39;account [!DNL Google BigQuery] a Experience Platform utilizzando l&#39;autenticazione dell&#39;account del servizio. Per ulteriori informazioni, leggere la [[!DNL Google BigQuery] panoramica](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). <br> ![Immagine dell&#39;interfaccia utente di Experience Platform che evidenzia l&#39;opzione Modifica pianificazione e cartelle nel passaggio di pianificazione.](../2024/assets/september/service_auth.png "Autenticazione del servizio per BigQuery Google."){width="250" align="center" zoomable="yes"} |
| Supporto per ignorare l’anteprima dei dati di esempio | Ora puoi scegliere di saltare l’anteprima dei dati durante la creazione di una connessione di origine con le seguenti origini: <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> Puoi saltare l’anteprima dei dati per evitare un timeout che potrebbe verificarsi durante l’acquisizione di dati in batch di grandi dimensioni. Questa operazione potrebbe impedire la convalida automatica dei campi calcolati e obbligatori. Se scegli di saltare l’anteprima dei dati, potrebbe essere necessario convalidare manualmente i campi calcolati e obbligatori durante la mappatura. |
| Supporto per la disattivazione del blocco in [!DNL SFTP] | È ora possibile configurare un&#39;impostazione che consente di disabilitare il blocco nell&#39;origine [!DNL SFTP]. Per ulteriori informazioni, consulta la [[!DNL SFTP] panoramica](../../sources/connectors/cloud-storage/sftp.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle origini](../../sources/home.md).
