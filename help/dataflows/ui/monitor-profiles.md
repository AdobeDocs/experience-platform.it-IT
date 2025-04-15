---
keywords: Experience Platform;home;argomenti popolari;monitorare i profili;monitorare i flussi di dati;flusso di dati;profilo;profilo cliente in tempo reale;
description: Real-Time Customer Profile consente di visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Questo tutorial fornisce istruzioni su come monitorare i flussi di dati con i profili utilizzando l’interfaccia utente di Experience Platform.
title: Monitorare i flussi di dati per i profili nell’interfaccia utente
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 7%

---

# Monitorare i flussi di dati per i profili nell’interfaccia utente

Real-Time Customer Profile consente di visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

La dashboard di monitoraggio offre una rappresentazione visiva dell’attività dei dati all’interno di Profilo, incluso lo stato dei Profili dei dati. Questa esercitazione fornisce istruzioni su come utilizzare il dashboard di monitoraggio per monitorare i profili dei dati utilizzando l’interfaccia utente di Experience Platform, che consente di tenere traccia dello stato di elaborazione del profilo.

## Introduzione {#getting-started}

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

Per accedere al dashboard **[!UICONTROL Profili]**, selezionare **[!UICONTROL Monitoraggio]** nell&#39;area di navigazione a sinistra. Nella pagina **[!UICONTROL Monitoraggio]**, seleziona la scheda **[!UICONTROL Profili]**.

![Scheda Profili. Vengono visualizzate informazioni sul numero di record ricevuti, sul numero di frammenti di profilo creati e aggiornati e sulla percentuale di successo.](../assets/ui/monitor-profiles/focus-card.png)

Nella dashboard principale di **[!UICONTROL Profili]**, la scheda **[!UICONTROL Profili]** mostra informazioni sul numero totale di record ricevuti, sul numero di frammenti di profilo creati e aggiornati, nonché sulla percentuale di successo dei frammenti di profilo creati e aggiornati.

La dashboard stessa contiene metriche sull’elaborazione del profilo. Per impostazione predefinita, nel dashboard vengono visualizzati i dettagli di elaborazione del profilo per le origini dell’organizzazione nelle ultime 24 ore.

![Dashboard dei profili. Vengono visualizzate informazioni sul numero di record di profilo ricevuti per origine.](../assets/ui/monitor-profiles/sources.png)

La [!UICONTROL pagina Elaborazione] profilo contiene informazioni sui record inseriti in [!DNL Profile], inclusi il numero di frammenti di profilo creati, i frammenti di profilo aggiornati e il numero totale di frammenti di profilo.

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Nome Source]** | Nome dell&#39;origine. |
| **[!UICONTROL Documenti ricevuti]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Record non riusciti]** | Il numero di record che sono stati ingeriti, ma non a [!DNL Profile] causa di errori. |
| **[!UICONTROL Frammenti di profilo creati]** | Numero di nuovi [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Frammenti di profilo aggiornati]** | Numero di frammenti esistenti [!DNL Profile] aggiornati. |
| **[!UICONTROL Totale frammenti di profilo]** | Numero totale di record scritti in [!DNL Profile], inclusi tutti i frammenti esistenti [!DNL Profile] aggiornati e i nuovi [!DNL Profile] frammenti creati. |
| **[!UICONTROL Totale flussi di dati non riusciti]** | Numero di esecuzioni del flusso di dati non riuscite. |

È possibile selezionare l&#39;icona del filtro ![Icona filtro](/help/images/icons/filter.png) accanto al nome dell&#39;origine per visualizzare le informazioni di elaborazione del profilo per i flussi di dati dell&#39;origine selezionata.

![L&#39;icona del filtro è evidenziata. La selezione di questa icona consente di visualizzare i flussi di dati dell&#39;origine selezionata.](../assets/ui/monitor-profiles/sources-filter.png)

In alternativa, puoi selezionare **[!UICONTROL Flussi dati]** sull&#39;interruttore per visualizzare i dettagli di elaborazione del profilo per i flussi dati della tua organizzazione per le ultime 24 ore.

![Dashboard dei profili. Vengono visualizzate informazioni sul numero di record di profilo ricevuti per flusso di dati.](../assets/ui/monitor-profiles/dataflows.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Flusso]** | Nome del flusso di dati. |
| **[!UICONTROL Dataset]** | Nome del set di dati in cui viene inserito il flusso di dati. |
| **[!UICONTROL Nome Origine]** | Nome dell&#39;origine a cui appartiene il flusso di dati. |
| **[!UICONTROL Documenti ricevuti**] | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Record non riusciti]** | Numero di record acquisiti, ma non in [!DNL Profile] a causa di errori. |
| **[!UICONTROL Frammenti di profilo creati]** | Numero di nuovi [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Frammenti di profilo aggiornati]** | Numero di frammenti [!DNL Profile] esistenti aggiornati |
| **[!UICONTROL Frammenti di profilo totali]** | Numero totale di record scritti in [!DNL Profile], inclusi tutti i frammenti [!DNL Profile] esistenti aggiornati e i nuovi frammenti [!DNL Profile] creati. |
| **[!UICONTROL Totale esecuzioni di flusso non riuscite]** | Numero di esecuzioni del flusso di dati non riuscite. |
| **[!UICONTROL Ultima attività]** | Il timestamp dell’ultima esecuzione del flusso di dati. |

Seleziona l&#39;icona filtro ![filter](/help/images/icons/filter.png) accanto all&#39;ora di inizio dell&#39;esecuzione del flusso di dati per visualizzare ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Profile].

![L&#39;icona del filtro è evidenziata. La selezione di questa icona consente di visualizzare i dettagli sul flusso di dati selezionato.](../assets/ui/monitor-profiles/dataflows-filter.png)

Nella pagina [!UICONTROL Dettagli esecuzione flusso di dati] sono visualizzate ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Profile], inclusi l&#39;ID organizzazione e l&#39;ID esecuzione flusso di dati. In questa pagina vengono inoltre visualizzati il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Profile], nel caso in cui si verifichino errori nel processo di acquisizione.

![Viene visualizzato un dashboard contenente informazioni dettagliate sul flusso di dati selezionato.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Record ricevuti]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Record non riusciti]** | Numero di record acquisiti, ma non in [!DNL Profile] a causa di errori. |
| **[!UICONTROL Frammenti di profilo creati]** | Numero di nuovi [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Frammenti di profilo aggiornati]** | Numero di frammenti [!DNL Profile] esistenti aggiornati. |
| **[!UICONTROL Stato]** | Definisce lo stato generale di un flusso di dati. I possibili valori dello stato sono: <ul><li>`Success`: indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita.</li><li>`Failed`: indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: indica che il flusso di dati non è ancora attivo. Questo stato si verifica spesso immediatamente dopo la creazione di un nuovo flusso di dati.</li></ul> |
| **[!UICONTROL Avvio esecuzione flusso dati]** | Data e ora di avvio dell&#39;esecuzione del flusso di dati. |
| **[!UICONTROL Ultimo aggiornamento]** | La data e l’ora dell’ultimo aggiornamento del flusso di dati. |
| **[!UICONTROL Errore riepilogo]** | Se l’esecuzione del flusso di dati non è riuscita, viene visualizzato un codice di errore e un riepilogo del motivo per cui non è riuscita. |
| **[!UICONTROL ID esecuzione flusso di dati]** | ID del flusso di dati eseguito. |
| **[!UICONTROL ID organizzazione IMS]** | ID organizzazione a cui appartiene il flusso di dati eseguito. |

È inoltre possibile selezionare l&#39;interruttore per visualizzare i record con errori o i record ignorati. La sezione errori include dettagli sul codice di errore e sul numero di record con errori o esclusi.
