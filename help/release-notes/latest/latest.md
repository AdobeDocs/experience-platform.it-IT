---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2025
description: Note sulla versione di Adobe Experience Platform di febbraio 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b29c63942b00fdf597ebfd3ab105519a6b05a476
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 22%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Questa versione include miglioramenti al componente aggiuntivo Federated Audience Composition. Per ulteriori informazioni, consulta le [note sulla versione di Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes).

**Data di rilascio: mercoledì 18 febbraio 2025**

Aggiornamenti alle funzioni e alla documentazione esistenti in Adobe Experience Platform:

- [Assistente IA](#ai-assistant)
- [Servizio catalogo](#catalog-service)
- [Preparazione dei dati](#data-prep)
- [Destinazioni](#destinations)
- [Origini](#sources)
- [Aggiornamenti della documentazione](#documentation-updates)
   - [Confronto tra rete e hub di Edge](#edge)
   - [API del servizio Flusso espanso per le origini](#flow-service)
   - [Eseguire il backup delle configurazioni degli oggetti utilizzando gli strumenti sandbox](#back-up-object-configurations)
   - [Abilitare un centro di eccellenza utilizzando gli strumenti sandbox](#center-of-excellence)
   - [Conservazione del set di dati di Experience Event nel data lake](#experience-event-dataset-retention)

## Assistente IA {#ai-assistant}

L’Assistente IA in Adobe Experience Platform è un’esperienza di conversazione che puoi utilizzare per accelerare i flussi di lavoro nelle applicazioni Adobe. È possibile utilizzare l’Assistente IA per accrescere la conoscenza del prodotto, risolvere i problemi o eseguire ricerche nelle informazioni e trovare approfondimenti operativi. L’Assistente AI supporta Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto per il completamento automatico delle domande | Quando si immette una domanda nell’Assistente AI, è ora possibile selezionare da un elenco di domande consigliate fornite dall’Assistente AI. Utilizza questa funzione per accelerare ulteriormente i flussi di lavoro con l’Assistente IA. Per ulteriori informazioni, leggere la guida su [utilizzo del completamento automatico delle domande con Assistente AI](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Supporto per l’osservabilità dei set di dati | Ora puoi utilizzare l’Assistente AI per rispondere a domande su metriche specifiche dei set di dati, come le dimensioni dell’archiviazione e il conteggio delle righe. Le domande sull’osservabilità dei dati supportano i qualificatori che possono essere utilizzati per filtrare le query in base a un determinato periodo di tempo. Per ulteriori informazioni, leggere la [Guida alle domande dell&#39;Assistente AI](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica dell&#39;Assistente AI](../../ai-assistant/home.md).

<!-- | General availability of operational insights | Operational insights in AI Assistant are now in GA. Operational insights refer to answers AI Assistant generates about your metadata objects (attributes, audiences, dataflows, datasets, destinations, journeys, schemas, and sources), including counts, lookups, and lineage impact. Operational insights does not look at any data within the sandbox. For more information, read the [AI Assistant UI guide](../../ai-assistant/ui-guide.md). | -->

## Servizio catalogo {#catalog-service}

Il servizio catalogo è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory. Il servizio catalogo, invece, contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

| Funzione | Descrizione |
| --- | --- |
| Nuovo endpoint API | Gestisci i metadati del set di dati di Adobe Experience Platform in modo più efficiente con il nuovo [endpoint API /v2/dataSets/{DATASET_ID} di Catalog Service](../../catalog/api/update-object.md#patch-v2-notation). Aggiornare facilmente attributi di set di dati complessi e nidificati in modo approfondito, poiché il sistema crea automaticamente livelli di percorso mancanti per risparmiare tempo, ridurre i passaggi manuali e ridurre al minimo gli errori. |

{style="table-layout:auto"}

Per ulteriori informazioni su Catalog Service, leggere la [Panoramica di Catalog Service](../../catalog/home.md).

## Preparazione dei dati {#data-prep}

Usa la preparazione dei dati per mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto migliorato per l’importazione e l’esportazione di mappature | Ora puoi esportare le mappature in un file CSV e configurarle localmente su un foglio di calcolo. Puoi quindi importare le mappature aggiornate in Experience Platform utilizzando l’interfaccia di mappatura nell’interfaccia utente. Puoi utilizzare questa funzionalità per configurare un numero elevato di mappature senza doverle creare manualmente nell’interfaccia utente. Inoltre, durante la creazione di un nuovo flusso di dati, puoi caricare una copia delle mappature direttamente in Experience Platform per accelerare il flusso di lavoro. Per ulteriori informazioni, leggere la guida su [importazione ed esportazione di mapping](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica sulla preparazione dati](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [(Beta) Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Utilizza il connettore [!DNL Marketo Engage Person Sync] per inviare in streaming gli aggiornamenti dai tipi di pubblico personali ai record corrispondenti nell&#39;istanza [!DNL Marketo Engage]. Questo connettore di destinazione è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso, contatta il rappresentante Adobe. |
| [Connessione CRM Trade Desk](/help/destinations/catalog/advertising/tradedesk-emails.md) disponibilità generale | La connessione [!DNL The Trade Desk CRM] è ora generalmente disponibile. Utilizza la destinazione CRM [!DNL The Trade Desk] per attivare i profili nell&#39;account [!DNL Trade Desk] per il targeting e l&#39;eliminazione del pubblico in base ai dati CRM. |
| [Connessione profili partecipanti RainFocus](/help/destinations/catalog/marketing-automation/rainfocus.md) | Utilizzare la destinazione [!DNL RainFocus Attendee Profiles] per eseguire lo streaming dei profili cliente da Adobe Experience Platform alla piattaforma [!DNL RainFocus] per creare e aggiornare i profili dei partecipanti. |
| [Connessione critica](/help/destinations/catalog/advertising/criteo.md) disponibilità generale | La connessione [!DNL Criteo] è ora generalmente disponibile. Criteo potenzia la pubblicità di fiducia e di impatto per offrire esperienze più ricche a ogni consumatore attraverso l&#39;internet aperto. Con il set di dati di e-commerce più grande al mondo e l’intelligenza artificiale migliore della classe, Criteo assicura che ogni punto di contatto nel percorso sia personalizzato per raggiungere i clienti con l’annuncio giusto, al momento giusto. |
| Connessione [[!DNL Amazon Ads] ](../../destinations/catalog/advertising/amazon-ads.md) | Il connettore [!DNL Amazon Ads], precedentemente in versione beta, è ora generalmente disponibile. Il connettore è stato anche aggiornato per inviare un segnale di consenso concesso per tutti i profili che hanno acconsentito a che i loro dati personali vengano utilizzati per la pubblicità. Ulteriori informazioni sul nuovo controllo [Segnale di consenso](../../destinations/catalog/advertising/amazon-ads.md#destination-details) di Amazon Ads. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| Utilizzare le etichette di accesso per gestire l’accesso degli utenti ai flussi di dati di destinazione | Come parte della funzionalità [[!UICONTROL controllo dell&#39;accesso basato su attributi]](/help/access-control/abac/overview.md) in Real-Time CDP, ora puoi applicare le etichette di accesso ai [flussi di dati di destinazione](/help/dataflows/ui/monitor-destinations.md). In questo modo, puoi garantire che solo un sottoinsieme di utenti dell’organizzazione abbia accesso a flussi di dati di destinazione specifici. <br> **Importante**: durante la ricerca dei flussi di dati di destinazione utilizzando la casella di ricerca nella parte superiore dell&#39;interfaccia utente di Experience Platform, i risultati potrebbero includere flussi di dati di destinazione che le etichette di accesso utente non consentono di visualizzare. Questo comportamento verrà corretto in un aggiornamento futuro. |
| [Generazione rapporti a livello di pubblico](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) per la [connessione Marketo Engage](/help/destinations/catalog/adobe/marketo-engage.md) | Ora puoi [visualizzare informazioni](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) sulle identità attivate, escluse o non riuscite suddivise a livello di pubblico, per ogni pubblico che fa parte dei flussi di dati per questa destinazione. |
| Supporto di pubblici esterni per le connessioni [TikTok](/help/destinations/catalog/social/tiktok.md) e [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) | Puoi attivare tipi di pubblico esterni per queste destinazioni da [caricamenti personalizzati](../../segmentation/ui/audience-portal.md#import-audience) e [Composizione pubblico federato](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

- È stato risolto un problema negli strumenti di test di Destination SDK. Alcuni clienti o partner hanno riscontrato problemi con lo strumento di [generazione del profilo di esempio](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) a causa di un formato non supportato quando lo schema utilizzato per la generazione dei profili includeva tipi di dati con un selettore `No format`.
- È stato risolto un problema che si verificava durante l&#39;aggiornamento delle specifiche di `targetConnection` delle destinazioni tramite l&#39;API del servizio Flusso. In alcuni casi, l’operazione PATCH si comporterebbe in modo simile a un’operazione POST, danneggiando i flussi di dati esistenti. Questo problema è ora risolto e tutti i clienti possono utilizzare l&#39;API del servizio Flusso per aggiornare le proprie specifiche `targetConnection`. [Ulteriori informazioni](/help/destinations/api/edit-destination.md#patch-target-connection).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Supporto per le visualizzazioni in [!DNL Microsoft Dynamics] | È ora possibile acquisire `"entityType": "view"` utilizzando l&#39;origine [!DNL Microsoft Dynamics]. Per ulteriori informazioni, consulta la guida su [connessione di un&#39;origine  [!DNL Microsoft Dynamics]  ad Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

## Aggiornamenti della documentazione {#documentation-updates}

### Confronto tra Edge Network e hub {#edge}

Il [confronto tra Edge Network e hub](../../landing/edge-and-hub-comparison.md) fornisce una panoramica delle differenze tra i due tipi di server per Adobe Experience Platform (hub e Edge Network), inclusi i servizi disponibili su ciascun tipo di server, le posizioni dei server e gli scenari consigliati per l&#39;utilizzo di ciascun tipo di server.

### Riferimento API del servizio Flusso espanso per le origini {#flow-service}

Il riferimento [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) per le origini è stato aggiornato con nuovi esempi di richieste e risposte API. Utilizza il riferimento API esteso per creare e aggiornare le specifiche di connessione durante l’integrazione della tua origine in Experience Platform. È inoltre possibile utilizzare il riferimento API espanso per eseguire transizioni di stato sulle entità di origine, aggiornare le connessioni di origine e di destinazione esistenti e recuperare flussi e specifiche di flusso in base a criteri di filtro specifici.

### Eseguire il backup delle configurazioni degli oggetti utilizzando gli strumenti sandbox {#back-up-object-configurations}

Per istruzioni dettagliate sulla creazione di un pacchetto di backup utilizzando gli strumenti sandbox, leggere la [guida alla configurazione dell&#39;oggetto di backup](../../sandboxes/use-cases/backup-object-configuration.md) per verificare che le configurazioni dell&#39;oggetto siano archiviate e protette.

### Abilitare un centro di eccellenza utilizzando gli strumenti sandbox {#center-of-excellence}

Leggi la [guida del centro di eccellenza](../../sandboxes/use-cases/center-of-excellence.md) per istruzioni dettagliate sulla creazione di un pacchetto &quot;sandbox d&#39;oro&quot; che funga da centro di eccellenza per condividere in modo efficiente le configurazioni chiave.

### Conservazione del set di dati di Experience Event nel data lake {#experience-event-dataset-retention}

Assumi il controllo della conservazione dei set di dati di Experience Event in Adobe Experience Platform utilizzando Time-To-Live (TTL). [Questa guida](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) illustra come valutare, configurare e gestire le impostazioni TTL per rimuovere automaticamente i record obsoleti, ottimizzare l&#39;archiviazione e mantenere rilevanti i dati. Scopri le best practice, i casi d’uso reali e le considerazioni chiave per migliorare la gestione del ciclo di vita dei dati.
