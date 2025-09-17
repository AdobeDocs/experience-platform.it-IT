---
title: Note pre-release di Experience Platform
description: Un’anteprima delle ultime note sulla versione di Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: c592d007932835f5263d7f78b2e8155790313840
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 45%

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

**Data di rilascio: settembre 2025**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Assistente IA](#ai-assistant)
- [Avvisi](#alerts)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio query](#query-service)
- [Profilo cliente in tempo reale](#profile)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Assistente IA {#ai-assistant}

Adobe Experience Platform AI Assistant è un’esperienza di conversazione che puoi utilizzare per accelerare e ottimizzare i flussi di lavoro tra le applicazioni Adobe Experience Cloud.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator è il livello intelligente che alimenta l’Assistente AI. Quando fai domande o richiedi assistenza, Agent Orchestrator chiama automaticamente agenti specializzati per ottenere le risposte giuste. Agent Orchestrator ricorda la cronologia delle conversazioni e consente di basarsi sulle domande precedenti in modo naturale, senza dover ripetere il contesto, e combina le informazioni provenienti da più agenti per fornire risposte chiare e unificate. |
| Audience Agent | Audience Agent consente di visualizzare informazioni approfondite sui tipi di pubblico, tra cui il rilevamento di modifiche significative nelle dimensioni del pubblico, il rilevamento di tipi di pubblico duplicati, l’esplorazione dell’inventario dei tipi di pubblico e il recupero delle dimensioni dei tipi di pubblico. |

Per ulteriori informazioni, consulta la [panoramica dell’Assistente IA](../ai-assistant/home.md).

## Avvisi {#alerts}

Experience Platform consente di iscriverti agli avvisi basati su eventi per varie attività di Experience Platform. Puoi iscriverti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell’interfaccia utente di Experience Platform e scegliere di ricevere messaggi di avviso nell’interfaccia stessa o tramite notifiche e-mail.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Avvisi di acquisizione del profilo di streaming | Ora puoi iscriverti a due nuovi avvisi per l’acquisizione in streaming a livello di flusso di dati: <ul><li>Frequenza di errori di acquisizione in streaming superata</li><li>Frequenza di acquisizione streaming ignorata superata</li></ul> Gli avvisi e-mail o in piattaforma ti avviseranno quando vengono superate le soglie per la soglia predefinita o per una soglia personalizzata da te definita. Per ulteriori informazioni, consulta la guida [Avvisi profilo](../observability/alerts/rules.md#profile). |

{style="table-layout:auto"}

Per ulteriori informazioni sugli avvisi, consulta la [[!DNL Observability Insights] panoramica](../observability/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Connettore [!BADGE Beta]{type=Informative} [!DNL Snowflake Batch] | È ora disponibile un nuovo connettore [!DNL Snowflake Batch] che fornisce un&#39;alternativa al connettore di streaming per casi d&#39;uso specifici. |
| Destinazione [!DNL Adform] | [!DNL Adform] è uno dei principali fornitori di soluzioni per l&#39;acquisto e la vendita di contenuti multimediali a livello di programmazione. Collegando Adform a Adobe Experience Platform, puoi attivare i tipi di pubblico di prime parti tramite Adform, in base all’Experience Cloud ID (ECID). |
| Supporto crittografia [!DNL Data Landing Zone] | È ora possibile allegare chiavi pubbliche in formato RSA per crittografare i file esportati, garantendo lo stesso livello di sicurezza fornito da altre destinazioni di archiviazione cloud per le informazioni riservate. |
| Dettagli scadenza autenticazione per [!DNL Pinterest] destinazioni | Le informazioni sulla scadenza dell’autenticazione per le destinazioni [!DNL Pinterest] sono ora visibili direttamente nell’interfaccia di Experience Platform, per consentirti di visualizzare quando scadrà l’autenticazione e di rinnovarla prima che causi interruzioni nei flussi di dati. Puoi monitorare le date di scadenza del token dalla colonna **[!UICONTROL Data di scadenza account]** nelle schede **[[!UICONTROL Account]](../destinations/ui/destinations-workspace.md#accounts)** o **[[!UICONTROL Sfoglia]](../destinations/ui/destinations-workspace.md#browse)**. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Funzionalità avanzate di gestione delle destinazioni nell’interfaccia utente di Experience Platform | Migliora il flusso di lavoro di gestione della destinazione con nuove funzionalità di ordinamento nelle schede [[!UICONTROL Sfoglia]](../destinations/ui/destinations-workspace.md#browse) e [[!UICONTROL Account]](../destinations/ui/destinations-workspace.md#accounts). Ora puoi anche vedere un indicatore visivo quando l’autenticazione dell’account sta per scadere. |

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Schemi basati su modelli | Semplifica la modellazione dei dati con schemi basati su modelli. Ora puoi creare gli schemi più facilmente con esempi e indicazioni completi. Questa funzione è attualmente disponibile per i titolari di licenze di Campaign Orchestration e verrà estesa ai clienti Data Distiller in GA, rendendo la modellazione dei dati più accessibile ed efficiente. Questa funzione include il supporto per i dati della serie temporale e le funzionalità di acquisizione dei dati di modifica. |

Per ulteriori informazioni, consulta la [panoramica su XDM](../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti al visualizzatore di profili | La versione di settembre 2025 include i seguenti miglioramenti al visualizzatore profili. <ul><li>**Visualizzazione combinata**: attributi, eventi e informazioni sono stati combinati in un&#39;unica visualizzazione.</li><li>**Informazioni generate da IA**: la pagina dei dettagli del profilo ora visualizza le informazioni generate da IA, consentendo di conoscere i dettagli generati dal profilo. Queste informazioni possono includere informazioni quali i punteggi di tendenza e l’analisi delle tendenze.</li><li>**Aggiornamento stile**: la pagina dei dettagli del profilo è stata aggiornata visivamente.</li><li>**Sfoglia**: ora puoi esplorare i profili tramite un carosello interattivo basato su schede con funzionalità di ricerca e personalizzazione.</li></ul> |

Per ulteriori informazioni, leggere la [Panoramica del profilo cliente in tempo reale](../profile/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Pubblico dell’account con eventi esperienza obsoleti | Dopo l’aggiornamento dell’architettura B2B, i tipi di pubblico dell’account con eventi di esperienza non sono più supportati. Invece, utilizza il nuovo approccio per segmenti: crea un pubblico Persone con eventi di esperienza, quindi fai riferimento a tale pubblico Persone durante la creazione di un pubblico Account. Questo fornisce un approccio più flessibile e gestibile alla creazione di tipi di pubblico B2B. |

**Aggiornamenti importanti**

| Aggiornamento | Descrizione |
| ------- | ----------- |
| Le stime del pubblico vengono aggiornate automaticamente | Il miglioramento dell’aggiornamento automatico per le stime del pubblico è stato ripristinato. Le stime del pubblico continueranno a essere generate in Segment Builder, ma la funzionalità di aggiornamento automatico è stata rimossa. |

Per ulteriori informazioni, consulta la [[!DNL Segmentation Service] panoramica](../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove origini in Disponibilità generale | Le seguenti origini sono ora in Disponibilità generale: Diversi connettori di origine sono stati aggiornati da Beta a GA: <ul><li>[Acquisizione dati Acxiom](../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Acquisizione dei dati di Acxiom Prospect](../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. Queste sorgenti sono ora completamente supportate e pronte per l’uso in produzione. |
| Supporto dell&#39;autenticazione con coppia di chiavi [!DNL Snowflake] | Sicurezza avanzata per le connessioni Snowflake con supporto per l’autenticazione con coppia di chiavi. L’autenticazione di base (nome utente/password) diventerà obsoleta entro novembre 2025, pertanto si consiglia ai clienti di migrare all’autenticazione con coppia di chiavi per migliorare la sicurezza. |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../sources/home.md).