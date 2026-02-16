---
title: Panoramica sull’esecuzione e l’utilizzo
description: Ispeziona, risolvi i problemi e ottimizza le implementazioni Adobe Experience Platform con gli strumenti Esegui e opera. Ottieni visibilità sulle attivazioni batch pianificate, identifica i problemi di configurazione e migliora l’affidabilità del sistema.
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 1%

---


# Panoramica sull’esecuzione e l’utilizzo

>[!AVAILABILITY]
>
>Le funzioni di esecuzione e funzionamento sono attualmente disponibili come versione limitata.

Quando i processi batch non riescono o forniscono dati incompleti, è necessario comprendere rapidamente la causa del problema. La causa principale potrebbe essere rappresentata da problemi di disponibilità dei dati, tempi non corretti, problemi di configurazione o vincoli di capacità del sistema. Senza una chiara visibilità, è possibile dedicare ore ad analizzare più sistemi prima di trovare la risposta.

Con [!UICONTROL Run and Operate] strumenti, puoi:

* **Verifica le operazioni sui dati**: ottieni una visualizzazione completa dello stato e dell&#39;integrità dell&#39;esecuzione dei processi in tutti i tuoi flussi di lavoro.
* **Risolvere i problemi più rapidamente**: accedere a informazioni di diagnostica dettagliate e alla cronologia di esecuzione per identificare rapidamente le cause principali e ridurre il tempo medio di risoluzione.
* **Previeni i problemi in modo proattivo**: analizza i modelli di processo, rileva i problemi di configurazione prima che causino errori e ottimizza le operazioni sui dati.

## Tipi di pubblico di destinazione {#target-audiences}

Gli strumenti [!UICONTROL Run and Operate] sono progettati per servire più tipi di pubblico in tutta l&#39;organizzazione:

* **Team di dati e IT**: amministratori di sistema e data engineer che gestiscono pipeline di dati affidabili e risolvono problemi tecnici.
* **Operazioni di marketing**: tecnici di marketing che controllano la distribuzione dei dati alle piattaforme di marketing e risolvono i problemi di attivazione.
* **Implementatori**: professionisti che convalidano l&#39;efficienza dell&#39;implementazione, l&#39;affidabilità e la risoluzione dei problemi tecnici.

## Prerequisiti {#prerequisites}

Per accedere agli strumenti di esecuzione e gestione, sono necessarie le **[!UICONTROL View Job Schedules]** e **[!UICONTROL View Profile Management]** [autorizzazioni di controllo dell&#39;accesso](/help/access-control/home.md#permissions).
La pagina [!UICONTROL Job Schedules] fornisce una panoramica di tutti i processi di elaborazione batch pianificati.
Contatta l’amministratore di sistema per assicurarti di disporre delle autorizzazioni appropriate.

## Guida introduttiva {#getting-started}

Per accedere agli strumenti Esegui e utilizza dall’interfaccia utente di Experience Platform:

1. Accedi al tuo account Experience Platform e seleziona **[!UICONTROL Run and Operate]** dal menu di navigazione a sinistra.
2. Selezionare lo strumento corrispondente alle proprie esigenze di ispezione o risoluzione dei problemi.

   >[!NOTE]
   >
   >Attualmente, l&#39;unica funzionalità disponibile è [Pianificazioni processi](job-schedules.md).

![Interfaccia utente di Experience Platform con barra di spostamento a sinistra Esegui e opera.](assets/overview/run-and-operate.png)

## Strumenti disponibili {#available-tools}

I seguenti strumenti consentono di controllare e ottimizzare le operazioni sui dati.

### Pianificazioni processi {#job-schedules}

>[!IMPORTANT]
>
>[!UICONTROL Job schedules] sono attualmente disponibili solo per i seguenti processi Real-Time CDP:
>
> * Acquisizione di un data lake batch
> * Acquisizione profilo batch
> * Segmentazione batch
> * Attivazione della destinazione batch.

Con [Pianificazioni processi](job-schedules.md), puoi controllare tutte le operazioni batch pianificate nell&#39;organizzazione, per sandbox, incluse l&#39;acquisizione del data lake, l&#39;acquisizione del profilo, la segmentazione e l&#39;attivazione della destinazione. Visualizzare lo stato di esecuzione dei job, le metriche delle prestazioni e la cronologia di esecuzione per identificare i pattern e diagnosticare i problemi di configurazione che influiscono sull&#39;affidabilità.

![Interfaccia utente di Experience Platform che mostra la schermata Pianificazioni processi.](assets/overview/job-schedules-interface.png)

Gli Schedules per i processi forniscono tre livelli di indagine:

* **[Controlla le pianificazioni dei processi](job-schedules.md)**: visualizza tutti i set di dati e i relativi processi pianificati in una sequenza temporale per identificare i pattern e i conflitti di pianificazione nell&#39;intera pipeline.
* **[Identificare gli anti-pattern](job-schedules-anti-patterns.md)**: scopri come individuare e risolvere i problemi di configurazione comuni, come la sovrapposizione della pianificazione, lo stacking di batch densi e l&#39;eccessiva gestione in batch che influiscono sulle prestazioni.
* **[Visualizza dettagli processo](job-schedules-details.md)**: espandere set di dati specifici ed eseguire singoli processi per analizzare gli errori, controllare la tempistica e verificare i record elaborati.

Puoi anche comprendere le dipendenze tra le fasi di elaborazione dei dati, per garantire un flusso di dati affidabile in tutti i flussi di lavoro di Experience Platform.

## Passaggi successivi {#next-steps}

Dopo aver compreso lo scopo e le funzionalità degli strumenti di [!UICONTROL Run and Operate], esplorare le risorse seguenti per approfondire le proprie conoscenze:

* Scopri come [acquisire batch](../ingestion/batch-ingestion/overview.md) per comprendere come vengono acquisiti i dati in Experience Platform
* Scopri come [controllare le pianificazioni dei processi](job-schedules.md) per l&#39;acquisizione e le attivazioni batch
* Scopri come [configurare le attivazioni pianificate](../destinations/ui/activate-batch-profile-destinations.md) per le destinazioni batch
* Esplora [monitoraggio del flusso di dati](../dataflows/ui/monitor-destinations.md) per le destinazioni

