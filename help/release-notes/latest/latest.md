---
title: Note sulla versione di Adobe Experience Platform di agosto 2024
description: Note sulla versione di Adobe Experience Platform di agosto 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4fecb47084a522b4eb9808dc317e0d70e7ef42c6
workflow-type: ht
source-wordcount: '1562'
ht-degree: 100%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 20 agosto 2024**

>[!TIP]
>
>Visualizza una [panoramica della documentazione sui casi d’uso di esempio](https://experienceleague.adobe.com/it/docs/experience-platform/rtcdp/use-cases/overview) per scoprire vari casi d’uso quali ricerca di potenziali clienti, acquisizione e altro ancora che l’organizzazione può ottenere con Real-Time CDP.

Aggiornamenti alle funzioni e alla documentazione esistenti in Experience Platform:

- [Controllo degli accessi basato su attributi](#abac)
- [Acquisizione dei dati](#data-ingestion)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Controllo degli accessi basato su attributi {#abac}

Il controllo degli accessi basato sugli attributi è una funzionalità di Adobe Experience Platform che offre ai brand attenti alla privacy una maggiore flessibilità per gestire l’accesso degli utenti. È possibile assegnare singoli oggetti, come campi e segmenti dello schema, ai ruoli utente. Questa funzione consente di concedere o revocare l’accesso a singoli oggetti per specifici utenti di Platform nell’organizzazione.

Tramite il controllo dell’accesso basato su attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti ai dati personali sensibili (SPD), alle informazioni personali (PII) e ad altri tipi di dati personalizzati in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.

**Nuova funzione**

| Aggiornamento funzionale | Descrizione |
| --- | --- |
| Nuova funzione di Gestione autorizzazioni | È ora possibile utilizzare [Gestione autorizzazioni](../../access-control/abac/permission-manager/overview.md) per generare rapporti utilizzando query semplici, che consentiranno di comprendere la gestione degli accessi e risparmiare tempo nella verifica delle autorizzazioni di accesso in diversi flussi di lavoro e livelli di granularità. Per ulteriori informazioni sulla creazione di rapporti per utenti e ruoli, consulta la [guida utente sulla Gestione autorizzazioni](../../access-control/abac/permission-manager/permissions.md). ![Immagine dell’interfaccia utente di Experience Platform di immagine che evidenzia Gestione autorizzazioni nella barra di navigazione a sinistra.](../2024/assets/august/permission-manager-rn.png "Gestione autorizzazioni nell’interfaccia utente."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Per ulteriori informazioni sul controllo degli accessi basato su attributi, consulta la [panoramica sul controllo degli accessi basato su attributi](../../access-control/abac/overview.md). Per una guida completa sul flusso di lavoro di controllo degli accessi basato su attributi, leggi la [guida completa per il controllo degli accessi basato su attributi](../../access-control/abac/end-to-end-guide.md).

## Acquisizione dei dati (aggiornato il 23 agosto) {#data-ingestion}

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. Puoi acquisire utilizzando le API Batch o Streaming, le origini create da Adobe, i partner di integrazione dei dati o l’interfaccia utente di Adobe Experience Platform.

**Aggiornamento della gestione del formato della data nell’acquisizione dei dati in batch**

Questa versione risolve un problema con la *gestione del formato data* nell’acquisizione di dati in batch. In precedenza, il sistema trasformava i campi data inseriti dalla clientela come `Date` nel formato `DateTime`. Ciò significa che il fuso orario è stato aggiunto automaticamente ai campi e ha causato problemi agli utenti che preferivano o richiedevano il formato `Date`. In futuro, il fuso orario non verrà aggiunto automaticamente ai campi di tipo `Date`. Questo aggiornamento garantisce che il formato dei dati esportati corrisponda al formato rappresentato nel profilo per quel campo come richiesto dalla clientela.

`Date` campi prima della versione: `"birthDate": "2018-01-12T00:00:00Z"` `Date` campi dopo la versione: `"birthDate": "2018-01-12"`

Ulteriori informazioni sull’[acquisizione batch](/help/ingestion/batch-ingestion/overview.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [Braze](/help/destinations/catalog/mobile-engagement/braze.md) | [!UICONTROL Braze] gestisce una serie di istanze diverse per la dashboard e gli endpoint REST. La clientela [!UICONTROL Braze] deve utilizzare l’endpoint REST corretto in base all’istanza per cui è stato eseguito il provisioning. Questa versione aggiunge un nuovo endpoint US-07 che puoi selezionare quando ti connetti a [!UICONTROL Braze]. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}


| Funzione | Descrizione |
| ----------- | ----------- |
| Esportazione di file on-demand nelle destinazioni batch ora disponibile per tutti. | L’opzione per esportare i file on-demand nelle destinazioni batch è ora disponibile per tutti. Per ulteriori informazioni, consulta la [documentazione specifica](../../destinations/ui/export-file-now.md). |
| Modifica dei programmi di esportazione per più tipi di pubblico esportati nel [passaggio di pianificazione](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | L’opzione per modificare i programmi di esportazione per più tipi di pubblico esportati direttamente dalla fase di pianificazione del flusso di lavoro di Audience Activation è ora disponibile per tutti. ![Immagine dell’interfaccia utente di Experience Platform in cui è evidenziata l’opzione Modifica pianificazione nel passaggio di pianificazione.](../2024/assets/august/edit-schedule.png "Opzione Modifica pianificazione nel passaggio di pianificazione."){width="250" align="center" zoomable="yes"} |
| Modifica dei nomi dei file per più tipi di pubblico esportati nel [passaggio di pianificazione](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | L’opzione per modificare i nomi di più file esportati direttamente dalla fase di pianificazione del flusso di lavoro di Audience Activation è ora disponibile per tutti. ![Immagine dell’interfaccia utente di Experience Platform in cui è evidenziata l’opzione Modifica nome file nel passaggio di pianificazione.](../2024/assets/august/edit-file-name.png "Opzione Modifica nome file nel passaggio di pianificazione."){width="250" align="center" zoomable="yes"} |
| Rimozione di più tipi di pubblico da un flusso di dati dalla pagina [Dettagli destinazione](../../destinations/ui/destination-details-page.md#bulk-remove). | L’opzione per rimuovere più tipi di pubblico dai flussi di dati esistenti dalla pagina **[!UICONTROL Dettagli destinazione]** è ora disponibile per tutti. ![Immagine dell’interfaccia utente di Experience Platform in cui è evidenziata l’opzione Rimuovi tipi di pubblico nella pagina Dettagli destinazione.](../2024/assets/august/bulk-remove-audiences.png "Opzione Rimuovi tipi di pubblico nella pagina Dettagli destinazione."){width="250" align="center" zoomable="yes"} |
| Esportazione di più file on-demand in destinazioni batch dalla pagina [Dettagli destinazione](../../destinations/ui/destination-details-page.md#bulk-export). | L’opzione per esportare più file on-demand in destinazioni batch dalla pagina **[!UICONTROL Dettagli destinazione]** è ora disponibile per tutti. ![Immagine dell’interfaccia utente di Experience Platform in cui è evidenziata l’opzione Esporta file nella pagina Dettagli destinazione.](../2024/assets/august/bulk-export-file-now.png "Opzione Esporta file ora nella pagina Dettagli destinazione."){width="250" align="center" zoomable="yes"} |
| Modifica dei nomi dei file per più tipi di pubblico esportati dalla pagina [Dettagli destinazione](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | È ora possibile modificare i nomi di più file esportati direttamente dalla pagina **[!UICONTROL Dettagli destinazione]**. ![Immagine dell’interfaccia utente di Experience Platform in cui è evidenziata l’opzione Modifica nome file nella pagina dei dettagli destinazione.](../2024/assets/august/edit-file-name-destination-details.png "Opzione Modifica nome file nella pagina dei dettagli destinazione."){width="250" align="center" zoomable="yes"} |
| Rimozione di più set di dati da un flusso di dati dalla pagina [Dettagli destinazione](../../destinations/ui/export-datasets.md#remove-dataset). | L’opzione per rimuovere più set di dati da un flusso di dati è ora disponibile per tutti. ![Immagine dell’interfaccia utente di Experience Platform in cui è evidenziata l’opzione Rimuovi set di dati nella pagina dei dettagli destinazione.](../2024/assets/august/bulk-remove-datasets.png "Opzione Rimuovi set di dati nella pagina dei dettagli destinazione."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Flusso di creazione schema assistito da machine learning (ML) | Utilizza algoritmi avanzati di machine learning per analizzare i tuoi file di dati di esempio e creare automaticamente schemi ottimizzati con campi standard e personalizzati.<br>Funzioni chiave:<br><ul><li>Creazione più rapida degli schemi: genera schemi direttamente dai tuoi file di dati di esempio utilizzando campi XDM consigliati e generati da ML.</li><li>Flexible Schema Evolution: consente di aggiungere o aggiornare facilmente i campi nello schema generato.</li><li>Integrazione diretta: completamente integrato con il flusso di creazione dello schema di base nell’interfaccia per gli schemi, per un’esperienza di utilizzo fluida e coesa.</li><li>Revisione e modifica efficienti: visualizza e aggiorna rapidamente lo schema utilizzando l’editor Flat View, per un processo di creazione più efficiente e semplice da usare.</li></ul><br>Per ulteriori informazioni, consulta la [Guida del flusso di lavoro per la creazione di schemi assistita da ML](../../xdm/ui/ml-assisted-schema-creation.md). |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [panoramica sul sistema XDM](../../xdm/home.md).

## Identity Service {#identity-service}

Utilizza Identity Service di Adobe Experience Platform per creare una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Documentazione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Guida alle configurazioni dei grafici | Leggi la [guida alle configurazioni dei grafici](../../identity-service/identity-graph-linking-rules/example-configurations.md) per informazioni sugli scenari di grafici più comuni che potresti incontrare durante l’utilizzo delle regole di collegamento del grafico delle identità e dei dati di identità. La guida alle configurazioni dei grafici fornisce esempi che vanno da semplici scenari di grafici per singola persona a scenari di grafici complessi e gerarchici per più persone. Puoi inoltre utilizzare la guida per esempi di eventi e configurazioni di algoritmi che puoi inserire nell’[interfaccia utente di simulazione del grafico](../../identity-service/identity-graph-linking-rules/graph-simulation.md), oltre a spiegazioni dettagliate su come vengono selezionate le identità primarie in determinati scenari di grafico. |

{style="table-layout:auto"}

Per ulteriori informazioni su Identity Service, leggi la [panoramica su Identity Service](../../identity-service/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Dettagli dell’acquisizione | Per i tipi di pubblico con origine di caricamento personalizzata, puoi visualizzare in modo più completo i dettagli dell’acquisizione del pubblico all’interno della pagina dei dettagli del pubblico. Inoltre, puoi applicare le etichette agli attributi del payload selezionando lo schema e selezionando gli attributi desiderati per l’etichettatura. Ulteriori informazioni sulla sezione dei dettagli di acquisizione sono disponibili nella [guida di Audience Portal](../../segmentation/ui/audience-portal.md#ingestion-details). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Aggiornamenti al connettore di origine di Adobe Analytics | La pagina dell’attività del set di dati non visualizza informazioni sui batch, poiché il connettore di origine di Analytics è interamente gestito da Adobe. Puoi monitorare il flusso dei dati osservando le metriche relative ai record acquisiti. Per ulteriori informazioni, leggi la guida sulla [connessione di origine per i dati di Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

**Documentazione aggiornata**

| Documentazione aggiornata | Descrizione |
| --- | --- |
| Documentazione estesa sull’aggiornamento dei flussi di dati | La guida sull’[aggiornamento dei flussi di dati di origine esistenti nell’interfaccia utente](../../sources/tutorials/ui/update-dataflows.md) è stata aggiornata per fornire ulteriori informazioni sulle diverse configurazioni che è possibile apportare a un flusso di dati esistente. La guida è stata aggiornata anche per chiarire il comportamento previsto quando un flusso di dati disabilitato viene riabilitato. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle origini](../../sources/home.md).