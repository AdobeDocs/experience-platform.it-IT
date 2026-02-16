---
description: Scopri come verificare e risolvere i problemi relativi ai processi di elaborazione batch pianificati utilizzando lo strumento Pianificazioni processi in Adobe Experience Platform.
solution: Experience Platform
title: Controlla gli Schedules per i Processi
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 1%

---


# Verifica pianificazioni processi

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] sono attualmente disponibili come versione limitata e solo per i seguenti processi Real-Time CDP:
>
> * Acquisizione di un data lake batch
> * Acquisizione profilo batch
> * Segmentazione batch
> * Attivazione della destinazione batch.

[!UICONTROL Job Schedules] fornisce una visualizzazione unificata di tutti i processi di elaborazione batch pianificati nella pipeline di dati, dall&#39;acquisizione all&#39;attivazione della destinazione. Esaminare lo stato di esecuzione, identificare i conflitti di pianificazione e diagnosticare i problemi di configurazione prima che influiscano sulle operazioni aziendali.

Utilizza le pianificazioni dei processi per analizzare gli errori, ottimizzare la tempistica dei processi e comprendere le dipendenze tra l’acquisizione del data lake, l’elaborazione del profilo, la segmentazione e l’attivazione della destinazione. Per informazioni sulla risoluzione dei problemi di configurazione comuni, consulta la documentazione su [identificazione degli anti-pattern di pianificazione dei processi](job-schedules-anti-patterns.md).

## Prerequisiti {#prerequisites}

Per accedere a [!UICONTROL Job Schedules], sono necessarie le **[!UICONTROL View Job Schedules]** e le **[!UICONTROL View Profile Management]** [autorizzazioni di controllo dell&#39;accesso](/help/access-control/home.md#permissions).

Contatta l’amministratore di sistema per assicurarti di disporre delle autorizzazioni appropriate.

## Guida introduttiva {#getting-started}

Prima di utilizzare [!UICONTROL Job Schedules], è necessario avere familiarità con i seguenti concetti di Experience Platform:

* **[Acquisizione batch](../ingestion/batch-ingestion/overview.md)**: modo in cui i dati vengono caricati nel data lake e nell&#39;archivio profili a intervalli pianificati.
* **[Segmentazione](../segmentation/home.md)**: come vengono valutati e aggiornati i tipi di pubblico in base ai dati di profilo e alle definizioni dei segmenti.
* **[Profilo cliente in tempo reale](../profile/home.md)**: unificazione e disponibilità dei dati del profilo per segmentazione e attivazione.
* **[Destinazioni](../destinations/home.md)**: dove e come i dati vengono attivati nei sistemi a valle e nelle piattaforme di marketing.

Comprendere questi componenti consente di interpretare i modelli di esecuzione dei processi e diagnosticare i problemi quando si verificano.

## Informazioni sull’interfaccia Schedules per i job {#understanding-interface}

Per accedere a [!UICONTROL Job Schedules]:

1. Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Run and Operate]** dal menu di navigazione a sinistra.
2. Seleziona **[!UICONTROL Job Schedules]**.

La pagina [!UICONTROL Job Schedules] fornisce una panoramica di tutti i processi di elaborazione batch pianificati.

![Navigazione a sinistra](assets/job-schedules/run-and-operate-left-nav.png)

### Schede di riepilogo {#summary-cards}

Nella parte superiore della pagina sono disponibili schede di riepilogo che forniscono informazioni rapide sui processi di elaborazione batch.

![Schede di riepilogo Pianificazioni processi che mostrano informazioni approfondite sui processi di elaborazione batch](assets/job-schedules/job-schedules-cards.png)

* **Esecuzioni dell&#39;acquisizione del data lake**: numero di processi di acquisizione del data lake eseguiti.
* **L&#39;acquisizione del profilo viene eseguita**: numero di processi di acquisizione del profilo eseguiti.
* **Segmentazione successiva**: quando verrà eseguito il successivo processo di segmentazione pianificato.
* **Attivazione destinazione successiva**: quando verrà eseguito il successivo processo di attivazione della destinazione pianificata.

Queste schede ti aiutano a comprendere l’attività e le pianificazioni future per la pipeline di dati. I valori per **esecuzioni dell&#39;acquisizione del lago** e **esecuzioni dell&#39;acquisizione del profilo** cambiano in base all&#39;intervallo di tempo selezionato (oggi, ieri o ultimi 7 giorni); le schede dell&#39;esecuzione successiva (**Segmentazione successiva** e **Attivazione successiva della destinazione**) non sono interessate dal selettore dell&#39;ora.

### Selettore periodo di tempo {#time-period}

Utilizza i selettori del periodo di tempo per scegliere quanto indietro nel tempo per esaminare i processi pianificati.

![Esempio animato dell&#39;interfaccia utente del selettore del periodo di tempo nelle pianificazioni processi](assets/job-schedules/time-selector.gif)

* **Oggi**: visualizza i processi pianificati per oggi (visualizzazione predefinita).
* **Ieri**: visualizza i processi eseguiti ieri.
* **Ultimi 7 giorni**: visualizza i processi della settimana scorsa.

### Dettagli pianificazioni processi batch {#job-schedules-details}

La visualizzazione principale mostra quando i processi batch sono programmati per l&#39;esecuzione nel corso della giornata. Puoi eseguire le seguenti operazioni:

* **Visualizza processi per set di dati o entità**: la colonna a sinistra mostra i nomi dei set di dati o dei processi di elaborazione (ad esempio, set di dati di acquisizione o processi di segmentazione).
* **Visualizza tempistica processo**: la timeline mostra quando è pianificata l&#39;esecuzione di ciascun processo, con indicatori visivi che indicano l&#39;ora pianificata.
* **Processi filtro**: utilizza l&#39;icona del filtro per limitare i set di dati da includere nel rapporto.
* **Comprendere i tipi di processo**: la legenda con codice colore nella parte inferiore consente di identificare diversi tipi di processo:
   * **Acquisizione lago** (verde): acquisizione di dati nel data lake
   * **Acquisizione profilo** (rosa): acquisizione dati nell&#39;archivio profili
   * **Segmentazione** (azzurro): processi di valutazione del pubblico
   * **Esportazione profilo** (blu): esportazione di dati profilo
   * **Attivazione** (grigio scuro): processi di attivazione della destinazione
   * **In corso** (con striping): processi attualmente in esecuzione o in coda

Questa visualizzazione della sequenza temporale consente di identificare i conflitti di programmazione, comprendere le dipendenze tra i processi e ottimizzare i programmi di elaborazione batch.

## Identificazione dei problemi di configurazione {#identifying-issues}

Durante l&#39;esame delle pianificazioni dei processi, è possibile che si notino modelli che indicano problemi di configurazione. I problemi comuni includono:

* Processi pianificati troppo vicini tra loro, causando conflitti di risorse
* Troppi batch in esecuzione nella stessa finestra temporale
* Singoli set di dati con processi batch giornalieri eccessivi
* Processi di acquisizione pianificati immediatamente prima dell’esecuzione della segmentazione

Questi pattern possono causare errori di processo, elaborazione incompleta dei dati e prestazioni di sistema insoddisfacenti. Per informazioni su come identificare e risolvere questi problemi, consulta la documentazione su [identificazione degli anti-pattern di pianificazione dei processi](job-schedules-anti-patterns.md).

Quando devi analizzare set di dati o esecuzioni di processi specifici, puoi approfondire le viste dettagliate per visualizzare la cronologia di esecuzione, i messaggi di errore, le metriche delle prestazioni e le dipendenze. Per informazioni sulla visualizzazione di questi dati dettagliati, consulta la documentazione su [visualizzazione dei dettagli del processo](job-schedules-details.md).


## Passaggi successivi {#next-steps}

Dopo aver appreso le pianificazioni dei processi, puoi esplorare i seguenti argomenti correlati:

* [Visualizza dettagli processo](job-schedules-details.md): scopri come espandere singoli set di dati ed eseguire processi per un&#39;indagine dettagliata.
* [Identifica gli anti-pattern della pianificazione dei processi](job-schedules-anti-patterns.md): scopri come individuare e risolvere i problemi di configurazione comuni che influiscono sulle prestazioni della pipeline.
* [Acquisizione batch](../ingestion/batch-ingestion/overview.md): scopri come acquisire dati in Experience Platform utilizzando l&#39;elaborazione batch.
* [Segmentazione](../segmentation/home.md): scopri come i tipi di pubblico vengono valutati e aggiornati a intervalli pianificati.
* [Monitorare i flussi di dati per le destinazioni](../dataflows/ui/monitor-destinations.md): scopri come monitorare i flussi di dati di attivazione delle destinazioni.
* [Pianifica esportazioni pubblico](../destinations/ui/activate-batch-profile-destinations.md): scopri come configurare le attivazioni delle destinazioni batch pianificate.
