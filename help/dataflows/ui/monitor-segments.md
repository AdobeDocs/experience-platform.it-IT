---
keywords: Experience Platform;home;argomenti popolari;monitorare segmenti;monitorare flussi di dati;flussi di dati;segmentazione;monitor;dataflows;segmentation
description: La segmentazione ti consente di creare segmenti e tipi di pubblico dai dati dei profili cliente in tempo reale. Questo tutorial fornisce istruzioni su come monitorare i flussi di dati durante la segmentazione utilizzando l’interfaccia utente di Experience Platform.
title: Monitorare i flussi di dati per i segmenti nell’interfaccia utente
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 4%

---

# Monitorare i flussi di dati per i segmenti nell’interfaccia utente

Il servizio di segmentazione consente di creare segmenti e tipi di pubblico dai dati dei profili cliente in tempo reale in Adobe Experience Platform. Platform fornisce flussi di dati per monitorare in modo trasparente questo flusso di dati dalle origini alle destinazioni.

La dashboard di monitoraggio fornisce una rappresentazione visiva dell’attività dei dati all’interno di un segmento, incluso lo stato della segmentazione dei dati. Questa esercitazione fornisce istruzioni su come utilizzare il dashboard di monitoraggio per monitorare la segmentazione dei dati utilizzando l’interfaccia utente di Experience Platform, che consente di monitorare lo stato dei processi di attivazione, valutazione ed esportazione dei segmenti.

## Introduzione {#getting-started}

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Flussi dati](../home.md): i flussi di dati sono una rappresentazione dei processi di dati che spostano i dati in Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile], e a [!DNL Destinations].
   - [Il flusso di dati viene eseguito](../../sources/notifications.md): le esecuzioni dei flussi di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
- [Segmentazione](../../segmentation/home.md): la segmentazione ti consente di creare segmenti e tipi di pubblico dai dati dei profili cliente in tempo reale.
   - [Processi di attivazione](../../destinations/ui/activation-overview.md): viene utilizzato un processo di attivazione per attivare il segmento in una destinazione specificata.
   - [Processi di valutazione](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): un processo di valutazione è un processo asincrono eseguito che crea un segmento di pubblico basato sul segmento specificato.
   - [Processi di esportazione](../../segmentation/api/export-jobs.md): un processo di esportazione è un processo asincrono utilizzato per rendere persistenti i membri del segmento di pubblico nei set di dati.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

## Monitoraggio del dashboard dei segmenti {#monitoring-segments-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Segmenti"
>abstract="La vista Segmenti contiene informazioni su tutti i segmenti dell’organizzazione, con ulteriori informazioni sui relativi processi di attivazione e valutazione."

Per accedere al **[!UICONTROL Segmenti]** dashboard, seleziona **[!UICONTROL Monitorare]** nel menu di navigazione a sinistra. Una volta al **[!UICONTROL Monitorare]** , seleziona la **[!UICONTROL Segmenti]** Card.

![La scheda Segmenti. Vengono visualizzate le informazioni sull’ultimo processo di valutazione e sull’ultimo processo di esportazione.](../assets/ui/monitor-segments/segment-card-monitoring.png)

Principale **[!UICONTROL Segmenti]** dashboard, il **[!UICONTROL Segmenti]** mostra lo stato e la data dell’ultimo processo di valutazione e dell’ultimo processo di esportazione.

Il dashboard contiene metriche sia per i segmenti che per i processi dei segmenti. Per impostazione predefinita, la dashboard mostra le metriche del segmento per le ultime 24 ore. Per ulteriori informazioni sulla visualizzazione dei processi di segmentazione, consulta [monitoraggio dei processi dei segmenti](#monitoring-segment-jobs-dashboard) sezione.

>[!IMPORTANT]
>
>Attualmente, solo i segmenti attivati in [destinazioni batch (basate su file)](../../destinations/destination-types.md#file-based) sono supportate per il dashboard dei segmenti di monitoraggio.

![Il dashboard dei segmenti. Vengono visualizzate le informazioni sui diversi segmenti nell’organizzazione e nella sandbox.](../assets/ui/monitor-segments/segment-monitoring-dashboard.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Nome segmento]** | Nome del segmento. |
| **[!UICONTROL Timestamp dell’ultima valutazione]** | La data e l’ora di esecuzione dell’ultimo processo di valutazione del segmento. |
| **[!UICONTROL Stato ultima valutazione]** | Lo stato dell’ultimo processo di valutazione del segmento. I valori possibili includono **[!UICONTROL Completato]**, **[!UICONTROL Nessuna esecuzione]**, e **[!UICONTROL Non riuscito]**. |
| **[!UICONTROL Ultimi profili di valutazione]** | Il numero di profili valutati nell’ultimo processo di valutazione del segmento. |
| **[!UICONTROL Timestamp ultima attivazione]** | La data e l’ora dell’ultimo processo di attivazione del segmento. |
| **[!UICONTROL Stato ultima attivazione]** | Lo stato dell’ultimo processo di attivazione del segmento. I valori possibili includono **[!UICONTROL Completato]**, **[!UICONTROL Nessuna esecuzione]**, e **[!UICONTROL Non riuscito]**. |
| **[!UICONTROL Identità ultima attivazione]** | Il numero di identità attivate nell’ultimo processo di attivazione del segmento. |
| **[!UICONTROL Destinazione ultima attivazione]** | Nome della destinazione a cui è stato attivato l’ultimo processo di attivazione del segmento. |

Puoi filtrare i risultati per un segmento specifico e visualizzarne i processi selezionando l’icona del filtro (![Icona del filtro.](../assets/ui/monitor-segments/filter-icon.png)). I processi di segmentazione sono ordinati in ordine cronologico, con i processi di segmentazione più recenti che appaiono per primi.

![L’icona del filtro viene evidenziata. Selezionando questa opzione è possibile visualizzare i processi di segmentazione per il segmento specificato.](../assets/ui/monitor-segments/filter-segment.png)

Viene visualizzato il quadro comandi del segmento filtrato. Il **[!UICONTROL Segmenti]** mostra lo stato e la data dell’ultimo processo di valutazione e dell’ultimo processo di attivazione.

![La scheda Segmenti. Vengono visualizzate le informazioni sull’ultimo processo di valutazione e sull’ultimo processo di attivazione.](../assets/ui/monitor-segments/specified-segment-card.png)

Il dashboard stesso visualizza l’ora e lo stato degli ultimi processi di valutazione e attivazione, un grafico che mostra il conteggio dei profili della valutazione del segmento e le metriche per i processi del segmento eseguiti. Per impostazione predefinita, il dashboard mostra le metriche del processo di segmentazione per le ultime 24 ore.

![Il dashboard dei segmenti filtrati. Vengono visualizzate informazioni sui vari processi di segmentazione eseguiti per questo segmento.](../assets/ui/monitor-segments/filter-specified-segment.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Inizio processo]** | La data e l’ora di inizio del processo di segmentazione. |
| **[!UICONTROL Tipo]** | Indica il tipo di processo di segmentazione. I due tipi di processo supportati sono **attivazione** e **valutazione** processi. |
| **[!UICONTROL Processo completato]** | La data e l’ora di completamento del processo di segmentazione. |
| **[!UICONTROL Tempo di elaborazione]** | Il tempo necessario per il completamento del processo di segmentazione. |
| **[!UICONTROL Stato del processo]** | Stato del processo di segmentazione. I valori supportati includono **[!UICONTROL Completato]**, **[!UICONTROL In corso]**, e **[!UICONTROL Non riuscito]**. |
| **[!UICONTROL Conteggio dei profili]** | Il numero di profili valutati dal processo di segmentazione. Ogni utente deve avere un profilo univoco. |
| **[!UICONTROL Conteggio identità]** | Il numero di identità attivate dal processo di segmentazione. Ogni profilo può avere più identità. Ad esempio, un profilo potrebbe avere come identità un’e-mail, un numero di telefono e un numero fedeltà. |
| **[!UICONTROL Nome destinazione]** | Nome della destinazione a cui viene attivato il processo di segmentazione. |

Puoi filtrare ulteriormente per un processo di segmentazione specifico e visualizzarne i dettagli selezionando l’icona del filtro (![Icona del filtro.](../assets/ui/monitor-segments/filter-icon.png)). È possibile filtrare due diversi tipi di processi di segmento: processi di attivazione e processi di valutazione.

### Dettagli processo di attivazione {#activation-job-details}

La pagina dei dettagli di esecuzione del flusso di dati del processo di attivazione mostra informazioni sulle metriche dell’esecuzione, sugli errori di esecuzione del flusso di dati e sui segmenti correlati al processo di segmentazione. Un processo di attivazione viene utilizzato per attivare il segmento per una destinazione specificata. Per impostazione predefinita, la pagina dei dettagli mostra gli errori di esecuzione del flusso di dati.

![Il dashboard dei segmenti filtrati. Vengono visualizzate informazioni sui vari processi di segmentazione eseguiti per questo segmento.](../assets/ui/monitor-segments/activation-job-details.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Profili ricevuti]** | Numero totale di profili ricevuti nel flusso di attivazione. |
| **[!UICONTROL Identità attivate]** | Numero totale di identità attivate correttamente nella destinazione, in base ai profili ricevuti. |
| **[!UICONTROL Identità escluse]** | Il numero totale di identità escluse dall’attivazione nella destinazione, in base ai profili ricevuti. Queste identità potrebbero essere escluse a causa di attributi mancanti o violazioni del consenso. |
| **[!UICONTROL Dimensione dei dati]** | Dimensione del flusso di dati da attivare. |
| **[!UICONTROL File totali]** | Numero totale di file attivati nel flusso di dati. |
| **[!UICONTROL Stato]** | Stato corrente del processo di attivazione. |
| **[!UICONTROL Avvio esecuzione flusso di dati]** | Data e ora di inizio del processo di attivazione. |
| **[!UICONTROL Fine esecuzione flusso di dati]** | La data e l’ora in cui è terminato il processo di attivazione. |
| **[!UICONTROL ID esecuzione flusso di dati]** | ID del processo di attivazione corrente. |
| **[!UICONTROL ID organizzazione IMS]** | ID dell&#39;organizzazione a cui appartiene il processo di attivazione. |
| **[!UICONTROL Nome destinazione]** | Nome della destinazione a cui vengono attivati i dati. |

Sotto le metriche, viene visualizzato un interruttore per selezionare tra gli errori di esecuzione del flusso di dati e i segmenti.

![Il dashboard dei segmenti filtrati. Viene evidenziato l’interruttore utilizzato per passare dagli errori di esecuzione del flusso di dati alla visualizzazione dei segmenti.](../assets/ui/monitor-segments/activation-job-details-toggle.png)

Nella sezione errori di esecuzione del flusso di dati, seleziona l’opzione per visualizzare i campi delle identità non riuscite o escluse. La sezione errori include dettagli sul codice di errore e sul numero di identità non riuscite o escluse.

![Il dashboard dei segmenti filtrati. Vengono evidenziate le informazioni sulle identità che non sono riuscite o che sono state escluse.](../assets/ui/monitor-segments/activation-job-details.png)

Nella sezione segmenti puoi visualizzare un elenco dei segmenti attivati come parte del processo di attivazione. Utilizza la barra di ricerca per filtrare l’elenco dei segmenti per nome.

![Il dashboard dei segmenti filtrati. Vengono evidenziate le informazioni sulle identità che non sono riuscite o che sono state escluse.](../assets/ui/monitor-segments/activation-job-details-segments.png)

Per la sezione segmenti sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Nome]** | Nome del segmento attivato. |
| **[!UICONTROL Identità attivate]** | Numero totale di identità attivate correttamente nella destinazione, in base ai profili ricevuti. |
| **[!UICONTROL Identità escluse]** | Il numero totale di identità escluse dall’attivazione nella destinazione, in base ai profili ricevuti. Queste identità potrebbero essere escluse a causa di attributi mancanti o di una violazione del consenso. |
| **[!UICONTROL Stato ultima esecuzione del flusso di dati]** | Lo stato dell’ultimo processo di attivazione eseguito per quel segmento. |
| **[!UICONTROL Data ultima esecuzione del flusso di dati]** | La data e l’ora dell’ultimo processo di attivazione eseguito per quel segmento. |

### Dettagli processo di valutazione {#evaluation-job-details}

La pagina dei dettagli dell’esecuzione del flusso di dati del processo di valutazione mostra informazioni sulle metriche dell’esecuzione e sui segmenti correlati al processo di segmentazione. Un processo di valutazione è un processo asincrono che crea un segmento di pubblico basato sul segmento specificato. Per ulteriori informazioni sui processi di valutazione, consulta l’esercitazione su [valutazione di un segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment).

![Dashboard del processo di valutazione. Vengono visualizzate le informazioni sul processo di valutazione del segmento.](../assets/ui/monitor-segments/evaluation-job-details.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Profili totali]** | Numero totale di profili da valutare. |
| **[!UICONTROL Stato]** | Stato del processo di valutazione. Gli stati possibili per il processo di valutazione includono **[!UICONTROL Completato]** e **[!UICONTROL Non riuscito]**. |
| **[!UICONTROL Inizio processo]** | Data e ora di inizio del processo di valutazione. |
| **[!UICONTROL Fine processo]** | Data e ora di fine del processo di valutazione. |
| **[!UICONTROL Tipo di processo]** | Il tipo di processo di segmentazione. In questo caso, sarà sempre un processo di valutazione del segmento. |
| **[!UICONTROL Tipo di valutazione]** | Tipo di valutazione in corso. Può essere **[!UICONTROL Batch]** o **[!UICONTROL Streaming]**. |
| **[!UICONTROL ID processo]** | ID del processo di valutazione. |
| **[!UICONTROL ID organizzazione IMS]** | ID dell&#39;organizzazione a cui appartiene il processo di valutazione. |
| **[!UICONTROL Nome segmento]** | Il nome del segmento che viene valutato. |
| **[!UICONTROL ID segmento]** | ID del segmento che viene valutato. |

Nella sezione segmenti puoi visualizzare un elenco dei segmenti che vengono valutati come parte del processo di valutazione. Puoi filtrare l’elenco dei segmenti per nome utilizzando la barra di ricerca.

>[!IMPORTANT]
>
>Questa visualizzazione dashboard supporta attualmente fino a 800 metriche di segmenti.

Per la sezione segmenti sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Nome]** | Il nome del segmento che viene valutato. |
| **[!UICONTROL Conteggio dei profili]** | Il numero di profili che vengono valutati. |

## Monitoraggio del dashboard dei processi di segmento {#monitoring-segment-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Processi dei segmenti"
>abstract="La vista Processi dei segmenti contiene informazioni sui processi di valutazione ed esportazione per tutti i segmenti."

Per accedere al **[!UICONTROL Segmenta processi]** dashboard, seleziona **[!UICONTROL Monitorare]** (![icona di monitoraggio](../assets/ui/monitor-destinations/monitoring-icon.png)) nel menu di navigazione a sinistra. Una volta al [!UICONTROL Monitorare] pagina, seleziona **[!UICONTROL Segmenta processi]**. Il [!UICONTROL Monitorare] la dashboard contiene metriche e informazioni sulla valutazione dei segmenti e sui processi di esportazione.

>[!NOTE]
>
>Solo **processi di valutazione dei segmenti** sono supportate per il monitoraggio per segmento. I processi di esportazione dei segmenti supportano solo il monitoraggio a livello di organizzazione.

![Dashboard di monitoraggio dei processi di segmento](../assets/ui/monitor-segments/segment-jobs-dashboard.png)

Utilizza il [!UICONTROL Segmenta processi] dashboard per capire se la valutazione e l’esportazione del profilo si verificano in tempo e senza eccezioni, in modo che i servizi a valle per l’attivazione della destinazione possano disporre dei dati di profilo valutati più recenti.

Per i processi di segmentazione sono disponibili le metriche seguenti:

| Metrica | Descrizione |
---------|----------|
| **[!UICONTROL Processo segmento]** | Indica il nome del processo del segmento. |
| **[!UICONTROL Tipo]** | Indica il tipo di processo di segmentazione: esportazione o valutazione. In entrambi i casi, il processo di segmentazione valuta o esporta **tutto** segmenti appartenenti a un’organizzazione. Per ulteriori informazioni sui processi di esportazione, consulta la guida [endpoint processi di esportazione](../../segmentation/api/export-jobs.md). Per ulteriori informazioni sui processi di valutazione, consulta l’esercitazione su [valutazione di un segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Inizio processo]** | La data e l’ora di inizio del processo di segmentazione. |
| **[!UICONTROL Fine processo]** | La data e l’ora di completamento del processo di segmentazione. |
| **[!UICONTROL Stato]** | Stato del processo completato. Gli stati possibili per il processo di segmentazione includono Completato o Non riuscito. |
