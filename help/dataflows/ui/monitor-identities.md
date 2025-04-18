---
keywords: Experience Platform;home;argomenti popolari;monitorare identità;monitorare flussi di dati;flussi di dati;identità;
description: Il servizio Adobe Experience Platform Identity offre una panoramica completa dei clienti e del loro comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali e di forte impatto in tempo reale. Questo tutorial fornisce istruzioni su come monitorare i flussi di dati con le identità tramite l’interfaccia utente di Experience Platform.
title: Monitorare i flussi di dati per le identità nell’interfaccia utente
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 9%

---

# Monitorare i flussi di dati per le identità nell’interfaccia utente

Adobe Experience Platform Identity Service offre una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

La dashboard di monitoraggio offre una rappresentazione visiva dell’attività dei dati all’interno delle identità, incluso lo stato delle identità dei dati. Questa esercitazione fornisce istruzioni su come utilizzare il dashboard di monitoraggio per monitorare le identità dei dati utilizzando l’interfaccia utente di Experience Platform, che consente di tenere traccia dello stato di elaborazione dell’identità.

## Introduzione {#getting-started}

- [Flussi dati](../home.md): i flussi dati sono una rappresentazione dei processi di dati che spostano i dati in Experience Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile] e a [!DNL Destinations].
   - [Esecuzioni flusso di dati](../../sources/notifications.md): le esecuzioni del flusso di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
- [Identity Service](../../identity-service/home.md): ottieni una migliore visione dei singoli clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Experience Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Dashboard di monitoraggio delle identità {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Elaborazione delle identità"
>abstract="La vista Elaborazione delle identità contiene informazioni sui record acquisiti in Identity Service, tra cui il numero di identità aggiunte, i grafi creati e i grafi aggiornati. Consulta la guida alla definizione delle metriche per ulteriori informazioni su metriche e grafi."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Dettagli dell’esecuzione del flusso di dati"
>abstract="Nella pagina Dettagli dell’esecuzione del flusso di dati sono visualizzate ulteriori informazioni sull’esecuzione del flusso di dati di Identità, inclusi l’ID organizzazione e l’ID di esecuzione del flusso di dati."

Per accedere al dashboard **[!UICONTROL Identità]**, seleziona **[!UICONTROL Monitoraggio]** nell&#39;area di navigazione a sinistra. Nella pagina **[!UICONTROL Monitoraggio]**, seleziona la scheda **[!UICONTROL Identità]**.

![Scheda Identità. Vengono visualizzate informazioni sul numero di record ricevuti, il numero di record acquisiti e il tasso di successo.](../assets/ui/monitor-identities/focus-card.png)

Nella dashboard principale delle **[!UICONTROL Identità]**, la scheda delle **[!UICONTROL Identità]** mostra informazioni sul numero totale di record ricevuti, sul numero di record acquisiti e sulla percentuale di successo dell&#39;acquisizione di record.

Il dashboard stesso contiene metriche sull’elaborazione dell’identità. Per impostazione predefinita, nel dashboard vengono visualizzati i dettagli di elaborazione dell’identità per le origini dell’organizzazione nelle ultime 24 ore.

![Dashboard delle identità. Vengono visualizzate informazioni sul numero di record ricevuti per origine.](../assets/ui/monitor-identities/sources.png)

La pagina [!UICONTROL Elaborazione identità] contiene informazioni sui record acquisiti in [!DNL Identity Service], tra cui il numero di identità aggiunte, i grafici creati e i grafici aggiornati.

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metriche delle identità | Descrizione |
| ---------------- | ----------- |
| **[!UICONTROL Record ricevuti]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Record non riusciti]** | Il numero di record che non sono stati acquisiti in Experience Platform a causa di errori nei dati. |
| **[!UICONTROL Record ignorati]** | Numero di record acquisiti, ma non in [!DNL Identity Service] perché nella riga del record era presente un solo identificatore. |
| **[!UICONTROL Record acquisiti]** | Numero di record acquisiti in [!DNL Identity Service]. |
| **[!UICONTROL Identità aggiunte]** | Numero di nuovi identificatori aggiunti a [!DNL Identity Service]. |
| **[!UICONTROL Grafici creati]** | Numero di nuovi grafi di identità creati in [!DNL Identity Service]. |
| **[!UICONTROL Grafici aggiornati]** | Numero di grafici di identità esistenti aggiornati con i nuovi bordi. |
| **[!UICONTROL Totale flussi di dati non riusciti]** | Numero di esecuzioni del flusso di dati non riuscite. |

È possibile selezionare l&#39;icona del filtro ![Icona filtro](/help/images/icons/filter.png) accanto al nome dell&#39;origine per visualizzare le informazioni sull&#39;elaborazione delle identità per i flussi di dati dell&#39;origine selezionata.

![L&#39;icona del filtro è evidenziata. La selezione di questa icona consente di visualizzare i flussi di dati dell&#39;origine selezionata.](../assets/ui/monitor-identities/sources-filter.png)

In alternativa, puoi selezionare **[!UICONTROL Flussi dati]** per visualizzare i dettagli di elaborazione delle identità per i flussi dati della tua organizzazione nelle ultime 24 ore.

![Dashboard delle identità. Vengono visualizzate informazioni sul numero di identità ricevute per flusso di dati.](../assets/ui/monitor-identities/dataflows.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Flusso di dati]** | Nome del flusso di dati. |
| **[!UICONTROL Set di dati]** | Nome del set di dati in cui il flusso di dati viene inserito. |
| **[!UICONTROL Nome Source]** | Nome dell’origine a cui appartiene il flusso di dati. |
| **[!UICONTROL Record ricevuti]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Record non riusciti]** | Il numero di record che non sono stati acquisiti in Experience Platform a causa di errori nei dati. |
| **[!UICONTROL Record ignorati]** | Numero di record acquisiti, ma non in [!DNL Identity Service] perché nella riga del record era presente un solo identificatore. |
| **[!UICONTROL Record acquisiti]** | Numero di record acquisiti in [!DNL Identity Service]. |
| **[!UICONTROL Record totali]** | Numero totale di tutti i record, inclusi quelli con errori, quelli ignorati, quelli con identità aggiunte e quelli duplicati. |
| **[!UICONTROL Identità aggiunte]** | Numero di nuovi identificatori aggiunti a [!DNL Identity Service]. |
| **[!UICONTROL Grafici creati]** | Numero di nuovi grafi di identità creati in [!DNL Identity Service]. |
| **[!UICONTROL Grafici aggiornati]** | Numero di grafici di identità esistenti aggiornati con i nuovi bordi. |
| **[!UICONTROL Totale flussi di dati non riusciti]** | Numero di esecuzioni del flusso di dati non riuscite. |

Seleziona l&#39;icona filtro ![filter](/help/images/icons/filter.png) accanto all&#39;ora di inizio dell&#39;esecuzione del flusso di dati per visualizzare ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Identity].

![L&#39;icona del filtro è evidenziata. La selezione di questa icona consente di visualizzare i dettagli sul flusso di dati selezionato.](../assets/ui/monitor-identities/dataflows-filter.png)

Nella pagina [!UICONTROL Dettagli esecuzione flusso di dati] sono visualizzate ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Identity], inclusi l&#39;ID organizzazione e l&#39;ID esecuzione flusso di dati. In questa pagina vengono inoltre visualizzati il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Identity Service], nel caso in cui si verifichino errori nel processo di acquisizione.

![Viene visualizzato un dashboard contenente informazioni dettagliate sul flusso di dati selezionato.](../assets/ui/monitor-identities/dataflow-run-details.png)

Per questa visualizzazione dashboard sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| -------| ----------- |
| **[!UICONTROL Record ricevuti]** | Numero di record ricevuti dal data lake. |
| **[!UICONTROL Record non riusciti]** | Il numero di record che non sono stati acquisiti in Experience Platform a causa di errori nei dati. |
| **[!UICONTROL Record ignorati]** | Numero di record acquisiti, ma non in [!DNL Identity Service] perché nella riga del record era presente un solo identificatore. |
| **[!UICONTROL Record acquisiti]** | Numero di record acquisiti in [!DNL Identity Service]. |
| **[!UICONTROL Identità aggiunte]** | Numero di nuovi identificatori aggiunti a [!DNL Identity Service]. |
| **[!UICONTROL Grafici creati]** | Numero di nuovi grafi di identità creati in [!DNL Identity Service]. |
| **[!UICONTROL Grafici aggiornati]** | Numero di grafici di identità esistenti aggiornati con i nuovi bordi. |
| **[!UICONTROL Stato]** | Definisce lo stato generale di un flusso di dati. I possibili valori dello stato sono: <ul><li>`Success`: indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita.</li><li>`Failed`: indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: indica che il flusso di dati non è ancora attivo. Questo stato si verifica spesso subito dopo la creazione di un nuovo flusso di dati.</li></ul> |
| **[!UICONTROL Inizio esecuzione flusso di dati]** | La data e l’ora in cui è iniziata l’esecuzione del flusso di dati. |
| **[!UICONTROL Ultimo aggiornamento]** | La data e l’ora dell’ultimo aggiornamento del flusso di dati. |
| **[!UICONTROL Riepilogo errori]** | Se l’esecuzione del flusso di dati non è riuscita, viene visualizzato un codice di errore e un riepilogo del motivo per cui non è riuscita. |
| **[!UICONTROL ID esecuzione flusso di dati]** | ID del flusso di dati eseguito. |
| **[!UICONTROL ID organizzazione IMS]** | ID organizzazione a cui appartiene il flusso di dati eseguito. |

È inoltre possibile selezionare l&#39;interruttore per visualizzare i record con errori o i record ignorati. La sezione errori include dettagli sul codice di errore e sul numero di record con errori o esclusi.
