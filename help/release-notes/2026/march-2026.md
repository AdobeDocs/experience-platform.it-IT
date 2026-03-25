---
title: Note sulla versione di Adobe Experience Platform - Marzo 2026
description: Note sulla versione di Adobe Experience Platform di marzo 2026.
exl-id: 66b948fd-caa0-4e5e-83dd-3b15b77c09fa
source-git-commit: 6b6a03fb8675ed01dd255f7206b23b05c809f2a6
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 20%

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
- [Stream di dati](#datastreams)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Profilo cliente in tempo reale](#real-time-customer-profile)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Gestione avanzata del ciclo di vita dei dati {#advanced-data-lifecycle-management}

Experience Platform fornisce una suite di funzionalità di igiene dei dati per aiutarti a gestire i dati memorizzati tramite l’eliminazione programmatica di record e set di dati dei consumatori. Utilizzando l’area di lavoro del ciclo di vita dei dati nell’interfaccia utente o le chiamate all’API di igiene dei dati, puoi gestire in modo efficace gli archivi di dati. Usa queste funzionaità per garantire che le informazioni vengano utilizzate come previsto, che vengano aggiornate quando è necessario correggere dati scorretti e che vengano eliminate quando i criteri organizzativi lo ritengono necessario.

| Funzione | Descrizione |
| --- | --- |
| Eliminazione di record con set di dati multipli e solo profilo (solo API) | È possibile inviare un singolo ID set di dati, un elenco separato da virgole di ID set di dati o il valore letterale `ALL` in `datasetId` per eliminare identità in uno, molti o tutti i set di dati. È inoltre possibile limitare l&#39;eliminazione ai servizi correlati al profilo impostando `targetServices` su `["identity","profile","ajo"]`, lasciando invariato il datalake. Questa funzionalità è disponibile solo tramite l&#39;API di igiene dei dati. Per ulteriori dettagli, vedere la [Guida all&#39;eliminazione degli ordini di lavoro](../../hygiene/api/workorder.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulla gestione avanzata del ciclo di vita dei dati](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Utilizza Agent Orchestrator per creare e distribuire agenti basati sull’intelligenza artificiale che automatizzano i flussi di lavoro e interagiscono con i clienti su più canali.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Adobe Marketing Agent per [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent per [!DNL Microsoft 365 Copilot] è il tuo agente incorporato che porta le informazioni di marketing di Adobe direttamente negli strumenti quotidiani come [!DNL Teams], [!DNL Word], [!DNL PowerPoint] e altre app di [!DNL Microsoft 365]. È possibile utilizzare questo agente per richiamare informazioni attendibili sulle campagne dalle applicazioni Adobe durante la pianificazione delle campagne, la revisione dei tipi di pubblico, la collaborazione con i colleghi per rispondere alle domande dei clienti e per prendere decisioni basate sui dati senza uscire dal flusso di lavoro [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [documentazione su Agent Orchestrator](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Stream di dati {#datastreams}

Un flusso di dati rappresenta la configurazione lato server durante l’implementazione degli SDK Adobe Experience Platform Web e Mobile e dell’API server di Adobe Experience Platform Edge Network. Il comando di configurazione dello stream di dati negli SDK gestisce tutti i servizi con cui un client interagisce.

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale delle configurazioni dello stream di dati dinamici | Le configurazioni dello stream di dati dinamici sono ora generalmente disponibili. Con le configurazioni dello stream di dati dinamici, puoi definire set di regole configurabili dall’utente per ciascun servizio abilitato per lo stream di dati, che determinano quale soluzione Experience Cloud deve ricevere ogni tipo di dati. Per ulteriori informazioni, consulta la [guida alle configurazioni dello stream di dati dinamici](../../datastreams/configure-dynamic-datastream.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [panoramica sugli stream di dati](../../datastreams/overview.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con le piattaforme di destinazione. Utilizza le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| [Selettore di area per il batch Snowflake](../../destinations/catalog/warehouses/snowflake-batch.md) | Ora è più facile trovare la tua regione con il nuovo menu a discesa ricercabile, che combina ricerca e menu a discesa in un unico controllo. Questo aggiornamento verrà introdotto entro la fine di marzo. |
| Nuova struttura di tabella per [destinazioni Batch Snowflake](../../destinations/catalog/warehouses/snowflake-batch.md) | Le tabelle condivise nel tuo account Snowflake ora dispongono di una nuova struttura che include colonne separate per il nome del pubblico e l’origine del pubblico. La nuova struttura di tabella si applica a tutte le nuove connessioni di destinazione impostate per il passaggio successivo. Per qualsiasi nuova connessione impostata, vengono create entrambe le strutture di tabella: la nuova struttura viene preceduta da V2 e la vecchia struttura viene mantenuta fino alla fine di giugno 2026, dopo di che verrà dichiarata obsoleta. Ulteriori informazioni sono disponibili nella sezione [Dati esportati](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) della documentazione di Snowflake Batch. Questo aggiornamento verrà introdotto entro la fine di marzo. |
| [Connessione Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-dsp-connection.md) | La nuova connessione Adobe Advertising DSP offre le stesse funzionalità della connessione legacy e il supporto di identità aggiuntive. Con il nuovo connettore, puoi anche esportare identità basate su cookie in Adobe Advertising DSP. |
| [Connessione FreeWheel](../../destinations/catalog/advertising/freewheel.md) | Invia [!DNL Real-Time CDP] tipi di pubblico a FreeWheel come file batch giornalieri in modo da poterli indirizzare a offerte e campagne FreeWheel su CTV, video e visualizzazione. Contatta il team del tuo account Adobe per accedere. |
| Supporto per il pubblico esterno per [il CRM del Trade Desk](../../destinations/catalog/advertising/tradedesk-emails.md) e [Pinterest](../../destinations/catalog/advertising/pinterest.md) | È ora possibile attivare i tipi di pubblico da origini diverse da Segmentation Service a CRM, Criteo e Pinterest del Trade Desk, inclusi i tipi di pubblico di caricamento personalizzati (importati da CSV), i tipi di pubblico simili, i tipi di pubblico federati e i tipi di pubblico creati in altre app di Experience Platform come [!DNL Adobe Journey Optimizer]. Questo aggiornamento verrà introdotto entro la fine di marzo. Per informazioni dettagliate, consulta la sezione [tipi di pubblico supportati](../../destinations/catalog/advertising/criteo.md#supported-audiences) nella pagina del catalogo di ciascuna destinazione. |
| Limite aumentato per i tipi di pubblico di caricamento personalizzati | Ora puoi attivare fino a 20 tipi di pubblico per caricamento personalizzato per istanza di destinazione. In precedenza, questo limite era di 10. Per informazioni dettagliate, consulta le [destinazioni guardrail](../../destinations/guardrails.md#batch-file-based-activation). |
| [Esporta ora il file](../../destinations/ui/export-file-now.md) e [supporto API di attivazione ad hoc](../../destinations/api/ad-hoc-activation-api.md) per tipi di pubblico esterni | È ora possibile utilizzare l’interfaccia Export file now (UI) e l’API di attivazione ad hoc con tipi di pubblico esterni (come caricamenti personalizzati, lookalike, federati e tipi di pubblico da altre app Experience Platform) durante l’attivazione di destinazioni basate su file in batch. Questo aggiornamento verrà introdotto entro la fine di marzo. |
| [Destinazioni API HTTP](../../destinations/catalog/streaming/http-destination.md) con OAuth 2 e mTLS | Ora puoi creare e autenticare destinazioni API HTTP che utilizzano OAuth 2 quando l’endpoint di autenticazione richiede TLS reciproco (mTLS); il recupero del token durante la configurazione della destinazione ora supporta mTLS. Questo aggiornamento verrà introdotto entro la fine di marzo. |

{style="table-layout:auto"}

**Correzioni e miglioramenti**

| Correzione | Descrizione |
| --- | --- |
| [hashing del numero di telefono del connettore TikTok](../../destinations/catalog/social/tiktok.md) | È stato risolto un problema che impediva l’attivazione a TikTok delle identità codificate dai numeri di telefono a causa di un’errata configurazione nella scheda di destinazione. Per beneficiare di questa correzione, imposta un nuovo flusso di attivazione o rimuovi la mappatura dei numeri di telefono dal flusso esistente, salvalo e aggiungilo nuovamente. |
| Convalida dell&#39;ID account [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) e [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) | Al passaggio ID account è stato aggiunto un validatore di espressioni regolari. Quando inserisci l&#39;ID, questo viene convalidato per garantire che l&#39;ID organizzazione e l&#39;ID account siano nel formato corretto (separati da un punto). Questo aggiornamento verrà introdotto entro la fine di marzo. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

| Funzione | Descrizione |
| --- | --- |
| Azioni entità XDM ed eliminazione del supporto | Consente di accedere alle azioni per schemi, classi, gruppi di campi e tipi di dati direttamente dai menu delle tabelle in linea e dai menu dell&#39;intestazione della pagina dei dettagli. Se disponi delle autorizzazioni necessarie, puoi anche eliminare le entità dell’organizzazione quando non sono utilizzate dai set di dati e non sono abilitate per il profilo. Per ulteriori dettagli, consulta la [guida dell&#39;interfaccia utente XDM](../../xdm/ui/explore.md). |

Per ulteriori informazioni, consulta la [panoramica su XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#real-time-customer-profile}

Real-Time Customer Profile offre una visualizzazione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi dati online, offline, del sistema CRM e di terze parti. Utilizza il profilo per consolidare i dati dei clienti in una visualizzazione unificata che offra un account actionable e con marca temporale per ogni interazione con il cliente.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Eventi | È ora possibile impostare il periodo di lookback degli eventi durante la navigazione nei profili. Questo consente di visualizzare gli eventi a cui è associato il profilo per il periodo di tempo specificato. Per ulteriori informazioni, leggere la [Guida dell&#39;interfaccia utente del profilo](../../profile/ui/user-guide.md#events). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [[!DNL Real-Time Customer Profile] panoramica](../../profile/home.md).

## Esecuzione e funzionamento {#run-and-operate}

Ispeziona, risolvi i problemi e ottimizza le implementazioni di Experience Platform con gli strumenti Esegui e opera. Ottieni visibilità sulle attivazioni batch pianificate, identifica i problemi di configurazione e migliora l’affidabilità del sistema.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Pianificazioni processi](../../run-and-operate/job-schedules.md) disponibilità generale | [!DNL Job Schedules] fornisce una visualizzazione unificata di tutti i processi di elaborazione batch pianificati nella pipeline di dati, dall&#39;acquisizione all&#39;attivazione della destinazione. Esaminare lo stato di esecuzione, identificare i conflitti di pianificazione e diagnosticare i problemi di configurazione prima che influiscano sulle operazioni aziendali. |
| [Verifiche stato](../../run-and-operate/health-checks.md) disponibilità generale | Configurazioni di schema e identità inadeguate causano significativi problemi a valle, tra cui creazione di profili errata, qualificazione dei segmenti non riuscita e attivazione imprecisa. <br>I controlli di integrità spostano il tuo approccio dalla risoluzione dei problemi reattiva alla manutenzione proattiva e preventiva. I controlli di integrità sono scansioni sempre attive degli schemi e delle identità utilizzati nella sandbox e forniscono un riepilogo dei problemi che è possibile utilizzare per esplorare e risolvere. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica sull&#39;esecuzione e l&#39;utilizzo](../../run-and-operate/overview.md), [Pianificazioni dei processi di ispezione](../../run-and-operate/job-schedules.md) e la [Guida all&#39;interfaccia utente di Platform](../../landing/ui-guide.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Tipo di acquisizione | Ora puoi visualizzare il tipo di acquisizione degli attributi. Questo consente di conoscere l’origine dei dati e di creare tipi di pubblico migliori. Per ulteriori informazioni su questa funzione, consulta la [guida del Generatore di segmenti](../../segmentation/ui/segment-builder.md). |
| Dati di riepilogo | Ora puoi visualizzare i dati di riepilogo per i tuoi attributi per i tipi di pubblico basati su account e persone. Per ulteriori informazioni su questa funzione nei tipi di pubblico dell&#39;account, leggere la [guida di Audience Builder](../../rtcdp/segmentation/audience-builder.md) dell&#39;account. Per ulteriori informazioni su questa funzione nei tipi di pubblico basati sulle persone, consulta la [guida del Generatore di segmenti](../../segmentation/ui/segment-builder.md). |

Per ulteriori informazioni, consulta la [[!DNL Segmentation Service] panoramica](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Utilizza queste connessioni di origine per autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| Nuovi indirizzi IP da | Nuovi indirizzi IP per GBR9: Regno Unito sono stati aggiunti all’elenco di indirizzi che è necessario inserire nell&#39;elenco Consentiti per garantire connessioni di origini batch efficaci ad Experience Platform su Azure. Per ulteriori informazioni, vedere l&#39;elenco nella [Guida alla inserisce nell&#39;elenco Consentiti degli indirizzi IP per l&#39;accesso ai dati di accesso ai dati personali](../../sources/ip-address-allow-list.md#gbr9-united-kingdom). |
| Supporto migliorato per Change Data Capture | È ora possibile utilizzare Change Data Capture con le origini [!DNL Marketo Engage], [!DNL Microsoft Dynamics] e [!DNL Salesforce CRM]. |
| Guida all&#39;autenticazione migliorata per [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | La guida all&#39;autenticazione per l&#39;origine [!DNL Google BigQuery] è stata espansa con le seguenti informazioni: <ul><li>Ambiti necessari per il token di aggiornamento.</li><li>I ruoli IAM richiesti per l&#39;identità [!DNL Google].</li><li>Ulteriori indicazioni sull&#39;utilizzo di `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).
