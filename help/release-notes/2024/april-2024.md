---
title: Note sulla versione di Adobe Experience Platform - Aprile 2024
description: Note sulla versione di Adobe Experience Platform di aprile 2024.
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: d6e306294d0a119108e2de7ba03ebed4f633fba1
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 100%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 30 aprile 2024**

>[!TIP]
>
>Utilizza il [glossario di Adobe Experience Platform](/help/landing/glossary.md) per acquisire familiarità con la terminologia utilizzata in Real-time Customer Data Platform e Adobe Experience Platform. Se non trovi un termine specifico, utilizza le opzioni di feedback nella pagina per richiedere che nuovi termini vengano aggiunti al glossario.

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Dashboard](#dashboards)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Identity Service](#identity-service)
- [Monitoraggio](#monitoring)
- [Servizio query](#query-service)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Dashboard {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Informazioni su B2B di Real-Time Customer Data Platform | Esplora informazioni preconfigurate [sui dati B2B di Real-Time CDP relativi ad account e opportunità](../../dashboards/insights/account-profiles.md) per aiutarti a comprendere i tuoi dati e a prendere decisioni aziendali. Puoi anche [creare informazioni personalizzate utilizzando il modello di dati B2B di Real-Time CDP](../../dashboards/data-models/cdp-insights-data-model-b2c.md) per visualizzare ed esplorare i dati e salvare le visualizzazioni personalizzate nella dashboard. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli a Edge Network di Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Estensioni | Estensione tag [!DNL Acxiom Anonymous Visitor Insights] | Scopri da dove provengono i visitatori del tuo sito web con [!DNL Acxiom's Visitor Insights]. Utilizzando la tecnologia di ricerca IP geografica, Acxiom può individuare la posizione dei browser anonimi. Una volta identificata, una ricerca nel database organizzato produce ulteriori informazioni che vengono rimandate al browser. I creatori di contenuti possono quindi adattare i loro contenuti in modo che corrispondano a questi punti dati, fornendo un’esperienza più personalizzata e coinvolgente per i visitatori, anche se hanno iniziato come estranei. |
| Stream di dati | [Rilevamento bot Edge Network](../../datastreams/bot-detection.md) | Il traffico proveniente da entità non umane, come programmi automatizzati, scraper web, spider, scanner scriptati, può rendere più difficile identificare gli eventi che si verificano dai visitatori umani. Questo tipo di traffico può influenzare negativamente importanti metriche aziendali, portando a rapporti di traffico errati. <br>Rilevamento bot consente di identificare gli eventi generati da [Web SDK](../../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) e [[!DNL Server API]](../../server-api/overview.md) come generati da spider e bot noti. Configurando il rilevamento di bot per gli stream di dati, puoi identificare indirizzi IP, intervalli IP e intestazioni di richiesta specifici che desideri classificare come eventi bot. <br> L’identificazione del traffico da bot può fornire una misurazione più accurata dell’attività degli utenti sul sito o sull’app mobile. |
| SDK mobile | Versione principale | Sono state rilasciate nuove versioni principali di SDK mobile per le seguenti piattaforme: iOS Mobile Core 5.x e estensioni compatibili di iOS, Android Mobile Core 3.x e estensioni compatibili di Android, React Native Core 6.x ed estensioni compatibili di React Native, Flutter Core 4.x ed estensioni compatibili di Flutter. Questa versione include diverse nuove funzioni e miglioramenti, tra cui il supporto SDK Android per Jetpack Compose, il supporto per esperienze basate su codice Adobe Journey Optimizer e la disponibilità generale dell’estensione di messaggistica di Adobe Journey Optimizer per Flutter. Per note sulla versione più dettagliate, consulta [Note sulla versione di SDK mobile](https://developer.adobe.com/client-sdks/home/release-notes/). |
| SDK mobile | Privacy | A causa dell’aggiornamento della policy di Apple, a partire dal 1° maggio 2024, gli sviluppatori devono implementare nuove funzioni per la privacy per inviare il messaggio a App Store. Tutti i clienti Adobe che utilizzano l’SDK mobile devono effettuare l’aggiornamento alla versione 5.x dell’SDK se desiderano ricevere l’approvazione di App Store dopo il 1° maggio. |
| SDK Roku | SDK Roku | La prima versione principale dell’SDK Roku è stata rilasciata con il supporto per contenuti in streaming per Edge Network di Platform. |
| Tag e inoltro eventi | Guide interne al prodotto | I [tag](../../tags/home.md) e [inoltro eventi](../../tags/ui/event-forwarding/overview.md) di Experience Platform offrono una nuova gamma di esperienze che possono aiutarti a iniziare rapidamente e a realizzare un time-to-value rapido. Queste esperienze includono nuove schermate di onboarding, tutorial interni al prodotto e descrizioni. <br>![Inoltro eventi con le guide interne al prodotto evidenziate.](../2024/assets/april/event-forwarding.png "Editor di schema con i campi Tipo e Tipo di valore mappa evidenziati."){width="100" zoomable="yes"}<br> |
| Web SDK | Adozione semplificata di Web SDK per clienti di Audience Manager | Più aggiornamenti Web SDK ora semplificano l’adozione di Web SDK senza utilizzare Experience Data Model (XDM) per soluzioni di Experience Cloud, come Audience Manager, Analytics e Target. Per saperne di più sull’adozione di Web SDK per Audience Manager, consulta le seguenti guide: <ul><li><a href="https://experienceleague.adobe.com/it/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Aggiorna la libreria di raccolta dati per Audience Manager dall’estensione tag di Audience Manager all’estensione tag Web SDK</li><li><a href="https://experienceleague.adobe.com/it/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Aggiorna la libreria di raccolta dati per Audience Manager dalla libreria JavaScript di AppMeasurement alla libreria JavaScript di SDK Web</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Per ulteriori informazioni sulle raccolte dati dati, consulta la [panoramica sulla raccolta dati](../../collection/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Il parametro `isRequired` è ora disponibile per i campi dati cliente nidificati in Destination SDK | Durante la configurazione di una destinazione in Destination SDK, ora puoi [impostare i campi dei dati cliente nidificati come richiesto](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). In questo modo, gli utenti che impostano la destinazione non possono procedere con il flusso di attivazione fino a quando non selezionano un valore per quel campo. |
| La segmentazione Edge non è più un requisito obbligatorio quando si imposta una destinazione Adobe Target con Web SDK | In precedenza, durante la configurazione di una [destinazione Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) con Web SDK, era necessario abilitare lo stream di dati per la personalizzazione e la segmentazione Edge. Il requisito che lo stream di dati sia abilitato per la segmentazione Edge [ è stato rimosso](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Tieni presente che questo modello di integrazione ti consente di beneficiare di un sottoinsieme di casi d’uso di personalizzazione solo quando utilizzi Adobe Target con Real-Time CDP. Ulteriori informazioni sui [casi d’uso abilitati dal tipo di integrazione](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases). |
| [!BADGE Beta]{type=Informative} Rimuovi più tipi di pubblico e set di dati dai flussi di attivazione | Ora puoi selezionare e rimuovere più tipi di pubblico e set di dati dai flussi di attivazione di destinazione. Per ulteriori dettagli, consulta la documentazione [dettagli di destinazione](../../destinations/ui/destination-details-page.md#bulk-remove) e [esportazione set di dati](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Identity Service {#identity-service}

Utilizza Identity Service di Adobe Experience Platform per creare una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Obsolescenza degli endpoint `/orgs/{ORG}/` nell’API | I seguenti endpoint nell‘[[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) sono stati dichiarati obsoleti:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> È possibile utilizzare gli endpoint `/idnamespace/identities` e `/idnamespace/identities/{ID}` per eseguire le stesse attività e recuperare tutti gli spazi dei nomi in un’organizzazione o uno spazio dei nomi specifico in un’organizzazione. |

{style="table-layout:auto"}

Per ulteriori informazioni su Identity Service, leggi la [panoramica s Identity Service](../../identity-service/home.md).

## Monitoraggio {#monitoring}

Utilizza la dashboard di monitoraggio nell’interfaccia utente di Experience Platform per monitorare il percorso dei dati da origini, Identity Service, profilo cliente in tempo reale, tipi di pubblico e destinazioni.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Espansione della dashboard di monitoraggio | Ora puoi utilizzare la dashboard di monitoraggio per diversi tipi di dati in base al caso d’uso aziendale. Utilizza la dashboard di monitoraggio per monitorare le attività relative ai tipi di dati di persone, account e potenziali clienti in origini, tipi di pubblico e destinazioni. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la guida sull’[utilizzo della dashboard di monitoraggio](../../dataflows/ui/monitor.md).

## Query Service {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire nel profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Quarantena della query | Isolamento automatico delle esecuzioni delle query non riuscite per evitare interruzioni e mantenere prestazioni coerenti. Per ulteriori informazioni, consulta la documentazione sulla [quarantena della query](../../query-service/ui/query-schedules.md#quarantine). |
| Annulla query | Controlla l’esecuzione delle query e migliora la produttività annullando le query con tempi di esecuzione lunghi. Per ulteriori informazioni, consulta la documentazione su [annulla query](../../query-service/ui/user-guide.md#cancel-query). |
| Avvisi query pianificata | Rimani informato con le notifiche proattive durante la pianificazione delle query per garantire una gestione efficiente e tempestiva delle attività. È possibile [abbonarsi agli avvisi durante la creazione di una query](../../query-service/ui/query-schedules.md#alerts-for-query-status) o utilizzando le azioni in linea per le query pianificate esistenti. Per ulteriori informazioni, consulta la documentazione sugli [abbonamenti agli avvisi con azioni in linea](../../query-service/ui/monitor-queries.md#alert-subscription). |
| Navigazione query pianificata migliorata | Naviga facilmente tra modelli di query ed esecuzioni pianificate per una maggiore produttività. Per ulteriori informazioni, consulta la documentazione sulla [visualizzazione delle esecuzioni delle query pianificate](../../query-service/ui/query-schedules.md#scheduled-query-runs). |
| Output query esteso | Accedi a un massimo di 500 righe di risultati di query nella console per un’analisi più approfondita dei dati. Per ulteriori informazioni, consulta la documentazione sul [conteggio dei risultati](../../query-service/ui/user-guide.md#result-count). |
| Disattivazione dell’editor di query precedente | A partire dal 30 aprile 2024, l’editor di query avanzato è diventato l’editor predefinito per tutti gli utenti. L’editor precedente diventerà obsoleto il 24 maggio 2024 e non sarà più disponibile. Per ulteriori informazioni, consulta la [guida utente dell’editor di query](../../query-service/ui/user-guide.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sul Servizio query, consulta la [Panoramica sul servizio query](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, Experience Platform fornisce ambienti sandbox che permettono di suddividere una singola istanza di Platform in ambienti virtuali separati, utili per le attività di sviluppo e evoluzione delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Strumenti sandbox](../../sandboxes/ui/sandbox-tooling.md) | Utilizza gli strumenti sandbox per [esportare](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) tutti i tipi di oggetto supportati in un pacchetto sandbox completo, quindi [importa](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) il pacchetto in varie sandbox per replicare le configurazioni degli oggetti. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle sandbox, leggi la [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Funzione aggiornata**

| Funzione | Descrizione |
| ------- | ----------- |
| Stati del ciclo di vita del pubblico | Gli stati del ciclo di vita del pubblico sono stati semplificati per facilitare la gestione del ciclo di vita. Per ulteriori informazioni su questi stati del ciclo di vita, leggi le [Domande frequenti sul servizio di segmentazione](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Nuove origini**

| Nuove origini | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Utilizza l’[[!DNL PathFactory] origine](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) per integrare i dati dei visitatori, delle sessioni e delle visualizzazioni di pagina da [!DNL PathFactory] a Experience Platform. Per informazioni su come iniziare, leggi la [[!DNL PathFactory] panoramica](../../sources/connectors/marketing-automation/pathfactory.md). |
| [!DNL Teradata Vantage] | Utilizza l’[[!DNL Teradata Vantage] origine](../../sources/tutorials/ui/create/databases/teradata-vantage.md) per acquisire i dati da ambienti multi-cloud ibridi a Experience Platform. Per informazioni su come iniziare, leggi la [[!DNL Teradata Vantage] panoramica](../../sources/connectors/databases/teradata-vantage.md). |

{style="table-layout:auto"}

**Funzioni nuove e aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Aggiornamenti agli indirizzi IP per l’elenco Consentiti in VA7 | I seguenti indirizzi IP sono stati aggiunti all’elenco di indirizzi IP da aggiungere all’elenco Consentiti per VA7 (Nord America): <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Per un elenco completo degli indirizzi IP da aggiungere all’elenco Consentiti, leggi il [documento dell’elenco Consentiti dell’indirizzo IP](../../sources/ip-address-allow-list.md). |
| Supporto per nuovi tipi di autenticazione con origine [!DNL Azure Event Hubs] | È ora possibile connettere l’origine [!DNL Event Hubs] a Experience Platform utilizzando [!DNL Azure Active Directory Authentication] o [!DNL Scoped Azure Active Directory Authentication]. Per ulteriori informazioni, leggi la guida sulla [connessione [!DNL Event Hubs] a Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md). |
| Aggiornamenti al recupero delle credenziali [!DNL Data Landing Zone] | È ora possibile utilizzare la barra corretta nell’area di lavoro delle origini per recuperare le credenziali di [!DNL Data Landing Zone]. Ora puoi anche utilizzare la barra a destra per aggiornare le credenziali. Per ulteriori informazioni, leggi la [[!DNL Data Landing Zone] guida dell’interfaccia utente](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Per ulteriori informazioni sulle origini, leggi la [panoramica sulle origini](../../sources/home.md).
