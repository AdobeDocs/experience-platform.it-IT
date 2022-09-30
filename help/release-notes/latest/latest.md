---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: 45281721c6fb26c303bb820fa39f5c6ed71b55f9
workflow-type: tm+mt
source-wordcount: '3064'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 28 settembre 2022**

Nuove funzioni in Adobe Experience Platform:

- [Controllo dell’accesso basato su attributi](#abac)
- [Igiene dei dati](#data-hygiene)

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

## Controllo dell’accesso basato su attributi {#abac}

>[!IMPORTANT]
>
>Il controllo degli accessi basato su attributi verrà attivato a partire da ottobre 2022. Se desideri essere un utente in anticipo, contatta il tuo rappresentante Adobe.

Il controllo dell&#39;accesso basato su attributi è una funzionalità di Adobe Experience Platform che offre ai marchi consapevoli della privacy una maggiore flessibilità per gestire l&#39;accesso degli utenti. I singoli oggetti, ad esempio i campi e i segmenti dello schema, possono essere assegnati ai ruoli utente. Questa funzione ti consente di concedere o revocare l’accesso a singoli oggetti per utenti Platform specifici della tua organizzazione.

Grazie al controllo degli accessi basato sugli attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti a dati personali sensibili (SPD), informazioni personali identificabili (PII) e altri tipi personalizzati di dati in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici corrispondenti a tali campi.

| Funzione | Descrizione |
| --- | --- |
| Controllo dell’accesso basato su attributi | Il controllo dell’accesso basato su attributi consente di etichettare i campi e i segmenti dello schema Experience Data Model (XDM) con etichette che definiscono ambiti di utilizzo organizzativi o dati. In parallelo, gli amministratori possono utilizzare l’interfaccia utente e l’interfaccia di amministrazione dei ruoli per definire i criteri di accesso che coprono i campi e i segmenti dello schema XDM per gestire meglio l’accesso dato a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Per ulteriori informazioni, consulta la sezione [panoramica sul controllo dell&#39;accesso basato sugli attributi](../../access-control/abac/overview.md). |
| Autorizzazioni | Le autorizzazioni sono l’area di Experience Cloud in cui gli amministratori possono definire ruoli utente e criteri di accesso per gestire le autorizzazioni di accesso per funzioni e oggetti all’interno di un’applicazione di prodotto. Tramite Autorizzazioni puoi creare e gestire ruoli, assegnare le autorizzazioni di risorse desiderate per questi ruoli e creare criteri per sfruttare le etichette e definire quali ruoli utente hanno accesso a risorse specifiche di Platform. Le autorizzazioni ti consentono inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico. Per ulteriori informazioni, consulta la sezione [Guida all’interfaccia utente per le autorizzazioni](../../access-control/abac/ui/browse.md). |

Per ulteriori informazioni sul controllo degli accessi basato su attributi, consulta la sezione [panoramica sul controllo dell&#39;accesso basato sugli attributi](../../access-control/abac/overview.md). Per una guida completa sul flusso di lavoro del controllo degli accessi basato sugli attributi, leggi la sezione [guida end-to-end per il controllo degli accessi basato su attributi](../../access-control/abac/end-to-end-guide.md).

## Igiene dei dati {#data-hygiene}

Adobe Experience Platform fornisce un solido set di strumenti per gestire operazioni complesse e di grandi dimensioni sui dati al fine di orchestrare le esperienze dei consumatori. Man mano che i dati vengono acquisiti nel sistema nel tempo, diventa sempre più importante gestire gli archivi di dati in modo che i dati vengano utilizzati come previsto, vengono aggiornati quando è necessario correggere i dati errati e vengono eliminati quando i criteri organizzativi lo ritengono necessario.

Le funzionalità di igiene dei dati di Adobe Experience Platform consentono di pulire i dati pianificando la scadenza automatica dei set di dati e l’eliminazione programmatica dei dati dei consumatori in base all’identità.

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati sono disponibili solo per le organizzazioni che hanno acquistato Adobe Healthcare Shield.

Per informazioni sull’igiene dei dati, consulta la seguente documentazione:

- [Panoramica sull&#39;igiene dei dati](../../hygiene/home.md): Scopri le nozioni di base sulle funzionalità di igiene dei dati di Platform.
- [[!UICONTROL Igiene dei dati] Guida all’interfaccia utente](../../hygiene/ui/overview.md): Scopri come pianificare le scadenze dei set di dati e le richieste di cancellazione del consumatore all’interno dell’interfaccia utente di Platform.
- [Guida all’API per l’igiene dei dati](../../hygiene/api/overview.md): Anche tutte le attività di igiene dei dati che puoi eseguire nell’interfaccia utente possono essere eseguite a livello di programmazione

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

I servizi AI/ML consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi d’uso della customer experience. Questo consente agli analisti di marketing di impostare modelli specifici per le esigenze aziendali utilizzando configurazioni a livello di business senza la necessità di disporre di competenze scientifiche in materia di dati.

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

| Funzione | Descrizione |
| --- | --- |
| Salva istanza bozza | Questa nuova funzione consente agli analisti di marketing di salvare una configurazione del modello come bozza di istanza e di continuare a modificarla fino al completamento prima della formazione e del punteggio. Gli scenari in cui questa funzione è utile includono quando un utente ha più campi da definire nel flusso di lavoro ma non può completarlo a causa di vincoli di tempo. Un altro scenario è quello in cui una o più statistiche del set di dati vengono elaborate e non sono ancora disponibili. Leggi la sezione [Guida utente di Attribution AI](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) per saperne di più. |
| Politiche di governance | Dopo che gli utenti si inviano per creare un&#39;istanza tramite il flusso di lavoro di configurazione, il nuovo servizio di imposizione dei criteri verifica se sono presenti violazioni dei criteri relativi all&#39;utilizzo dei dati e visualizza i dettagli in un pover. Garantisce che le operazioni di dati e le azioni di marketing siano conformi ai criteri di utilizzo dei dati configurati su Adobe Experience Platform. |

Per ulteriori informazioni sulle Attribution AI, consulta [Panoramica di Attribution AI](../../intelligent-services/attribution-ai/overview.md). Per informazioni sui criteri di governance dei dati, consulta la sezione [panoramica dei criteri](../../data-governance/policies/overview.md).

### Customer AI

Customer AI disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su scala.

| Funzione | Descrizione |
| --- | --- |
| Salva istanza bozza | Questa nuova funzione consente agli analisti di marketing di salvare una configurazione del modello come bozza di istanza e di continuare a modificarla fino al completamento prima della formazione e del punteggio. Gli scenari in cui questa funzione è utile includono quando un utente ha più campi da definire nel flusso di lavoro ma non può completarlo a causa di vincoli di tempo. Un altro scenario è quello in cui una o più statistiche del set di dati vengono elaborate e non sono ancora disponibili. Leggi la sezione [Guida utente di Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) per saperne di più. |
| Politiche di governance | Dopo che gli utenti si inviano per creare un&#39;istanza tramite il flusso di lavoro di configurazione, il nuovo servizio di imposizione dei criteri verifica se sono presenti violazioni dei criteri relativi all&#39;utilizzo dei dati e visualizza i dettagli in un pover. Garantisce che le operazioni di dati e le azioni di marketing siano conformi ai criteri di utilizzo dei dati configurati su Adobe Experience Platform. |

Per ulteriori informazioni su Customer AI, consulta la sezione [Panoramica di Customer AI](../../intelligent-services/customer-ai/overview.md). Per informazioni sui criteri di governance dei dati, consulta la sezione [panoramica dei criteri](../../data-governance/policies/overview.md).

## Registri di audit {#audit-logs}

L’Experience Platform ti consente di controllare l’attività dell’utente per vari servizi e funzionalità. I registri di controllo forniscono informazioni su chi ha fatto cosa e quando.

**Funzioni aggiornate**

| Funzione | Nome | Descrizione |
| --- | --- | --- |
| Risorse aggiunte | <ul><li>Attribution AI</li><li>Istanza di Customer AI</li><li>Datastream</li></ul> | Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività. Se la funzione è abilitata, non è necessario abilitare manualmente la raccolta dei registri. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sui diversi tipi di evento specifici per le risorse tracciati dai registri di controllo in Platform, consulta la sezione [panoramica dei registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform offre diverse dashboard attraverso le quali puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisiti durante le istantanee giornaliere.

| Funzione | Descrizione |
| --- | --- |
| Etichetta in uso | Quando viene visualizzata nella libreria dei widget, l’etichetta in-use identifica facilmente la presenza di widget esistenti nel dashboard. Questo rende facile evitare la duplicazione, anche se è ancora possibile aggiungere lo stesso widget più di una volta che si desidera. |
| Dashboard definiti dall&#39;utente | Le dashboard definite dall’utente consentono di accelerare le informazioni e personalizzare le visualizzazioni mediante la creazione e la gestione di dashboard personalizzati. Con le dashboard definite dall’utente è possibile creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave pertinenti per la propria organizzazione. Leggi la sezione [guida alle funzioni](../../dashboards/user-defined-dashboards.md) per saperne di più. |
| Modello dati di Approfondimenti piattaforma dati cliente | La funzione Customer Data Platform (CDP) Insights Data Model espone i modelli di dati e le istruzioni SQL che consentono di acquisire informazioni per vari widget di profilo, destinazione e segmentazione. Puoi personalizzare questi modelli di query SQL per creare rapporti CDP per i tuoi casi d’uso di marketing e indicatori di prestazioni chiave. Queste informazioni possono quindi essere utilizzate come widget personalizzati per le dashboard definite dall’utente. Leggi la sezione [Guida alle funzioni di CDP Insights Data Model](../../dashboards/cdp-insights-data-model.md) per saperne di più. |
| Widget per report sulla sovrapposizione del pubblico | Questo widget è disponibile per entrambi [!UICONTROL Profili] e [!UICONTROL Segmenti] dashboard. Il rapporto fornisce un elenco ordinato di tipi di pubblico classificati in base alle percentuali di sovrapposizione più alte o più basse per il segmento scelto. Da [!UICONTROL Profili] dashboard ti consente di filtrare e visualizzare la sovrapposizione del pubblico unendo i criteri di tutti i segmenti disponibili. La [!UICONTROL Segmenti] le dashboard ti consentono di filtrare la sovrapposizione del pubblico di un segmento specifico.<br>Utilizza questa analisi per creare nuovi segmenti ad alte prestazioni ed evita di inviare lo stesso pubblico a destinazioni diverse. Il rapporto aiuta inoltre a identificare informazioni nascoste per migliorare la segmentazione o individuare profili univoci da perseguire. Leggi i rispettivi [profiles](../../dashboards/guides/profiles.md#audience-overlap-report) e [segmenti](../../dashboards/guides/segments.md#audience-overlap-report) guide per ulteriori informazioni. |

Per ulteriori informazioni su [!DNL Dashboards], vedi [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network dove possono essere arricchiti, trasformati e distribuiti su destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Integrazione della navigazione a sinistra nell’interfaccia utente di Platform | Tutte le funzionalità precedentemente esclusive dell’interfaccia utente di raccolta dati (compresi tag, inoltro eventi e datastreams) sono ora disponibili anche nella navigazione a sinistra in Experience Platform, nella categoria **[!UICONTROL Raccolta dati]**. Questo elimina la necessità di passare da un’interfaccia utente all’altra quando si lavora con le funzionalità di raccolta dati in Platform. |
| Attribuzione utente in tag e inoltro evento | Quando l’elenco è disponibile [!UICONTROL Proprietà] in tag e inoltro eventi, ogni proprietà elencata ora mostra quando è stata aggiornata per l&#39;ultima volta e quale utente ha effettuato l&#39;aggiornamento. |
| [[!DNL User-Agent Client Hints] in SDK per web](../../edge/fundamentals/user-agent-client-hints.md) | L&#39;SDK per web supporta ora [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). I suggerimenti client consentono ai proprietari del sito web di accedere a molte delle stesse informazioni disponibili nel [!DNL User-Agent] Stringa, ma in un modo più rispettoso della privacy. |
| [Migrazione pagina per pagina dell’SDK per web](../../edge/home.md#migrating-to-web-sdk) | Ora puoi eseguire la migrazione delle proprietà web esistenti da altre librerie di Experienci Cloud, come [!DNL at.js], all’SDK per web, una pagina alla volta. Questo consente un approccio graduale alla migrazione dell’SDK per web, senza la necessità di eseguire la migrazione di tutte le pagine contemporaneamente. |

{style=&quot;table-layout:auto&quot;}

<!-- | [[!DNL Adobe Journey Optimizer] support for datastreams](../../edge/datastreams/overview.md#aep)| The Adobe Experience Platform service for datastreams now supports [!DNL Adobe Journey Optimizer]. This option allows you to use web and app-based inbound channels in [!DNL Adobe Journey Optimizer].|
-->

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| SDK di destinazione | Destination SDK ora offre supporto completo per i partner e i clienti che creano destinazioni batch (o basate su file) o private. Per ulteriori informazioni, consulta le seguenti pagine della documentazione: <ul><li>[Panoramica sulla Destination SDK](/help/destinations/destination-sdk/overview.md)</li><li>[Configurare una destinazione basata su file](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Configurare le opzioni di formattazione per le destinazioni basate su file](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Verifica delle destinazioni basate su file](/help/destinations/destination-sdk/file-based-destination-testing-overview.md)</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services fornisce una piattaforma per la progettazione di esperienze cliente cross-channel e un ambiente per l’orchestrazione visiva delle campagne, la gestione delle interazioni in tempo reale e l’esecuzione cross-channel. [Guida introduttiva a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Questa integrazione funziona con Nota che questa integrazione funziona con [Adobe Campaign versione 8.4 o successiva](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | La [!DNL Salesforce CRM] destinazione è stata aggiornata per supportare sia gli aggiornamenti di contatti e lead, sia i miglioramenti delle prestazioni per aggiornamenti più rapidi. |

{style=&quot;table-layout:auto&quot;}

**Documentazione nuova o aggiornata**

| Documentazione | Descrizione |
| ----------- | ----------- |
| Documentazione API del servizio Flusso delle destinazioni | La [Documentazione di riferimento API per le destinazioni](https://developer.adobe.com/experience-platform-apis/references/destinations/) è stato aggiornato per includere istruzioni su come eseguire operazioni sulle destinazioni basate su file. Le operazioni per le destinazioni di streaming verranno aggiunte in un secondo momento. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’interfaccia utente di enum e valori consigliati | Oltre agli enum che abilitano la convalida dei dati, ora puoi [aggiungere o rimuovere valori consigliati](../../xdm/ui/fields/enum.md) per i campi stringa standard o personalizzati in modo che gli utenti di Platform dispongano di un elenco di valori descrittivi da selezionare durante la creazione dei segmenti. |

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Campi di classificazione AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Proprietà di un elemento specifico interagito con il quale è stato attivato l&#39;evento di proposizione. |
| Gruppo di campi | [[!UICONTROL Dettagli dell’interazione con MediaAnalytics]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Tiene traccia delle interazioni multimediali nel tempo. |
| Gruppo di campi | [[!UICONTROL Informazioni sui dati multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Tiene traccia delle informazioni sui dettagli multimediali. |
| Gruppo di campi | [[!UICONTROL Adobe CJM ExperienceEvent - Superfici]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Descrive le superfici per gli eventi di esperienza in Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Comportamento | [[!UICONTROL Serie temporali]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Sono stati aggiunti valori per `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Valori rimossi per `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Gruppo di campi | (Multipli) | [Sono state aggiornate diverse descrizioni dei campi](https://github.com/adobe/xdm/pull/1628/files) tra i componenti di Journey Orchestration. |
| Gruppo di campi | (Multipli) | [Sono stati aggiornati i titoli per diversi componenti di Adobe Workfront](https://github.com/adobe/xdm/pull/1634/files) per coerenza. |
| Gruppo di campi | [[!UICONTROL Campi di classificazione AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Sono stati aggiornati i namespace di diversi campi in `xdm`. |
| Gruppo di campi | [[!UICONTROL Campi comuni evento evento passaggio Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | È stato aggiunto un nuovo campo , `isReadSegmentTriggerStartEvent`. |
| Gruppo di campi | [[!UICONTROL Tempo previsto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Modificato il `xdm:uvIndex` è stato aggiunto il campo a un tipo di numero intero e il `xdm` spazio dei nomi in diversi campi in cui era mancante. |
| Gruppo di campi | [[!UICONTROL Informazioni sui dati multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` e `xdm:implementationDetails` sono stati rimossi dal gruppo di campi. |
| Tipo di dati | (Multipli) | [Sono stati aggiornati diversi nomi di proprietà multimediali](https://github.com/adobe/xdm/pull/1626/files) tra diversi tipi di dati per coerenza. |
| Tipo di dati | [[!UICONTROL Dettagli di implementazione]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Aggiunti nomi noti per lo scaricamento. |
| Tipo di dati | [[!UICONTROL Dettagli del punto di interesse]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Il tipo di dati può ora accettare un elenco di coppie chiave-valore di metadati associate al punto di interesse. |
| Tipo di dati | [[!UICONTROL Azione proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] è stato rinominato in [!UICONTROL Azione proposta]. |
| Tipo di dati | [[!UICONTROL Tipo evento proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] è stato rinominato in [!UICONTROL Azione proposta]. |
| (Multipli) | (Multipli) | Le proprietà sperimentali sono state [stabilizzato su tutti i componenti B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Multipli) | (Multipli) | Le entità Adobe Journey Optimizer sono state [stabilizzato](https://github.com/adobe/xdm/pull/1625/files). |
| (Multipli) | (Multipli) | I namespace di alcuni campi in diversi componenti sperimentali sono stati [aggiornato per coerenza](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Servizio Identity {#identity-service}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni cliente sembri avere più &quot;identità&quot;.

Il servizio Adobe Experience Platform Identity consente di acquisire una visione migliore del cliente e del suo comportamento collegando le identità tra dispositivi e sistemi, consentendoti di fornire in tempo reale esperienze digitali personali di impatto.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’eliminazione dei set di dati | Il servizio Identity supporta ora l’eliminazione dei set di dati durante la richiesta tramite [API del servizio catalogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), l’interfaccia utente o l’igiene dei dati. Leggi la guida su [eliminazione di set di dati nell’interfaccia utente](../../catalog/datasets/user-guide.md#delete-a-dataset) per ulteriori informazioni. |

Per ulteriori informazioni sul servizio Identity, consulta la sezione [Panoramica del servizio Identity](../../identity-service/home.md).

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento in Profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| API di abbonamento agli avvisi | Adobe Experience Platform Query Service consente di sottoscrivere avvisi per query ad hoc e pianificate. Gli avvisi possono essere ricevuti tramite e-mail, all’interno dell’interfaccia utente di Platform o per entrambi. Attualmente, gli avvisi di query possono essere abbonati solo a utilizzando [API del servizio query](https://developer.adobe.com/experience-platform-apis/references/query-service/). Consulta la sezione [documentazione sugli avvisi di query](../../query-service/api/alert-subscriptions.md) per saperne di più. |
| Esempi di set di dati | Gli esempi di set di dati del servizio query consentono di eseguire query esplorative su grandi dati con tempi di elaborazione notevolmente ridotti a costo di precisione della query. Consulta la sezione [guida a esempi di set di dati](../../query-service/sql/dataset-samples.md) per saperne di più. |

Per ulteriori informazioni su [!DNL Query Service], vedi [[!DNL Query Service] panoramica](../../query-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Audience Manager dell’impatto sulla popolazione del segmento sul profilo cliente in tempo reale | L’acquisizione di popolazioni di segmenti di Audience Manager di grandi dimensioni ha un impatto diretto sul conteggio totale dei profili quando invii per la prima volta un segmento di Audience Manager a Platform utilizzando l’origine di Audience Manager. Ciò significa che la selezione di tutti i segmenti può potenzialmente portare a un conteggio di profili superiore all’adesione all’utilizzo della licenza. Per ulteriori informazioni, consulta la sezione [Panoramica di Audience Manager Source](../../sources/connectors/adobe-applications/audience-manager.md). Per informazioni sull&#39;utilizzo della licenza, consulta la documentazione su [utilizzo del dashboard di utilizzo della licenza](../../dashboards/guides/license-usage.md). |
| Supporto per il Cloud Service gestito di Adobe Campaign | Utilizza l’origine Adobe Campaign Managed Cloud Service per fornire Experience Platform dei dati dei registri di consegna e di tracciamento di Adobe Campaign v8.4. Leggi la guida su [creazione di una connessione sorgente Adobe Campaign Managed Cloud Service nell’interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/campaign.md) per ulteriori informazioni. |
| Supporto API per l’acquisizione on-demand di origini batch | Utilizza l’acquisizione on-demand per creare esecuzioni di flussi ad hoc per un determinato flusso di dati con [!DNL Flow Service] API. Le esecuzioni di flusso create devono essere impostate su acquisizione una tantum. Per ulteriori informazioni, consulta la guida su [creazione di un’esecuzione di flusso per l’acquisizione on-demand tramite API](../../sources/tutorials/api/on-demand-ingestion.md) per ulteriori informazioni. |
| Supporto API per il nuovo tentativo di esecuzione non riuscita del flusso di dati per origini batch | Utilizza la `re-trigger` per riprovare il flusso di dati non riuscito tramite l&#39;API. Leggi la guida su [nuovo tentativo di esecuzione di un flusso di dati non riuscito tramite API](../../sources/tutorials/api/retry-flows.md) per ulteriori informazioni. |
| Supporto API per il filtraggio dei dati a livello di riga per il [!DNL Google BigQuery] e [!DNL Snowflake] origini | Utilizza gli operatori logici e di confronto per filtrare i dati a livello di riga per [!DNL Google BigQuery] e [!DNL Snowflake] fonti. Leggi la guida su [filtraggio dei dati per una sorgente tramite API](../../sources/tutorials/api/filter.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).