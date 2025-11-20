---
description: Scopri come monitorare i flussi di dati durante la segmentazione utilizzando l’interfaccia utente di Experience Platform.
title: Monitorare i flussi di dati per i tipi di pubblico nell’interfaccia utente
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 4%

---

# Monitorare i flussi di dati per il pubblico nell’interfaccia utente

Il servizio di segmentazione consente di creare tipi di pubblico tramite definizioni di segmenti o altre origini dai dati di [!DNL Real-Time Customer Profile]. Experience Platform fornisce flussi di dati per monitorare in modo trasparente questo flusso di dati dalle origini alle destinazioni.

Utilizza il dashboard di monitoraggio per visualizzare una rappresentazione visiva dell’attività dei dati all’interno di un pubblico, incluso lo stato della segmentazione dei dati. Leggi il tutorial per istruzioni su come utilizzare il dashboard di monitoraggio per monitorare la segmentazione dei dati utilizzando l’interfaccia utente di Experience Platform, che consente di monitorare lo stato dei processi di attivazione, valutazione ed esportazione del pubblico.

## Introduzione {#getting-started}

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Flussi dati](../home.md): i flussi dati sono una rappresentazione dei processi di dati che spostano i dati in Experience Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile] e a [!DNL Destinations].
   - [Esecuzioni flusso di dati](../../sources/notifications.md): le esecuzioni del flusso di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
- [Segmentazione](../../segmentation/home.md): la segmentazione ti consente di creare tipi di pubblico dai dati del tuo Profilo cliente in tempo reale.
   - [Processi di attivazione](../../destinations/ui/activation-overview.md): viene utilizzato un processo di attivazione per attivare il pubblico in una destinazione specificata.
   - [Processi di valutazione](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): un processo di valutazione è un processo asincrono che valuta il pubblico.
   - [Processi di esportazione](../../segmentation/api/export-jobs.md): un processo di esportazione è un processo asincrono utilizzato per rendere persistenti i membri del pubblico nei set di dati.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Experience Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Dashboard di monitoraggio dei tipi di pubblico {#monitoring-audiences-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Tipi di pubblico"
>abstract="La vista Tipi di pubblico contiene informazioni su tutti i tipi di pubblico dell’organizzazione, con ulteriori informazioni sui relativi processi di attivazione e valutazione."

Per accedere al dashboard **[!UICONTROL Audiences]**, seleziona **[!UICONTROL Monitoring]** nel menu di navigazione a sinistra. Una volta nella pagina **[!UICONTROL Monitoring]**, seleziona la scheda **[!UICONTROL Audiences]**.

![Scheda Pubblico. Vengono visualizzate le informazioni sull&#39;ultimo processo di valutazione e sull&#39;ultimo processo di esportazione.](../assets/ui/monitor-audiences/audience-card.png)

Nel dashboard **[!UICONTROL Audiences]** principale, la scheda **[!UICONTROL Audiences]** mostra lo stato e la data dell&#39;ultimo processo di valutazione e dell&#39;ultimo processo di esportazione.

La dashboard stessa contiene metriche sia per i tipi di pubblico che per i processi di segmentazione. Per impostazione predefinita, la dashboard mostra le metriche relative al pubblico delle ultime 24 ore. Per ulteriori informazioni sulla visualizzazione dei processi di segmentazione, consulta la sezione [monitoraggio dei processi di segmentazione](#monitoring-segmentation-jobs-dashboard).

>[!IMPORTANT]
>
>Attualmente, solo i tipi di pubblico attivati nelle destinazioni [batch (basate su file)](../../destinations/destination-types.md#file-based) sono supportati per il dashboard dei tipi di pubblico di monitoraggio.

![Dashboard del pubblico. Vengono visualizzate le informazioni sui diversi tipi di pubblico nell&#39;organizzazione e nella sandbox.](../assets/ui/monitor-audiences/audience-dashboard.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Audience name]** | Il nome del pubblico. |
| **[!UICONTROL Data type]** | Il tipo di dati del pubblico. I valori possibili sono **[!UICONTROL Customer]**, **[!UICONTROL Account]** e **[!UICONTROL Prospect]**. Puoi visualizzare per i tipi di pubblico di un tipo di dati specificato utilizzando il filtro [!UICONTROL Data type] sopra la barra multifunzione delle schede. |
| **[!UICONTROL Last evaluation timestamp]** | La data e l’ora di esecuzione dell’ultimo processo di valutazione del pubblico. |
| **[!UICONTROL Last evaluation status]** | Lo stato dell’ultimo processo di valutazione del pubblico. I valori possibili sono **[!UICONTROL Success]**, **[!UICONTROL No runs]** e **[!UICONTROL Failed]**. |
| **[!UICONTROL Last evaluation method]** | Il metodo di valutazione del pubblico. Poiché è supportata solo la segmentazione batch, l&#39;unico valore possibile è **[!UICONTROL Batch]**. |
| **[!UICONTROL Last evaluation profiles]** | Il numero di profili valutati nell’ultimo processo di valutazione del pubblico. |
| **[!UICONTROL Last activation timestamp]** | La data e l’ora di esecuzione dell’ultimo processo di attivazione del pubblico. |
| **[!UICONTROL Last activation status]** | Lo stato dell’ultimo processo di attivazione del pubblico. I valori possibili sono **[!UICONTROL Success]**, **[!UICONTROL No runs]** e **[!UICONTROL Failed]**. |
| **[!UICONTROL Last activation identities]** | Il numero di identità attivate nell’ultimo processo di attivazione del pubblico. |
| **[!UICONTROL Last activation destination]** | Il nome della destinazione a cui è stato attivato l’ultimo processo di attivazione del pubblico. |

Puoi filtrare i risultati per un pubblico specifico e visualizzare i relativi processi di segmentazione selezionando l&#39;icona del filtro (![Icona del filtro.](/help/images/icons/filter-add.png)). I processi di segmentazione sono ordinati in ordine cronologico, con i processi di segmentazione più recenti che appaiono per primi.

![L&#39;icona del filtro è evidenziata. Selezionando questa opzione è possibile visualizzare i processi di segmentazione per il pubblico specificato.](../assets/ui/monitor-audiences/filter-audience.png)

Viene visualizzato il dashboard del pubblico filtrato. La scheda **[!UICONTROL Audiences]** mostra lo stato e la data dell&#39;ultimo processo di valutazione e dell&#39;ultimo processo di attivazione.

![Scheda Pubblico. Vengono visualizzate le informazioni sull&#39;ultimo processo di valutazione e sull&#39;ultimo processo di attivazione.](../assets/ui/monitor-audiences/specified-audience-card.png)

Il dashboard stesso visualizza l’ora e lo stato degli ultimi processi di valutazione e attivazione, un grafico che mostra il conteggio dei profili della valutazione del pubblico e le metriche per i processi di segmentazione eseguiti. Per impostazione predefinita, il dashboard mostra le metriche del processo di segmentazione per le ultime 24 ore.

![Dashboard del pubblico filtrato. Vengono visualizzate informazioni sui vari processi di segmentazione eseguiti per questo pubblico.](../assets/ui/monitor-audiences/filter-audience.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Job start]** | La data e l’ora di inizio del processo di segmentazione. |
| **[!UICONTROL Type]** | Indica il tipo di processo di segmentazione. I due tipi di processo supportati sono **attivazione** e **valutazione** processi. |
| **[!UICONTROL Job complete]** | La data e l’ora in cui il processo di segmentazione è stato completato. |
| **[!UICONTROL Processing time]** | Il tempo necessario per il completamento del processo di segmentazione. |
| **[!UICONTROL Job status]** | Stato del processo di segmentazione. I valori supportati sono **[!UICONTROL Success]**, **[!UICONTROL In Progress]** e **[!UICONTROL Failed]**. |
| **[!UICONTROL Profile count]** | Il numero di profili che il processo di segmentazione sta valutando. Ogni utente deve avere un profilo univoco. |
| **[!UICONTROL Identity activated]** | Il numero di identità attivate dal processo di segmentazione. Ogni profilo può avere più identità. Ad esempio, un profilo potrebbe avere come identità un’e-mail, un numero di telefono e un numero fedeltà. |
| **[!UICONTROL Destination name]** | Il nome della destinazione in cui viene attivato il processo di segmentazione. |

Puoi filtrare ulteriormente per un processo di segmentazione specifico e visualizzarne i dettagli selezionando l&#39;icona del filtro (![Icona del filtro.](/help/images/icons/filter.png)). Esistono due diversi tipi di processi di segmentazione che possono essere filtrati: processi di attivazione e processi di valutazione.

### Dettagli processo di attivazione {#activation-job-details}

La pagina dei dettagli di esecuzione del flusso di dati del processo di attivazione mostra informazioni sulle metriche dell’esecuzione, sugli errori di esecuzione del flusso di dati e sui tipi di pubblico correlati al processo di segmentazione. Un processo di attivazione viene utilizzato per attivare il pubblico per una destinazione specificata.

![Dashboard del processo di attivazione. Vengono visualizzate informazioni sui vari processi di segmentazione eseguiti per questo pubblico.](../assets/ui/monitor-audiences/activation-job-dashboard.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Profiles received]** | Numero totale di profili ricevuti nel flusso di attivazione. |
| **[!UICONTROL Identities activated]** | Numero totale di identità attivate correttamente nella destinazione, in base ai profili ricevuti. |
| **[!UICONTROL Identities excluded]** | Il numero totale di identità escluse dall’attivazione nella destinazione, in base ai profili ricevuti. Queste identità potrebbero essere escluse a causa di attributi mancanti o violazioni del consenso. |
| **[!UICONTROL Size of data]** | Dimensione del flusso di dati da attivare. |
| **[!UICONTROL Total files]** | Numero totale di file attivati nel flusso di dati. |
| **[!UICONTROL Status]** | Stato corrente del processo di attivazione. |
| **[!UICONTROL Dataflow run start]** | Data e ora di inizio del processo di attivazione. |
| **[!UICONTROL Dataflow run end]** | La data e l’ora in cui è terminato il processo di attivazione. |
| **[!UICONTROL Dataflow run ID]** | ID del processo di attivazione corrente. |
| **[!UICONTROL IMS org ID]** | ID dell&#39;organizzazione a cui appartiene il processo di attivazione. |
| **[!UICONTROL Destination name]** | Nome della destinazione a cui vengono attivati i dati. |

Nella sezione tipi di pubblico puoi visualizzare un elenco dei tipi di pubblico attivati come parte del processo di attivazione.

![Dashboard del processo di attivazione. Le informazioni sulle identità non riuscite o escluse sono evidenziate.](../assets/ui/monitor-audiences/activation-job-audiences.png)

Per la sezione dei tipi di pubblico sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Name]** | Il nome del pubblico che è stato attivato. |
| **[!UICONTROL Identities activated]** | Numero totale di identità attivate correttamente nella destinazione, in base ai profili ricevuti. |
| **[!UICONTROL Identities excluded]** | Il numero totale di identità escluse dall’attivazione nella destinazione, in base ai profili ricevuti. Queste identità potrebbero essere escluse a causa di attributi mancanti o di una violazione del consenso. |
| **[!UICONTROL Last dataflow run status]** | Lo stato dell’ultimo processo di attivazione eseguito per quel pubblico. |
| **[!UICONTROL Last dataflow run date]** | La data e l’ora dell’ultimo processo di attivazione eseguito per quel pubblico. |

Inoltre, puoi visualizzare i dettagli sugli errori di esecuzione del flusso di dati. Nella sezione errori di esecuzione del flusso di dati, puoi visualizzare sia le identità con errori che quelle escluse. La sezione errori include dettagli sul codice di errore e sul numero di identità non riuscite o escluse.

![Dashboard del processo di attivazione. Le informazioni sulle identità non riuscite o escluse sono evidenziate.](../assets/ui/monitor-audiences/activation-job-errors.png)

### Dettagli processo di valutazione {#evaluation-job-details}

La pagina dei dettagli dell’esecuzione del flusso di dati del processo di valutazione mostra le informazioni sulle metriche dell’esecuzione e sui tipi di pubblico correlati al processo di segmentazione.

![Dashboard del processo di valutazione. Vengono visualizzate informazioni sul processo di valutazione del pubblico.](../assets/ui/monitor-audiences/evaluation-job-details.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Total profiles]** | Numero totale di profili da valutare. |
| **[!UICONTROL Status]** | Stato del processo di valutazione. Gli stati possibili per il processo di valutazione includono **[!UICONTROL Success]** e **[!UICONTROL Failed]**. |
| **[!UICONTROL Job start]** | Data e ora di inizio del processo di valutazione. |
| **[!UICONTROL Job end]** | Data e ora di fine del processo di valutazione. |
| **[!UICONTROL Job type]** | Il tipo di processo di segmentazione. In questo caso, sarà sempre un processo **[!UICONTROL Segment evaluation]**. |
| **[!UICONTROL Evaluation type]** | Tipo di valutazione in corso. Può essere **[!UICONTROL Batch]** o **[!UICONTROL Streaming]**. |
| **[!UICONTROL Job ID]** | ID del processo di valutazione. |
| **[!UICONTROL IMS org ID]** | ID dell&#39;organizzazione a cui appartiene il processo di valutazione. |
| **[!UICONTROL Audience name]** | Il nome del pubblico che viene valutato. |
| **[!UICONTROL Audience ID]** | ID del pubblico che viene valutato. |

Nella sezione [!UICONTROL Audiences] è possibile visualizzare un elenco dei tipi di pubblico che vengono valutati come parte del processo di valutazione. Puoi filtrare l’elenco dei tipi di pubblico per nome utilizzando la barra di ricerca.

>[!IMPORTANT]
>
>Questa visualizzazione dashboard supporta attualmente fino a 800 metriche per il pubblico.

Per la sezione [!UICONTROL Audiences] sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Name]** | Il nome del pubblico che viene valutato. |
| **[!UICONTROL Profile count]** | Il numero di profili che vengono valutati. |

## Dashboard di monitoraggio dei processi di segmentazione {#monitoring-segmentation-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Processi di segmentazione"
>abstract="La vista processi di segmentazione contiene informazioni sui processi di valutazione ed esportazione per tutti i tipi di pubblico."

Per accedere al dashboard **[!UICONTROL Segmentation Jobs]**, selezionare **[!UICONTROL Segmentation jobs]** nel dashboard [!UICONTROL Audiences]. Il dashboard [!UICONTROL Monitoring] contiene metriche e informazioni sui processi di valutazione ed esportazione.

>[!NOTE]
>
>Solo **processi di valutazione della segmentazione** sono supportati per il monitoraggio per pubblico. I processi di esportazione della segmentazione supportano solo il monitoraggio a livello di organizzazione.

![Viene visualizzato il dashboard di monitoraggio dei processi di segmentazione. L&#39;opzione per passare da Audiences a Segmentation job è evidenziata.](../assets/ui/monitor-audiences/segmentation-jobs-dashboard.png)

Utilizzare il dashboard [!UICONTROL Segmentation Jobs] per capire se la valutazione e l&#39;esportazione del profilo si verificano in tempo e senza eccezioni, in modo che i servizi a valle per l&#39;attivazione della destinazione possano disporre dei dati di profilo valutati più recenti.

Per i processi di segmentazione sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Segmentation job]** | Indica il nome del processo di segmentazione. |
| **[!UICONTROL Type]** | Indica il tipo di processo di segmentazione, esportazione o valutazione. In entrambi i casi, il processo di segmentazione valuta o esporta **tutti** i tipi di pubblico appartenenti a un&#39;organizzazione. Per ulteriori informazioni sui processi di esportazione, leggere la guida sull&#39;endpoint dei [processi di esportazione](../../segmentation/api/export-jobs.md). Per ulteriori informazioni sui processi di valutazione, consulta l&#39;esercitazione su [valutazione di una definizione di segmento](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Job start]** | La data e l’ora di inizio del processo di segmentazione. |
| **[!UICONTROL Job end]** | La data e l’ora in cui il processo di segmentazione è stato completato. |
| **[!UICONTROL Status]** | Stato del processo completato. Gli stati possibili per il processo di segmentazione includono Completato o Non riuscito. |
