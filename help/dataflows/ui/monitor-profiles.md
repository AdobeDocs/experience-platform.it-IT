---
keywords: Experience Platform;home;argomenti popolari;monitorare i profili;monitorare i flussi di dati;flusso di dati;profilo;profilo cliente in tempo reale;
description: Real-Time Customer Profile consente di visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Questo tutorial fornisce istruzioni su come monitorare i flussi di dati con i profili utilizzando l’interfaccia utente di Experience Platform.
title: Monitorare i flussi di dati per i profili nell’interfaccia utente
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1d60afdf486642398a2d31302db339eb9cb45130
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 6%

---

# Monitorare i flussi di dati per i profili nell’interfaccia utente

Real-Time Customer Profile consente di visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

La dashboard di monitoraggio offre una rappresentazione visiva dell’attività dei dati all’interno di Profilo, incluso lo stato dei Profili dei dati. Questa esercitazione fornisce istruzioni su come utilizzare il dashboard di monitoraggio per monitorare i profili dei dati utilizzando l’interfaccia utente di Experience Platform, che consente di tenere traccia dello stato di elaborazione del profilo.

## Guida introduttiva {#getting-started}

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Flussi dati](../home.md): i flussi dati sono una rappresentazione dei processi di dati che spostano i dati in Experience Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile] e a [!DNL Destinations].
   - [Esecuzioni flusso di dati](../../sources/notifications.md): le esecuzioni del flusso di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
- [Profilo cliente in tempo reale](../../profile/home.md): fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Experience Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Dashboard di monitoraggio dei profili {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Elaborazione dei profili"
>abstract="La vista Elaborazione dei profili contiene informazioni sui record acquisiti in Profile Service, tra cui il numero di frammenti di profilo creati, i frammenti di profilo aggiornati e il numero totale di frammenti di profilo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Dettagli dell’esecuzione del flusso di dati"
>abstract="Nella pagina Dettagli dell’esecuzione del flusso di dati sono visualizzate ulteriori informazioni sull’esecuzione del flusso di dati Profilo, inclusi l’ID organizzazione e l’ID di esecuzione del flusso di dati."

Per accedere al dashboard **[!UICONTROL Profiles]**, seleziona **[!UICONTROL Monitoring]** nel menu di navigazione a sinistra. Una volta nella pagina **[!UICONTROL Monitoring]**, seleziona la scheda **[!UICONTROL Profiles]**.

![Scheda Profili. Vengono visualizzate informazioni sul numero di record ricevuti, sul numero di frammenti di profilo creati e aggiornati e sulla percentuale di successo.](../assets/ui/monitor-profiles/focus-card.png)

Nella dashboard principale di **[!UICONTROL Profiles]**, la scheda **[!UICONTROL Profiles]** mostra informazioni sul numero totale di record ricevuti, il numero di frammenti di profilo creati e aggiornati, nonché il tasso di successo dei frammenti di profilo creati e aggiornati.

La dashboard stessa contiene metriche sull’elaborazione del profilo. Per impostazione predefinita, nel dashboard vengono visualizzati i dettagli di elaborazione del profilo per le origini dell’organizzazione nelle ultime 24 ore.

![Dashboard dei profili. Vengono visualizzate informazioni sul numero di record di profilo ricevuti per origine.](../assets/ui/monitor-profiles/sources.png)

La pagina [!UICONTROL Profile processing] contiene informazioni sui record acquisiti in [!DNL Profile], tra cui il numero di frammenti di profilo creati, i frammenti di profilo aggiornati e il numero totale di frammenti di profilo.

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Source name]** | Nome dell&#39;origine. |
| **[!UICONTROL Records received]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Records failed]** | Numero di record acquisiti, ma non in [!DNL Profile] a causa di errori. |
| **[!UICONTROL Profile fragments created]** | Numero di nuovi [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Profile fragments updated]** | Numero di frammenti [!DNL Profile] esistenti aggiornati. |
| **[!UICONTROL Total Profile fragments]** | Numero totale di record scritti in [!DNL Profile], inclusi tutti i frammenti [!DNL Profile] esistenti aggiornati e i nuovi frammenti [!DNL Profile] creati. |
| **[!UICONTROL Total failed dataflows]** | Numero di esecuzioni del flusso di dati non riuscite. |

È possibile selezionare l&#39;icona del filtro ![Icona filtro](/help/images/icons/filter.png) accanto al nome dell&#39;origine per visualizzare le informazioni di elaborazione del profilo per i flussi di dati dell&#39;origine selezionata.

In alternativa, puoi selezionare **[!UICONTROL Dataflows]** sull&#39;interruttore per visualizzare i dettagli di elaborazione del profilo per i flussi di dati della tua organizzazione per le ultime 24 ore.

![Dashboard dei profili. Vengono visualizzate informazioni sul numero di record di profilo ricevuti per flusso di dati.](../assets/ui/monitor-profiles/dataflows.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | Nome del flusso di dati. |
| **[!UICONTROL Dataset]** | Nome del set di dati in cui il flusso di dati viene inserito. |
| **[!UICONTROL Source name]** | Nome dell’origine a cui appartiene il flusso di dati. |
| **[!UICONTROL Data type]** | Tipo di dati ricevuto dal set di dati. |
| **[!UICONTROL Records received**] | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Records failed]** | Numero di record acquisiti, ma non in [!DNL Profile] a causa di errori. |
| **[!UICONTROL Profile fragments created]** | Numero di nuovi [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Profile fragments updated]** | Numero di frammenti [!DNL Profile] esistenti aggiornati |
| **[!UICONTROL Total Profile fragments]** | Numero totale di record scritti in [!DNL Profile], inclusi tutti i frammenti [!DNL Profile] esistenti aggiornati e i nuovi frammenti [!DNL Profile] creati. |
| **[!UICONTROL Total failed flow runs]** | Numero di esecuzioni del flusso di dati non riuscite. |
| **[!UICONTROL Last active]** | Il timestamp dell’ultima esecuzione del flusso di dati. |

Seleziona l&#39;icona filtro ![filter](/help/images/icons/filter.png) accanto all&#39;ora di inizio dell&#39;esecuzione del flusso di dati per visualizzare ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Profile].

Viene visualizzato un dashboard in cui vengono visualizzati tutti i flussi di dati eseguiti. Questo dashboard contiene metriche sul flusso di dati eseguito, nonché grafici che mostrano il tasso di successo, i frammenti di profilo creati e i frammenti di profilo aggiornati.

![Il flusso di dati esegue il dashboard. Vengono visualizzate informazioni sul flusso di dati in esecuzione.](../assets/ui/monitor-profiles/dataflow-run.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

>[!NOTE]
>
>Quando l’esecuzione del flusso di dati è nello stato **[!UICONTROL Processing]**, puoi visualizzare le informazioni sullo stato di preparazione visualizzando gli stati dei punti di controllo nel processo di acquisizione.
>
>![Viene visualizzata la bolla di preparazione all&#39;acquisizione del profilo.](../assets/ui/monitor-profiles/profile-ingestion-readiness.png){zoomable="yes" width="300"}

| Metrica | Descrizione |
| ------ | ----------- |
| **[!UICONTROL Dataflow run start]** | L’ora in cui l’esecuzione del flusso di dati è iniziata in UTC. |
| **[!UICONTROL Data type]** | Tipo di dati ricevuti dal flusso di dati. |
| **[!UICONTROL Records received]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Records failed]** | Numero di record acquisiti, ma non in [!DNL Profile] a causa di errori. |
| **[!UICONTROL Profile fragments created]** | Numero di nuovi [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Profile fragments updated]** | Numero di frammenti [!DNL Profile] esistenti aggiornati. |
| **[!UICONTROL Total profile fragments]** | Numero totale di record scritti in [!DNL Profile], inclusi tutti i frammenti [!DNL Profile] esistenti aggiornati e i nuovi frammenti [!DNL Profile] creati. |
| **[!UICONTROL Processing time]** | Quantità di tempo necessaria per l’elaborazione dell’esecuzione del flusso di dati. |
| **[!UICONTROL Status]** | Stato dell’esecuzione del flusso di dati. I valori possibili sono [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] e [!UICONTROL Processing]. |
| **[!UICONTROL Ready for customer segmentation]** | Uno stato che indica se i record acquisiti sono pronti per essere utilizzati nella segmentazione del cliente. I valori possibili sono [!UICONTROL Yes], [!UICONTROL Failed], [!UICONTROL Queued] e [!UICONTROL Processing]. Anche se il **Stato** del flusso di dati è in elaborazione, se il valore di questo campo è Sì, puoi utilizzare i profili nella segmentazione del cliente. |
| **[!UICONTROL Ready for lookup]** | Uno stato che indica se i record acquisiti sono pronti per l’utilizzo nella ricerca Adobe Journey Optimizer.  I valori possibili sono [!UICONTROL Yes], [!UICONTROL Failed], [!UICONTROL Queued] e [!UICONTROL Processing]. Anche se il **Stato** del flusso di dati è in elaborazione, se il valore di questo campo è Sì, puoi utilizzare i profili nella ricerca Journey Optimizer. |

Nella pagina [!UICONTROL Dataflow run details] vengono visualizzate ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Profile], inclusi l&#39;ID organizzazione e l&#39;ID esecuzione flusso di dati. In questa pagina vengono inoltre visualizzati il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Profile], nel caso in cui si verifichino errori nel processo di acquisizione.

![Viene visualizzato un dashboard contenente informazioni dettagliate sul flusso di dati selezionato.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Records received]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Records failed]** | Numero di record acquisiti, ma non in [!DNL Profile] a causa di errori. |
| **[!UICONTROL Profile fragments created]** | Numero di nuovi [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Profile fragments updated]** | Numero di frammenti [!DNL Profile] esistenti aggiornati. |
| **[!UICONTROL Status]** | Definisce lo stato generale di un flusso di dati. I possibili valori dello stato sono: <ul><li>`Success`: indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita.</li><li>`Failed`: indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: indica che il flusso di dati non è ancora attivo. Questo stato si verifica spesso subito dopo la creazione di un nuovo flusso di dati.</li></ul> |
| **[!UICONTROL Dataflow run start]** | La data e l’ora in cui è iniziata l’esecuzione del flusso di dati. |
| **[!UICONTROL Last updated]** | La data e l’ora dell’ultimo aggiornamento del flusso di dati. |
| **[!UICONTROL Error summary]** | Se l’esecuzione del flusso di dati non è riuscita, viene visualizzato un codice di errore e un riepilogo del motivo per cui non è riuscita. |
| **[!UICONTROL Dataflow run ID]** | ID del flusso di dati eseguito. |
| **[!UICONTROL IMS org ID]** | ID organizzazione a cui appartiene il flusso di dati eseguito. |

È inoltre possibile selezionare l&#39;interruttore per visualizzare i record con errori o i record ignorati. La sezione errori include dettagli sul codice di errore e sul numero di record con errori o esclusi.
