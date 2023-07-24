---
title: Note sulla versione di Adobe Experience Platform di settembre 2022
description: Note sulla versione di settembre 2022 per Adobe Experience Platform.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '2940'
ht-degree: 11%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 28 settembre 2022**

Nuove funzioni di Adobe Experience Platform:

- [Controllo degli accessi basato su attributi](#abac)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Registri di controllo](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio Identity](#identity-service)
- [Servizio query](#query-service)
- [Origini](#sources)

## Controllo degli accessi basato su attributi {#abac}

>[!IMPORTANT]
>
>Il controllo degli accessi basato su attributi verrà abilitato a partire da ottobre 2022. Se desideri essere uno dei primi ad adottare, contatta il tuo rappresentante Adobe.

Il controllo degli accessi basato sugli attributi è una funzionalità di Adobe Experience Platform che offre ai brand attenti alla privacy una maggiore flessibilità per gestire l’accesso degli utenti. È possibile assegnare singoli oggetti, come campi e segmenti dello schema, ai ruoli utente. Questa funzione ti consente di concedere o revocare l’accesso a singoli oggetti per specifici utenti di Platform nella tua organizzazione.

Tramite il controllo dell’accesso basato su attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti a, dati personali sensibili (SPD), informazioni personali (PII) e altri tipi di dati personalizzati in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.

| Funzione | Descrizione |
| --- | --- |
| Controllo degli accessi basato su attributi | Il controllo dell’accesso basato su attributi consente di etichettare i campi e i segmenti dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. In parallelo, gli amministratori possono utilizzare l’interfaccia di amministrazione di utenti e ruoli per definire i criteri di accesso che coprono i campi e i segmenti dello schema XDM per gestire meglio l’accesso concesso a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Per ulteriori informazioni, vedere [panoramica sul controllo degli accessi basato su attributi](../../access-control/abac/overview.md). |
| Autorizzazioni | Autorizzazioni è l’area di Experience Cloud in cui gli amministratori possono definire i ruoli utente e i criteri di accesso per gestire le autorizzazioni di accesso per funzioni e oggetti all’interno di un’applicazione di prodotto. Tramite le Autorizzazioni, puoi creare e gestire i ruoli, assegnare le autorizzazioni per le risorse desiderate per questi ruoli e creare criteri per sfruttare le etichette e definire quali ruoli utente hanno accesso a risorse Platform specifiche. Le autorizzazioni ti consentono inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico. Per ulteriori informazioni, vedere [Guida dell’interfaccia utente Autorizzazioni](../../access-control/abac/ui/browse.md). |

Per ulteriori informazioni sul controllo degli accessi basato su attributi, vedere [panoramica sul controllo degli accessi basato su attributi](../../access-control/abac/overview.md). Per una guida completa sul flusso di lavoro di controllo degli accessi basato su attributi, leggi [guida end-to-end per il controllo degli accessi basato su attributi](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

I servizi di intelligenza artificiale e machine learning consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi di utilizzo dell’esperienza del cliente. Questo consente agli analisti di marketing di impostare modelli specifici per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science.

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

| Funzione | Descrizione |
| --- | --- |
| Salva bozza di istanza | Questa nuova funzione consente agli analisti di marketing di salvare una configurazione del modello come istanza in stato di bozza e di continuare a modificarla fino a quando non viene completata prima dell’apprendimento e del punteggio. Gli scenari in cui questa funzione è utile includono, quando un utente dispone di più campi da definire nel flusso di lavoro ma non può completarlo a causa di vincoli di tempo. Un altro scenario si verifica quando una o più statistiche di set di dati vengono elaborate e non sono ancora disponibili. Leggi le [Guida utente di Attribution AI](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) per ulteriori informazioni. |
| Criteri di governance | Dopo che gli utenti si sono inviati per creare un’istanza tramite il flusso di lavoro di configurazione, il nuovo servizio di applicazione dei criteri controlla se vi sono violazioni dei criteri di utilizzo dei dati e visualizza i dettagli in un messaggio a comparsa. In questo modo le operazioni sui dati e le azioni di marketing sono conformi ai criteri di utilizzo dei dati configurati in Adobe Experience Platform. |

Per ulteriori informazioni sull&#39;Attribution AI, vedere [Panoramica di Attribution AI](../../intelligent-services/attribution-ai/overview.md). Per informazioni sui criteri di governance dei dati, consulta [panoramica dei criteri](../../data-governance/policies/overview.md).

### IA per l’analisi dei clienti

IA per l’analisi dei clienti disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su larga scala.

| Funzione | Descrizione |
| --- | --- |
| Salva bozza di istanza | Questa nuova funzione consente agli analisti di marketing di salvare una configurazione del modello come istanza in stato di bozza e di continuare a modificarla fino a quando non viene completata prima dell’apprendimento e del punteggio. Gli scenari in cui questa funzione è utile includono, quando un utente dispone di più campi da definire nel flusso di lavoro ma non può completarlo a causa di vincoli di tempo. Un altro scenario si verifica quando una o più statistiche di set di dati vengono elaborate e non sono ancora disponibili. Leggi le [Guida utente di Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) per ulteriori informazioni. |
| Criteri di governance | Dopo che gli utenti si sono inviati per creare un’istanza tramite il flusso di lavoro di configurazione, il nuovo servizio di applicazione dei criteri controlla se vi sono violazioni dei criteri di utilizzo dei dati e visualizza i dettagli in un messaggio a comparsa. In questo modo le operazioni sui dati e le azioni di marketing sono conformi ai criteri di utilizzo dei dati configurati in Adobe Experience Platform. |

Per ulteriori informazioni su Customer AI, leggi [Panoramica di Customer AI](../../intelligent-services/customer-ai/overview.md). Per informazioni sui criteri di governance dei dati, consulta [panoramica dei criteri](../../data-governance/policies/overview.md).

## Registri di audit {#audit-logs}

Experience Platform consente di controllare l’attività dell’utente per vari servizi e funzionalità. I registri di audit forniscono informazioni su chi ha fatto cosa e quando.

**Funzioni aggiornate**

| Funzione | Nome | Descrizione |
| --- | --- | --- |
| Risorse aggiunte | <ul><li>istanza Attribution AI</li><li>Istanza di Customer AI</li><li>Datastream</li></ul> | Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività. Se la funzione è abilitata, non è necessario abilitare manualmente la raccolta dei registri. |

{style="table-layout:auto"}

Per ulteriori informazioni sui diversi tipi di eventi specifici delle risorse tracciati dai registri di audit in Platform, consulta [panoramica dei registri di audit](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso i quali è possibile visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

| Funzione | Descrizione |
| --- | --- |
| Etichetta in uso | Quando viene visualizzata nella libreria dei widget, l’etichetta in uso identifica facilmente la presenza di widget esistenti nel dashboard. Questo consente di evitare facilmente la duplicazione, anche se è comunque possibile aggiungere lo stesso widget più di una volta, se lo si desidera. |
| Dashboard definiti dall&#39;utente | Le dashboard definite dall’utente consentono di velocizzare le informazioni approfondite e personalizzare le visualizzazioni creando e gestendo dashboard personalizzate. Con le dashboard definite dall’utente puoi creare, aggiungere e modificare widget personalizzati per visualizzare metriche chiave rilevanti per la tua organizzazione. Leggi le [guida alle funzioni](../../dashboards/user-defined-dashboards.md) per ulteriori informazioni. |
| Modello dati di Customer Data Platform Insights | La funzione Customer Data Platform (CDP) Insights Data Model espone i modelli di dati e le istruzioni SQL che alimentano le informazioni per vari widget di profilo, destinazione e segmentazione. Puoi personalizzare questi modelli di query SQL per creare rapporti CDP per i casi di utilizzo degli indicatori di prestazioni chiave e di marketing. Queste informazioni possono quindi essere utilizzate come widget personalizzati per le dashboard definite dall’utente. Leggi le [Guida alle funzioni del modello dati di approfondimenti CDP](../../dashboards/cdp-insights-data-model.md) per ulteriori informazioni. |
| Widget report di sovrapposizione pubblico | Questo widget è disponibile per entrambi [!UICONTROL Profili] e [!UICONTROL Segmenti] dashboard. Il rapporto fornisce un elenco ordinato di tipi di pubblico classificati in base alle percentuali di sovrapposizione più alte o più basse per il segmento scelto. Dalla sezione [!UICONTROL Profili] dashboard puoi filtrare e visualizzare la sovrapposizione dei tipi di pubblico tramite il criterio di unione da tutti i segmenti disponibili. Il [!UICONTROL Segmenti] le dashboard ti consentono di filtrare la sovrapposizione del pubblico in base a un segmento specifico.<br>Utilizza questa analisi per creare nuovi segmenti ad alte prestazioni ed evitare di inviare lo stesso pubblico a destinazioni diverse. Il rapporto consente inoltre di identificare informazioni nascoste per migliorare la segmentazione o individuare profili univoci da perseguire. Leggi le rispettive [profili](../../dashboards/guides/profiles.md#audience-overlap-report) e [segmenti](../../dashboards/guides/audiences.md#audience-overlap-report) guide per ulteriori informazioni. |

Per ulteriori informazioni su [!DNL Dashboards], consultare il [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Integrazione della navigazione a sinistra nell’interfaccia utente di Platform | Tutte le funzionalità che in precedenza erano esclusive dell’interfaccia utente di Data Collection (inclusi tag, inoltro eventi e flussi di dati) ora sono disponibili anche nella barra di navigazione a sinistra di Experience Platform, nella categoria **[!UICONTROL Raccolta dati]**. Questo elimina la necessità di passare da un’interfaccia utente all’altra quando si lavora con le funzionalità di raccolta dati in Platform. |
| Attribuzione degli utenti nei tag e nell’inoltro degli eventi | Quando l’inserzione è disponibile [!UICONTROL Proprietà] in tag e inoltro eventi, ogni proprietà elencata ora mostra quando è stata aggiornata per l’ultima volta e quale utente ha effettuato l’aggiornamento. |
| [[!DNL Snap Conversions API] estensione](https://exchange.adobe.com/apps/ec/108550) per l’inoltro di eventi | Ora puoi inviare dati a [!DNL Snapchat Conversions API] utilizzando un [inoltro eventi](../../tags/ui/event-forwarding/overview.md) estensione. Per ulteriori informazioni su come autenticare e utilizzare l’API, consulta [[!DNL Snapchat Marketing API] documentazione](https://marketingapi.snapchat.com/docs/conversion.html). |
| [[!DNL User-Agent Client Hints] in Web SDK](../../edge/fundamentals/user-agent-client-hints.md) | L’SDK per web ora supporta [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Gli hint client consentono ai proprietari di siti web di accedere a gran parte delle stesse informazioni disponibili in [!DNL User-Agent] stringa, ma in modo più rispettoso della privacy. |
| [Migrazione pagina per pagina dell’SDK web](../../edge/home.md#migrating-to-web-sdk) | Ora puoi migrare le proprietà web esistenti da altre librerie Experience Cloud, come [!DNL at.js], a Web SDK, una pagina alla volta. Questo consente un approccio graduale alla migrazione dell’SDK web, senza la necessità di eseguire la migrazione di tutte le pagine contemporaneamente. |
| [[!DNL Adobe Journey Optimizer] supporto per gli stream di dati](../../datastreams/overview.md#aep) | Il servizio Adobe Experience Platform per gli stream di dati ora supporta [!DNL Adobe Journey Optimizer]. Questa opzione consente di utilizzare i canali in entrata basati su Web e app in [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| SDK di destinazione | Destination SDK fornisce ora supporto completo ai partner e ai clienti che creano destinazioni in batch (o basate su file) prodotte o private. Per ulteriori informazioni, consulta le seguenti pagine della documentazione: <ul><li>[Panoramica di Destination SDK](../../destinations/destination-sdk/overview.md)</li><li>[Configurare una destinazione basata su file](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[Configurare le opzioni di formattazione dei file per le destinazioni basate su file](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[Verificare le destinazioni basate su file](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services fornisce una piattaforma per la progettazione di customer experience cross-channel e un ambiente per l’orchestrazione visiva delle campagne, la gestione delle interazioni in tempo reale e l’esecuzione cross-channel. [Introduzione a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Questa integrazione funziona con [Adobe Campaign versione 8.4 o successiva](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | Il [!DNL Salesforce CRM] la destinazione è stata aggiornata per supportare sia gli aggiornamenti dei contatti che quelli dei lead, oltre a miglioramenti delle prestazioni per aggiornamenti più veloci. |

{style="table-layout:auto"}

**Documentazione nuova o aggiornata**

| Documentazione | Descrizione |
| ----------- | ----------- |
| Documentazione API del servizio Flusso delle destinazioni | Il [Documentazione di riferimento dell’API Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/) è stato aggiornato per includere istruzioni su come eseguire operazioni sulle destinazioni basate su file. Le operazioni per le destinazioni di streaming verranno aggiunte in un secondo momento. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto dell’interfaccia utente per enum e valori suggeriti | Oltre alle enumerazioni che consentono la convalida dei dati, ora puoi [aggiungi o rimuovi valori suggeriti](../../xdm/ui/fields/enum.md) per campi stringa standard o personalizzati, in modo che gli utenti di Platform abbiano un elenco intuitivo di valori tra cui scegliere durante la creazione di segmenti. |

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
| Gruppo di campi | (Multiplo) | [Sono state aggiornate diverse descrizioni dei campi](https://github.com/adobe/xdm/pull/1628/files) tra i componenti del Journey Orchestration. |
| Gruppo di campi | (Multiplo) | [Sono stati aggiornati i titoli di diversi componenti di Adobe Workfront.](https://github.com/adobe/xdm/pull/1634/files) per coerenza. |
| Gruppo di campi | [[!UICONTROL Campi di classificazione AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Sono stati aggiornati gli spazi dei nomi di diversi campi in `xdm`. |
| Gruppo di campi | [[!UICONTROL Campi comuni evento passaggio Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | È stato aggiunto un nuovo campo, `isReadSegmentTriggerStartEvent`. |
| Gruppo di campi | [[!UICONTROL Previsioni meteorologiche]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | È stato modificato il `xdm:uvIndex` a un tipo intero e ha aggiunto il `xdm` spazio dei nomi in diversi campi in cui è mancante. |
| Gruppo di campi | [[!UICONTROL Informazioni sui dettagli dei contenuti multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` e `xdm:implementationDetails` sono stati rimossi dal gruppo di campi. |
| Tipo di dati | (Multiplo) | [Sono stati aggiornati diversi nomi di proprietà dei contenuti multimediali](https://github.com/adobe/xdm/pull/1626/files) su diversi tipi di dati per coerenza. |
| Tipo di dati | [[!UICONTROL Dettagli di implementazione]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Aggiunti nomi noti per flutter. |
| Tipo di dati | [[!UICONTROL Dettagli del punto di interesse]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Il tipo di dati può ora accettare un elenco di coppie chiave-valore di metadati associate al punto di interesse. |
| Tipo di dati | [[!UICONTROL Azione proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] è stato rinominato in [!UICONTROL Azione proposta]. |
| Tipo di dati | [[!UICONTROL Tipo di evento proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] è stato rinominato in [!UICONTROL Azione proposta]. |
| (Multiplo) | (Multiplo) | Le proprietà sperimentali sono state [stabilizzato su tutti i componenti B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Multiplo) | (Multiplo) | Le entità Adobe Journey Optimizer sono state [stabilizzato](https://github.com/adobe/xdm/pull/1625/files). |
| (Multiplo) | (Multiplo) | I namespace di alcuni campi in diversi componenti sperimentali sono stati [aggiornato per coerenza](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta [Panoramica del sistema XDM](../../xdm/home.md).

## Servizio Identity {#identity-service}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Questo è reso più difficile quando i dati del cliente sono frammentati tra sistemi diversi, facendo apparire ogni cliente con più &quot;identità&quot;.

Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore del cliente e del suo comportamento, collegando le identità tra dispositivi e sistemi diversi e consentendo di fornire esperienze digitali personali e di impatto in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’eliminazione di set di dati | Identity Service ora supporta l’eliminazione dei set di dati quando si richiede tramite il [API Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/), interfaccia utente o igiene dei dati. Leggi la guida su [eliminazione di set di dati nell’interfaccia utente](../../catalog/datasets/user-guide.md#delete-a-dataset) per ulteriori informazioni. |

Per ulteriori informazioni sul servizio Identity, consulta [Panoramica del servizio Identity](../../identity-service/home.md).

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati da [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’acquisizione in Real-time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| API di sottoscrizione avvisi | Adobe Experience Platform Query Service consente di ricevere avvisi sia per le query ad hoc che per quelle pianificate. Gli avvisi possono essere ricevuti tramite e-mail, nell’interfaccia di Platform o in entrambe le modalità. Attualmente, gli avvisi di query possono essere abbonati solo utilizzando [API servizio query](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Esempi di set di dati | Gli esempi di set di dati di Query Service consentono di eseguire query esplorative sui big data con tempi di elaborazione notevolmente ridotti a scapito della precisione delle query. Consulta la [guida agli esempi di set di dati](../../query-service/essential-concepts/dataset-samples.md) per ulteriori informazioni. |

Per ulteriori informazioni su [!DNL Query Service], consultare il [[!DNL Query Service] panoramica](../../query-service/home.md).

Consulta la [documentazione degli avvisi di query](../../query-service/api/alert-subscriptions.md) per ulteriori informazioni.

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Audience Manager dell’impatto della popolazione del segmento sul profilo cliente in tempo reale | L’acquisizione di popolazioni di segmenti Audience Manager di dimensioni considerevoli ha un impatto diretto sul conteggio totale dei profili quando invii un segmento di Audience Manager a Platform per la prima volta utilizzando l’origine di Audience Manager. Ciò significa che la selezione di tutti i segmenti può potenzialmente causare un conteggio dei profili superiore al limite di utilizzo della licenza consentito. Per ulteriori informazioni, leggere [Panoramica origine Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Per informazioni sull’utilizzo della licenza, consulta la documentazione su [utilizzo del dashboard utilizzo licenze](../../dashboards/guides/license-usage.md). |
| Supporto per Adobe Campaign Managed Cloud Service | Utilizza l’origine del Cloud Service gestito di Adobe Campaign per dare Experience Platform ai dati dei registri di consegna e tracciamento di Adobe Campaign v8.4. Leggi la guida su [creazione di una connessione sorgente del Cloud Service gestito di Adobe Campaign nell’interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/campaign.md) per ulteriori informazioni. |
| Supporto API per l’acquisizione su richiesta per le origini batch | Utilizza l’acquisizione su richiesta per creare esecuzioni di flussi ad hoc per un dato flusso di dati con [!DNL Flow Service] API. Le esecuzioni del flusso create devono essere impostate su acquisizione una tantum. Per ulteriori informazioni, consulta la guida su [creazione di un’esecuzione del flusso per l’acquisizione on-demand tramite l’API](../../sources/tutorials/api/on-demand-ingestion.md) per ulteriori informazioni. |
| Supporto API per il nuovo tentativo di esecuzione del flusso di dati non riuscito per le origini batch | Utilizza il `re-trigger` operazione per ritentare il flusso di dati non riuscito tramite l’API. Leggi la guida su [nuovo tentativo di esecuzione del flusso di dati non riuscito tramite l’API](../../sources/tutorials/api/retry-flows.md) per ulteriori informazioni. |
| Supporto API per filtrare i dati a livello di riga per [!DNL Google BigQuery] e [!DNL Snowflake] sorgenti | Utilizzare gli operatori logici e di confronto per filtrare i dati a livello di riga per [!DNL Google BigQuery] e [!DNL Snowflake] origini. Leggi la guida su [filtrare i dati per un’origine utilizzando l’API](../../sources/tutorials/api/filter.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle origini, leggi la [panoramica sulle origini](../../sources/home.md).
