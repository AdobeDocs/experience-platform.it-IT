---
keywords: Experience Platform;home;argomenti popolari;monitorare gli account;monitorare i flussi di dati;origini
description: Questa esercitazione fornisce i passaggi per monitorare il flusso di dati, utilizzando sia la vista di monitoraggio aggregato che il monitoraggio interservizio.
solution: Experience Platform
title: Monitorare i flussi di dati per le origini nell’interfaccia utente
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Monitorare i flussi di dati per le origini nell’interfaccia utente

>[!IMPORTANT]
>
>Origini di streaming, come [Origine API HTTP](../../sources/connectors/streaming/http.md) non sono attualmente supportati dal dashboard di monitoraggio. Al momento, è possibile utilizzare il dashboard solo per monitorare le origini batch.

In Adobe Experience Platform, i dati vengono acquisiti da un’ampia varietà di fonti, analizzati all’interno di Experience Platform e attivati in un’ampia varietà di destinazioni. Platform semplifica il processo di tracciamento di questo flusso di dati potenzialmente non lineare fornendo trasparenza con i flussi di dati.

La dashboard di monitoraggio fornisce una rappresentazione visiva del percorso di un flusso di dati. Puoi utilizzare una vista di monitoraggio aggregata e passare verticalmente dal livello di origine a un flusso di dati e a un’esecuzione di flusso di dati, per visualizzare le metriche corrispondenti che contribuiscono al successo o all’errore di un flusso di dati. Puoi anche utilizzare la capacità di monitoraggio cross-service del dashboard di monitoraggio per monitorare il percorso di un flusso di dati da un’origine a [!DNL Identity Service], e a [!DNL Profile].

Questa esercitazione fornisce i passaggi per monitorare il flusso di dati, utilizzando sia la vista di monitoraggio aggregato che il monitoraggio interservizio.

## Introduzione {#getting-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Flussi dati](../home.md): i flussi di dati sono una rappresentazione dei processi di dati che spostano i dati in Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile], e a [!DNL Destinations].
   * [Il flusso di dati viene eseguito](../../sources/notifications.md): le esecuzioni dei flussi di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
* [Sorgenti](../../sources/home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Servizio identità](../../identity-service/home.md): ottieni una visione migliore dei singoli clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Visualizzazione di monitoraggio aggregato {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Acquisizione sorgente"
>abstract="La visualizzazione Acquisizione origine contiene informazioni sullo stato dell’attività dati e sulle metriche nel servizio del data lake, inclusi i record acquisiti e quelli con errori. Per ulteriori informazioni su metriche e grafici, consulta la guida alla definizione delle metriche."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Dettagli dell’esecuzione del flusso di dati"
>abstract="L’elaborazione delle origini contiene informazioni sullo stato dell’attività dati e sulle metriche nel servizio del data lake, inclusi i record acquisiti e quelli con errore. Per ulteriori informazioni su metriche e grafici, consulta la guida alla definizione delle metriche."
>text="Learn more in documentation"

In [Interfaccia utente di Platform](https://platform.adobe.com), seleziona **[!UICONTROL Monitorare]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Monitorare] dashboard. Il [!UICONTROL Monitorare] la dashboard contiene metriche e informazioni su tutti i flussi di dati di origine, incluse informazioni sullo stato del traffico dati da un’origine a [!DNL Identity Service], e a [!DNL Profile].

Al centro del dashboard è presente [!UICONTROL Acquisizione sorgente] , che contiene metriche e grafici che visualizzano i dati sui record acquisiti e sui record con errori.

![monitoraggio-dashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

Per impostazione predefinita, i dati visualizzati contengono i tassi di acquisizione delle ultime 24 ore. Seleziona **[!UICONTROL Ultime 24 ore]** per regolare l&#39;intervallo di tempo dei record visualizzati.

![change-date](../assets/ui/monitor-sources/change-date.png)

Viene visualizzata una finestra a comparsa del calendario che fornisce opzioni per intervalli di tempo di acquisizione alternativi. Seleziona **[!UICONTROL Ultimi 30 giorni]** e quindi seleziona **[!UICONTROL Applica]**

![adjust-time-frame](../assets/ui/monitor-sources/adjust-timeframe.png)

I grafici sono attivati per impostazione predefinita e puoi disattivarli per espandere l’elenco delle sorgenti di seguito. Seleziona la **[!UICONTROL Metriche e grafici]** per disattivare i grafici.

![metriche e grafici](../assets/ui/monitor-sources/metrics-graphs.png)

| Acquisizione sorgente | Descrizione |
| ---------------- | ----------- |
| [!UICONTROL Record acquisiti ] | Numero totale di record acquisiti. |
| [!UICONTROL Record non riusciti] | Numero totale di record che non sono stati acquisiti a causa di errori nei dati. |
| [!UICONTROL Totale flussi di dati non riusciti] | Numero totale di flussi di dati con un `failed` stato. |

Nell’elenco di acquisizione delle origini vengono visualizzate tutte le origini che contengono almeno un account esistente. L’elenco include anche informazioni sul tasso di acquisizione di ogni origine, sul numero di record con errori e sul numero totale di flussi di dati con errori in base all’intervallo di tempo applicato.

![source-ingestion](../assets/ui/monitor-sources/source-ingestion.png)

Per ordinare l&#39;elenco delle origini, selezionare **[!UICONTROL Le mie sorgenti]** quindi seleziona la categoria desiderata dal menu a discesa. Ad esempio, per concentrarti sugli archivi cloud, seleziona  **[!UICONTROL Archiviazione cloud]**

![sort-by-category](../assets/ui/monitor-sources/sort-by-category.png)

Per visualizzare tutti i flussi di dati esistenti tra tutte le origini, seleziona **[!UICONTROL Flussi dati]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

In alternativa, è possibile immettere un&#39;origine nella barra di ricerca per isolare una singola origine. Una volta identificata l’origine, seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto per visualizzare un elenco dei relativi flussi di dati attivi.

![ricerca](../assets/ui/monitor-sources/search.png)

Viene visualizzato un elenco di flussi di dati. Per limitare l’elenco e concentrarti sui flussi di dati con errori, seleziona **[!UICONTROL Mostra solo errori]**.

![show-failures-only](../assets/ui/monitor-sources/show-failures-only.png)

Individua il flusso di dati che desideri monitorare, quindi seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto a esso, per visualizzare ulteriori informazioni sul suo stato di esecuzione.

![flusso di dati](../assets/ui/monitor-sources/dataflow.png)

La pagina di esecuzione del flusso di dati visualizza informazioni sulla data di inizio dell’esecuzione del flusso di dati, sulle dimensioni dei dati, sullo stato e sulla durata dell’elaborazione. Seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto all’ora di inizio dell’esecuzione del flusso di dati per visualizzarne i dettagli.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

Il [!UICONTROL Dettagli dell’esecuzione del flusso di dati] Questa pagina visualizza informazioni sui metadati del flusso di dati, sullo stato di acquisizione parziale e sul riepilogo degli errori. Il riepilogo degli errori contiene l’errore specifico di primo livello che mostra in quale fase il processo di acquisizione ha riscontrato un errore.

Scorri verso il basso per visualizzare informazioni più specifiche sull’errore che si è verificato.

![dettagli dell’esecuzione del flusso di dati](../assets/ui/monitor-sources/dataflow-run-details.png)

Il [!UICONTROL Errori di esecuzione del flusso di dati] nel pannello viene visualizzato l’errore specifico e il codice di errore che ha provocato l’errore di acquisizione del flusso di dati. In questo scenario, si è verificato un errore di trasformazione del mapper, che ha causato il fallimento di 24 record.

Seleziona **[!UICONTROL File]** per ulteriori informazioni.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

Il [!UICONTROL File] Il pannello contiene informazioni sul nome e il percorso del file.

Per una rappresentazione più granulare dell’errore, seleziona **[!UICONTROL Anteprima diagnostica errori]**.

![file](../assets/ui/monitor-sources/files.png)

Il [!UICONTROL Anteprima diagnostica errori] viene visualizzata una finestra che mostra un’anteprima di un massimo di 100 errori nel flusso di dati. Puoi selezionare **[!UICONTROL Scarica]** per recuperare un comando curl, che consente di scaricare la diagnostica degli errori.

Al termine, seleziona **[!UICONTROL Chiudi]**

![error-diagnostics](../assets/ui/monitor-sources/error-diagnostics.png)

Puoi utilizzare il sistema di breadcrumb nell’intestazione superiore per tornare al [!UICONTROL Monitorare] dashboard. Seleziona **[!UICONTROL Avvio esecuzione: 2/14/2021, 21:47]** per tornare alla pagina precedente, quindi selezionare **[!UICONTROL Flusso di dati: demo di acquisizione dati fedeltà - Non riuscito]** per tornare alla pagina dei flussi di dati.

![percorso di navigazione](../assets/ui/monitor-sources/breadcrumbs.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai monitorato correttamente il flusso di dati di acquisizione dal livello di origine utilizzando **[!UICONTROL Monitorare]** dashboard. Inoltre, hai identificato correttamente gli errori che hanno contribuito al fallimento dei flussi di dati durante il processo di acquisizione. Per ulteriori informazioni, consulta i seguenti documenti:

* [Monitoraggio delle identità nei flussi di dati](./monitor-identities.md)
* [Monitoraggio dei profili nei flussi di dati](./monitor-profiles.md)
