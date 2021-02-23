---
keywords: ' Experience Platform;home;argomenti popolari;monitorare account;monitorare flussi di dati;flussi di dati;origini'
description: Questa esercitazione fornisce i passaggi necessari per monitorare il flusso di dati, utilizzando sia la visualizzazione di monitoraggio aggregata che il monitoraggio tra più servizi.
solution: Experience Platform
title: Monitorare i flussi di dati per le origini nell'interfaccia utente
topic: ' - Panoramica'
type: Tutorial
translation-type: tm+mt
source-git-commit: 4c668a47e62ba7736dd2d7afe4e71fd015198356
workflow-type: tm+mt
source-wordcount: '1529'
ht-degree: 0%

---


# Monitorare i flussi di dati per le sorgenti nell’interfaccia utente

In Adobe Experience Platform, i dati vengono acquisiti da un&#39;ampia varietà di fonti, analizzati all&#39;interno  Experience Platform, e attivati in un&#39;ampia gamma di destinazioni. La piattaforma semplifica il processo di tracciamento di questo flusso di dati potenzialmente non lineare fornendo trasparenza con i flussi di dati.

Il pannello di controllo offre una rappresentazione visiva del percorso di un flusso di dati. Puoi utilizzare una visualizzazione di monitoraggio aggregata e navigare verticalmente dal livello di origine, a un flusso di dati e a un&#39;esecuzione del flusso di dati, per visualizzare le metriche corrispondenti che contribuiscono al successo o all&#39;errore di un flusso di dati. È inoltre possibile utilizzare la capacità di monitoraggio cross-service del dashboard di monitoraggio per monitorare il percorso di un flusso di dati da un&#39;origine, a [!DNL Identity Service] e a [!DNL Profile].

Questa esercitazione fornisce i passaggi necessari per monitorare il flusso di dati, utilizzando sia la visualizzazione di monitoraggio aggregata che il monitoraggio tra più servizi.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Flussi di dati](../home.md): I flussi di dati sono una rappresentazione dei processi di dati che consentono di spostare i dati tra piattaforme. I flussi di dati sono configurati tra diversi servizi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile] e a [!DNL Destinations].
   * [Esecuzione](../../sources/notifications.md) del flusso di dati: Le esecuzioni dei flussi di dati sono i processi pianificati periodici in base alla configurazione di frequenza dei flussi di dati selezionati.
* [Origini](../../sources/home.md):  Experience Platform consente l&#39;acquisizione di dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Piattaforma.
* [Servizio](../../identity-service/home.md) identità: Ottenete una visione migliore dei singoli clienti e del loro comportamento, collegando le identità tra dispositivi e sistemi.
* [Profilo](../../profile/home.md) cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Vista di monitoraggio aggregata

Nell&#39; [interfaccia utente della piattaforma](https://platform.adobe.com), selezionare **[!UICONTROL Monitoring]** dalla barra di navigazione a sinistra per accedere al dashboard [!UICONTROL Monitoring]. Il dashboard di [!UICONTROL Monitoring] contiene metriche e informazioni su tutti i flussi di dati di origine, comprese informazioni sullo stato del traffico di dati da un&#39;origine a [!DNL Identity Service] e a [!DNL Profile].

Al centro del dashboard c&#39;è il pannello [!UICONTROL Source ingestion], che contiene metriche e grafici che mostrano i dati sui record acquisiti e i record non riusciti.

![dashboard di monitoraggio](../assets/ui/monitor-sources/monitoring-dashboard.png)

Per impostazione predefinita, i dati visualizzati contengono le frequenze di assimilazione delle ultime 24 ore. Selezionare **[!UICONTROL Last 24 hours]** per regolare l&#39;intervallo di tempo dei record visualizzati.

![change-date](../assets/ui/monitor-sources/change-date.png)

Viene visualizzata una finestra a comparsa del calendario che fornisce opzioni per fotogrammi temporali di assimilazione alternativi. Selezionare **[!UICONTROL Last 30 days]**, quindi selezionare **[!UICONTROL Apply]**

![frame di regolazione](../assets/ui/monitor-sources/adjust-timeframe.png)

I grafici sono attivati per impostazione predefinita e potete disabilitarli per espandere l&#39;elenco delle origini elencate di seguito. Selezionate l&#39;opzione **[!UICONTROL Metrics and graphs]** per disattivare i grafici.

![metriche e grafici](../assets/ui/monitor-sources/metrics-graphs.png)

| Caricamento origine | Descrizione |
| ---------------- | ----------- |
| [!UICONTROL Records ingested ] | Numero totale di record acquisiti. |
| [!UICONTROL Records failed] | Il numero totale di record che non sono stati trasferiti a causa di errori nei dati. |
| [!UICONTROL Total failed dataflows] | Il numero totale di flussi di dati con stato `failed`. |

Nell&#39;elenco di assimilazione dell&#39;origine sono visualizzate tutte le origini che contengono almeno un account esistente. L&#39;elenco include inoltre informazioni sulla frequenza di assimilazione di ogni origine, sul numero di record con errore e sul numero totale di flussi di dati con errore in base all&#39;intervallo di tempo applicato.

![origine](../assets/ui/monitor-sources/source-ingestion.png)

Per ordinare le origini nell&#39;elenco, selezionare **[!UICONTROL My sources]**, quindi selezionare la categoria desiderata dal menu a discesa. Ad esempio, per concentrarsi sugli archivi cloud, selezionare **[!UICONTROL Cloud storage]**

![ordinamento per categoria](../assets/ui/monitor-sources/sort-by-category.png)

Per visualizzare tutti i flussi di dati esistenti tra tutte le origini, selezionare **[!UICONTROL Dataflows]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

In alternativa, potete inserire una sorgente nella barra di ricerca per isolare una singola sorgente. Una volta identificata la sorgente, seleziona l&#39;icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto ad essa per visualizzare un elenco dei relativi flussi di dati attivi.

![search](../assets/ui/monitor-sources/search.png)

Viene visualizzato un elenco dei flussi di dati. Per restringere l&#39;elenco e rendere attivi i flussi di dati con errori, selezionare **[!UICONTROL Show failures only]**.

![show-failures-only](../assets/ui/monitor-sources/show-failures-only.png)

Individuare il flusso di dati da monitorare, quindi selezionare l&#39;icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto ad esso, per visualizzare ulteriori informazioni sullo stato di esecuzione.

![dataflow](../assets/ui/monitor-sources/dataflow.png)

La pagina di esecuzione del flusso di dati visualizza informazioni sulla data di inizio dell&#39;esecuzione del flusso di dati, sulla dimensione dei dati, sullo stato e sulla durata dell&#39;elaborazione. Selezionate l&#39;icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto all&#39;ora di inizio del flusso di dati per visualizzarne i dettagli di esecuzione.

![dataFlow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

Nella pagina [!UICONTROL Dataflow run details] sono visualizzate informazioni sui metadati del flusso di dati, sullo stato di inserimento parziale e sul riepilogo degli errori. Il riepilogo degli errori contiene l&#39;errore di livello principale specifico che mostra in quale fase il processo di assimilazione ha rilevato un errore.

Scorrete verso il basso per visualizzare informazioni più specifiche sull&#39;errore che si è verificato.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

Il pannello [!UICONTROL Dataflow run errors] visualizza il codice di errore e di errore specifico che causava l&#39;errore di inserimento del flusso di dati. In questo scenario, si è verificato un errore di trasformazione di mappatura, con conseguente errore di 24 record.

Selezionare **[!UICONTROL Files]** per ulteriori informazioni.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

Il pannello [!UICONTROL Files] contiene informazioni sul nome e sul percorso del file.

Per una rappresentazione più dettagliata dell&#39;errore, selezionare **[!UICONTROL Preview error diagnostics]**.

![files](../assets/ui/monitor-sources/files.png)

Viene visualizzata la finestra [!UICONTROL Error diagnostics preview], con un&#39;anteprima di un massimo di 100 errori nel flusso di dati. È possibile selezionare **[!UICONTROL Download]** per recuperare un comando curl, che consente di scaricare la diagnostica degli errori.

Al termine, selezionare **[!UICONTROL Close]**

![error-diagnostics](../assets/ui/monitor-sources/error-diagnostics.png)

Potete utilizzare il sistema di breadcrumb nell&#39;intestazione superiore per tornare al dashboard [!UICONTROL Monitoring]. Selezionare **[!UICONTROL Run start: 2/14/2021, 9:47 PM]** per tornare alla pagina precedente, quindi selezionare **[!UICONTROL Dataflow: Loyalty Data Ingestion Demo - Failed]** per tornare alla pagina dei flussi di dati.

![pane grattugiato](../assets/ui/monitor-sources/breadcrumbs.png)

## Monitoraggio interservizi

La parte superiore del dashboard contiene una rappresentazione del flusso di assimilazione dal livello di origine a [!DNL Identity Service] e a [!DNL Profile]. Ogni cella include un marcatore punto che indica la presenza di errori che si sono verificati in quella fase di assimilazione. Un punto verde indica un inserimento privo di errori, mentre un punto rosso indica che si è verificato un errore in quel particolare stadio di assimilazione.

![monitoraggio incrociato](../assets/ui/monitor-sources/cross-service-monitoring.png)

Dalla pagina dei flussi di dati, individua un flusso di dati di successo e seleziona l&#39;icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto ad esso, per visualizzare le informazioni di esecuzione del flusso di dati.

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

La pagina [!UICONTROL Source ingestion] contiene informazioni che confermano il corretto caricamento del flusso di dati. Da qui, è possibile iniziare a monitorare il percorso del flusso di dati dal livello di origine a [!DNL Identity Service], quindi a [!DNL Profile].

Selezionare **[!UICONTROL Identities]** per visualizzare l&#39;assimilazione nell&#39;area [!UICONTROL Identities].

![sources](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] metriche

La pagina [!UICONTROL Identity processing] contiene informazioni sui record trasferiti a [!DNL Identity Service], compreso il numero di identità aggiunte, i grafici creati e i grafici aggiornati.

Selezionate l&#39;icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto all&#39;ora di inizio del flusso di dati per visualizzare ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Identity].

![identità](../assets/ui/monitor-sources/identities.png)

| Metriche identità | Descrizione |
| ---------------- | ----------- |
| [!UICONTROL Records received] | Numero di record ricevuti da [!DNL Data Lake]. |
| [!UICONTROL Records failed] | Il numero di record che non sono stati trasferiti nella piattaforma a causa di errori nei dati. |
| [!UICONTROL Records skipped] | Il numero di record che sono stati acquisiti, ma non in [!DNL Identity Service] perché nella riga del record era presente un solo identificatore. |
| [!UICONTROL Records ingested] | Il numero di record trasferiti in [!DNL Identity Service]. |
| [!UICONTROL Total records] | Totale di tutti i record, inclusi quelli con errore, record ignorati, [!DNL Identities] aggiunti e record duplicati. |
| [!UICONTROL Identities added] | Il numero di nuovi identificatori netti aggiunti a [!DNL Identity Service]. |
| [!UICONTROL Graphs created] | Il numero di nuovi grafici identità netti creati in [!DNL Identity Service]. |
| [!UICONTROL Graphs updated] | Numero di grafici identità esistenti aggiornati con nuovi bordi. |
| [!UICONTROL Failed dataflow runs] | Il numero di esecuzioni del flusso di dati che non sono riuscite. |
| [!UICONTROL Processing time] | Il timestamp dall’inizio dell’assimilazione al completamento. |
| [!UICONTROL Status] | Definisce lo stato generale di un flusso di dati. I possibili valori di stato sono: <ul><li>`Success`: Indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita.</li><li>`Failed`: Indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: Indica che il flusso di dati non è ancora attivo. Questo stato si verifica spesso subito dopo la creazione di un nuovo flusso di dati.</li></ul> |

Nella pagina [!UICONTROL Dataflow run details] sono visualizzate ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Identity], inclusi l&#39;ID organizzazione IMS e l&#39;ID esecuzione del flusso di dati. In questa pagina vengono visualizzati anche il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Identity Service], qualora si verifichino errori nel processo di assimilazione.

Selezionare **[!UICONTROL Run start: 2/14/2021, 9:47 PM]** per tornare alla pagina precedente.

![identità-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Dalla pagina [!UICONTROL Identity processing], selezionare **[!UICONTROL Profiles]** per visualizzare lo stato dell&#39;inserimento dei record nell&#39;area [!UICONTROL Profiles].

![selectProfile](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] metriche

La pagina [!UICONTROL Profile processing] contiene informazioni sui record acquisiti in [!DNL Profile], compreso il numero di frammenti di profilo creati, i frammenti di profilo aggiornati e il numero totale di frammenti di profilo.

Selezionate l&#39;icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto all&#39;ora di inizio del flusso di dati per visualizzare ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Profile].

![profili](../assets/ui/monitor-sources/profiles.png)

| Metriche profilo | Descrizione |
| --------------- | ----------- |
| [!UICONTROL Records received] | Numero di record ricevuti da [!DNL Data Lake]. |
| [!UICONTROL Records failed ] | Il numero di record che sono stati acquisiti, ma non in [!DNL Profile] a causa di errori. |
| [!UICONTROL Profile fragments added] | Numero di nuovi frammenti [!DNL Profile] aggiunti. |
| [!UICONTROL Profile fragments updated] | Numero di frammenti [!DNL Profile] esistenti aggiornati |
| [!UICONTROL Total Profile fragments] | Il numero totale di record scritti in [!DNL Profile], inclusi tutti i frammenti [!DNL Profile] esistenti aggiornati e i nuovi frammenti [!DNL Profile] creati. |
| [!UICONTROL Failed dataflow runs] | Il numero di esecuzioni del flusso di dati che non sono riuscite. |
| [!UICONTROL Processing time] | Il timestamp dall’inizio dell’assimilazione al completamento. |
| [!UICONTROL Status] | Definisce lo stato generale di un flusso di dati. I possibili valori di stato sono: <ul><li>`Success`: Indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita.</li><li>`Failed`: Indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: Indica che il flusso di dati non è ancora attivo. Questo stato si verifica spesso subito dopo la creazione di un nuovo flusso di dati.</li></ul> |

Nella pagina [!UICONTROL Dataflow run details] sono visualizzate ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Profile], inclusi l&#39;ID organizzazione IMS e l&#39;ID esecuzione del flusso di dati. In questa pagina vengono visualizzati anche il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Profile], qualora si verifichino errori nel processo di assimilazione.

![profile-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Passaggi successivi

Seguendo questa esercitazione, il flusso di dati di assimilazione è stato monitorato correttamente dal livello di origine, da [!DNL Identity Service] e a [!DNL Profile] utilizzando il dashboard **[!UICONTROL Monitoring]**. Sono stati inoltre identificati degli errori che hanno contribuito al fallimento dei flussi di dati durante il processo di assimilazione. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](../../profile/home.md)
* [Panoramica di Analysis Workspace](../../data-science-workspace/home.md)
