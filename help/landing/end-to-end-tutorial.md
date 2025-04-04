---
keywords: Experience Platform;home;argomenti popolari;CJA;analisi percorso;analisi percorso clienti;orchestrazione campagna;orchestrazione;percorso clienti;percorso;orchestrazione percorso;funzionalità;area
title: Flusso di lavoro di esempio end-to-end di Adobe Experience Platform
description: Scopri ad alto livello il flusso di lavoro end-to-end di base per Adobe Experience Platform.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 1%

---

# Flusso di lavoro di esempio end-to-end di Adobe Experience Platform

Adobe Experience Platform è il sistema più potente, flessibile e aperto sul mercato per la creazione e la gestione di soluzioni complete che guidano la customer experience. Experience Platform consente alle organizzazioni di centralizzare e standardizzare i dati e i contenuti dei clienti da qualsiasi sistema, e di applicare tecniche di data science e apprendimento automatico al fine di migliorare la progettazione e la consegna di esperienze personalizzate.

Basato sulle API RESTful, Experience Platform espone agli sviluppatori la piena funzionalità del sistema, supportando la facile integrazione delle soluzioni aziendali tramite strumenti familiari. Experience Platform consente di ottenere una visione olistica dei clienti acquisendo i dati dei clienti, segmentando i dati per i tipi di pubblico desiderati e attivando tali tipi di pubblico in una destinazione esterna. L’esercitazione seguente mostra un flusso di lavoro end-to-end, con tutti i passaggi dall’acquisizione tramite origini all’attivazione tramite destinazioni.

![Flusso di lavoro end-to-end di Experience Platform](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Introduzione

Questo flusso di lavoro end-to-end utilizza più servizi Adobe Experience Platform. Di seguito è riportato un elenco dei servizi utilizzati in questo flusso di lavoro con collegamenti alle relative panoramiche:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alle [best practice per la modellazione dei dati](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): fornisce una panoramica completa dei clienti e del loro comportamento, collegando le identità tra dispositivi e sistemi diversi.
- [Origini](../sources/home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Experience Platform].
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] consente di suddividere i dati archiviati in [!DNL Experience Platform] relativi a singoli utenti (ad esempio clienti, potenziali clienti, utenti o organizzazioni) in gruppi più piccoli.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Set di dati](../catalog/datasets/overview.md): il costrutto di archiviazione e gestione per la persistenza dei dati in [!DNL Experience Platform].
- [Destinazioni](../destinations/home.md): le destinazioni sono integrazioni predefinite con applicazioni di uso comune che consentono l&#39;attivazione diretta dei dati da Experience Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d&#39;uso.

## Creare uno schema XDM

Prima di acquisire i dati in Experience Platform, devi innanzitutto creare uno schema XDM per descrivere la struttura di tali dati. Quando acquisisci i dati nel passaggio successivo, mapperai i dati in arrivo su questo schema. Per informazioni su come creare uno schema XDM di esempio, leggi l&#39;esercitazione su [creazione di uno schema tramite l&#39;Editor di schema](../xdm/tutorials/create-schema-ui.md).

L’esercitazione precedente mostra come impostare i campi di identità per gli schemi. Un campo di identità rappresenta un campo che può essere utilizzato per identificare una singola persona correlata a un record o a un evento di serie temporale. I campi di identità sono un componente cruciale nel modo in cui i grafici di identità del cliente vengono costruiti in Experience Platform, il che influisce in ultima analisi sul modo in cui Real-Time Customer Profile unisce frammenti di dati diversi per ottenere una visualizzazione completa del cliente. Per ulteriori dettagli su come visualizzare i grafici delle identità in Experience Platform, consulta l&#39;esercitazione su [come utilizzare il visualizzatore del grafico delle identità](../identity-service/features/identity-graph-viewer.md).

Devi abilitare lo schema per l’utilizzo in Real-Time Customer Profile in modo che i profili dei clienti possano essere costruiti dai dati in base allo schema. Per ulteriori informazioni, vedere la sezione relativa all&#39;abilitazione di uno schema per il profilo ](../xdm/ui/resources/schemas.md#profile) nella guida dell&#39;interfaccia utente degli schemi.[

## Inserire i dati in Experience Platform

Dopo aver creato uno schema XDM, puoi iniziare a inserire i dati nel sistema.

Tutti i dati introdotti in Experience Platform vengono memorizzati in singoli set di dati al momento dell’acquisizione. Un set di dati è una raccolta di record di dati mappati a uno schema XDM specifico. Prima che i dati possano essere utilizzati da [!DNL Real-Time Customer Profile], il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete su come abilitare un set di dati per il profilo, consulta la [Guida dell&#39;interfaccia utente dei set di dati](../catalog/datasets/user-guide.md#enable-profile) e l&#39;esercitazione sull&#39;API per la configurazione del [set di dati](../profile/tutorials/dataset-configuration.md). Una volta configurato il set di dati, puoi iniziare a acquisirvi i dati.

Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archivi basati su cloud, database e molte altre. Ad esempio, puoi acquisire i tuoi dati utilizzando [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Un elenco completo delle origini disponibili è disponibile nella [panoramica dei connettori di origine](../sources/home.md).

Se utilizzi Amazon S3 come connettore di origine, puoi seguire le istruzioni contenute nell&#39;esercitazione API [creazione di un connettore Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) o nell&#39;esercitazione interfaccia utente [creazione di un connettore Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) per scoprire come creare, connettersi e acquisire dati all&#39;interno del connettore.

Per istruzioni più dettagliate sui connettori di origine, leggere la [panoramica dei connettori di origine](../sources/home.md). Per ulteriori informazioni su Flow Service, l&#39;API da cui si basano le origini, leggere il [riferimento API del servizio Flow](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Una volta che i dati vengono introdotti in Experience Platform tramite il connettore di origine e memorizzati nel set di dati abilitato per il profilo, i profili cliente vengono creati automaticamente in base ai dati di identità configurati nello schema XDM.

Quando si caricano dati in un nuovo set di dati per la prima volta o quando si imposta un nuovo processo ETL o una nuova origine dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati correttamente e che i profili generati contengano i dati previsti. Per ulteriori informazioni su come accedere ai profili cliente nell&#39;interfaccia utente di Experience Platform, consulta la [guida all&#39;interfaccia utente del profilo cliente in tempo reale](../profile/ui/user-guide.md). Per informazioni dettagliate su come accedere ai profili tramite l&#39;API Profilo cliente in tempo reale, consulta la guida su [utilizzo dell&#39;endpoint entità](../profile/api/entities.md).

## Valutare i dati

Dopo aver generato correttamente i profili dai dati acquisiti, puoi valutare i dati utilizzando la segmentazione. La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di singoli utenti dell’archivio Profili, al fine di distinguere un gruppo commerciabile di persone dalla base dei clienti. Per ulteriori informazioni sulla segmentazione, leggere la [panoramica del servizio di segmentazione](../segmentation/home.md).

### Creare una definizione di segmento

Per iniziare, devi creare una definizione del segmento per raggruppare i clienti e creare il pubblico di destinazione. Una definizione di segmento è una raccolta di regole che puoi utilizzare per definire il pubblico di destinazione. Per creare una definizione di segmento, puoi seguire le istruzioni contenute nella guida dell&#39;interfaccia utente per l&#39;utilizzo di [Segment Builder](../segmentation/ui/segment-builder.md) o nell&#39;esercitazione dell&#39;API per [la creazione di un segmento](../segmentation/tutorials/create-a-segment.md).

Dopo aver creato una definizione di segmento, tieni presente l’ID di definizione del segmento.

### Valuta la definizione del segmento

Dopo aver creato la definizione del segmento, puoi creare un processo per il segmento per valutarlo come istanza unica oppure puoi creare una pianificazione per valutare il segmento su base continuativa.

Per valutare una definizione di segmento su richiesta, puoi creare un processo di segmentazione. Un processo di segmentazione è un processo asincrono che crea un nuovo segmento di pubblico basato sulla definizione del segmento e sui criteri di unione di cui si fa riferimento. Un criterio di unione è un insieme di regole che Experience Platform utilizza per determinare quali dati verranno utilizzati per creare i profili dei clienti e quali dati avranno priorità in caso di discrepanze tra origini diverse. Per informazioni su come utilizzare i criteri di unione, consulta la [guida dell&#39;interfaccia utente dei criteri di unione](../profile/merge-policies/ui-guide.md).

Una volta creato e valutato il processo di segmentazione, puoi ottenere informazioni sul segmento, ad esempio le dimensioni del pubblico o gli errori che possono essersi verificati durante l’elaborazione. Per informazioni su come creare un processo di segmentazione, inclusi tutti i dettagli da fornire, consulta la [guida per gli sviluppatori di processi di segmentazione](../segmentation/api/segment-jobs.md).

Per valutare una definizione di segmento su base continuativa, puoi creare e abilitare una pianificazione. Una pianificazione è uno strumento che può essere utilizzato per eseguire automaticamente un processo di segmentazione una volta al giorno a un’ora specificata. Per informazioni su come creare e abilitare una pianificazione, seguire le istruzioni riportate nella guida dell&#39;API sull&#39;[endpoint per le pianificazioni](../segmentation/api/schedules.md).

## Esportare i dati valutati

Dopo aver creato il processo di segmentazione una tantum o la pianificazione continua, puoi creare un processo di esportazione del segmento per esportare i risultati in un set di dati o esportare i risultati in una destinazione. Le sezioni seguenti forniscono indicazioni su entrambe queste opzioni.

### Esportare i dati valutati in un set di dati

Dopo aver creato il processo di segmentazione una tantum o la pianificazione continua, puoi esportare i risultati creando un processo di esportazione del segmento. Un processo di esportazione di segmenti è un’attività asincrona che invia informazioni sul pubblico valutato a un set di dati.

Prima di creare un processo di esportazione, devi creare un set di dati in cui esportare i dati. Per informazioni su come creare un set di dati, leggi la sezione sulla [creazione di un set di dati di destinazione](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) nell&#39;esercitazione sulla valutazione di un segmento, assicurandoti di prendere nota dell&#39;ID del set di dati dopo la creazione. Dopo aver creato un set di dati, puoi creare un processo di esportazione. Per informazioni su come creare un processo di esportazione, seguire le istruzioni contenute nella guida API sull&#39;[endpoint per processi di esportazione](../segmentation/api/export-jobs.md).

### Esportare i dati valutati in una destinazione

In alternativa, dopo aver creato il processo di segmentazione una tantum o la pianificazione in corso, puoi esportare i risultati in una destinazione. Una destinazione è un endpoint, ad esempio un’applicazione Adobe su un servizio esterno, in cui è possibile attivare e distribuire un pubblico. Un elenco completo delle destinazioni disponibili si trova nel [catalogo delle destinazioni](../destinations/catalog/overview.md).

Per istruzioni su come attivare i dati nelle destinazioni di marketing in batch o tramite e-mail, consulta il tutorial su [come attivare i dati del pubblico nelle destinazioni di esportazione dei profili in batch utilizzando l&#39;interfaccia utente di Experience Platform](../destinations/ui/activate-batch-profile-destinations.md) e la [guida su come connettersi alle destinazioni in batch e attivare i dati utilizzando l&#39;API del servizio Flusso](../destinations/api/connect-activate-batch-destinations.md).

## Monitorare le attività di dati in Experience Platform

Experience Platform consente di monitorare il modo in cui i dati vengono elaborati attraverso l’utilizzo dei flussi di dati, che sono rappresentazioni di processi che spostano i dati tra i vari componenti di Experience Platform. Questi flussi di dati sono configurati tra servizi diversi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono utilizzati da [!DNL Identity Service] e [!DNL Real-Time Customer Profile] prima di essere infine attivati nelle destinazioni. La dashboard di monitoraggio fornisce una rappresentazione visiva del percorso di un flusso di dati. Per informazioni su come monitorare i flussi di dati nell&#39;interfaccia utente di Experience Platform, consulta le esercitazioni su [flussi di dati di monitoraggio per origini](../dataflows/ui/monitor-sources.md) e [flussi di dati di monitoraggio per destinazioni](../dataflows/ui/monitor-destinations.md).

È inoltre possibile monitorare le attività di Experience Platform utilizzando metriche statistiche e notifiche di eventi utilizzando [!DNL Observability Insights]. Puoi abbonarti alle notifiche di avviso tramite l’interfaccia utente di Experience Platform o inviarle a un webhook configurato. Per ulteriori dettagli su come visualizzare, abilitare, disabilitare e sottoscrivere gli avvisi disponibili dall&#39;interfaccia utente di Experience Platform, consulta la [[!UICONTROL Guida dell&#39;interfaccia utente Avvisi]](../observability/alerts/ui.md). Per informazioni dettagliate su come ricevere gli avvisi tramite i webhook, consulta la guida su [abbonamento alle notifiche degli eventi di Adobe I/O](../observability/alerts/subscribe.md).

## Passaggi successivi

Dopo aver letto questa esercitazione, riceverai un’introduzione di base a un semplice flusso end-to-end per Experience Platform. Per ulteriori informazioni su Adobe Experience Platform, leggere la [panoramica di Experience Platform](./home.md). Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente di Experience Platform e dell&#39;API di Experience Platform, leggere rispettivamente la [guida dell&#39;interfaccia utente di Experience Platform](./ui-guide.md) e la [guida dell&#39;API di Experience Platform](./api-guide.md).
