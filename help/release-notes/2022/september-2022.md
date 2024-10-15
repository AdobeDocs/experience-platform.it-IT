---
title: Note sulla versione di Adobe Experience Platform di settembre 2022
description: Note sulla versione di Adobe Experience Platform di settembre 2022.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '2762'
ht-degree: 26%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 28 settembre 2022**

Nuove funzioni di Adobe Experience Platform:

- [Controllo degli accessi basato su attributi](#abac)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Registri di audit](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Query Service](#query-service)
- [Origini](#sources)

## Controllo degli accessi basato su attributi {#abac}

>[!IMPORTANT]
>
>Il controllo degli accessi basato su attributi verrà abilitato a partire da ottobre 2022. Se desideri essere uno dei primi ad adottare, contatta il rappresentante del tuo Adobe.

Il controllo degli accessi basato sugli attributi è una funzionalità di Adobe Experience Platform che offre ai brand attenti alla privacy una maggiore flessibilità per gestire l’accesso degli utenti. È possibile assegnare singoli oggetti, come campi e segmenti dello schema, ai ruoli utente. Questa funzione consente di concedere o revocare l’accesso a singoli oggetti per specifici utenti di Platform nell’organizzazione.

Tramite il controllo dell’accesso basato su attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti a dati personali sensibili (SPD), informazioni personali (PII) e altri tipi di dati personalizzati in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.

| Funzione | Descrizione |
| --- | --- |
| Controllo degli accessi basato su attributi | Il controllo dell’accesso basato su attributi consente di etichettare i campi e i segmenti dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. In parallelo, gli amministratori possono utilizzare l’interfaccia di amministrazione di utenti e ruoli per definire i criteri di accesso che coprono i campi e i segmenti dello schema XDM per gestire meglio l’accesso concesso a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Per ulteriori informazioni, vedere la [panoramica sul controllo degli accessi basato su attributi](../../access-control/abac/overview.md). |
| Autorizzazioni | Autorizzazioni è l’area di Experience Cloud in cui gli amministratori possono definire i ruoli utente e i criteri di accesso per gestire le autorizzazioni di accesso per funzioni e oggetti all’interno di un’applicazione di prodotto. Tramite le Autorizzazioni, puoi creare e gestire i ruoli, assegnare le autorizzazioni per le risorse desiderate per questi ruoli e creare criteri per sfruttare le etichette e definire quali ruoli utente hanno accesso a risorse Platform specifiche. Le autorizzazioni ti consentono inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico. Per ulteriori informazioni, vedere la [Guida dell&#39;interfaccia utente delle autorizzazioni](../../access-control/abac/ui/browse.md). |

Per ulteriori informazioni sul controllo degli accessi basato su attributi, consulta la [panoramica sul controllo degli accessi basato su attributi](../../access-control/abac/overview.md). Per una guida completa sul flusso di lavoro del controllo degli accessi basato su attributi, leggi la [guida completa per il controllo degli accessi basato su attributi](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

I servizi di intelligenza artificiale e machine learning consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi di utilizzo dell’esperienza del cliente. Questo consente agli analisti di marketing di impostare modelli specifici per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science.

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzata dai marketer per quantificare l’impatto di ogni punto di contatto di marketing lungo i percorsi della clientela.

| Funzione | Descrizione |
| --- | --- |
| Salva bozza di istanza | Questa nuova funzione consente agli analisti di marketing di salvare una configurazione del modello come istanza in stato di bozza e di continuare a modificarla fino a quando non viene completata prima dell’apprendimento e del punteggio. Gli scenari in cui questa funzione è utile includono, quando un utente dispone di più campi da definire nel flusso di lavoro ma non può completarlo a causa di vincoli di tempo. Un altro scenario si verifica quando una o più statistiche di set di dati vengono elaborate e non sono ancora disponibili. Per ulteriori informazioni, consulta la [guida utente di Attribution AI](../../intelligent-services/attribution-ai/user-guide.md#governance-policies). |
| Criteri di governance | Dopo che gli utenti si sono inviati per creare un’istanza tramite il flusso di lavoro di configurazione, il nuovo servizio di applicazione dei criteri controlla se vi sono violazioni dei criteri di utilizzo dei dati e visualizza i dettagli in un messaggio a comparsa. In questo modo le operazioni sui dati e le azioni di marketing sono conformi ai criteri di utilizzo dei dati configurati in Adobe Experience Platform. |

Per ulteriori informazioni sull&#39;Attribution AI, vedere [Panoramica sull&#39;Attribution AI](../../intelligent-services/attribution-ai/overview.md). Per informazioni sui criteri di governance dei dati, leggere la [panoramica dei criteri](../../data-governance/policies/overview.md).

### IA per l’analisi dei clienti

IA per l’analisi dei clienti disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su larga scala.

| Funzione | Descrizione |
| --- | --- |
| Salva bozza di istanza | Questa nuova funzione consente agli analisti di marketing di salvare una configurazione del modello come istanza in stato di bozza e di continuare a modificarla fino a quando non viene completata prima dell’apprendimento e del punteggio. Gli scenari in cui questa funzione è utile includono, quando un utente dispone di più campi da definire nel flusso di lavoro ma non può completarlo a causa di vincoli di tempo. Un altro scenario si verifica quando una o più statistiche di set di dati vengono elaborate e non sono ancora disponibili. Per ulteriori informazioni, consulta la [guida utente di Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies). |
| Criteri di governance | Dopo che gli utenti si sono inviati per creare un’istanza tramite il flusso di lavoro di configurazione, il nuovo servizio di applicazione dei criteri controlla se vi sono violazioni dei criteri di utilizzo dei dati e visualizza i dettagli in un messaggio a comparsa. In questo modo le operazioni sui dati e le azioni di marketing sono conformi ai criteri di utilizzo dei dati configurati in Adobe Experience Platform. |

Per ulteriori informazioni su Customer AI, consulta la [Panoramica di Customer AI](../../intelligent-services/customer-ai/overview.md). Per informazioni sui criteri di governance dei dati, leggere la [panoramica dei criteri](../../data-governance/policies/overview.md).

## Registri di audit {#audit-logs}

Experience Platform consente di controllare l’attività dell’utente per vari servizi e funzionalità. I registri di audit forniscono informazioni su chi ha fatto cosa e quando.

**Funzioni aggiornate**

| Funzione | Nome | Descrizione |
| --- | --- | --- |
| Risorse aggiunte | <ul><li>istanza Attribution AI</li><li>Istanza di Customer AI</li><li>Stream di dati</li></ul> | Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività. Se la funzione è abilitata, non è necessario abilitare manualmente la raccolta dei registri. |

{style="table-layout:auto"}

Per ulteriori informazioni sui diversi tipi di eventi specifici delle risorse tracciati dai registri di controllo in Platform, consulta la [panoramica dei registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

| Funzione | Descrizione |
| --- | --- |
| Etichetta in uso | Quando viene visualizzata nella libreria dei widget, l’etichetta in uso identifica facilmente la presenza di widget esistenti nel dashboard. Questo consente di evitare facilmente la duplicazione, anche se è comunque possibile aggiungere lo stesso widget più di una volta, se lo si desidera. |
| Dashboard definite dall’utente | Le dashboard definite dall’utente consentono di velocizzare le informazioni approfondite e personalizzare le visualizzazioni creando e gestendo dashboard personalizzate. Con le dashboard definite dall’utente puoi creare, aggiungere e modificare widget personalizzati per visualizzare metriche chiave rilevanti per la tua organizzazione. Per ulteriori informazioni, consulta la [guida alle funzionalità](../../dashboards/standard-dashboards.md). |
| Modello dati di Customer Data Platform Insights | La funzione Customer Data Platform (CDP) Insights Data Model espone i modelli di dati e le istruzioni SQL che alimentano le informazioni per vari widget di profilo, destinazione e segmentazione. Puoi personalizzare questi modelli di query SQL per creare rapporti CDP per i casi di utilizzo degli indicatori di prestazioni chiave e di marketing. Queste informazioni possono quindi essere utilizzate come widget personalizzati per le dashboard definite dall’utente. Per ulteriori informazioni, consulta la [guida alle funzioni del modello dati per approfondimenti CDP](../../dashboards/data-models/cdp-insights-data-model-b2c.md). |
| Widget report di sovrapposizione pubblico | Questo widget è disponibile per entrambi i dashboard [!UICONTROL Profili] e [!UICONTROL Segmenti]. Il rapporto fornisce un elenco ordinato di tipi di pubblico classificati in base alle percentuali di sovrapposizione più alte o più basse per il segmento scelto. Dal dashboard [!UICONTROL Profili] puoi filtrare e visualizzare la sovrapposizione dei tipi di pubblico tramite il criterio di unione da tutti i segmenti disponibili. I dashboard [!UICONTROL Segmenti] ti consentono di filtrare la sovrapposizione del pubblico per un segmento specifico.<br>Utilizza questa analisi per creare nuovi segmenti ad alte prestazioni ed evitare di inviare lo stesso pubblico a destinazioni diverse. Il rapporto consente inoltre di identificare informazioni nascoste per migliorare la segmentazione o individuare profili univoci da perseguire. Per ulteriori informazioni, leggi le rispettive guide dei widget [profili](../../dashboards/guides/profiles.md#audience-overlap-report) e [segmenti](../../dashboards/guides/audiences.md#audience-overlap-report). |

Per ulteriori informazioni su [!DNL Dashboards], vedere la [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Integrazione della navigazione a sinistra nell’interfaccia utente di Platform | Tutte le funzionalità che in precedenza erano esclusive dell&#39;interfaccia utente di Data Collection (inclusi tag, inoltro eventi e flussi di dati) sono ora disponibili anche nella barra di navigazione a sinistra di Experience Platform, nella categoria **[!UICONTROL Raccolta dati]**. Questo elimina la necessità di passare da un’interfaccia utente all’altra quando si utilizzano le funzionalità di raccolta dati in Platform. |
| Attribuzione degli utenti nei tag e nell’inoltro degli eventi | Quando si elencano le [!UICONTROL proprietà] disponibili nei tag e nell&#39;inoltro degli eventi, ogni proprietà elencata ora viene visualizzata quando è stato eseguito l&#39;ultimo aggiornamento e quale utente ha effettuato l&#39;aggiornamento. |
| [[!DNL Snap Conversions API] estensione](https://exchange.adobe.com/apps/ec/108550) per l&#39;inoltro degli eventi | È ora possibile inviare dati a [!DNL Snapchat Conversions API] utilizzando un&#39;estensione [inoltro eventi](../../tags/ui/event-forwarding/overview.md). Per ulteriori informazioni su come autenticarsi e utilizzare l’API, consulta la [[!DNL Snapchat Marketing API] documentazione](https://marketingapi.snapchat.com/docs/conversion.html?lang=it). |
| [User-Agent Client Hints in Web SDK](/help/web-sdk/use-cases/client-hints.md) | Web SDK ora supporta [User-Agent Client Hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Gli hint client consentono ai proprietari del sito Web di accedere a gran parte delle stesse informazioni disponibili nella stringa [!DNL User-Agent], ma in modo più sicuro per la privacy. |
| [Migrazione dell&#39;SDK Web pagina per pagina](../../web-sdk/home.md#migrating-to-web-sdk) | È ora possibile migrare le proprietà Web esistenti da altre librerie Experience Cloud, ad esempio [!DNL at.js], a Web SDK, una pagina alla volta. Questo consente un approccio graduale alla migrazione dell’SDK web, senza la necessità di eseguire la migrazione di tutte le pagine contemporaneamente. |
| [[!DNL Adobe Journey Optimizer] supporto per gli stream di dati](../../datastreams/overview.md#aep) | Il servizio Adobe Experience Platform per gli stream di dati ora supporta [!DNL Adobe Journey Optimizer]. Questa opzione consente di utilizzare i canali in entrata basati su Web e app in [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

Per ulteriori informazioni sulla raccolta dati in Platform, consulta la [panoramica sulla raccolta dati](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| Destination SDK | Destination SDK fornisce ora supporto completo ai partner e ai clienti che creano destinazioni in batch (o basate su file) prodotte o private. Per ulteriori informazioni, consulta le seguenti pagine della documentazione: <ul><li>[Destination SDK panoramica](../../destinations/destination-sdk/overview.md)</li><li>[Configurare una destinazione basata su file](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[Configurare le opzioni di formattazione per le destinazioni basate su file](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[Verifica le destinazioni basate su file](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services fornisce una piattaforma per la progettazione di customer experience cross-channel e un ambiente per l’orchestrazione visiva delle campagne, la gestione delle interazioni in tempo reale e l’esecuzione cross-channel. [Introduzione a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Questa integrazione funziona con [Adobe Campaign versione 8.4 o successiva](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | La destinazione [!DNL Salesforce CRM] è stata aggiornata per supportare gli aggiornamenti dei contatti e dei lead, nonché miglioramenti delle prestazioni per aggiornamenti più veloci. |

{style="table-layout:auto"}

**Documentazione nuova o aggiornata**

| Documentazione | Descrizione |
| ----------- | ----------- |
| Documentazione API del servizio Flusso delle destinazioni | La documentazione di riferimento dell&#39;API [Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/) è stata aggiornata per includere istruzioni su come eseguire operazioni sulle destinazioni basate su file. Le operazioni per le destinazioni di streaming verranno aggiunte in un secondo momento. |

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto dell’interfaccia utente per enum e valori suggeriti | Oltre alle enumerazioni che abilitano la convalida dei dati, ora è possibile [aggiungere o rimuovere i valori suggeriti](../../xdm/ui/fields/enum.md) per i campi stringa standard o personalizzati, in modo che gli utenti di Platform abbiano un elenco intuitivo di valori da selezionare durante la creazione di segmenti. |

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Campi di classificazione AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Proprietà di un elemento specifico interagito con cui è stato attivato l’evento proposition. |
| Gruppo di campi | [[!UICONTROL Dettagli dell’interazione di Media Analytics]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Tiene traccia delle interazioni multimediali nel tempo. |
| Gruppo di campi | [[!UICONTROL Informazioni sui dettagli dei contenuti multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Tiene traccia delle informazioni sui dettagli dei contenuti multimediali. |
| Gruppo di campi | [[!UICONTROL Adobe CJM ExperienceEvent - Superfici]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Descrive le superfici per gli eventi esperienza in Adobe Journey Optimizer. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Comportamento | [[!UICONTROL Serie temporali]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Valori aggiunti per `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Valori rimossi per `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Gruppo di campi | (Multiplo) | [Sono state aggiornate diverse descrizioni dei campi](https://github.com/adobe/xdm/pull/1628/files) in tutti i componenti del Journey Orchestration. |
| Gruppo di campi | (Multiplo) | [Sono stati aggiornati i titoli di diversi componenti di Adobe Workfront](https://github.com/adobe/xdm/pull/1634/files) per coerenza. |
| Gruppo di campi | [[!UICONTROL Campi di classificazione AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Gli spazi dei nomi di diversi campi sono stati aggiornati a `xdm`. |
| Gruppo di campi | [[!UICONTROL Campi comuni evento passaggio Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | È stato aggiunto un nuovo campo, `isReadSegmentTriggerStartEvent`. |
| Gruppo di campi | [[!UICONTROL Condizioni meteorologiche previste]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Il campo `xdm:uvIndex` è stato modificato in un tipo intero e lo spazio dei nomi `xdm` è stato aggiunto a diversi campi in cui mancava. |
| Gruppo di campi | [[!UICONTROL Informazioni sui dettagli dei contenuti multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` e `xdm:implementationDetails` sono stati rimossi dal gruppo di campi. |
| Tipo di dati | (Multiplo) | [Sono stati aggiornati diversi nomi di proprietà multimediali](https://github.com/adobe/xdm/pull/1626/files) in diversi tipi di dati per coerenza. |
| Tipo di dati | [[!UICONTROL Dettagli implementazione]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Aggiunti nomi noti per flutter. |
| Tipo di dati | [[!UICONTROL Dettagli punto di interesse]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Il tipo di dati può ora accettare un elenco di coppie chiave-valore di metadati associate al punto di interesse. |
| Tipo di dati | [[!UICONTROL Azione proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] è stato rinominato in [!UICONTROL Azione proposta]. |
| Tipo di dati | [[!UICONTROL Tipo di evento proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] è stato rinominato in [!UICONTROL Azione proposta]. |
| (Multiplo) | (Multiplo) | Le proprietà sperimentali sono state [stabilizzate in tutti i componenti B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Multiplo) | (Multiplo) | Entità Adobe Journey Optimizer [stabilizzate](https://github.com/adobe/xdm/pull/1625/files). |
| (Multiplo) | (Multiplo) | Gli spazi dei nomi di alcuni campi in diversi componenti sperimentali sono stati [aggiornati per coerenza](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [panoramica sul sistema XDM](../../xdm/home.md).

## Identity Service {#identity-service}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Questo è reso più difficile quando i dati del cliente sono frammentati tra sistemi diversi, facendo apparire ogni cliente con più &quot;identità&quot;.

Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore del cliente e del suo comportamento, collegando le identità tra dispositivi e sistemi diversi e consentendo di fornire esperienze digitali personali e di impatto in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’eliminazione di set di dati | Identity Service ora supporta l&#39;eliminazione dei set di dati quando viene richiesto tramite l&#39;API [Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/), l&#39;interfaccia utente o l&#39;igiene dei dati. Per ulteriori informazioni, consulta la guida sull&#39;eliminazione di [set di dati nell&#39;interfaccia utente](../../catalog/datasets/user-guide.md#delete-a-dataset). |

Per ulteriori informazioni su Identity Service, consulta la [Panoramica di Identity Service](../../identity-service/home.md).

## Query Service {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire nel profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| API di sottoscrizione avvisi | Adobe Experience Platform Query Service consente di ricevere avvisi sia per le query ad hoc che per quelle pianificate. Gli avvisi possono essere ricevuti tramite e-mail, nell’interfaccia di Platform o in entrambe le modalità. Attualmente, gli avvisi di query possono essere sottoscritti solo utilizzando l&#39;API [Query Service](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Esempi di set di dati | Gli esempi di set di dati di Query Service consentono di eseguire query esplorative sui big data con tempi di elaborazione notevolmente ridotti a scapito della precisione delle query. Per ulteriori informazioni, consulta la [guida sugli esempi di set di dati](../../query-service/key-concepts/dataset-samples.md). |

Per ulteriori informazioni su [!DNL Query Service], vedere la [[!DNL Query Service] panoramica](../../query-service/home.md).

Per ulteriori informazioni, consulta la [documentazione sugli avvisi per le query](../../query-service/api/alert-subscriptions.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Audience Manager dell’impatto della popolazione del segmento sul profilo cliente in tempo reale | L’acquisizione di popolazioni di segmenti Audience Manager di dimensioni considerevoli ha un impatto diretto sul conteggio totale dei profili quando invii un segmento di Audience Manager a Platform per la prima volta utilizzando l’origine di Audience Manager. Ciò significa che la selezione di tutti i segmenti può potenzialmente causare un conteggio dei profili superiore al limite di utilizzo della licenza consentito. Per ulteriori informazioni, leggere l&#39;[Audience Manager di panoramica dell&#39;origine](../../sources/connectors/adobe-applications/audience-manager.md). Per informazioni sull&#39;utilizzo delle licenze, leggere la documentazione su [utilizzando il dashboard utilizzo licenze](../../dashboards/guides/license-usage.md). |
| Supporto per Adobe Campaign Managed Cloud Service | Utilizza l’origine del Cloud Service gestito di Adobe Campaign per dare Experience Platform ai dati dei registri di consegna e tracciamento di Adobe Campaign v8.4. Per ulteriori informazioni, leggere la guida sulla [creazione di una connessione di origine di Adobe Campaign Managed Cloud Service nell&#39;interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/campaign.md). |
| Supporto API per l’acquisizione su richiesta per le origini batch | Utilizza l&#39;acquisizione su richiesta per creare esecuzioni di flussi ad hoc per un dato flusso di dati con l&#39;API [!DNL Flow Service]. Le esecuzioni del flusso create devono essere impostate su acquisizione una tantum. Per ulteriori informazioni, leggere la guida in [creazione di un&#39;esecuzione del flusso per l&#39;acquisizione su richiesta tramite l&#39;API](../../sources/tutorials/api/on-demand-ingestion.md). |
| Supporto API per il nuovo tentativo di esecuzione del flusso di dati non riuscito per le origini batch | Utilizzare l&#39;operazione `re-trigger` per ritentare il flusso di dati non riuscito tramite l&#39;API. Per ulteriori informazioni, leggere la guida di [nuovo tentativo di esecuzione del flusso di dati non riuscito utilizzando l&#39;API](../../sources/tutorials/api/retry-flows.md). |
| Supporto API per il filtraggio dei dati a livello di riga per le origini [!DNL Google BigQuery] e [!DNL Snowflake] | Utilizzare gli operatori logici e di confronto per filtrare i dati a livello di riga per le origini [!DNL Google BigQuery] e [!DNL Snowflake]. Per ulteriori informazioni, consulta la guida su come [filtrare i dati per un’origine utilizzando l’API](../../sources/tutorials/api/filter.md). |

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sources/home.md).
