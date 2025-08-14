---
title: Note pre-release di Experience Platform
description: Un’anteprima delle ultime note sulla versione di Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: bcf3045fbbf4f9673e954a5ebf95d1225d4cdcd7
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 35%

---

# Note preliminari su Adobe Experience Platform

>[!IMPORTANT]
>
>Questo documento è destinato ad essere **anteprima** delle note sulla versione per il mese corrente. Gli elementi da rilasciare sono soggetti a modifiche e possono essere aggiunti o rimossi nella versione finale.

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: agosto 2025**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Avvisi {#alerts}

Experience Platform consente di iscriverti agli avvisi basati su eventi per varie attività di Experience Platform. Puoi iscriverti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell’interfaccia utente di Experience Platform e scegliere di ricevere messaggi di avviso nell’interfaccia stessa o tramite notifiche e-mail.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Avvisi sulla capacità di throughput in streaming | Tre nuovi avvisi consentono agli utenti di abbonarsi e configurare gli avvisi per gestire e monitorare in modo proattivo le prestazioni della capacità di velocità effettiva in streaming. I nuovi avvisi includono quando la velocità effettiva dello streaming ha raggiunto l’80%, il 90% o supera i limiti di capacità. Per ulteriori informazioni, leggere la [guida alle regole per gli avvisi sulla capacità](../observability/alerts/rules.md#capacity). |

Per ulteriori informazioni sugli avvisi, consulta la [[!DNL Observability Insights] panoramica](../observability/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l&#39;attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

>[!IMPORTANT]
>
>**Estensione pianificazione esportazione set di dati**
>
>Se nell&#39;organizzazione sono presenti flussi di dati di esportazione del set di dati creati prima di novembre 2024, questi flussi di dati cesseranno di funzionare il **1 settembre 2025**. Se i flussi di dati sono necessari per continuare a esportare dati dopo il 1° settembre 2025, è necessario estendere le pianificazioni per ogni destinazione in cui si esportano i set di dati, seguendo i passaggi descritti in [questa guida](../destinations/ui/dataset-expiration-update.md).

**Nuove destinazioni**

| Destinazione | Descrizione |
| --- | --- |
| [!DNL Acxiom Real ID Audience] destinazione | Utilizza la destinazione [!DNL Acxiom Real ID Audience Connection] per migliorare i tipi di pubblico con la tecnologia [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) e attivare i tipi di pubblico su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora. |

**Destinazioni aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Dettagli scadenza autenticazione per [!DNL LinkedIn] e [!DNL Pinterest] destinazioni | Le informazioni sulla scadenza dell&#39;account sono ora visibili direttamente nell&#39;interfaccia di Experience Platform, quindi puoi vedere quando scadrà l&#39;autenticazione [!DNL LinkedIn] e [!DNL Pinterest] e rinnovarla prima che causi interruzioni ai flussi di dati. |
| Supporto crittografia per [!DNL Data Landing Zone] destinazioni | Protezione dei dati esportati con crittografia. È ora possibile allegare chiavi pubbliche in formato RSA per crittografare i file esportati, garantendo lo stesso livello di sicurezza fornito da altre destinazioni di archiviazione cloud per le informazioni riservate. |
| Aggiornamento interno di [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) | A partire dal martedì 11 agosto 2025 nel catalogo delle destinazioni, puoi visualizzare due schede **[!DNL Microsoft Bing]** affiancate. Questo è dovuto a un aggiornamento interno del servizio destinazioni. Il connettore di destinazione **[!DNL Microsoft Bing]** esistente è stato rinominato in **[!UICONTROL (obsoleto) Microsoft Bing]** ed è ora disponibile una nuova scheda con il nome **[!UICONTROL Microsoft Bing]**. Utilizza la nuova connessione **[!UICONTROL Microsoft Bing]** nel catalogo per i nuovi flussi di dati di attivazione. Se sono presenti flussi di dati attivi nella destinazione **[!UICONTROL (obsoleto) Microsoft Bing]**, questi verranno aggiornati automaticamente, pertanto non è richiesta alcuna azione da parte dell&#39;utente. <br><br>Se stai creando flussi di dati tramite [API Flow Service ](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare l’[!DNL flow spec ID] e l’[!DNL connection spec ID] ai seguenti valori:<ul><li>Flow spec ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Connection spec ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> In seguito a questo aggiornamento, potrebbe verificarsi un calo di **del numero di profili attivati** nei flussi di dati a [!DNL Microsoft Bing]. Questo calo è causato dall&#39;introduzione del **requisito di mappatura ECID** per tutte le attivazioni su questa piattaforma di destinazione. |
| Consolidamento di [!DNL Marketo] schede di destinazione | Semplifica la configurazione della destinazione [!DNL Marketo] con la scheda di destinazione unificata. Abbiamo consolidato [!DNL Marketo] schede V2 e V3 in un&#39;unica opzione semplificata, semplificando la scelta della destinazione giusta e consentendo di iniziare rapidamente. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Funzionalità avanzate di ricerca, filtro e assegnazione di tag per le destinazioni | Migliora il flusso di lavoro di gestione della destinazione con funzionalità avanzate di ricerca, filtro e assegnazione di tag nelle schede Sfoglia e Account. Ora puoi cercare flussi di dati e account specifici per nome, filtrare in base a vari criteri, tra cui piattaforma di destinazione, stato e date, e creare tag personalizzati per organizzare le destinazioni. L’ordinamento a colonne è disponibile anche per campi chiave come l’ultimo runtime del flusso di dati, facilitando l’identificazione e la gestione delle connessioni di destinazione. |

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Schemi basati su modelli | Semplifica la modellazione dei dati con schemi basati su modelli. Ora puoi creare gli schemi più facilmente con esempi e indicazioni completi. Questa funzione è attualmente disponibile per i titolari di licenze di Campaign Orchestration e verrà estesa ai clienti Data Distiller in GA, rendendo la modellazione dei dati più accessibile ed efficiente. |

Per ulteriori informazioni, leggere la [panoramica XDM](../xdm/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Stime del pubblico | Le stime del pubblico ora vengono generate automaticamente in Segment Builder (Generatore di segmenti). Questo valore viene aggiornato ogni volta che modifichi il pubblico e riflette sempre le regole del pubblico più recenti. |

Per ulteriori informazioni, consulta la [[!DNL Segmentation Service] panoramica](../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [!BADGE Supporto di Beta]{type=Informative} Azure Private Link nell&#39;interfaccia utente | Proteggi i tuoi dati con le connessioni di rete private. Ora puoi creare endpoint privati e impostare flussi di dati che ignorino Internet pubblico, garantendo maggiore sicurezza e isolamento della rete per i dati sensibili. |
| [!DNL Marketo] aggiornamenti della documentazione di origine | Ottieni visibilità completa sulla trasformazione dei dati di [!DNL Marketo] quando entrano in Experience Platform. Tutte le mappature dei campi ora includono spiegazioni dettagliate sulle trasformazioni dei dati, in modo da poter capire esattamente come `PersonID` diventa `leadID` e `eventType` diventa `activityType`. |
| Supporto per l&#39;autenticazione dell&#39;entità servizio per [!DNL Azure Blob Storage] | È ora possibile collegare l&#39;account [!DNL Azure Blob Storage] ad Experience Platform con l&#39;autenticazione dell&#39;entità servizio. |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../sources/home.md).

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
