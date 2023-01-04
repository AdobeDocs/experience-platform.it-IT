---
keywords: Experience Platform;home;argomenti popolari;CJA;analisi dei percorsi;analisi dei percorsi dei clienti;orchestrazione della campagna;orchestrazione;percorso cliente;percorso;orchestrazione percorso;funzionalità;area geografica
title: Flusso di lavoro di esempio end-to-end di Adobe Experience Platform
topic-legacy: getting started
description: Scopri il flusso di lavoro end-to-end di base per Adobe Experience Platform ad alto livello.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 3%

---

# Flusso di lavoro di esempio end-to-end di Adobe Experience Platform

Adobe Experience Platform è il sistema più potente, flessibile e aperto sul mercato per la creazione e la gestione di soluzioni complete che guidano la customer experience. Platform consente alle organizzazioni di centralizzare e standardizzare i dati e i contenuti dei clienti da qualsiasi sistema, e di applicare tecniche di data science e apprendimento automatico al fine di migliorare la progettazione e la consegna di esperienze personalizzate.

Basata sulle API RESTful, Platform espone agli sviluppatori la piena funzionalità del sistema, sostenendo la facile integrazione delle soluzioni aziendali utilizzando strumenti familiari. Platform consente di ottenere una visione olistica dei clienti acquisendo i dati dei clienti, segmentando i dati per i tipi di pubblico di cui desideri eseguire il targeting e attivando tali tipi di pubblico in una destinazione esterna. L’esercitazione seguente mostra un flusso di lavoro end-to-end , che mostra tutti i passaggi dall’acquisizione tramite origini all’attivazione del pubblico tramite destinazioni.

![Flusso di lavoro end-to-end di Experience Platform](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Introduzione

Questo flusso di lavoro end-to-end utilizza più servizi Adobe Experience Platform. Di seguito è riportato un elenco dei servizi utilizzati in questo flusso di lavoro con collegamenti alle relative panoramiche:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience. Per utilizzare al meglio la segmentazione, assicurati che i tuoi dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): Offre una visione completa dei clienti e del loro comportamento attraverso il collegamento di identità tra dispositivi e sistemi.
- [Origini](../sources/home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] consente di dividere i dati memorizzati in [!DNL Experience Platform] che si riferisce a singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in gruppi più piccoli.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Set di dati](../catalog/datasets/overview.md): Il costrutto di archiviazione e gestione per la persistenza dei dati in [!DNL Experience Platform].
- [Destinazioni](../destinations/home.md): Le destinazioni sono integrazioni predefinite con applicazioni comunemente utilizzate che consentono l’attivazione senza soluzione di continuità dei dati da Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

## Creare uno schema XDM

Prima di inserire i dati in Platform, devi innanzitutto creare uno schema XDM per descrivere la struttura di tali dati. Quando trasferisci i dati nel passaggio successivo, mapperai i dati in arrivo a questo schema. Per scoprire come creare uno schema XDM di esempio, leggi l’esercitazione su [creazione di uno schema tramite l’Editor di schema](../xdm/tutorials/create-schema-ui.md).

L’esercitazione precedente mostra come impostare i campi di identità per gli schemi. Un campo di identità rappresenta un campo che può essere utilizzato per identificare una singola persona correlata a un record o a un evento della serie temporale. I campi di identità sono un componente fondamentale per la creazione dei grafici di identità del cliente in Platform, che in ultima analisi influisce sul modo in cui il profilo del cliente in tempo reale unisce diversi frammenti di dati per ottenere una visione completa del cliente. Per ulteriori dettagli su come visualizzare i grafici di identità in Platform, consulta l’esercitazione su [come utilizzare il visualizzatore grafico dell’identità](../identity-service/ui/identity-graph-viewer.md).

Devi abilitare lo schema per l’utilizzo nel Profilo cliente in tempo reale in modo che i profili cliente possano essere costruiti a partire dai dati in base allo schema. Vedi la sezione su [abilitazione di uno schema per il profilo](../xdm/ui/resources/schemas.md#profile) per ulteriori informazioni, consulta la guida dell’interfaccia utente di schemas .

## Inserire i dati in Platform

Dopo aver creato uno schema XDM, puoi iniziare a inserire i dati nel sistema.

Tutti i dati inseriti in Platform vengono memorizzati in singoli set di dati al momento dell’acquisizione. Un set di dati è una raccolta di record di dati da associare a uno schema XDM specifico. Prima che i dati possano essere utilizzati da [!DNL Real-Time Customer Profile], il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete su come abilitare un set di dati per Profilo, consulta la [Guida all’interfaccia utente dei set di dati](../catalog/datasets/user-guide.md#enable-profile) e [esercitazione API per la configurazione dei set di dati](../profile/tutorials/dataset-configuration.md). Una volta configurato il set di dati, puoi iniziare a assimilarvi i dati.

Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archivi basati su cloud, database e molte altre. Ad esempio, puoi acquisire i dati utilizzando [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Un elenco completo delle fonti disponibili è disponibile nella sezione [panoramica dei connettori sorgente](../sources/home.md).

Se utilizzi Amazon S3 come connettore di origine, puoi seguire le istruzioni contenute nell’esercitazione API su [creazione di un connettore Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) o l’esercitazione sull’interfaccia utente [creazione di un connettore Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) per scoprire come creare, connettersi e acquisire dati all’interno del connettore.

Per istruzioni più dettagliate sui connettori sorgente, leggere il [panoramica dei connettori sorgente](../sources/home.md). Per ulteriori informazioni sul servizio Flusso, sull’API basata sulle origini, consulta la sezione [Riferimento API del servizio di flusso](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Una volta portati i dati in Platform tramite il connettore di origine e memorizzati nel set di dati abilitato per il profilo, i profili dei clienti vengono creati automaticamente in base ai dati di identità configurati nello schema XDM.

Quando carichi i dati in un nuovo set di dati per la prima volta o quando configuri un nuovo processo ETL o una nuova origine dati, è consigliabile controllare attentamente i dati per assicurarsi che siano stati caricati correttamente e che i profili generati contengano i dati previsti. Per ulteriori informazioni su come accedere ai profili dei clienti nell’interfaccia utente di Platform, consulta [Guida all’interfaccia utente del profilo cliente in tempo reale](../profile/ui/user-guide.md). Per i dettagli su come accedere ai profili utilizzando l’API del profilo cliente in tempo reale, consulta la guida su [utilizzo dell’endpoint entità](../profile/api/entities.md).

## Valutare i dati

Dopo aver generato correttamente i profili dai dati acquisiti, puoi valutare i dati utilizzando la segmentazione. La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di individui dal tuo profilo store, al fine di distinguere un gruppo di persone commerciabili dalla tua base di clienti. Per ulteriori informazioni sulla segmentazione, consulta la sezione [panoramica del servizio di segmentazione](../segmentation/home.md).

### Creare una definizione di segmento

Per iniziare, devi creare una definizione di segmento per cluster i clienti e creare il pubblico di destinazione. Una definizione di segmento è una raccolta di regole che puoi utilizzare per definire il pubblico a cui desideri rivolgerti. Per creare una definizione di segmento, puoi seguire le istruzioni contenute nella guida dell’interfaccia utente su come utilizzare il [Generatore di segmenti](../segmentation/ui/segment-builder.md) o l’esercitazione API su [creazione di un segmento](../segmentation/tutorials/create-a-segment.md).

Dopo aver creato una definizione di segmento, accertati di tenere nota dell’ID di definizione del segmento.

### Valutare la definizione del segmento

Dopo aver creato la definizione del segmento, puoi creare un processo di segmento per valutare il segmento come un’istanza una tantum oppure creare una pianificazione per valutare il segmento su base continuativa.

Per valutare una definizione di segmento su richiesta, è possibile creare un processo di segmento. Un processo di segmento è un processo asincrono che crea un nuovo segmento di pubblico in base alla definizione del segmento e ai criteri di unione indicati. Un criterio di unione è un insieme di regole utilizzato da Platform per determinare quali dati verranno utilizzati per creare profili cliente e quali dati saranno classificati come prioritari in caso di discrepanze tra le origini. Per informazioni su come utilizzare i criteri di unione, vedere [guida all’interfaccia utente per i criteri di unione](../profile/merge-policies/ui-guide.md).

Una volta creato e valutato il processo del segmento, puoi ottenere informazioni sul segmento, ad esempio le dimensioni del pubblico o gli errori che potrebbero essersi verificati durante l’elaborazione. Per informazioni su come creare un processo di segmento, compresi tutti i dettagli necessari, consulta la sezione [guida per gli sviluppatori di segmenti](../segmentation/api/segment-jobs.md).

Per valutare una definizione di segmento su base continuativa, puoi creare e abilitare una pianificazione. Una pianificazione è uno strumento che può essere utilizzato per eseguire automaticamente un lavoro di segmento una volta al giorno a un&#39;ora specificata. Per scoprire come creare e abilitare una pianificazione, segui le istruzioni contenute nella guida API nella sezione [endpoint di programmazione](../segmentation/api/schedules.md).

## Esportare i dati valutati

Dopo aver creato il processo di segmento una tantum o la pianificazione in corso, puoi creare un processo di esportazione del segmento per esportare i risultati in un set di dati o esportare i risultati in una destinazione. Le sezioni seguenti forniscono indicazioni su entrambe queste opzioni.

### Esportare i dati valutati in un set di dati

Dopo aver creato il processo di segmento una tantum o la pianificazione in corso, puoi esportare i risultati creando un processo di esportazione del segmento. Un processo di esportazione dei segmenti è un’attività asincrona che invia informazioni sul pubblico valutato a un set di dati.

Prima di creare un processo di esportazione, è necessario creare un set di dati in cui esportare i dati. Per scoprire come creare un set di dati, leggi la sezione su [creazione di un set di dati di destinazione](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) nell’esercitazione sulla valutazione di un segmento, accertati di notare l’ID del set di dati dopo la creazione. Dopo aver creato un set di dati, puoi creare un processo di esportazione. Per scoprire come creare un processo di esportazione, segui le istruzioni contenute nella guida API nella sezione [endpoint dei processi di esportazione](../segmentation/api/export-jobs.md).

### Esportare i dati valutati in una destinazione

In alternativa, dopo aver creato un processo di segmento una tantum o la pianificazione in corso, puoi esportare i risultati in una destinazione. Una destinazione è un endpoint, ad esempio un’applicazione Adobe su un servizio esterno, in cui un pubblico può essere attivato e consegnato. Un elenco completo delle destinazioni disponibili è disponibile nella sezione [catalogo delle destinazioni](../destinations/catalog/overview.md).

Per istruzioni su come attivare dati su destinazioni di marketing in batch o tramite e-mail, consulta l’esercitazione su [come attivare i dati del pubblico per le destinazioni di esportazione di profili in batch utilizzando l’interfaccia utente di Platform](../destinations/ui/activate-batch-profile-destinations.md) e [guida su come connettersi alle destinazioni batch e attivare i dati utilizzando l’API del servizio di flusso](../destinations/api/connect-activate-batch-destinations.md).

## Monitorare le attività relative ai dati di Platform

Platform consente di monitorare il modo in cui i dati vengono elaborati tramite l’uso di flussi di dati, che sono rappresentazioni di processi che spostano i dati tra i vari componenti di Platform. Questi flussi di dati sono configurati tra diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono quindi utilizzati da [!DNL Identity Service] e [!DNL Real-Time Customer Profile] prima di essere infine attivato nelle destinazioni. Il dashboard di monitoraggio fornisce una rappresentazione visiva del percorso di un flusso di dati. Per informazioni su come monitorare i flussi di dati nell’interfaccia utente di Platform, consulta le esercitazioni su [monitoraggio dei flussi di dati per le origini](../dataflows/ui/monitor-sources.md) e [monitoraggio dei flussi di dati per le destinazioni](../dataflows/ui/monitor-destinations.md).

Puoi anche monitorare le attività di Platform utilizzando le metriche statistiche e le notifiche degli eventi utilizzando [!DNL Observability Insights]. Puoi abbonarti alle notifiche di avviso tramite l’interfaccia utente di Platform o inviarle a un webhook configurato. Per ulteriori dettagli su come visualizzare, abilitare, disabilitare e sottoscrivere gli avvisi disponibili nell’interfaccia utente di Experience Platform, consulta la sezione [[!UICONTROL Avvisi] Guida all’interfaccia utente](../observability/alerts/ui.md). Per informazioni dettagliate su come ricevere avvisi tramite i webhook, consulta la guida su [sottoscrizione ad Adobi I/O notifiche evento](../observability/alerts/subscribe.md).

## Passaggi successivi

Leggendo questa esercitazione, ti è stata fornita un’introduzione di base a un flusso end-to-end semplice per Platform. Per ulteriori informazioni su Adobe Experience Platform, consulta la sezione [Panoramica di Platform](./home.md). Per ulteriori informazioni sull’utilizzo dell’interfaccia utente di Platform e dell’API di Platform, consulta la sezione [Guida all’interfaccia utente di Platform](./ui-guide.md) e [Guida all’API di Platform](./api-guide.md) rispettivamente.
