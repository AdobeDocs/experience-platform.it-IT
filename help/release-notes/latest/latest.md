---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2025
description: Note sulla versione di Adobe Experience Platform di febbraio 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c4064771a384a90d94903ba1761fc9ee20f47747
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 97%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Questa versione include miglioramenti al componente aggiuntivo Composizione di pubblico federato. Per ulteriori informazioni, consulta la [documentazione sulla composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/release-notes).

**Data di rilascio: 18 febbraio 2025**

Aggiornamenti alle funzioni e alla documentazione esistenti in Adobe Experience Platform:

- [Assistente IA](#ai-assistant)
- [Servizio catalogo](#catalog-service)
- [Preparazione dei dati](#data-prep)
- [Destinazioni](#destinations)
- [Origini](#sources)
- [Servizio di segmentazione](#segmentation)
- [Aggiornamenti della documentazione](#documentation-updates)
   - [Confronto tra rete Edge e hub](#edge)
   - [API del servizio Flusso estesa per le origini](#flow-service)
   - [Eseguire il backup delle configurazioni degli oggetti utilizzando gli strumenti di sandbox](#back-up-object-configurations)
   - [Abilitare un centro di eccellenza utilizzando gli strumenti di sandbox](#center-of-excellence)
   - [Conservazione del set di dati dell’evento esperienza nel data lake](#experience-event-dataset-retention)

## Assistente IA {#ai-assistant}

L’Assistente IA in Adobe Experience Platform è un’esperienza di conversazione che puoi utilizzare per accelerare i flussi di lavoro nelle applicazioni Adobe. È possibile utilizzare l’Assistente IA per accrescere la conoscenza del prodotto, risolvere i problemi o eseguire ricerche nelle informazioni e trovare approfondimenti operativi. L’Assistente IA supporta Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale delle informazioni operative | Le informazioni operative nell’assistente IA sono ora in disponibilità generale. Le informazioni operative si riferiscono alle risposte che l’Assistente IA genera sugli oggetti di metadati (attributi, tipi di pubblico, flussi di dati, set di dati, destinazioni, percorsi, schemi e origini), inclusi i conteggi, le ricerche e l’impatto sulla derivazione. Le informazioni operative non esaminano alcun dato all’interno della sandbox. Per ulteriori informazioni, consulta la [Guida all’interfaccia utente dell’Assistente IA](../../ai-assistant/ui-guide.md). |
| Supporto per il completamento automatico delle domande | Quando si immette una domanda per l’Assistente IA, è ora possibile selezionare da un elenco di domande consigliate fornite dall’Assistente IA. Utilizza questa funzione per accelerare ulteriormente i flussi di lavoro con l’Assistente IA. Per ulteriori informazioni, consulta la guida sull’[utilizzo del completamento automatico delle domande con l’Assistente IA](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Supporto per l’osservabilità dei set di dati | Ora puoi utilizzare l’Assistente IA per rispondere a domande su metriche specifiche dei set di dati, come le dimensioni dell’archiviazione e il conteggio delle righe. Le domande sull’osservabilità dei dati supportano i qualificatori che ti possono servire per filtrare le query in base a un determinato periodo di tempo. Per ulteriori informazioni, consulta la [Guida alle domande dell’Assistente IA](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica dell’Assistente IA](../../ai-assistant/home.md).

## Servizio catalogo {#catalog-service}

Il servizio catalogo è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory. Il servizio catalogo, invece, contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

| Funzione | Descrizione |
| --- | --- |
| Nuovo endpoint API | Gestisci i metadati del set di dati di Adobe Experience Platform in modo più efficiente con il nuovo [endpoint API /v2/dataSets/{DATASET_ID} del servizio catalogo](../../catalog/api/update-object.md#patch-v2-notation). Puoi aggiornare facilmente attributi di set di dati complessi e nidificati in modo approfondito, poiché il sistema crea automaticamente livelli di percorso mancanti per risparmiare tempo, limitare i passaggi manuali e ridurre al minimo gli errori. |

{style="table-layout:auto"}

Per ulteriori informazioni sul Servizio catalogo, consulta la [panoramica sul servizio catalogo](../../catalog/home.md).

## Preparazione dei dati {#data-prep}

Usa la preparazione dei dati per mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto migliorato per l’importazione e l’esportazione di mappature | Ora puoi esportare le mappature in un file CSV e configurarle localmente su un foglio di calcolo. Puoi quindi importare le mappature aggiornate in Experience Platform utilizzando l’interfaccia di mappatura nell’interfaccia utente. Puoi utilizzare questa funzionalità per configurare un numero elevato di mappature senza doverle creare manualmente nell’interfaccia utente. Inoltre, durante la creazione di un nuovo flusso di dati, puoi caricare una copia delle mappature direttamente in Experience Platform per accelerare il flusso di lavoro. Per ulteriori informazioni, leggi la guida sull’ [Importazione ed esportazione delle mappature](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Destinazioni (aggiornato il 20 febbraio) {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [(Beta) Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Utilizza il connettore [!DNL Marketo Engage Person Sync] per inviare in streaming gli aggiornamenti dai tipi di pubblico della Persona ai record corrispondenti nell’istanza [!DNL Marketo Engage]. Al momento il connettore destinazione è in versione Beta ed è disponibile solo per una clientela selezionata. Per richiedere l’accesso, contatta il tuo rappresentante Adobe. |
| [Connessione Trade Desk al CRM](/help/destinations/catalog/advertising/tradedesk-emails.md) disponibilità generale | La connessione [!DNL The Trade Desk CRM] è ora in disponibilità generale. Utilizza la destinazione CRM [!DNL The Trade Desk] per attivare i profili nell’account [!DNL Trade Desk] per il targeting e l’eliminazione del pubblico in base ai dati CRM. |
| [Connessione ai profili dei partecipanti RainFocus](/help/destinations/catalog/marketing-automation/rainfocus.md) | Utilizza la destinazione [!DNL RainFocus Attendee Profiles] per eseguire lo streaming dei profili cliente da Adobe Experience Platform alla piattaforma [!DNL RainFocus] per creare e aggiornare i profili dei partecipanti. |
| [Connessione Criteo](/help/destinations/catalog/advertising/criteo.md) disponibilità generale | La connessione [!DNL Criteo] è ora in disponibilità generale. Criteo potenzia la pubblicità affidabile e di impatto per offrire esperienze più ricche a ogni consumatore attraverso l’intera Internet. Con il set di dati di e-commerce più grande al mondo e l’intelligenza artificiale migliore della categoria, Criteo assicura che ogni punto di contatto nel percorso di acquisto sia personalizzato per raggiungere la clientela con l’annuncio giusto, al momento giusto. |
| Connessione [[!DNL Amazon Ads] ](../../destinations/catalog/advertising/amazon-ads.md) | Il connettore [!DNL Amazon Ads], precedentemente in versione Beta, è ora in disponibilità generale. Il connettore è stato anche aggiornato per inviare un segnale di consenso concesso a tutti i profili che hanno acconsentito all’utilizzo del loro dati personali per la pubblicità. Ulteriori informazioni sul nuovo controllo [Segnale di consenso di Amazon Ads](../../destinations/catalog/advertising/amazon-ads.md#destination-details). |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| Utilizzare le etichette di accesso per gestire l’accesso degli utenti ai flussi di dati di destinazione | Come parte della funzionalità del [[!UICONTROL controllo degli accessi basato su attributi]](/help/access-control/abac/overview.md) in Real-Time CDP, ora puoi applicare le etichette di accesso ai [flussi di dati di destinazione](/help/dataflows/ui/monitor-destinations.md). In questo modo, puoi garantire che solo un sottoinsieme di utenti dell’organizzazione abbia accesso a specifici flussi di dati di destinazione. <br> **Importante**: durante la ricerca dei flussi di dati di destinazione utilizzando la casella di ricerca nella parte superiore dell’interfaccia utente di Experience Platform, i risultati potrebbero includere flussi di dati di destinazione che le tue etichette di accesso utente non consentono di visualizzare. Questo comportamento verrà corretto nelle versioni future. |
| [Reporting a livello di pubblico](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) per la [connessione Marketo Engage](/help/destinations/catalog/adobe/marketo-engage.md) | Ora puoi [visualizzare informazioni](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) sulle identità attivate, escluse o non riuscite suddivise a livello di pubblico, per ogni pubblico che fa parte dei flussi di dati per questa destinazione. |
| Supporto di tipi di pubblico esterni per le connessioni [TikTok](/help/destinations/catalog/social/tiktok.md) e [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) | Puoi attivare tipi di pubblico esterni per queste destinazioni da [caricamenti personalizzati](../../segmentation/ui/audience-portal.md#import-audience) e dalla [composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/start/audiences). |
| Esportare array, mappe e oggetti nelle destinazioni di archiviazione cloud | Attivando o disattivando il nuovo pulsante **[!UICONTROL Esporta array, mappe, oggetti]** durante la connessione a una destinazione di archiviazione cloud, ora puoi esportare oggetti complessi alle destinazioni selezionate. [Ulteriori informazioni](/help/destinations/ui/export-arrays-calculated-fields.md) sulla nuova funzionalità. |

{style="table-layout:auto"}

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

- È stato risolto un problema negli strumenti di test di Destination SDK. Alcuni clienti o partner hanno riscontrato problemi con lo [strumento di generazione del profilo di esempio](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) a causa di un formato non supportato quando lo schema utilizzato per la generazione dei profili includeva tipi di dati con un selettore `No format`.
- È stato risolto un problema che si verificava durante l’aggiornamento delle specifiche di `targetConnection` delle destinazioni tramite l’API del servizio Flusso. In alcuni casi, l’operazione PATCH si comportava in modo simile a un’operazione POST, danneggiando i flussi di dati esistenti. Questo problema è ora risolto e tutta la clientela può utilizzare l’API del servizio Flusso per aggiornare le proprie specifiche `targetConnection`. [Ulteriori informazioni](/help/destinations/api/edit-destination.md#patch-target-connection).
- Durante l’esportazione di profili in destinazioni basate su file, la deduplica garantisce che venga esportato un solo profilo quando più profili condividono la stessa chiave di deduplica e la stessa marca temporale di riferimento. Questa versione include un aggiornamento del processo di deduplica affinché esecuzioni successive con le stesse coordinate producano sempre gli stessi risultati, per una maggiore coerenza. [Ulteriori informazioni](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp).

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Divisione persistente | La composizione del pubblico ora supporta le suddivisioni persistenti. Puoi fare in modo che i tipi di pubblico suddivisi rimangano costanti quando si suddividono per profilo, aggiungendo uno spazio dei nomi delle identità al blocco di suddivisione. Ulteriori informazioni su questa funzione sono disponibili nella [documentazione sulla composizione del pubblico](../../segmentation/ui/audience-composition.md). |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Supporto per le visualizzazioni in [!DNL Microsoft Dynamics] | È ora possibile acquisire `"entityType": "view"` utilizzando l’origine [!DNL Microsoft Dynamics]. Per ulteriori informazioni, consulta la guida sulla [connessione di un’origine  [!DNL Microsoft Dynamics]  ad Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

## Aggiornamenti della documentazione {#documentation-updates}

### Confronto tra rete Edge e hub {#edge}

Il [confronto tra la rete Edge e l’hub](../../landing/edge-and-hub-comparison.md) fornisce una panoramica delle differenze tra i due tipi di server per Adobe Experience Platform (hub e rete Edge), inclusi i servizi disponibili su ciascun tipo di server, le posizioni dei server e gli scenari consigliati per l’utilizzo di ciascun tipo di server.

### Riferimento API esteso del servizio Flusso per le origini {#flow-service}

Il riferimento [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) per le origini è stato aggiornato con nuovi esempi di API per richieste e risposte. Utilizza il riferimento API esteso per creare e aggiornare le specifiche di connessione durante l’integrazione della tua origine in Experience Platform. È inoltre possibile utilizzare il riferimento API esteso per eseguire transizioni di stato sulle entità di origine, aggiornare le connessioni di origine e di destinazione esistenti e recuperare flussi e specifiche di flusso in base a criteri di filtro specifici.

### Eseguire il backup delle configurazioni degli oggetti utilizzando gli strumenti di sandbox {#back-up-object-configurations}

Per istruzioni dettagliate sulla creazione di un pacchetto di backup utilizzando gli strumenti della sandbox, consulta la [guida alla configurazione dell’oggetto di backup](../../sandboxes/use-cases/backup-object-configuration.md) per verificare che le configurazioni dell’oggetto siano archiviate e protette.

### Abilitare un centro di eccellenza utilizzando gli strumenti di sandbox {#center-of-excellence}

Leggi la [guida del centro di eccellenza](../../sandboxes/use-cases/center-of-excellence.md) per istruzioni dettagliate sulla creazione di un pacchetto “golden sandbox” che funga da centro di eccellenza per condividere in modo efficiente le configurazioni chiave.

### Conservazione del set di dati dell’evento esperienza nel data lake {#experience-event-dataset-retention}

Assumi il controllo della conservazione dei set di dati dell’evento esperienza in Adobe Experience Platform utilizzando Time-To-Live (TTL). [Questa guida](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) illustra come valutare, configurare e gestire le impostazioni TTL per rimuovere automaticamente i record obsoleti, ottimizzare l’archiviazione e mantenere rilevanti i dati. Scopri le best practice, i casi d’uso reali e le considerazioni chiave per migliorare la gestione del ciclo di vita dei dati.
