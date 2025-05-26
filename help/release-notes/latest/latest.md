---
title: Note sulla versione di Adobe Experience Platform - Maggio 2025
description: Note sulla versione di Adobe Experience Platform di maggio 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: cf88ed1082085fac28553dcc7c7be27c517adb22
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 81%

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

**Data di rilascio: 20 maggio 2025**

Aggiornamenti alle funzioni e alla documentazione esistenti di Adobe Experience Platform:

- [Servizio catalogo](#catalog-service)
- [Preparazione dei dati](#data-prep)
- [Destinazioni](#destinations)
- [Identity Service](#identity)
- [Query Service](#query-service)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Servizio catalogo {#catalog-service}

Il servizio catalogo è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory. Il servizio catalogo, invece, contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

| Funzione | Descrizione |
| --- | --- |
| Ottimizzare l’archiviazione dei dati con regole di conservazione a livello di set di dati | Gestisci in modo efficiente l’archiviazione dei dati con regole di conservazione che eliminano i dati obsoleti in base all’intervallo temporale specificato. <ul><li>**Conservazione set di dati**: definisci le regole del set di dati per rimuovere i dati obsoleti dal data lake e dall’archivio profili.</li><li>**Informazioni sull’archiviazione**: monitora l’utilizzo e garantisci la conformità con i diritti concessi in licenza tramite metriche in linea.</li><li>**Visibilità migliorata**: tieni traccia dell’attività del set di dati dall’acquisizione all’eliminazione con un monitoraggio migliorato.</li><li>**Gestione semplificata**: accedi alle impostazioni di conservazione, al monitoraggio, ai registri di audit e alle informazioni in un’unica vista unificata.</li></ul> Per ulteriori informazioni, consulta la guida sulle [regole di conservazione dei set di dati](../../catalog/datasets/user-guide.md#data-retention-policy). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sul servizio catalog](../../catalog/home.md).

## Preparazione dei dati {#data-prep}

Usa la preparazione dei dati per mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’importazione e l’esportazione di mappature per Adobe Analytics | Puoi ora utilizzare le funzionalità di mappatura di importazione ed esportazione per i dati della suite di rapporti di Adobe Analytics quando utilizzi il connettore di origine di Adobe Analytics. <br><br>Esporta le mappature in un file CSV e configurale localmente su un foglio di calcolo. Puoi quindi importare le mappature aggiornate in Experience Platform utilizzando l’interfaccia di mappatura nell’interfaccia utente. Puoi utilizzare questa funzionalità per configurare un numero elevato di mappature senza doverle creare manualmente nell’interfaccia utente. Inoltre, durante la creazione di un nuovo flusso di dati, puoi caricare una copia delle mappature direttamente in Experience Platform per accelerare il flusso di lavoro. <br><br>Per ulteriori informazioni, consulta la guida sulla [connessione di Adobe Analytics ad Experience Platform](../../sources/tutorials/ui/create/adobe-applications/analytics.md).</br> |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| [Aggiornamento e supporto del pubblico personalizzato di Facebook](../../destinations/catalog/social/facebook.md) per gli identificatori relativi agli indirizzi | A partire dal 23 maggio 2025 e per tutto il mese di giugno 2025, potresti vedere temporaneamente due schede di destinazione **[!DNL Facebook Custom Audience]** nel catalogo delle destinazioni, per un massimo di alcune ore. Ciò è dovuto a un aggiornamento interno al servizio delle destinazioni e al supporto di nuovi campi per un targeting migliore e la corrispondenza con i profili sulle proprietà di Facebook. Per informazioni dettagliate sui nuovi campi relativi all&#39;indirizzo, consulta la sezione [identità supportate](#supported-identities). <br><br>Se vedi una scheda con l&#39;etichetta **[!UICONTROL (Nuovo) pubblico personalizzato Facebook]**, usa questa scheda per i nuovi flussi di dati di attivazione. I flussi di dati esistenti verranno aggiornati automaticamente, pertanto non è richiesta alcuna azione da parte tua. Eventuali modifiche apportate ai flussi di dati esistenti durante questo periodo verranno mantenute dopo l’aggiornamento. Al termine dell&#39;aggiornamento, la scheda di destinazione **[!UICONTROL (Nuovo) Pubblico personalizzato di Facebook]** verrà rinominata **[!DNL Facebook Custom Audience]**. <br><br>Se si creano flussi di dati utilizzando l&#39;[API del servizio di flusso](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare [!DNL flow spec ID] e [!DNL connection spec ID] ai valori seguenti: <ul><li>Flow spec ID: `bb181d00-58d7-41ba-9c15-9689fdc831d3`</li><li>Connection spec ID: `c8b97383-2d65-4b7a-9913-db0fbfc71727`</li></ul> |
| Supporto ID mobile advertising per la destinazione [Google Customer Match + Display &amp; Video 360](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities) | Ora puoi attivare i tipi di pubblico nella destinazione [Google Customer Match + Display &amp; Video 360](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities) in base agli ID mobile advertising, ad esempio [!DNL GAID] e [!DNL IDFA]. |
| Supporto di identificatori aggiuntivi per [Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md) | La destinazione Google Customer Match ora supporta la mappatura dei campi correlati all’indirizzo per migliorare le percentuali di corrispondenza nella piattaforma di Google. <br><br>Per assicurarti che Google faccia corrispondere l’indirizzo, devi mappare tutti e quattro i campi degli indirizzi (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` e `address_info_postal_code`) e assicurarti che in nessuno di questi campi manchino i dati nei profili esportati. <br> Se un campo non è mappato o contiene dati mancanti, Google non farà corrispondere l’indirizzo. |
| Colonna di scadenza account per le connessioni [Facebook](../../destinations/catalog/social/facebook.md) | Ora puoi visualizzare le date di scadenza del token dell’account Facebook nelle schede [Sfoglia](../../destinations/ui/destinations-workspace.md#browse) e [Account](../../destinations/ui/destinations-workspace.md#accounts). |
| Esportare set di dati creati dall’API | Ora puoi esportare i set di dati creati dall’API. È stata rimossa la limitazione precedente in cui solo i set di dati creati nell’interfaccia utente erano disponibili per l’esportazione. Ulteriori informazioni sull’[esportazione dei set di dati](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [Panoramica sulle destinazioni](../../destinations/home.md).

## Identity Service {#identity}

Utilizza Identity Service di Adobe Experience Platform per creare una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Identity Graph Linking Rules] | [!DNL Identity Graph Linking Rules] è ora generalmente disponibile. [!DNL Identity Graph Linking Rules] evita il &quot;collasso del grafico&quot;, garantendo profili cliente distinti e precisi per il marketing personalizzato in Experience Platform &amp; Applications. Le caratteristiche principali includono:<ul><li>[Strumento di simulazione grafico](../../identity-service/identity-graph-linking-rules/graph-simulation.md): Esplorare l&#39;algoritmo e verificare le configurazioni delle impostazioni di identità.</li><li> [Impostazioni identità](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md): Configura spazi dei nomi univoci e imposta le priorità.</li><li>[Dashboard identità](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs): monitora i grafici e convalida le impostazioni di identità.</li></ul> **Nota**: i dati non verranno modificati finché non configuri manualmente le impostazioni di identità. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [Panoramica su Identity Service](../../identity-service/home.md).

## Query Service {#query-service}

Eseguire query sui dati nel data lake di Adobe Experience Platform utilizzando SQL standard con Query Service. Combina facilmente i set di dati e generane nuovi dai risultati delle query per alimentare il reporting, i flussi di lavoro data science o facilitare l’acquisizione nel profilo cliente in tempo reale. Ad esempio, puoi unire i dati di transazione della clientela con i dati comportamentali per identificare tipi di pubblico ad alto valore per campagne di marketing mirate.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
|--------|-------------|
| Migrazione delle credenziali da JWT a OAuth | Per evitare interruzioni del servizio, entro il 30 giugno 2025 è necessario migrare le credenziali JWT senza scadenza a quelle da server a server OAuth. Questa modifica migliora la sicurezza e la coerenza della piattaforma. Per ulteriori dettagli, consulta la [Guida sulla migrazione delle credenziali JWT alle credenziali da server a server OAuth](../../query-service/ui/migrate-jwt-to-oauth.md). |
| Tabella dei risultati legacy (disponibilità limitata) | Gli utenti che si affidano al trascinamento per selezionare i flussi di lavoro possono richiedere l’accesso a una tabella dei risultati legacy che supporta la selezione e il comportamento di copia nativi del browser. L’output incollato è delimitato da tabulazioni, pertanto le colonne rimangono allineate e leggibili in Excel, facilitando la revisione del foglio di calcolo e i processi di controllo qualità. Per ulteriori informazioni, consulta la [Guida dell’interfaccia utente all’editor di query](../../query-service/ui/user-guide.md#legacy-results-table). |

Per ulteriori informazioni su [!DNL Query Service], consulta la [[!DNL Query Service] panoramica](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, Experience Platform fornisce sandbox che permettono di suddividere una singola istanza di Experience Platform in ambienti virtuali separati, utili per lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto ampliato per il plug-in degli strumenti sandbox | È ora possibile migrare le campagne con oggetti dipendenti aggiuntivi tramite strumenti sandbox, tra cui configurazione del canale, decisione unificata, impostazioni/varianti di esperimento e altro ancora. Per un elenco completo degli oggetti delle campagne e di tutti gli oggetti di Adobe Journey Optimizer supportati, consulta la guida agli [strumenti di sandbox](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento dei criteri di segmentazione in streaming | A partire dalla versione di maggio 2025, i criteri per i tipi di pubblico idonei per la segmentazione in streaming sono stati aggiornati. Ulteriori informazioni su queste modifiche sono disponibili nell’[aggiornamento dei criteri di idoneità per la segmentazione in streaming](../../segmentation/eligibility-criteria-update.md). |

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’autenticazione di base per [!DNL MySQL] | Ora puoi utilizzare l’autenticazione di base per connettere il database [!DNL MySQL] a Experience Platform. Per ulteriori informazioni, consulta la [[!DNL MySQL] Panoramica sull’origine](../../sources/connectors/databases/mysql.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [Panoramica sulle origini](../../sources/home.md).