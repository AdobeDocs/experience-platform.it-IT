---
keywords: Experience Platform;home;argomenti popolari;monitorare i profili;monitorare i flussi di dati;flusso di dati;profilo;profilo cliente in tempo reale;
description: Real-Time Customer Profile consente di visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Questo tutorial fornisce istruzioni su come monitorare i flussi di dati con i profili utilizzando l’interfaccia utente di Experienci Platform.
title: Monitorare i flussi di dati per i profili nell’interfaccia utente
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 10%

---

# Monitorare i flussi di dati per i profili nell’interfaccia utente

Real-Time Customer Profile consente di visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

La dashboard di monitoraggio offre una rappresentazione visiva dell’attività dei dati all’interno di Profilo, incluso lo stato dei Profili dei dati. Questa esercitazione fornisce istruzioni su come utilizzare il dashboard di monitoraggio per monitorare i profili dei dati utilizzando l’interfaccia utente di Experienci Platform, che consente di tenere traccia dello stato di elaborazione del profilo.

## Introduzione {#getting-started}

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Flussi dati](../home.md): i flussi di dati sono una rappresentazione dei processi di dati che spostano i dati in Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile], e a [!DNL Destinations].
   - [Il flusso di dati viene eseguito](../../sources/notifications.md): le esecuzioni dei flussi di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
- [Profilo cliente in tempo reale](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

## Monitoraggio del dashboard dei profili {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Elaborazione dei profili"
>abstract="La vista Elaborazione dei profili contiene informazioni sui record acquisiti in Profile Service, tra cui il numero di frammenti di profilo creati, i frammenti di profilo aggiornati e il numero totale di frammenti di profilo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Dettagli dell’esecuzione del flusso di dati"
>abstract="Nella pagina Dettagli dell’esecuzione del flusso di dati sono visualizzate ulteriori informazioni sull’esecuzione del flusso di dati Profilo, inclusi l’ID organizzazione e l’ID di esecuzione del flusso di dati."

Per accedere al **[!UICONTROL Profili]** dashboard, seleziona **[!UICONTROL Monitorare]** nel menu di navigazione a sinistra. Una volta al **[!UICONTROL Monitorare]** , seleziona la **[!UICONTROL Profili]** Card.

![La scheda Profili. Vengono visualizzate informazioni sul numero di record ricevuti, sul numero di frammenti di profilo creati e aggiornati e sulla percentuale di successo.](../assets/ui/monitor-profiles/focus-card.png)

Principale **[!UICONTROL Profili]** dashboard, il **[!UICONTROL Profili]** Questa scheda mostra informazioni sul numero totale di record ricevuti, sul numero di frammenti di profilo creati e aggiornati e sulla percentuale di successo di frammenti di profilo creati e aggiornati.

La dashboard stessa contiene metriche sull’elaborazione del profilo. Per impostazione predefinita, nel dashboard vengono visualizzati i dettagli di elaborazione del profilo per le origini dell’organizzazione nelle ultime 24 ore.

![Il dashboard Profili. Vengono visualizzate informazioni sul numero di record di profilo ricevuti per origine.](../assets/ui/monitor-profiles/sources.png)

Il [!UICONTROL Elaborazione profilo] La pagina contiene informazioni sui record acquisiti in [!DNL Profile], compreso il numero di frammenti di profilo creati, di frammenti di profilo aggiornati e il numero totale di frammenti di profilo.

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Nome origine]** | Nome dell&#39;origine. |
| **[!UICONTROL Record ricevuti]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Record con errori]** | Numero di record acquisiti, ma non in [!DNL Profile] per errori. |
| **[!UICONTROL Frammenti di profilo creati]** | Numero di nuove reti [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Frammenti di profilo aggiornati]** | Il numero di [!DNL Profile] frammenti aggiornati. |
| **[!UICONTROL Frammenti di profilo totali]** | Numero totale di record scritti in [!DNL Profile], inclusi tutti gli esistenti [!DNL Profile] frammenti aggiornati e nuovi [!DNL Profile] frammenti creati. |
| **[!UICONTROL Totale flussi di dati non riusciti]** | Numero di esecuzioni del flusso di dati non riuscite. |

Puoi selezionare l’icona del filtro ![Icona Filtro](../assets/ui/monitor-profiles/filter.png) accanto al nome dell’origine per visualizzare le informazioni di elaborazione del profilo per i flussi di dati dell’origine selezionata.

![L’icona del filtro viene evidenziata. Selezionando questa icona è possibile visualizzare i flussi di dati dell&#39;origine selezionata.](../assets/ui/monitor-profiles/sources-filter.png)

In alternativa, è possibile selezionare **[!UICONTROL Flussi dati]** sull’interruttore per visualizzare i dettagli di elaborazione del profilo per i flussi di dati della tua organizzazione per le ultime 24 ore.

![Il dashboard Profili. Vengono visualizzate informazioni sul numero di record profilo ricevuti per flusso di dati.](../assets/ui/monitor-profiles/dataflows.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Flusso di dati]** | Nome del flusso di dati. |
| **[!UICONTROL Set di dati]** | Nome del set di dati in cui il flusso di dati viene inserito. |
| **[!UICONTROL Nome origine]** | Nome dell’origine a cui appartiene il flusso di dati. |
| **[!UICONTROL Record ricevuti**] | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Record con errori]** | Numero di record acquisiti, ma non in [!DNL Profile] per errori. |
| **[!UICONTROL Frammenti di profilo creati]** | Numero di nuove reti [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Frammenti di profilo aggiornati]** | Il numero di [!DNL Profile] frammenti aggiornati |
| **[!UICONTROL Frammenti di profilo totali]** | Numero totale di record scritti in [!DNL Profile], inclusi tutti gli esistenti [!DNL Profile] frammenti aggiornati e nuovi [!DNL Profile] frammenti creati. |
| **[!UICONTROL Totale esecuzioni di flusso non riuscite]** | Numero di esecuzioni del flusso di dati non riuscite. |
| **[!UICONTROL Ultima attività]** | Il timestamp dell’ultima esecuzione del flusso di dati. |

Seleziona l’icona del filtro ![filter](../assets/ui/monitor-profiles/filter.png) accanto all’ora di inizio dell’esecuzione del flusso di dati per visualizzare ulteriori informazioni sul [!DNL Profile] esecuzione del flusso di dati.

![L’icona del filtro viene evidenziata. Selezionando questa icona puoi visualizzare i dettagli del flusso di dati selezionato.](../assets/ui/monitor-profiles/dataflows-filter.png)

Il [!UICONTROL Dettagli dell’esecuzione del flusso di dati] visualizza ulteriori informazioni sul [!DNL Profile] esecuzione del flusso di dati, inclusi l’ID organizzazione e l’ID esecuzione del flusso di dati. In questa pagina vengono inoltre visualizzati il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Profile], se si verificano errori nel processo di acquisizione.

![Viene visualizzato un dashboard che mostra informazioni dettagliate sul flusso di dati selezionato.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Record ricevuti]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Record con errori]** | Numero di record acquisiti, ma non in [!DNL Profile] per errori. |
| **[!UICONTROL Frammenti di profilo creati]** | Numero di nuove reti [!DNL Profile] frammenti aggiunti. |
| **[!UICONTROL Frammenti di profilo aggiornati]** | Il numero di [!DNL Profile] frammenti aggiornati. |
| **[!UICONTROL Stato]** | Definisce lo stato generale di un flusso di dati. I possibili valori dello stato sono: <ul><li>`Success`: indica che un flusso di dati è attivo e acquisisce i dati in base alla pianificazione fornita.</li><li>`Failed`: indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: indica che il flusso di dati non è ancora attivo. Questo stato si verifica spesso subito dopo la creazione di un nuovo flusso di dati.</li></ul> |
| **[!UICONTROL Avvio esecuzione flusso di dati]** | La data e l’ora in cui è iniziata l’esecuzione del flusso di dati. |
| **[!UICONTROL Ultimo aggiornamento]** | La data e l’ora dell’ultimo aggiornamento del flusso di dati. |
| **[!UICONTROL Riepilogo errori]** | Se l’esecuzione del flusso di dati non è riuscita, viene visualizzato un codice di errore e un riepilogo del motivo per cui non è riuscita. |
| **[!UICONTROL ID esecuzione flusso di dati]** | ID del flusso di dati eseguito. |
| **[!UICONTROL ID organizzazione IMS]** | ID organizzazione a cui appartiene il flusso di dati eseguito. |

È inoltre possibile selezionare l&#39;interruttore per visualizzare i record con errori o i record ignorati. La sezione errori include dettagli sul codice di errore e sul numero di record con errori o esclusi.
