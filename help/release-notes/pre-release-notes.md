---
title: Note pre-release di Experience Platform
description: Un’anteprima delle ultime note sulla versione di Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5cbf63cc0a149d54de63e3e1797cae4098498fe8
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 29%

---

# Note preliminari su Adobe Experience Platform

>[!IMPORTANT]
>
>Questo documento è destinato ad essere **anteprima** delle note sulla versione per il mese corrente. Gli elementi da rilasciare sono soggetti a modifiche e possono essere aggiunti o rimossi nella versione finale.

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/latest)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: marzo 2026**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Gestione avanzata del ciclo di vita dei dati](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Destinazioni](#destinations)
- [Query Service](#query-service)
- [Profilo cliente in tempo reale](#profile)
- [Esecuzione e funzionamento](#run-and-operate)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Gestione avanzata del ciclo di vita dei dati {#advanced-data-lifecycle-management}

Experience Platform offre una suite di funzionalità di igiene dei dati che ti consentono di gestire i dati archiviati tramite l’eliminazione programmatica di record e set di dati del consumatore. Utilizzando l’area di lavoro del ciclo di vita dei dati nell’interfaccia utente o tramite chiamate all’API di igiene dei dati, puoi gestire in modo efficace gli archivi di dati. Usa queste funzionaità per garantire che le informazioni vengano utilizzate come previsto, che vengano aggiornate quando è necessario correggere dati scorretti e che vengano eliminate quando i criteri organizzativi lo ritengono necessario.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Eliminazione di più set di dati e record di solo profilo (solo API) | È possibile inviare un singolo ID set di dati, un elenco separato da virgole di ID set di dati o il valore letterale `ALL` in `datasetId` per eliminare identità in uno, molti o tutti i set di dati. È inoltre possibile limitare l&#39;eliminazione ai servizi di profilo impostando `targetServices` su `["identity","profile","ajo"]`, lasciando invariato il datalake. Per ulteriori dettagli, consulta la [Guida all&#39;eliminazione dei record degli ordini di lavoro](../hygiene/api/workorder.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulla gestione avanzata del ciclo di vita dei dati](../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator consente di creare e distribuire agenti basati sull’intelligenza artificiale in grado di automatizzare i flussi di lavoro e interagire con i clienti su più canali.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Adobe Marketing Agent per [!DNL Microsoft 365 Copilot] | Adobe Marketing Agent per [!DNL Microsoft 365 Copilot] è il tuo agente incorporato che porta le informazioni di marketing di Adobe direttamente negli strumenti quotidiani come [!DNL Teams], [!DNL Word], [!DNL PowerPoint] e altre app di [!DNL Microsoft 365]. È possibile utilizzare questo agente per acquisire informazioni attendibili sulle campagne dalle applicazioni Adobe durante la pianificazione delle campagne, la revisione dei tipi di pubblico o la collaborazione con colleghi, rispondere alle domande dei clienti e prendere decisioni basate sui dati senza uscire dal flusso di lavoro [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [documentazione di Agent Orchestrator](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| [Selettore di area per il batch Snowflake](../destinations/catalog/warehouses/snowflake-batch.md) | Ora è più facile trovare la tua regione con il nuovo menu a discesa ricercabile, che combina ricerca e menu a discesa in un unico controllo. |
| Esporta metadati del pubblico in [destinazioni Batch Snowflake](../destinations/catalog/warehouses/snowflake-batch.md) | I file esportati in questa destinazione ora includono metadati del pubblico. La nuova struttura di tabella si applica a tutte le nuove connessioni di destinazione impostate per il passaggio successivo. La vecchia struttura della tabella verrà mantenuta per altri tre mesi prima di essere dichiarata obsoleta. |
| Connessione [!DNL Adobe Advertising Cloud DSP] | La nuova connessione Adobe Advertising DSP offre le stesse funzionalità della connessione legacy e il supporto di identità aggiuntive. |
| Supporto per il pubblico esterno per [Il CRM del Trade Desk](../destinations/catalog/advertising/tradedesk-emails.md), [Criteo](../destinations/catalog/advertising/criteo.md) e [Pinterest](../destinations/catalog/advertising/pinterest.md) | Ora puoi attivare i tipi di pubblico oltre i segmenti del servizio di segmentazione in Trade Desk CRM, Criteo e Pinterest, inclusi i tipi di pubblico di caricamento personalizzati (importati da CSV), i tipi di pubblico simili, i tipi di pubblico federati e i tipi di pubblico creati in altre app di Experience Platform come Adobe Journey Optimizer. Per informazioni dettagliate, consulta la sezione [tipi di pubblico supportati](../destinations/catalog/advertising/criteo.md#supported-audiences) nella pagina del catalogo di ciascuna destinazione. |
| Limite aumentato per i tipi di pubblico di caricamento personalizzati | Ora puoi attivare fino a 20 tipi di pubblico per caricamento personalizzato per istanza di destinazione. In precedenza, questo limite era di 10. |
| [Esporta ora il file](../destinations/ui/export-file-now.md) e [supporto API di attivazione ad hoc](../destinations/api/ad-hoc-activation-api.md) per tipi di pubblico esterni | È ora possibile utilizzare l’interfaccia Export file now (UI) e l’API di attivazione ad hoc con tipi di pubblico esterni (come caricamenti personalizzati, lookalike, federati e tipi di pubblico da altre app Experience Platform) durante l’attivazione di destinazioni basate su file in batch. |
| Destinazioni API HTTP con OAuth 2 e mTLS | Ora puoi creare e autenticare destinazioni API HTTP che utilizzano OAuth 2 quando l’endpoint di autenticazione richiede TLS reciproco (mTLS); il recupero del token durante la configurazione della destinazione ora supporta mTLS. |
| Destinazione account ZoomInfo | Ora puoi inviare il pubblico dell’account a ZoomInfo da Real-Time Customer Data Platform (B2B). |

{style="table-layout:auto"}

**Correzioni e miglioramenti**

| Correzione | Descrizione |
| --- | --- |
| Convalida dell&#39;ID account [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) | Al passaggio ID account è stato aggiunto un validatore di espressioni regolari. Quando inserisci l&#39;ID, questo viene convalidato per garantire che l&#39;ID organizzazione e l&#39;ID account siano nel formato corretto (separati da un punto). |
| [hashing del numero di telefono del connettore TikTok](../destinations/catalog/social/tiktok.md) | È stato risolto un problema che impediva l’attivazione a TikTok delle identità codificate dai numeri di telefono a causa di un’errata configurazione nella scheda di destinazione. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../destinations/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con Real-Time Customer Profile puoi visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, del sistema CRM e di terze parti.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Selettore ora eventi profilo | È ora possibile impostare una finestra temporale nella scheda eventi profilo per visualizzare e analizzare gli eventi all’interno di tale intervallo. È possibile impostare la finestra temporale su un massimo di 30 giorni. Per impostazione predefinita, mostra gli eventi delle ultime 48 ore. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sul profilo cliente in tempo reale](../profile/home.md).

## Query Service {#query-service}

Il servizio Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire nel profilo cliente in tempo reale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Acceleratori Data Distiller | È ora possibile scegliere un acceleratore dalla scheda Acceleratori, immettere i parametri richiesti ed eseguire o pianificare l&#39;istruzione SQL generata senza scriverla personalmente; clonare qualsiasi acceleratore in un modello personalizzato da modificare. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica di Query Service](../query-service/home.md).

## Esecuzione e funzionamento {#run-and-operate}

Ispeziona, risolvi i problemi e ottimizza le implementazioni di Experience Platform con gli strumenti Esegui e opera. Ottieni visibilità sulle attivazioni batch pianificate, identifica i problemi di configurazione e migliora l’affidabilità del sistema.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Pianificazioni processi](../run-and-operate/job-schedules.md) disponibilità generale | [!DNL Job Schedules] fornisce una visualizzazione unificata di tutti i processi di elaborazione batch pianificati nella pipeline di dati, dall&#39;acquisizione all&#39;attivazione della destinazione. Esaminare lo stato di esecuzione, identificare i conflitti di pianificazione e diagnosticare i problemi di configurazione prima che influiscano sulle operazioni aziendali. |
| Verifica della disponibilità generale | Configurazioni di schema e identità inadeguate causano significativi problemi a valle, tra cui creazione di profili errata, qualificazione dei segmenti non riuscita e attivazione imprecisa. <br>I controlli di integrità spostano il tuo approccio dalla risoluzione dei problemi reattiva alla manutenzione proattiva e preventiva. I controlli di integrità sono scansioni sempre attive degli schemi e delle identità utilizzati nella sandbox e forniscono un riepilogo dei problemi che è possibile utilizzare per esplorare e risolvere. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica sull&#39;esecuzione e l&#39;utilizzo](../run-and-operate/overview.md), [Pianificazioni dei processi di ispezione](../run-and-operate/job-schedules.md) e la [Guida all&#39;interfaccia utente di Platform](../landing/ui-guide.md).

## Servizio di segmentazione {#segmentation}

Experience Platform consente di creare segmenti di pubblico dai dati dei clienti e consente la gestione completa del ciclo di vita di tali tipi di pubblico.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Origine di acquisizione in Audience Builder | Ora puoi vedere se ogni attributo proviene da un batch, streaming o sorgente Edge in Audience Builder per evitare di creare tipi di pubblico in streaming non validi o inefficienti. |
| Mostra solo campi con dati in Account Audience Builder | Ora è possibile filtrare per mostrare solo gli attributi che contengono dati durante la creazione di tipi di pubblico per gli account. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica tipi di pubblico](../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| Supporto migliorato per Change Data Capture | È ora possibile utilizzare Change Data Capture con le origini [!DNL Marketo Engage], [!DNL Microsoft Dynamics] e [!DNL Salesforce CRM]. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../sources/home.md).

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

| [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) multiregion support | The Snowflake Streaming connector is now available to customers beyond the US VA7 region. Use the region dropdown selector to select which Snowflake region your account is in. The documentation has been updated with the expected data structure for Snowflake streaming tables. |
| Audience filtering in activation workflow | You can now find and filter audiences in the **[!UICONTROL Select audiences]** step with the same experience as the Audiences page; for example, you can filter on audience origin to easily find the audience you are looking for. |

-->