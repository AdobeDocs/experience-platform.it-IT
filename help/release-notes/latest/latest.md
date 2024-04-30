---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Adobe Experience Platform di marzo 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6ad7d55ca0a544879db9738c0a4ab914fdc363bd
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 18%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: mercoledì 30 aprile 2024**

>[!TIP]
>
>Utilizza il [Glossario di Adobe Experience Platform](/help/landing/glossary.md) per acquisire familiarità con la terminologia utilizzata in Real-time Customer Data Platform e Adobe Experience Platform. Se non riesci a trovare un termine specifico che stai cercando, utilizza le opzioni di feedback nella pagina per richiedere che nuovi termini vengano aggiunti al glossario.

Aggiornamenti alle funzioni esistenti in Experienci Platform:

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

Adobe Experience Platform fornisce più dashboard attraverso i quali è possibile visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Informazioni B2B di Real-time Customer Data Platform | Esplora informazioni preconfigurate sui dati B2B di Real-Time CDP relative agli account e alle opportunità per aiutarti a comprendere i tuoi dati e a prendere decisioni aziendali. Puoi anche creare informazioni personalizzate utilizzando il modello di dati B2B di Real-Time CDP per visualizzare ed esplorare i dati e salvare le visualizzazioni personalizzate nel dashboard. |

{style=“table-layout:auto”}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli all’Edge Network di Experience Platform in cui possono essere arricchiti, trasformati e distribuiti a destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Approfondimenti | [!DNL Acxiom] Approfondimenti visitatore anonimo | Scopri da dove provengono i visitatori del tuo sito web con [!DNL Acxiom's] Approfondimenti visitatore. Utilizzando la tecnologia di ricerca IP geografica, individuiamo la posizione dei browser anonimi. Una volta identificata, una ricerca rapida nel nostro database organizzato produce ulteriori informazioni che vengono rimandate al browser. Per i creatori di contenuti, ciò significa un’opportunità d’oro per adattare i loro contenuti in modo che corrispondano a questi punti di dati, fornendo un’esperienza più personalizzata e coinvolgente per i visitatori, anche se sono partiti come estranei. |
| Stream di dati | [Edge Network di rilevamento di bot](../../datastreams/bot-detection.md) | Il traffico proveniente da entità non umane, come programmi automatizzati, web scraper, ragni, scanner scriptati, può rendere più difficile identificare gli eventi che si verificano dai visitatori umani. Questo tipo di traffico può influenzare negativamente importanti metriche aziendali, portando a rapporti di traffico errati. <br>Il rilevamento dei bot consente di identificare gli eventi generati dai [SDK per web](../../web-sdk/home.md), [SDK per dispositivi mobili](https://developer.adobe.com/client-sdks/home/) e [[!DNL Server API]](../../server-api/overview.md) come generate da spider e bot noti. Configurando il rilevamento di bot per gli stream di dati, puoi identificare indirizzi IP, intervalli IP e intestazioni di richiesta specifici che desideri classificare come eventi bot. <br> L’identificazione del traffico da bot può fornire una misurazione più accurata dell’attività degli utenti sul sito o sull’app mobile. |
| Mobile SDK | Versione principale | Sono state rilasciate nuove versioni principali dell’SDK di Mobile per le seguenti piattaforme: iOS Mobile Core 5.x e estensioni compatibili per iOS, Android Mobile Core 3.x ed estensioni compatibili per Android, React Native Core 6.x e estensioni compatibili per React Native, Flutter Core 4.x ed estensioni compatibili per Flutter. Questa versione include diverse nuove funzioni e miglioramenti, tra cui il supporto nell’SDK per Android per Jetpack Compose, il supporto per esperienze basate su codice Adobe Journey Optimizer e la disponibilità generale dell’estensione Adobe Journey Optimizer Messaging per Flutter. Per note sulla versione più dettagliate, consulta [Note sulla versione dell’SDK Mobile](https://developer.adobe.com/client-sdks/home/release-notes/). |
| Mobile SDK | Privacy | A causa dell’aggiornamento della policy di Apple, a partire dal 1° maggio 2024, gli sviluppatori devono implementare nuove funzioni per la privacy per inviare il messaggio a App Store. Tutti i clienti Adobe che utilizzano l’SDK di Mobile devono effettuare l’aggiornamento alla versione 5.x dell’SDK se desiderano ricevere l’approvazione di App Store dopo il 1° maggio. |
| SDK Roku | SDK Roku | La prima versione principale dell’SDK Roku è stata rilasciata con il supporto per Streaming Media per l’Edge Network di Platform. |
| Tag e inoltro eventi | Linee guida interne al prodotto | Experience Platform [Tag](../../tags/home.md) e [Inoltro eventi](../../tags/ui/event-forwarding/overview.md) offre una nuova gamma di esperienze che possono aiutarti a iniziare rapidamente e a realizzare un time-to-value rapido. Queste esperienze includono nuove schermate di onboarding, esercitazioni interne al prodotto e descrizioni. <br>![Inoltro eventi con le linee guida interne al prodotto evidenziate.](../2024/assets/april/event-forwarding.png "Editor schemi con i campi Tipo e Tipo di valore mappa evidenziati."){width="100" zoomable="yes"}<br> |
| SDK per web | Adozione semplificata di Web SDK per Audienci Manager clienti | Più aggiornamenti dell’SDK per web ora semplificano l’adozione dell’SDK web senza utilizzare Experience Data Model (XDM) per soluzioni di Experience Cloud, come Audienci Manager, Analytics e Target. Per saperne di più sull’adozione di Audienci Manager Web SDK, consulta le seguenti guide: <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Aggiorna la libreria di raccolta dati, ad Audience Manager dall’estensione tag Audienci Manager all’estensione tag Web SDK</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Aggiorna la libreria di raccolta dati, ad Audience Manager dalla libreria JavaScript di AppMeasurement alla libreria JavaScript di Web SDK</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Per ulteriori informazioni sulle raccolte di dati, consulta [panoramica sulla raccolta dati](../../collection/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| `isRequired` Il parametro è ora disponibile per i campi dati cliente nidificati in Destination SDK | Durante la configurazione di una destinazione in Destination SDK, ora puoi [imposta i campi dati cliente nidificati come richiesto](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). In questo modo, gli utenti che impostano la destinazione non possono procedere con il flusso di attivazione fino a quando non selezionano un valore per quel campo. |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

<!--| [!BADGE Beta]{type=Informative} Remove multiple audiences and datasets from activation flows | You can now select and remove multiple audiences and datasets from destination activation flows. See the [destination details](../../destinations/ui/destination-details-page.md#bulk-remove) and [dataset export](../../destinations/ui/export-datasets.md) documentation for more details. |-->

## Identity Service {#identity-service}

Utilizza il servizio Adobe Experience Platform Identity per creare una visione completa dei clienti e dei loro comportamenti, collegando le identità tra dispositivi e sistemi e consentendo di fornire esperienze digitali personali e di impatto in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Obsolescenza del `/orgs/{ORG}/` endpoint nell’API | I seguenti endpoint nella [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) sono stati dichiarati obsoleti:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> È possibile utilizzare `/idnamespace/identities` e `/idnamespace/identities/{ID}` endpoint per eseguire le stesse attività e recuperare tutti gli spazi dei nomi di un&#39;organizzazione o uno spazio dei nomi specifico di un&#39;organizzazione. |

{style="table-layout:auto"}

Per ulteriori informazioni sul servizio Identity, consulta [Panoramica del servizio Identity](../../identity-service/home.md).

## Monitoraggio {#monitoring}

Utilizza la dashboard di monitoraggio nell’interfaccia utente di Experienci Platform per monitorare il percorso dei dati da Sorgenti, Servizio identità, Profilo cliente in tempo reale, Tipi di pubblico e Destinazioni.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Monitoraggio dell’espansione della dashboard | Ora puoi utilizzare la dashboard di monitoraggio per diversi tipi di dati in base al caso di utilizzo aziendale. Utilizza il dashboard di monitoraggio per monitorare le attività relative ai tipi di dati di persone, account e potenziali clienti in origini, tipi di pubblico e destinazioni. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la guida su [utilizzo del dashboard di monitoraggio](../../dataflows/ui/monitor.md).

## Servizio query {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform.[!DNL Data Lake] Puoi unire qualsiasi set di dati da [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’acquisizione in Real-time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Quarantena query | Isolamento automatico delle esecuzioni delle query non riuscite per evitare interruzioni e mantenere prestazioni coerenti. |
| Annulla query | Controlla l’esecuzione delle query e migliora la produttività annullando le query con tempi di esecuzione lunghi. |
| Avvisi di query pianificate | Notifiche proattive durante la pianificazione delle query per garantire una gestione efficiente e tempestiva delle attività. È possibile sottoscrivere gli avvisi durante la creazione di una query o utilizzando le azioni in linea per le query pianificate esistenti. |
| Navigazione query pianificata migliorata | Navigazione semplice tra modelli di query ed esecuzioni pianificate per una maggiore produttività. |
| Output query esteso | Puoi accedere a un massimo di 500 righe di risultati di query nella console per un’analisi più approfondita dei tuoi dati. |
| Fine dell’editor di query legacy | A partire dal 30 aprile 2024, l’Editor query avanzato è diventato l’editor predefinito per tutti gli utenti. L’editor legacy diventerà obsoleto il 30 maggio 2024 e non sarà più disponibile. |

{style=“table-layout:auto”}

Per ulteriori informazioni sul Servizio query, consulta la [Panoramica sul servizio query](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experienci Platform fornisce sandbox che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Strumenti sandbox](../../sandboxes/ui/sandbox-tooling.md) | Utilizzare gli strumenti sandbox per [esportare](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) tutti i tipi di oggetto supportati in un pacchetto sandbox completo, quindi [importa](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) il pacchetto in diverse sandbox per replicare le configurazioni degli oggetti. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle sandbox, consulta [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Funzione aggiornata**

| Funzione | Descrizione |
| ------- | ----------- |
| Stati del ciclo di vita del pubblico | Gli stati del ciclo di vita del pubblico sono stati semplificati per semplificare la gestione del ciclo di vita. Per ulteriori informazioni su questi stati del ciclo di vita, leggere [Domande frequenti sul servizio di segmentazione](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experienci Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Nuove sorgenti**

| Nuove sorgenti | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Utilizza il [[!DNL PathFactory] sorgente](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) per integrare i dati di visitatori, sessioni e visualizzazioni di pagina da [!DNL PathFactory] all&#39;Experience Platform. Leggi le [[!DNL PathFactory] panoramica](../../sources/connectors/marketing-automation/pathfactory.md) per informazioni su come iniziare. |
| [!DNL Teradata Vantage] | Utilizza il [[!DNL Teradata Vantage] sorgente](../../sources/tutorials/ui/create/databases/teradata-vantage.md) per acquisire dati da ambienti ibridi multi-cloud ad Experienci Platform. Leggi le [[!DNL Teradata Vantage] panoramica](../../sources/connectors/databases/teradata-vantage.md) per informazioni su come iniziare. |

{style="table-layout:auto"}

**Funzioni nuove e aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Aggiornamenti agli indirizzi IP per l’inserimento nell’elenco Consentiti in VA7 | I seguenti indirizzi IP sono stati aggiunti all’elenco di indirizzi IP da aggiungere al tuo elenco consentiti per VA7 (Nord America): <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Per un elenco completo degli indirizzi IP da aggiungere all’elenco consentiti, leggi [Documento elenco consentiti indirizzo IP](../../sources/ip-address-allow-list.md). |
| Supporto per nuovi tipi di autenticazione con [!DNL Azure Event Hubs] sorgente | Ora puoi collegare il tuo [!DNL Event Hubs] origine dell’Experience Platform utilizzando [!DNL Azure Active Directory Authentication] o [!DNL Scoped Azure Active Directory Authentication]. Leggi la guida su [connessione [!DNL Event Hubs] all&#39;Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) per ulteriori informazioni. |
| Aggiornamenti a [!DNL Data Landing Zone] recupero credenziali | Ora puoi utilizzare la barra a destra nell’area di lavoro sorgenti per recuperare [!DNL Data Landing Zone] credenziali. Ora puoi anche utilizzare la barra a destra per aggiornare le credenziali. Leggi le [[!DNL Data Landing Zone] Guida all’interfaccia utente](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) per ulteriori informazioni. |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Per ulteriori informazioni sulle origini, leggere [panoramica sulle origini](../../sources/home.md).
