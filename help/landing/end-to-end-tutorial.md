---
keywords: Experience Platform;home;argomenti popolari;CJA;analisi percorso;analisi percorso clienti;orchestrazione campagna;orchestrazione;percorso clienti;percorso;orchestrazione percorso;capacità;area geografica
title: Flusso di lavoro di esempio end-to-end di Adobe Experience Platform
description: Scopri ad alto livello il flusso di lavoro end-to-end di base per Adobe Experience Platform.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 1%

---

# Flusso di lavoro di esempio end-to-end di Adobe Experience Platform

Adobe Experience Platform è il sistema più potente, flessibile e aperto sul mercato per la creazione e la gestione di soluzioni complete che guidano la customer experience. Platform consente alle organizzazioni di centralizzare e standardizzare i dati e i contenuti dei clienti da qualsiasi sistema, e di applicare tecniche di data science e apprendimento automatico al fine di migliorare la progettazione e la consegna di esperienze personalizzate.

Basata sulle API RESTful, Platform espone agli sviluppatori la piena funzionalità del sistema, supportando la facile integrazione di soluzioni aziendali tramite strumenti familiari. Platform consente di ottenere una visione olistica dei clienti acquisendo i dati dei clienti, segmentando i dati per i tipi di pubblico desiderati e attivando tali tipi di pubblico in una destinazione esterna. L’esercitazione seguente mostra un flusso di lavoro end-to-end, con tutti i passaggi dall’acquisizione tramite origini all’attivazione tramite destinazioni.

![Experience Platform di flusso di lavoro end-to-end](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Introduzione

Questo flusso di lavoro end-to-end utilizza più servizi Adobe Experience Platform. Di seguito è riportato un elenco dei servizi utilizzati in questo flusso di lavoro con collegamenti alle relative panoramiche:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): offre una visione completa dei clienti e del loro comportamento, collegando le identità tra dispositivi e sistemi diversi.
- [Sorgenti](../sources/home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] consente di suddividere i dati memorizzati in [!DNL Experience Platform] che si riferisce a singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in gruppi più piccoli.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Set di dati](../catalog/datasets/overview.md): costrutto di archiviazione e gestione per la persistenza dei dati in [!DNL Experience Platform].
- [Destinazioni](../destinations/home.md): le destinazioni sono integrazioni predefinite con applicazioni di uso comune che consentono l’attivazione diretta dei dati da Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

## Creare uno schema XDM

Prima di acquisire i dati in Platform, è necessario creare uno schema XDM per descrivere la struttura di tali dati. Quando acquisisci i dati nel passaggio successivo, mapperai i dati in arrivo su questo schema. Per scoprire come creare un esempio di schema XDM, leggi l’esercitazione su [creazione di uno schema tramite l’Editor di schema](../xdm/tutorials/create-schema-ui.md).

L’esercitazione precedente mostra come impostare i campi di identità per gli schemi. Un campo di identità rappresenta un campo che può essere utilizzato per identificare una singola persona correlata a un record o a un evento di serie temporale. I campi di identità sono un componente fondamentale della costruzione dei grafici di identità del cliente in Platform, che influisce in ultima analisi sul modo in cui Real-Time Customer Profile unisce frammenti di dati diversi per ottenere una visualizzazione completa del cliente. Per ulteriori dettagli su come visualizzare i grafici delle identità in Platform, consulta l’esercitazione su [come utilizzare il visualizzatore del grafico delle identità](../identity-service/features/identity-graph-viewer.md).

Devi abilitare lo schema per l’utilizzo in Real-Time Customer Profile in modo che i profili dei clienti possano essere costruiti dai dati in base allo schema. Consulta la sezione su [abilitazione di uno schema per il profilo](../xdm/ui/resources/schemas.md#profile) nella guida dell’interfaccia utente degli schemi per ulteriori informazioni.

## Inserire i dati in Platform

Dopo aver creato uno schema XDM, puoi iniziare a inserire i dati nel sistema.

Tutti i dati introdotti in Platform vengono memorizzati in singoli set di dati al momento dell’acquisizione. Un set di dati è una raccolta di record di dati mappati a uno schema XDM specifico. Prima che i dati possano essere utilizzati da [!DNL Real-Time Customer Profile], il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete su come abilitare un set di dati per il profilo, consulta [Guida all’interfaccia utente dei set di dati](../catalog/datasets/user-guide.md#enable-profile) e [tutorial sull’API per la configurazione del set di dati](../profile/tutorials/dataset-configuration.md). Una volta configurato il set di dati, puoi iniziare a acquisirvi i dati.

Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archivi basati su cloud, database e molte altre. Ad esempio, puoi acquisire i dati utilizzando [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Un elenco completo delle fonti disponibili è disponibile nella [panoramica dei connettori di origini](../sources/home.md).

Se utilizzi Amazon S3 come connettore di origine, puoi seguire le istruzioni contenute nell’esercitazione API su [creazione di un connettore Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) oppure il tutorial sull’interfaccia utente su [creazione di un connettore Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) per scoprire come creare, connettersi e acquisire dati all’interno del connettore.

Per istruzioni più dettagliate sui connettori di origine, leggere [panoramica dei connettori di origini](../sources/home.md). Per ulteriori informazioni su Flow Service, l’API da cui si basano le sorgenti, leggi la sezione [Riferimento API del servizio Flusso](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Una volta che i dati vengono introdotti in Platform tramite il connettore di origine e memorizzati nel set di dati abilitato per il profilo, i profili cliente vengono creati automaticamente in base ai dati di identità configurati nello schema XDM.

Quando si caricano dati in un nuovo set di dati per la prima volta o quando si imposta un nuovo processo ETL o una nuova origine dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati correttamente e che i profili generati contengano i dati previsti. Per ulteriori informazioni su come accedere ai profili dei clienti nell’interfaccia utente di Platform, consulta [Guida all’interfaccia utente del profilo cliente in tempo reale](../profile/ui/user-guide.md). Per informazioni dettagliate su come accedere ai profili utilizzando l’API Real-Time Customer Profile, consulta la guida su [utilizzo dell’endpoint delle entità](../profile/api/entities.md).

## Valutare i dati

Dopo aver generato correttamente i profili dai dati acquisiti, puoi valutare i dati utilizzando la segmentazione. La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di singoli utenti dell’archivio dei profili, al fine di distinguere un gruppo commerciabile di persone dalla base dei clienti. Per ulteriori informazioni sulla segmentazione, consulta la sezione [panoramica del servizio di segmentazione](../segmentation/home.md).

### Creare una definizione di segmento

Per iniziare, devi creare una definizione del segmento per raggruppare i clienti e creare il pubblico di destinazione. Una definizione di segmento è una raccolta di regole che puoi utilizzare per definire il pubblico di destinazione. Per creare una definizione di segmento, puoi seguire le istruzioni contenute nella guida dell’interfaccia utente per l’utilizzo di [Generatore di segmenti](../segmentation/ui/segment-builder.md) o l’esercitazione API su [creazione di un segmento](../segmentation/tutorials/create-a-segment.md).

Dopo aver creato una definizione di segmento, tieni presente l’ID di definizione del segmento.

### Valuta la definizione del segmento

Dopo aver creato la definizione del segmento, puoi creare un processo per il segmento per valutarlo come istanza unica oppure puoi creare una pianificazione per valutare il segmento su base continuativa.

Per valutare una definizione di segmento su richiesta, puoi creare un processo di segmentazione. Un processo di segmentazione è un processo asincrono che crea un nuovo segmento di pubblico basato sulla definizione del segmento e sui criteri di unione di cui si fa riferimento. Un criterio di unione è un insieme di regole che Platform utilizza per determinare quali dati verranno utilizzati per creare i profili dei clienti e quali dati avranno priorità in caso di discrepanze tra origini. Per informazioni su come utilizzare i criteri di unione, vedi [guida dell’interfaccia utente per i criteri di unione](../profile/merge-policies/ui-guide.md).

Una volta creato e valutato il processo di segmentazione, puoi ottenere informazioni sul segmento, ad esempio le dimensioni del pubblico o gli errori che possono essersi verificati durante l’elaborazione. Per informazioni su come creare un processo di segmentazione, inclusi tutti i dettagli da fornire, leggi la sezione [guida per gli sviluppatori di processi di segmenti](../segmentation/api/segment-jobs.md).

Per valutare una definizione di segmento su base continuativa, puoi creare e abilitare una pianificazione. Una pianificazione è uno strumento che può essere utilizzato per eseguire automaticamente un processo di segmentazione una volta al giorno a un’ora specificata. Per scoprire come creare e abilitare una pianificazione, puoi seguire le istruzioni riportate nella guida dell’API nella sezione [pianifica endpoint](../segmentation/api/schedules.md).

## Esportare i dati valutati

Dopo aver creato il processo di segmentazione una tantum o la pianificazione continua, puoi creare un processo di esportazione del segmento per esportare i risultati in un set di dati o esportare i risultati in una destinazione. Le sezioni seguenti forniscono indicazioni su entrambe queste opzioni.

### Esportare i dati valutati in un set di dati

Dopo aver creato il processo di segmentazione una tantum o la pianificazione continua, puoi esportare i risultati creando un processo di esportazione del segmento. Un processo di esportazione di segmenti è un’attività asincrona che invia informazioni sul pubblico valutato a un set di dati.

Prima di creare un processo di esportazione, devi creare un set di dati in cui esportare i dati. Per informazioni su come creare un set di dati, consulta la sezione su [creazione di un set di dati di destinazione](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) nell’esercitazione sulla valutazione di un segmento, assicurandoti di prendere nota dell’ID del set di dati dopo la creazione. Dopo aver creato un set di dati, puoi creare un processo di esportazione. Per informazioni su come creare un processo di esportazione, segui le istruzioni contenute nella guida API su [endpoint processi di esportazione](../segmentation/api/export-jobs.md).

### Esportare i dati valutati in una destinazione

In alternativa, dopo aver creato il processo di segmentazione una tantum o la pianificazione in corso, puoi esportare i risultati in una destinazione. Una destinazione è un endpoint, ad esempio un’applicazione di Adobe su un servizio esterno, in cui è possibile attivare e distribuire un pubblico. Un elenco completo delle destinazioni disponibili è disponibile nella [catalogo delle destinazioni](../destinations/catalog/overview.md).

Per istruzioni su come attivare i dati nelle destinazioni di marketing in batch o tramite e-mail, consulta l’esercitazione su [come attivare i dati sul pubblico nelle destinazioni di esportazione dei profili in batch utilizzando l’interfaccia utente di Platform](../destinations/ui/activate-batch-profile-destinations.md) e [guida su come connettersi alle destinazioni batch e attivare i dati utilizzando l’API del servizio Flusso](../destinations/api/connect-activate-batch-destinations.md).

## Monitorare le attività dati di Platform

Platform consente di monitorare il modo in cui i dati vengono elaborati attraverso l’utilizzo di flussi di dati, che sono rappresentazioni di processi che spostano i dati tra i vari componenti di Platform. Questi flussi di dati sono configurati tra servizi diversi, aiutando a spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono quindi utilizzati da [!DNL Identity Service] e [!DNL Real-Time Customer Profile] prima di essere infine attivato sulle destinazioni. La dashboard di monitoraggio fornisce una rappresentazione visiva del percorso di un flusso di dati. Per informazioni su come monitorare i flussi di dati nell’interfaccia utente di Platform, consulta i tutorial su [monitoraggio dei flussi di dati per le origini](../dataflows/ui/monitor-sources.md) e [monitoraggio dei flussi di dati per le destinazioni](../dataflows/ui/monitor-destinations.md).

Puoi anche monitorare le attività di Platform tramite l’utilizzo di metriche statistiche e notifiche di eventi utilizzando [!DNL Observability Insights]. Puoi abbonarti alle notifiche di avviso tramite l’interfaccia utente di Platform o inviarle a un webhook configurato. Per ulteriori dettagli su come visualizzare, abilitare, disabilitare e sottoscrivere gli avvisi disponibili dall’interfaccia utente di Experienci Platform, vedi [[!UICONTROL Avvisi] Guida all’interfaccia utente](../observability/alerts/ui.md). Per informazioni dettagliate su come ricevere gli avvisi tramite i webhook, consulta la guida su [abbonamento a notifiche Adobe I/O Event](../observability/alerts/subscribe.md).

## Passaggi successivi

Dopo aver letto questa esercitazione, riceverai un’introduzione di base a un semplice flusso end-to-end per Platform. Per ulteriori informazioni su Adobe Experience Platform, leggere [Panoramica della piattaforma](./home.md). Per ulteriori informazioni sull’utilizzo dell’interfaccia utente e dell’API di Platform, consulta la sezione [Guida all’interfaccia utente di Platform](./ui-guide.md) e [Guida all’API di Platform](./api-guide.md) rispettivamente.
