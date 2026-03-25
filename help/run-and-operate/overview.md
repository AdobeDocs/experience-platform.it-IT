---
title: Panoramica sull’esecuzione e l’utilizzo
description: Ispeziona, risolvi i problemi e ottimizza le implementazioni di Experience Platform con gli strumenti Esegui e opera. Ottieni visibilità sulle attivazioni batch pianificate, identifica i problemi di configurazione e migliora l’affidabilità del sistema.
solution: Experience Platform
type: Documentation
role: Admin, User
exl-id: 7f44cdf3-4db1-47f9-bcde-401f6dcfc551
source-git-commit: 41abc542b11dcd9c295d29cdfad68720ad50129d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 2%

---

# Panoramica sull’esecuzione e l’utilizzo

Quando i processi batch non riescono o forniscono dati incompleti, è necessario comprendere rapidamente la causa del problema. La causa principale potrebbe essere rappresentata da problemi di disponibilità dei dati, tempi non corretti, problemi di configurazione o vincoli di capacità del sistema. Senza una chiara visibilità, è possibile dedicare ore ad analizzare più sistemi prima di trovare la risposta.

Con [!UICONTROL Run and Operate] strumenti, puoi:

* **Verifica le operazioni sui dati**: ottieni una visualizzazione completa dello stato e dell&#39;integrità dell&#39;esecuzione dei processi in tutti i tuoi flussi di lavoro.
* **Risolvere i problemi più rapidamente**: accedere a informazioni di diagnostica dettagliate e alla cronologia di esecuzione per identificare rapidamente le cause principali e ridurre il tempo medio di risoluzione.
* **Previeni i problemi in modo proattivo**: analizza i modelli di processo, rileva i problemi di configurazione prima che causino errori e ottimizza le operazioni sui dati.

## Tipi di pubblico di destinazione {#target-audiences}

Gli strumenti [!UICONTROL Run and Operate] sono progettati per servire più tipi di pubblico in tutta l&#39;organizzazione:

* **Team di dati e IT**: amministratori di sistema e data engineer che gestiscono pipeline di dati affidabili e risolvono problemi tecnici.
* **Operazioni di marketing**: tecnici di marketing che controllano la distribuzione dei dati alle piattaforme di marketing e risolvono i problemi di attivazione.
* **Implementatori**: professionisti che convalidano l&#39;efficienza e l&#39;affidabilità dell&#39;implementazione e che risolvono problemi tecnici.

## Prerequisiti {#prerequisites}

Per accedere agli strumenti di esecuzione e gestione, sono necessarie le **[!UICONTROL View Job Schedules]** e **[!UICONTROL View Profile Management]** [autorizzazioni di controllo dell&#39;accesso](/help/access-control/home.md#permissions). Contatta l’amministratore di sistema per assicurarti di disporre delle autorizzazioni appropriate.

## Guida introduttiva {#getting-started}

Per accedere agli strumenti Esegui e utilizza dall’interfaccia utente di Experience Platform:

1. Accedi al tuo account Experience Platform e seleziona **[!UICONTROL Run and Operate]** dal menu di navigazione a sinistra.
2. Selezionare lo strumento corrispondente alle proprie esigenze di ispezione o risoluzione dei problemi.

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
> * Segmentazione in batch
> * Attivazione destinazione batch

Con [Pianificazioni processi](job-schedules.md), puoi controllare tutte le operazioni batch pianificate nell&#39;organizzazione, per sandbox, incluse l&#39;acquisizione del data lake, l&#39;acquisizione del profilo, la segmentazione e l&#39;attivazione della destinazione. Visualizzare lo stato di esecuzione dei job, le metriche delle prestazioni e la cronologia di esecuzione per identificare i pattern e diagnosticare i problemi di configurazione che influiscono sull&#39;affidabilità.

![Interfaccia utente di Experience Platform che mostra la schermata Pianificazioni processi.](assets/overview/job-schedules-interface.png)

Gli Schedules per i processi forniscono tre livelli di indagine:

* **[Controlla le pianificazioni dei processi](job-schedules.md)**: visualizza tutti i set di dati e i relativi processi pianificati in una sequenza temporale per identificare i pattern e i conflitti di pianificazione nell&#39;intera pipeline.
* **[Identificare gli anti-pattern](job-schedules-anti-patterns.md)**: scopri come individuare e risolvere i problemi di configurazione comuni, come la sovrapposizione della pianificazione, lo stacking di batch densi e l&#39;eccessiva gestione in batch che influiscono sulle prestazioni.
* **[Visualizza dettagli processo](job-schedules-details.md)**: espandere set di dati specifici ed eseguire singoli processi per analizzare gli errori, controllare la tempistica e verificare i record elaborati.

Puoi anche comprendere le dipendenze tra le fasi di elaborazione dei dati, per garantire un flusso di dati affidabile in tutti i flussi di lavoro di Experience Platform.

### Verifiche stato {#health-checks}

Con [Verifiche stato](health-checks.md), puoi rilevare in modo proattivo i problemi di configurazione dello schema e dell&#39;identità prima che influiscano sulle operazioni aziendali. Attualmente, i controlli di integrità eseguono scansioni statiche giornaliere tra gli schemi e gli spazi dei nomi delle identità, evidenziando best practice mancanti, configurazioni errate e pattern che portano a errori a valle.

I controlli sanitari valutano attualmente cinque aree fondamentali:

* **[Convalida del campo di identità](health-checks.md#identity-field-validation)**: verificare che la lunghezza e i vincoli del modello dei campi di identità siano corretti.
* **[Regole di collegamento del grafo delle identità](health-checks.md#identity-graph-linking-rules)**: verificare che le regole di collegamento siano configurate in modo da evitare la compressione del profilo.
* **[Configurazione identità persone e non persone](health-checks.md#people-non-people-identity)**: convalida l&#39;utilizzo corretto del tipo di identità tra le classi dello schema.
* **[Descrizione spazio dei nomi identità personalizzato](health-checks.md#namespace-missing-description)**: verificare che i metadati dello spazio dei nomi siano completi.
* **[Spazi dei nomi delle identità obsoleti](health-checks.md#deprecated-namespace)**: rileva spazi dei nomi obsoleti per la pulizia.

## Passaggi successivi {#next-steps}

Dopo aver compreso lo scopo e le funzionalità degli strumenti di [!UICONTROL Run and Operate], esplorare le risorse seguenti per approfondire le proprie conoscenze:

* Scopri come utilizzare [controlli di integrità](health-checks.md) per rilevare problemi di configurazione di schemi e identità
* Scopri come [controllare le pianificazioni dei processi](job-schedules.md) per l&#39;acquisizione e le attivazioni batch
* Scopri come [acquisire batch](../ingestion/batch-ingestion/overview.md) per comprendere come vengono acquisiti i dati in Experience Platform
* Scopri come [configurare le attivazioni pianificate](../destinations/ui/activate-batch-profile-destinations.md) per le destinazioni batch
* Esplora [monitoraggio del flusso di dati](../dataflows/ui/monitor-destinations.md) per le destinazioni
