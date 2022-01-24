---
keywords: Experience Platform;home;argomenti comuni;monitorare account;monitorare flussi di dati;flussi di dati;destinazioni
description: Le destinazioni ti consentono di attivare i tuoi dati da Adobe Experience Platform a innumerevoli partner esterni. Questa esercitazione fornisce istruzioni su come monitorare i flussi di dati per le destinazioni utilizzando l’interfaccia utente di Experience Platform.
solution: Experience Platform
title: Monitorare i flussi di dati per le destinazioni nell’interfaccia utente
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: b9f9e709fe51000a32eaea7a1a7c76488a36dd9b
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 0%

---

# Monitorare i flussi di dati per le destinazioni nell’interfaccia utente

Le destinazioni ti consentono di attivare i tuoi dati da Adobe Experience Platform a innumerevoli partner esterni. Platform semplifica il processo di tracciamento del flusso di dati verso le destinazioni fornendo trasparenza con i flussi di dati.

Il dashboard di monitoraggio fornisce una rappresentazione visiva del percorso di un flusso di dati, inclusa la destinazione a cui vengono attivati i dati. Questa esercitazione fornisce istruzioni su come monitorare i flussi di dati direttamente nell’area di lavoro delle destinazioni o utilizza il dashboard di monitoraggio per monitorare i flussi di dati per le destinazioni tramite l’interfaccia utente di Experience Platform.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Flussi di dati](../home.md): I flussi di dati sono una rappresentazione dei processi di trasferimento dei dati in Platform. I flussi di dati sono configurati su diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, fino a [!DNL Identity] e [!DNL Profile]e a [!DNL Destinations].
   - [Corse del flusso di dati](../../sources/notifications.md): Le esecuzioni dei flussi di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
- [Destinazioni](../../destinations/home.md): Le destinazioni sono integrazioni predefinite con applicazioni comunemente utilizzate che consentono l’attivazione senza soluzione di continuità dei dati da Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Monitorare i flussi di dati nell’area di lavoro Destinazioni {#monitor-dataflows-in-the-destinations-workspace}

In **[!UICONTROL Destinazioni]** nell’interfaccia utente di Platform, passa alla **[!UICONTROL Sfoglia]** e selezionare il nome di una destinazione che si desidera visualizzare.

![](../assets/ui/monitor-destinations/select-destination.png)

Viene visualizzato un elenco dei flussi di dati esistenti. In questa pagina è riportato un elenco di flussi di dati visualizzabili, con informazioni sulla loro destinazione, nome utente, numero di flussi di dati e stato.

Per ulteriori informazioni sugli stati, consulta la tabella seguente:

| Stato | Descrizione |
| ------ | ----------- |
| Abilitata | The `Enabled` status indicates that a dataflow is active and is exporting data according to the schedule it was provided. |
| Disabilitata | La `Disabled` lo stato indica che un flusso di dati è inattivo e non esporta alcun dato. |
| Elaborazione | La `Processing` lo stato indica che un flusso di dati non è ancora attivo. Questo stato viene spesso rilevato immediatamente dopo la creazione di un nuovo flusso di dati. |
| Errore | La `Error` lo stato indica che il processo di attivazione di un flusso di dati è stato interrotto. |

### Il flusso di dati viene eseguito per le destinazioni di streaming {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated"
>title="Identità attivate"
>abstract="Numero di singole identità di profilo attivate correttamente nella destinazione selezionata."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded"
>title="Identità escluse"
>abstract="Il conteggio dei singoli record di profilo esclusi dall’attivazione per la destinazione selezionata in base agli attributi mancanti e alla violazione del consenso."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed"
>title="Identità non riuscite"
>abstract="Numero di singole identità di profilo che non sono riuscite per la destinazione selezionata. Per ulteriori informazioni, controlla la diagnostica degli errori."
>additional-url="https://adobe.com/go/destinations-monitor-dataflows-batch-en" text="Ulteriori informazioni nella documentazione"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Dettagli dell&#39;esecuzione del dataflow"
>abstract="I dettagli dell’esecuzione del flusso di dati di destinazione contengono informazioni sullo stato di attivazione del segmento e sulle metriche prelevate da Profilo cliente in tempo reale per generare identità univoche. Per ulteriori informazioni, consulta la guida alle definizioni delle metriche ."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Profili ricevuti"
>abstract="Numero totale di profili ricevuti nel flusso di dati. Questo valore viene aggiornato ogni 60 minuti."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Identità attivate"
>abstract="Numero di singole identità di profilo attivate correttamente nella destinazione selezionata."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Identità escluse"
>abstract="Il conteggio dei singoli record di profilo esclusi dall’attivazione per la destinazione selezionata in base agli attributi mancanti e alla violazione del consenso."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Identità non riuscite"
>abstract="Numero di singole identità di profilo che non sono riuscite per la destinazione selezionata. Per ulteriori informazioni, controlla la diagnostica degli errori."
>text="Learn more in documentation"

Per le destinazioni di streaming, l’ [!UICONTROL Corse del flusso di dati] La scheda fornisce un aggiornamento orario per i dati delle metriche in esecuzione nel flusso di dati. Le statistiche più importanti etichettate sono quelle sulle identità.

Le identità rappresentano i diversi facet di un profilo. Ad esempio, se un profilo contiene sia un numero di telefono che un indirizzo e-mail, questo avrà due identità.

Viene visualizzato un elenco di singole esecuzioni e le relative metriche specifiche, insieme ai seguenti totali per le identità:

- **[!UICONTROL Identità attivate]**: Numero totale di identità di profilo create o aggiornate per l’attivazione.
- **[!UICONTROL Identità escluse]**: Numero totale di identità di profilo saltate per l’attivazione in base agli attributi mancanti e alla violazione del consenso.
- **[!UICONTROL Identità non riuscite]**: Numero totale di identità di profilo non attivate nella destinazione a causa di errori.

![](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Ogni singola esecuzione di un flusso di dati mostra i seguenti dettagli:

- **[!UICONTROL Avvio esecuzione flusso di dati]**: Data di inizio dell&#39;esecuzione del flusso di dati.
- **[!UICONTROL Tempo di elaborazione]**: Il tempo necessario all’elaborazione del flusso di dati.
- **[!UICONTROL Profili ricevuti]**: Numero totale di profili ricevuti nel flusso di dati.
- **[!UICONTROL Identità attivate]**: Numero totale di identità di profilo attivate correttamente nella destinazione selezionata.
- **[!UICONTROL Identità escluse]**: Il numero totale di identità di profilo escluse dall’attivazione in base agli attributi mancanti e alla violazione del consenso.
- **[!UICONTROL Identità non riuscite]** Numero totale di identità di profilo non attivate nella destinazione a causa di errori.
- **[!UICONTROL Tasso di attivazione]**: Percentuale di identità ricevute che sono state attivate o saltate correttamente. La formula seguente illustra come viene calcolato questo valore:
   ![](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Stato]**: Rappresenta lo stato in cui si trova il flusso di dati: o [!UICONTROL Completato] o [!UICONTROL Elaborazione]. [!UICONTROL Completato] significa che tutte le identità per l’esecuzione del flusso di dati corrispondente sono state esportate entro un periodo di un’ora. [!UICONTROL Elaborazione] significa che l’esecuzione del flusso di dati non è ancora stata completata.

Per visualizzare i dettagli di una particolare esecuzione di un flusso di dati, selezionare l’ora di inizio dell’esecuzione dall’elenco.

La pagina dei dettagli di un’esecuzione del flusso di dati contiene informazioni aggiuntive, come il numero di profili ricevuti, il numero di identità attivate, il numero di identità non riuscite e il numero di identità escluse.

![](../assets/ui/monitor-destinations/dataflow-details-stream.png)

Nella pagina dei dettagli viene inoltre visualizzato un elenco di identità con errore e identità escluse. Vengono visualizzate informazioni sia per le identità non riuscite che per quelle escluse, incluso il codice di errore, il conteggio delle identità e la descrizione. Per impostazione predefinita, nell’elenco sono visualizzate le identità non riuscite. Per mostrare le identità saltate, seleziona la **[!UICONTROL Identità escluse]** alternare.

![](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### Esecuzione del flusso di dati per le destinazioni batch {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received"
>title="Profili ricevuti"
>abstract="Numero totale di profili ricevuti nel flusso di dati. Questo valore viene aggiornato ogni 60 minuti."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_batch"
>title="Dettagli dell&#39;esecuzione del dataflow"
>abstract="I dettagli dell’esecuzione del flusso di dati di destinazione contengono informazioni sullo stato di attivazione del segmento e sulle metriche prelevate da Profilo cliente in tempo reale per generare identità univoche. Per ulteriori informazioni, consulta la guida alle definizioni delle metriche ."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Profili ricevuti"
>abstract="Numero totale di profili ricevuti nel flusso di dati. Questo valore viene aggiornato ogni 60 minuti."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Identità attivate"
>abstract="The count of individual profile identities successfully activated to the selected destination."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Identità escluse"
>abstract="The count of individual profile records excluded from activation for the selected destination based on missing attributes and consent violation."
>text="Learn more in documentation"

Per le destinazioni batch, [!UICONTROL Corse del flusso di dati] fornisce i dati delle metriche sulle esecuzioni del flusso di dati. Viene visualizzato un elenco di singole esecuzioni e le relative metriche specifiche, insieme ai seguenti totali per le identità:

- **[!UICONTROL Identità attivate]**: Numero di singole identità di profilo attivate correttamente nella destinazione selezionata.
- **[!UICONTROL Identità escluse]**: Il conteggio delle singole identità di profilo escluse dall’attivazione per la destinazione selezionata, in base agli attributi mancanti e alla violazione del consenso.

![](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Ogni singola esecuzione di un flusso di dati mostra i seguenti dettagli:

- **[!UICONTROL Dataflow run start]**: The time that the dataflow run started at.
- **[!UICONTROL Tempo di elaborazione]**: Il tempo necessario all’elaborazione dell’esecuzione del flusso di dati.
- **[!UICONTROL Profili ricevuti]**: Numero totale di profili ricevuti nel flusso di dati. Questo valore viene aggiornato ogni 60 minuti.
- **[!UICONTROL Identità attivate]**: Numero totale di identità di profilo attivate correttamente nella destinazione selezionata.
- **[!UICONTROL Identità escluse]**: Il numero totale di identità di profilo escluse dall’attivazione in base agli attributi mancanti e alla violazione del consenso.
- **[!UICONTROL Stato]**: Rappresenta lo stato in cui si trova il flusso di dati. Può essere uno dei tre stati seguenti: [!UICONTROL Completato], [!UICONTROL Non riuscito]e [!UICONTROL Elaborazione]. [!UICONTROL Completato] significa che il flusso di dati è attivo ed esporta i dati in base alla pianificazione fornita. [!UICONTROL Non riuscito] significa che l’attivazione dei dati è stata sospesa a causa di errori. [!UICONTROL Elaborazione] significa che il flusso di dati non è ancora attivo e viene generalmente rilevato quando viene creato un nuovo flusso di dati.

Per visualizzare i dettagli di un’esecuzione di un flusso di dati specifico, selezionare l’ora di inizio dell’esecuzione dall’elenco.

>[!NOTE]
>
>Le esecuzioni dei flussi di dati vengono generate in base alla frequenza di pianificazione del flusso di dati di destinazione. Viene eseguita un&#39;esecuzione separata del flusso di dati per ogni criterio di unione applicato a un segmento.

The details page for a dataflow, in addition to the details shown on the dataflows list, displays more specific information about the dataflow:

- **[!UICONTROL Dimensione dei dati]**: Dimensione del flusso di dati da esportare.
- **[!UICONTROL File totali]**: Numero totale di file esportati nel flusso di dati.
- **[!UICONTROL Ultimo aggiornamento]**: L’ora dell’ultimo aggiornamento del flusso di dati.

![](../assets/ui/monitor-destinations/dataflow-batch.png)

The details page also displays a list of identities that failed and identities that were excluded. Vengono visualizzate le informazioni sia per le identità non riuscite che per quelle escluse, compreso il codice di errore e la descrizione. By default, the list displays the failed identities. To show excluded identities, select the **[!UICONTROL Identities excluded]** toggle.

![](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## Monitoring Destinations dashboard {#monitoring-destinations-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activation"
>abstract="L’attivazione di destinazione contiene informazioni sullo stato di attivazione del segmento e sulle metriche prelevate da Profilo cliente in tempo reale per generare identità univoche."

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Processi dei segmenti"
>abstract="Il dashboard processi segmento contiene informazioni sui processi di valutazione ed esportazione per tutti i segmenti."

Per accedere al [!UICONTROL Monitoraggio] dashboard, seleziona **[!UICONTROL Monitoraggio]** (![icona di monitoraggio](../assets/ui/monitor-destinations/monitoring-icon.png)) nella navigazione a sinistra. Una volta sul [!UICONTROL Monitoraggio] pagina, seleziona [!UICONTROL Destinazioni]. La [!UICONTROL Monitoraggio] il dashboard contiene metriche e informazioni sui processi di esecuzione di destinazione.

Al centro del dashboard c&#39;è il pannello Activation , che contiene metriche e grafici che mostrano dati sulla frequenza di attivazione dei dati esportati nelle destinazioni.

![](../assets/ui/monitor-destinations/dashboard-graph.png)


Per impostazione predefinita, i dati visualizzati contengono i tassi di attivazione delle ultime 24 ore. Seleziona **[!UICONTROL Ultime 24 ore]** per regolare l&#39;intervallo di tempo dei record visualizzati. Le opzioni disponibili includono **[!UICONTROL Ultime 24 ore]**, **[!UICONTROL Ultimi 7 giorni]** e **[!UICONTROL Ultimi 30 giorni]**. In alternativa, è possibile selezionare le date nella finestra a comparsa del calendario visualizzata. Dopo aver selezionato le date, seleziona **[!UICONTROL Applica]** per regolare l&#39;intervallo di tempo delle informazioni visualizzate.

>[!NOTE]
>
>La schermata seguente mostra il tasso di attivazione per gli ultimi 30 giorni invece delle ultime 24 ore. È possibile regolare l&#39;intervallo di tempo selezionando **[!UICONTROL Ultimi 30 giorni]**.

![](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Il grafico viene visualizzato per impostazione predefinita ed è possibile disattivarlo per espandere l’elenco di destinazioni riportato di seguito. Seleziona la **[!UICONTROL Metriche e grafici]** per disattivare i grafici.

La **[!UICONTROL Attivazione]** visualizza un elenco di destinazioni che contengono almeno un account esistente. Questo elenco include anche informazioni sui profili ricevuti, sui record di profilo attivati, sui record di profilo non riusciti, sui record di profilo saltati, sul totale dei flussi di dati non riusciti e sull’ultima data di aggiornamento per queste destinazioni.

![](../assets/ui/monitor-destinations/dashboard-destinations.png)

Puoi anche filtrare l’elenco di destinazioni per visualizzare solo la categoria di destinazioni selezionata. Seleziona la **[!UICONTROL Destinazioni personali]** e seleziona il tipo di destinazione in cui desideri filtrare.

![](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Inoltre, puoi inserire una destinazione nella barra di ricerca per isolarla in una singola destinazione. Per visualizzare i flussi di dati della destinazione, seleziona il filtro ![filter](../assets/ui/monitor-destinations/filter.png) accanto a per visualizzare un elenco dei relativi flussi di dati attivi.

![](../assets/ui/monitor-destinations/filtered-destinations.png)

Se desideri visualizzare tutti i flussi di dati esistenti tra tutte le destinazioni, seleziona **[!UICONTROL Flussi di dati]**.

Viene visualizzato un elenco di flussi di dati raggruppati per destinazione. Puoi visualizzare ulteriori dettagli per un flusso di dati specifico individuando la destinazione da monitorare, selezionando il filtro ![filter](../assets/ui/monitor-destinations/filter.png) accanto a esso, quindi selezionando il filtro ![filter](../assets/ui/monitor-destinations/filter.png) accanto al flusso di dati desideri ulteriori informazioni.

![](../assets/ui/monitor-destinations/dashboard-dataflows.png)


La pagina delle esecuzioni del flusso di dati visualizza informazioni sulle esecuzioni del flusso di dati, tra cui l’ora di inizio del flusso di dati, il tempo di elaborazione, i profili ricevuti, le identità attivate, le identità escluse, le identità non riuscite, il tasso di attivazione e lo stato. Per visualizzare ulteriori dettagli sull’esecuzione di un flusso di dati specifico, seleziona il filtro ![filter](../assets/ui/monitor-destinations/filter.png) accanto all’ora di avvio del flusso di dati.

![](../assets/ui/monitor-destinations/dashboard-dataflows-filter.png)

Oltre ai dettagli visualizzati nell’elenco dei flussi di dati, nella pagina dei dettagli dei flussi di dati vengono visualizzate informazioni più specifiche relative al flusso di dati:

- **[!UICONTROL ID esecuzione flusso di dati]**: ID del flusso di dati.
- **[!UICONTROL ID organizzazione IMS]**: Organizzazione IMS a cui appartiene il flusso di dati.
- **[!UICONTROL Ultimo aggiornamento]**: L’ora dell’ultimo aggiornamento del flusso di dati.

Nella pagina dei dettagli viene inoltre visualizzato un elenco di identità con errore e identità escluse. Vengono visualizzate informazioni sia per le identità non riuscite che per quelle escluse, incluso il codice di errore, il conteggio delle identità e la descrizione. Per impostazione predefinita, nell’elenco sono visualizzate le identità non riuscite. Per mostrare le identità saltate, seleziona la **[!UICONTROL Identità escluse]** alternare.

![](../assets/ui/monitor-destinations/identities-excluded.png)

## Passaggi successivi

Seguendo questa guida, ora sai come monitorare i flussi di dati sia per le destinazioni batch che per quelle in streaming, comprese tutte le informazioni rilevanti quali il tempo di elaborazione, il tasso di attivazione e lo stato. Per ulteriori informazioni sui flussi di dati in Platform, consulta la sezione [panoramica dei dataflows](../home.md). Per ulteriori informazioni sulle destinazioni, consulta il [panoramica sulle destinazioni](../../destinations/home.md).