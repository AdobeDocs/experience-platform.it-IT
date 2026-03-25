---
title: Note sulla versione di Adobe Experience Platform - Marzo 2026
description: Note sulla versione di Adobe Experience Platform di marzo 2026.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 8c55aebcb65327394ffbdf59db1d2a203182ed18
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 36%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/latest)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: mercoledì 24 marzo 2026**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Gestione avanzata del ciclo di vita dei dati](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Gestione avanzata del ciclo di vita dei dati {#advanced-data-lifecycle-management}

Experience Platform offre una suite di funzionalità di igiene dei dati che ti consentono di gestire i dati archiviati tramite l’eliminazione programmatica di record e set di dati del consumatore. Utilizzando l’area di lavoro del ciclo di vita dei dati nell’interfaccia utente o le chiamate all’API di igiene dei dati, puoi gestire in modo efficace gli archivi di dati. Usa queste funzionaità per garantire che le informazioni vengano utilizzate come previsto, che vengano aggiornate quando è necessario correggere dati scorretti e che vengano eliminate quando i criteri organizzativi lo ritengono necessario.

| Funzione | Descrizione |
| --- | --- |
| Eliminazione di record con set di dati multipli e solo profilo (solo API) | È possibile inviare un singolo ID set di dati, un elenco separato da virgole di ID set di dati o il valore letterale `ALL` in `datasetId` per eliminare identità in uno, molti o tutti i set di dati. È inoltre possibile limitare l&#39;eliminazione ai servizi correlati al profilo impostando `targetServices` su `["identity","profile","ajo"]`, lasciando invariato il datalake. Questa funzionalità è disponibile solo tramite l&#39;API di igiene dei dati. Per ulteriori dettagli, vedere la [Guida all&#39;eliminazione degli ordini di lavoro](../../hygiene/api/workorder.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulla gestione avanzata del ciclo di vita dei dati](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator consente di creare e distribuire agenti basati sull’intelligenza artificiale in grado di automatizzare i flussi di lavoro e interagire con i clienti su più canali.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Adobe Marketing Agent per [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent per [!DNL Microsoft 365 Copilot] è il tuo agente incorporato che porta le informazioni di marketing di Adobe direttamente negli strumenti quotidiani come [!DNL Teams], [!DNL Word], [!DNL PowerPoint] e altre app di [!DNL Microsoft 365]. È possibile utilizzare questo agente per richiamare informazioni attendibili sulle campagne dalle applicazioni Adobe durante la pianificazione delle campagne, la revisione dei tipi di pubblico, la collaborazione con i colleghi per rispondere alle domande dei clienti e per prendere decisioni basate sui dati senza uscire dal flusso di lavoro [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [documentazione su Agent Orchestrator](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| [Connessione Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | La nuova connessione Adobe Advertising DSP offre le stesse funzionalità della connessione legacy e il supporto di identità aggiuntive. Con il nuovo connettore, puoi anche esportare identità basate su cookie in Adobe Advertising DSP. |
| [Connessione FreeWheel](../../destinations/catalog/advertising/freewheel.md) | Invia [!DNL Real-Time CDP] tipi di pubblico a FreeWheel come file batch giornalieri in modo da poterli indirizzare a offerte e campagne FreeWheel su CTV, video e visualizzazione. Contatta il team del tuo account Adobe per accedere. |
| Supporto per il pubblico esterno per [il CRM del Trade Desk](../../destinations/catalog/advertising/tradedesk-emails.md) e [Pinterest](../../destinations/catalog/advertising/pinterest.md) | È ora possibile attivare i tipi di pubblico da origini diverse da Segmentation Service a CRM, Criteo e Pinterest del Trade Desk, inclusi i tipi di pubblico di caricamento personalizzati (importati da CSV), i tipi di pubblico simili, i tipi di pubblico federati e i tipi di pubblico creati in altre app di Experience Platform come [!DNL Adobe Journey Optimizer]. Questo aggiornamento verrà introdotto entro la fine di marzo. Per informazioni dettagliate, consulta la sezione [tipi di pubblico supportati](../../destinations/catalog/advertising/criteo.md#supported-audiences) nella pagina del catalogo di ciascuna destinazione. |
| Limite aumentato per i tipi di pubblico di caricamento personalizzati | Ora puoi attivare fino a 20 tipi di pubblico per caricamento personalizzato per istanza di destinazione. In precedenza, questo limite era di 10. Per informazioni dettagliate, consulta le [destinazioni guardrail](../../destinations/guardrails.md#batch-file-based-activation). |
| [Esporta ora il file](../../destinations/ui/export-file-now.md) e [supporto API di attivazione ad hoc](../../destinations/api/ad-hoc-activation-api.md) per tipi di pubblico esterni | È ora possibile utilizzare l’interfaccia Export file now (UI) e l’API di attivazione ad hoc con tipi di pubblico esterni (come caricamenti personalizzati, lookalike, federati e tipi di pubblico da altre app Experience Platform) durante l’attivazione di destinazioni basate su file in batch. Questo aggiornamento verrà introdotto entro la fine di marzo. |

{style="table-layout:auto"}

**Correzioni e miglioramenti**

| Correzione | Descrizione |
| --- | --- |
| [hashing del numero di telefono del connettore TikTok](../../destinations/catalog/social/tiktok.md) | È stato risolto un problema che impediva l’attivazione a TikTok delle identità codificate dai numeri di telefono a causa di un’errata configurazione nella scheda di destinazione. Per beneficiare di questa correzione, imposta un nuovo flusso di attivazione o rimuovi la mappatura dei numeri di telefono dal flusso esistente, salvalo e aggiungilo nuovamente. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

| Funzione | Descrizione |
| --- | --- |
| Azioni entità XDM ed eliminazione del supporto | Consente di accedere alle azioni per schemi, classi, gruppi di campi e tipi di dati direttamente dai menu delle tabelle in linea e dai menu dell&#39;intestazione della pagina dei dettagli. Se disponi delle autorizzazioni necessarie, puoi anche eliminare le entità dell’organizzazione quando non sono utilizzate dai set di dati e non sono abilitate per il profilo. Per ulteriori dettagli, consulta la [guida dell&#39;interfaccia utente XDM](../../xdm/ui/explore.md). |

Per ulteriori informazioni, consulta la [panoramica su XDM](../../xdm/home.md).

<!-- 
## Run and Operate {#run-and-operate}

Inspect, troubleshoot, and optimize your Experience Platform implementations with the Run and Operate tools. Gain visibility into scheduled batch activations, identify configuration issues, and improve system reliability.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Job Schedules](../../run-and-operate/job-schedules.md) general availability | [!DNL Job Schedules] provides a unified view of all scheduled batch processing jobs across your data pipeline, from ingestion through destination activation. Inspect execution status, identify scheduling conflicts, and diagnose configuration issues before they impact your business operations. |
| [Health Checks](../../run-and-operate/health-checks.md) general availability | Poor schema and identity configurations lead to significant downstream issues, including incorrect profile creation, failed segment qualification, and inaccurate activation. <br>Health checks shift your approach from reactive troubleshooting to proactive, preventative maintenance. Health checks are always-on scans of your schemas and identities used in your sandbox and provide a summary of issues that you can use to explore and troubleshoot. |

{style="table-layout:auto"}

For more information, read the [Run and Operate overview](../run-and-operate/overview.md), [Inspect job schedules](../run-and-operate/job-schedules.md), and the [Platform UI guide](../landing/ui-guide.md). -->

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Tipo di acquisizione | Ora puoi visualizzare il tipo di acquisizione degli attributi. Questo consente di conoscere l’origine dei dati e di creare tipi di pubblico migliori. Per ulteriori informazioni su questa funzione, consulta la [guida del Generatore di segmenti](/help/segmentation/ui/segment-builder.md). |
| Dati di riepilogo | Ora puoi visualizzare i dati di riepilogo per i tuoi attributi per i tipi di pubblico basati su account e persone. Per ulteriori informazioni su questa funzione nei tipi di pubblico dell&#39;account, leggere la [guida di Audience Builder](/help/rtcdp/segmentation/audience-builder.md) dell&#39;account. Per ulteriori informazioni su questa funzione nei tipi di pubblico basati sulle persone, consulta la [guida del Generatore di segmenti](/help/segmentation/ui/segment-builder.md). |

Per ulteriori informazioni, consulta la [[!DNL Segmentation Service] panoramica](../../segmentation/home.md).

## Origini

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| [!DNL Talon.One] | È ora possibile connettere Experience Platform a [!DNL Talon.One] utilizzando le nuove origini [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) e [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md). Utilizza le nuove origini per acquisire i dati del profilo fedeltà e gli eventi di transazione e attività fedeltà in Experience Platform. |
| Nuovi indirizzi IP da | Nuovi indirizzi IP per GBR9: Regno Unito sono stati aggiunti all’elenco di indirizzi che è necessario inserire nell&#39;elenco Consentiti per garantire connessioni di origini batch efficaci ad Experience Platform su Azure. Per ulteriori informazioni, vedere l&#39;elenco nella [Guida alla inserisce nell&#39;elenco Consentiti degli indirizzi IP per l&#39;accesso ai dati di accesso ai dati personali](../../sources/ip-address-allow-list.md#gbr9-united-kingdom). |
| Supporto migliorato per Change Data Capture | È ora possibile utilizzare Change Data Capture con le origini [!DNL Marketo Engage], [!DNL Microsoft Dynamics] e [!DNL Salesforce CRM]. |
| Guida all&#39;autenticazione migliorata per [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | La guida all&#39;autenticazione per l&#39;origine [!DNL Google BigQuery] è stata espansa con le seguenti informazioni: <ul><li>Ambiti necessari per il token di aggiornamento.</li><li>I ruoli IAM richiesti per l&#39;identità [!DNL Google].</li><li>Ulteriori indicazioni sull&#39;utilizzo di `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

<!--

NOTE FOR VLAD, CRITEO WAS REMOVED FROM EXTERNAL AUDIENCE SUPPORT

| Destination | Description |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) region selector | You can now find your region more easily with the new searchable dropdown, which combines search and dropdown into one control. |
| New table structure for [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) destinations | Tables shared into your Snowflake account now have a new structure which includes separate audience name and audience origin columns. The new table structure applies to all new destination connections set up moving forward. For any new connections that you set up, an old format and new format table are created. The old table structure will be kept for another three months before being deprecated. Read more in the [Exported data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) section of the Snowflake Batch documentation. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) destinations with OAuth 2 and mTLS | You can now create and authenticate HTTP API destinations that use OAuth 2 when the authentication endpoint requires mutual TLS (mTLS); token retrieval during destination setup now supports mTLS. |

| Fix | Description |
| --- | --- |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) and [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) account ID validation | A regular expression validator has been added to the Account ID step. When you enter your ID, it is now validated to ensure organization ID and account ID are in the correct format (separated by a dot). |

-->