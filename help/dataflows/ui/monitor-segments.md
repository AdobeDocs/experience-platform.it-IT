---
keywords: Experience Platform;home;argomenti comuni;monitorare segmenti;monitorare flussi di dati;flussi di dati;segmentazione
description: La segmentazione ti consente di creare segmenti e tipi di pubblico dai dati del profilo cliente in tempo reale. Questa esercitazione fornisce istruzioni su come monitorare i flussi di dati durante la segmentazione utilizzando l’interfaccia utente di Experience Platform.
title: Monitorare i flussi di dati per i segmenti nell’interfaccia utente
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 3%

---

# Monitorare i flussi di dati per i segmenti nell’interfaccia utente

Il servizio di segmentazione consente di creare segmenti e tipi di pubblico dai dati del profilo cliente in tempo reale in Adobe Experience Platform. Platform fornisce flussi di dati per monitorare in modo trasparente questo flusso di dati dalle sorgenti alle destinazioni.

Il dashboard di monitoraggio fornisce una rappresentazione visiva dell’attività dei dati all’interno di un segmento, incluso lo stato della segmentazione dei dati. Questa esercitazione fornisce istruzioni su come utilizzare il dashboard di monitoraggio per monitorare la segmentazione dei dati tramite l’interfaccia utente di Experience Platform, consentendo di tenere traccia dello stato dei processi di attivazione, valutazione ed esportazione dei segmenti.

## Introduzione {#getting-started}

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Flussi di dati](../home.md): I flussi di dati sono una rappresentazione dei processi di trasferimento dei dati in Platform. I flussi di dati sono configurati su diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, fino a [!DNL Identity] e [!DNL Profile]e a [!DNL Destinations].
   - [Corse del flusso di dati](../../sources/notifications.md): Le esecuzioni dei flussi di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
- [Segmentazione](../../segmentation/home.md): La segmentazione ti consente di creare segmenti e tipi di pubblico dai dati del profilo cliente in tempo reale.
   - [Processi di attivazione](../../destinations/ui/activation-overview.md): Un processo di attivazione viene utilizzato per attivare il segmento in una destinazione specifica.
   - [Processi di valutazione](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): Un processo di valutazione è un processo asincrono che crea un segmento di pubblico in base al segmento specificato.
   - [Esportare i processi](../../segmentation/api/export-jobs.md): Un processo di esportazione è un processo asincrono utilizzato per persistere i membri del segmento di pubblico nei set di dati.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Dashboard dei segmenti di monitoraggio {#monitoring-segments-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Segmenti"
>abstract="La visualizzazione dei segmenti contiene informazioni su tutti i segmenti dell’organizzazione, con ulteriori informazioni sui processi di attivazione e valutazione."

Per accedere al **[!UICONTROL Segmenti]** dashboard, seleziona **[!UICONTROL Monitoraggio]** nella navigazione a sinistra. Una volta sul **[!UICONTROL Monitoraggio]** , seleziona la **[!UICONTROL Segmenti]** il Card.

![La scheda Segmenti . Vengono visualizzate informazioni sull’ultimo processo di valutazione e sull’ultimo processo di esportazione.](../assets/ui/monitor-segments/segment-card-monitoring.png)

Sul principale **[!UICONTROL Segmenti]** dashboard **[!UICONTROL Segmenti]** la scheda mostra lo stato e la data dell’ultimo processo di valutazione e dell’ultimo processo di esportazione.

Il dashboard stesso contiene metriche per segmenti e processi di segmento. Per impostazione predefinita, il dashboard mostrerà le metriche del segmento per le ultime 24 ore. Per ulteriori informazioni sulla visualizzazione dei processi del segmento, consulta la sezione [monitoraggio dei processi dei segmenti](#monitoring-segment-jobs-dashboard) sezione .

>[!IMPORTANT]
>
>Attualmente, solo i segmenti a cui è stata attivata la [destinazioni batch (basate su file)](../../destinations/destination-types.md#file-based) sono supportate per il dashboard dei segmenti di monitoraggio.

![Dashboard dei segmenti. Vengono visualizzate informazioni sui diversi segmenti nell’organizzazione e nella sandbox.](../assets/ui/monitor-segments/segment-monitoring-dashboard.png)

Per questa vista dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Nome del segmento]** | Nome del segmento. |
| **[!UICONTROL Timestamp ultima valutazione]** | Data e ora dell’esecuzione dell’ultimo processo di valutazione del segmento. |
| **[!UICONTROL Stato dell&#39;ultima valutazione]** | Lo stato dell’ultimo processo di valutazione del segmento. Eventuali valori includono **[!UICONTROL Completato]**, **[!UICONTROL Nessuna esecuzione]** e **[!UICONTROL Non riuscito]**. |
| **[!UICONTROL Ultimi profili di valutazione]** | Il numero di profili valutati nell’ultimo processo di valutazione del segmento. |
| **[!UICONTROL Timestamp ultima attivazione]** | Data e ora dell’esecuzione dell’ultimo processo di attivazione del segmento. |
| **[!UICONTROL Stato ultima attivazione]** | Lo stato dell’ultimo processo di attivazione del segmento. Eventuali valori includono **[!UICONTROL Completato]**, **[!UICONTROL Nessuna esecuzione]** e **[!UICONTROL Non riuscito]**. |
| **[!UICONTROL Ultime identità di attivazione]** | Numero di identità attivate nell’ultimo processo di attivazione del segmento. |
| **[!UICONTROL Ultima destinazione di attivazione]** | Nome della destinazione a cui è stato attivato l’ultimo processo di attivazione del segmento. |

Puoi filtrare i risultati in un segmento specifico e visualizzarne i processi di segmento selezionando l’icona di filtro (![Icona del filtro.](../assets/ui/monitor-segments/filter-icon.png)). I lavori del segmento vengono ordinati in ordine cronologico, con i lavori del segmento più recenti che compaiono per primi.

![L’icona del filtro è evidenziata. Selezionando questa opzione è possibile visualizzare i processi del segmento per il segmento specificato.](../assets/ui/monitor-segments/filter-segment.png)

Viene visualizzato il dashboard dei segmenti filtrati. La **[!UICONTROL Segmenti]** la scheda mostra lo stato e la data dell’ultimo processo di valutazione e dell’ultimo processo di attivazione.

![La scheda Segmenti . Vengono visualizzate informazioni sull’ultimo processo di valutazione e sull’ultimo processo di attivazione.](../assets/ui/monitor-segments/specified-segment-card.png)

Il dashboard stesso visualizza l’ora e lo stato degli ultimi processi di valutazione e attivazione, un grafico che mostra il conteggio del profilo della valutazione del segmento e le metriche per i processi del segmento eseguiti. Per impostazione predefinita, il dashboard mostra le metriche dei processi dei segmenti per le ultime 24 ore.

![Dashboard dei segmenti filtrati. Vengono visualizzate le informazioni sui vari processi del segmento eseguiti per questo segmento.](../assets/ui/monitor-segments/filter-specified-segment.png)

Per questa vista dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Inizio processo]** | Data e ora di inizio del processo del segmento. |
| **[!UICONTROL Tipo]** | Indica il tipo di processo del segmento. I due tipi di processi supportati sono **attivazione** e **valutazione** posti di lavoro. |
| **[!UICONTROL Processo completato]** | La data e l’ora in cui il processo del segmento è stato completato. |
| **[!UICONTROL Tempo di elaborazione]** | Il tempo necessario al completamento del processo del segmento. |
| **[!UICONTROL Stato del processo]** | Lo stato del processo del segmento. I valori supportati includono **[!UICONTROL Completato]**, **[!UICONTROL In corso]** e **[!UICONTROL Non riuscito]**. |
| **[!UICONTROL Conteggio dei profili]** | Il numero di profili che il processo del segmento sta valutando. Ogni utente deve avere un profilo univoco. |
| **[!UICONTROL Numero di identità]** | Il numero di identità che il processo del segmento sta attivando. Ogni profilo può avere più identità. Ad esempio, un profilo potrebbe avere un’e-mail, un numero di telefono e un numero fedeltà come identità. |
| **[!UICONTROL Nome destinazione]** | Nome della destinazione a cui viene attivato il processo del segmento. |

Puoi filtrare ulteriormente un processo di segmento specifico e visualizzarne i dettagli selezionando l’icona di filtro (![Icona del filtro.](../assets/ui/monitor-segments/filter-icon.png)). Esistono due tipi diversi di processi di segmento che possono essere filtrati: processi di attivazione e processi di valutazione.

### Dettagli del processo di attivazione {#activation-job-details}

La pagina dei dettagli dell’esecuzione del flusso di dati del processo di attivazione mostra informazioni sulle metriche dell’esecuzione, sugli errori di esecuzione del flusso di dati e sui segmenti correlati al processo del segmento. Un processo di attivazione viene utilizzato per attivare il segmento per una destinazione specifica. Per impostazione predefinita, la pagina dei dettagli mostra gli errori di esecuzione del flusso di dati.

![Dashboard dei segmenti filtrati. Vengono visualizzate le informazioni sui vari processi del segmento eseguiti per questo segmento.](../assets/ui/monitor-segments/activation-job-details.png)

Per questa vista dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Profili ricevuti]** | Numero totale di profili ricevuti nel flusso di attivazione. |
| **[!UICONTROL Identità attivate]** | Numero totale di identità attivate correttamente nella destinazione in base ai profili ricevuti. |
| **[!UICONTROL Identità escluse]** | Numero totale di identità escluse dall’attivazione nella destinazione in base ai profili ricevuti. Queste identità potrebbero essere escluse a causa di attributi mancanti o violazioni del consenso. |
| **[!UICONTROL Dimensione dei dati]** | Dimensione del flusso di dati da attivare. |
| **[!UICONTROL File totali]** | Numero totale di file attivati nel flusso di dati. |
| **[!UICONTROL Stato]** | Lo stato corrente del processo di attivazione. |
| **[!UICONTROL Avvio esecuzione flusso di dati]** | Data e ora di inizio del processo di attivazione. |
| **[!UICONTROL Fine del flusso di dati]** | Data e ora di fine del processo di attivazione. |
| **[!UICONTROL ID esecuzione flusso di dati]** | ID del processo di attivazione corrente. |
| **[!UICONTROL ID organizzazione IMS]** | ID dell&#39;organizzazione a cui appartiene il processo di attivazione. |
| **[!UICONTROL Nome destinazione]** | Nome della destinazione a cui vengono attivati i dati. |

Sotto le metriche, viene visualizzato un interruttore per selezionare tra gli errori di esecuzione del flusso di dati e i segmenti.

![Dashboard dei segmenti filtrati. L’interruttore utilizzato per passare dagli errori di esecuzione del flusso di dati alla visualizzazione dei segmenti viene evidenziato.](../assets/ui/monitor-segments/activation-job-details-toggle.png)

Nella sezione errori di esecuzione del flusso di dati , seleziona l’opzione per visualizzare le identità non riuscite o i campi delle identità escluse. La sezione Errori include dettagli sul codice di errore e sul numero di identità non riuscite o escluse.

![Dashboard dei segmenti filtrati. Vengono evidenziate le informazioni sulle identità che non sono riuscite o che sono state escluse.](../assets/ui/monitor-segments/activation-job-details.png)

Nella sezione segmenti , puoi visualizzare un elenco dei segmenti attivati come parte del processo di attivazione. Utilizza la barra di ricerca per filtrare l’elenco di segmenti per nome.

![Dashboard dei segmenti filtrati. Vengono evidenziate le informazioni sulle identità che non sono riuscite o che sono state escluse.](../assets/ui/monitor-segments/activation-job-details-segments.png)

Per la sezione dei segmenti sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Nome]** | Nome del segmento attivato. |
| **[!UICONTROL Identità attivate]** | Numero totale di identità attivate correttamente nella destinazione in base ai profili ricevuti. |
| **[!UICONTROL Identità escluse]** | Numero totale di identità escluse dall’attivazione nella destinazione in base ai profili ricevuti. Queste identità possono essere escluse a causa di attributi mancanti o violazione del consenso. |
| **[!UICONTROL Stato dell&#39;ultima esecuzione del flusso di dati]** | Lo stato dell’ultimo processo di attivazione eseguito per quel segmento. |
| **[!UICONTROL Data ultima esecuzione del flusso di dati]** | Data e ora dell’ultimo processo di attivazione eseguito per quel segmento. |

### Dettagli processo di valutazione {#evaluation-job-details}

La pagina dei dettagli dell’esecuzione del flusso di dati del processo di valutazione mostra informazioni sulle metriche dell’esecuzione e sui segmenti correlati al processo del segmento. Un processo di valutazione è un processo asincrono che crea un segmento di pubblico in base al segmento specificato. Per ulteriori informazioni sui processi di valutazione, consulta l’esercitazione su [valutazione di un segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment).

![Dashboard dei processi di valutazione. Vengono visualizzate informazioni sul processo di valutazione del segmento.](../assets/ui/monitor-segments/evaluation-job-details.png)

Per questa vista dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Profili totali]** | Numero totale di profili in fase di valutazione. |
| **[!UICONTROL Stato]** | Stato del processo di valutazione. Gli stati possibili per il processo di valutazione includono **[!UICONTROL Completato]** e **[!UICONTROL Non riuscito]**. |
| **[!UICONTROL Inizio processo]** | Data e ora di inizio del processo di valutazione. |
| **[!UICONTROL Fine del processo]** | Data e ora di fine del processo di valutazione. |
| **[!UICONTROL Tipo di processo]** | Il tipo di processo del segmento. In questo caso, sarà sempre un processo di valutazione del segmento. |
| **[!UICONTROL Tipo di valutazione]** | Tipo di valutazione in corso. Può essere **[!UICONTROL Batch]** o **[!UICONTROL Streaming]**. |
| **[!UICONTROL ID processo]** | ID del processo di valutazione. |
| **[!UICONTROL ID organizzazione IMS]** | ID dell&#39;organizzazione a cui appartiene il processo di valutazione. |
| **[!UICONTROL Nome del segmento]** | Nome del segmento oggetto della valutazione. |
| **[!UICONTROL ID segmento]** | ID del segmento oggetto della valutazione. |

Nella sezione Segmenti è disponibile un elenco dei segmenti che vengono valutati come parte del processo di valutazione. Puoi filtrare l’elenco di segmenti per nome utilizzando la barra di ricerca.

>[!IMPORTANT]
>
>Questa vista dashboard supporta attualmente fino a 800 metriche di segmenti.

Per la sezione dei segmenti sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Nome]** | Nome del segmento oggetto della valutazione. |
| **[!UICONTROL Conteggio dei profili]** | Il numero di profili in fase di valutazione. |

## Dashboard dei processi dei segmenti {#monitoring-segment-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Processi dei segmenti"
>abstract="La vista Processi dei segmenti contiene informazioni sui processi di valutazione ed esportazione per tutti i segmenti."

Per accedere al **[!UICONTROL Processi dei segmenti]** dashboard, seleziona **[!UICONTROL Monitoraggio]** (![icona di monitoraggio](../assets/ui/monitor-destinations/monitoring-icon.png)) nella navigazione a sinistra. Una volta sul [!UICONTROL Monitoraggio] pagina, seleziona **[!UICONTROL Processi dei segmenti]**. La [!UICONTROL Monitoraggio] il dashboard contiene metriche e informazioni sui processi di valutazione dei segmenti e di esportazione.

>[!NOTE]
>
>Solo **processi di valutazione dei segmenti** sono supportate per il monitoraggio per segmento. I processi di esportazione dei segmenti supportano solo il monitoraggio a livello di organizzazione.

![Dashboard di monitoraggio dei processi dei segmenti](../assets/ui/monitor-segments/segment-jobs-dashboard.png)

Utilizza la [!UICONTROL Processi dei segmenti] dashboard per capire se la valutazione e l’esportazione del profilo avviene in tempo e senza eccezioni, in modo che i servizi a valle per l’attivazione della destinazione possano avere i dati del profilo più recenti valutati.

Le metriche seguenti sono disponibili per i processi di segmento:

| Metrica | Descrizione |
---------|----------|
| **[!UICONTROL Processo del segmento]** | Indica il nome del processo del segmento. |
| **[!UICONTROL Tipo]** | Indica il tipo di processo del segmento: esportazione o valutazione. Nota che in entrambi i casi il processo del segmento valuta o esporta **tutto** segmenti appartenenti a un’organizzazione. Per ulteriori informazioni sui lavori di esportazione, consulta la guida in [endpoint dei processi di esportazione](../../segmentation/api/export-jobs.md). Per ulteriori informazioni sui processi di valutazione, consulta l’esercitazione su [valutazione di un segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Inizio processo]** | Data e ora di inizio del processo del segmento. |
| **[!UICONTROL Fine del processo]** | La data e l’ora in cui il processo del segmento è stato completato. |
| **[!UICONTROL Stato]** | Stato del processo completato. Gli stati possibili per il processo del segmento includono successo o non riuscito. |
