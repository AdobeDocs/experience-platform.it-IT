---
title: Panoramica di Advanced Data Lifecycle Management
description: Advanced Data Lifecycle Management consente di gestire il ciclo di vita dei dati aggiornando o eliminando record obsoleti o imprecisi.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 1f82403d4f8f5639f6a9181a7ea98bd27af54904
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 2%

---

# Gestione avanzata del ciclo di vita dei dati in Adobe Experience Platform

Adobe Experience Platform fornisce un solido set di strumenti per gestire operazioni di dati complesse e di grandi dimensioni al fine di orchestrare le esperienze dei consumatori. Man mano che i dati vengono acquisiti nel sistema nel tempo, diventa sempre più importante gestire gli archivi di dati in modo che vengano utilizzati come previsto, vengano aggiornati quando i dati errati devono essere corretti e vengano eliminati quando le politiche organizzative lo ritengono necessario.

<!-- Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Queste attività possono essere eseguite utilizzando l&#39;area di lavoro dell&#39;interfaccia utente [[!UICONTROL Ciclo di vita dei dati]](#ui) o l&#39;API [Igiene dei dati](#api). Quando viene eseguito un processo del ciclo di vita dei dati, il sistema fornisce aggiornamenti di trasparenza in ogni fase del processo. Consulta la sezione su [timeline e trasparenza](#timelines-and-transparency) per ulteriori informazioni sulla rappresentazione di ogni tipo di processo nel sistema.

>[!NOTE]
>
>Advanced Data Lifecycle Management supporta le eliminazioni dei dataset tramite l&#39;[endpoint di scadenza del dataset](./api/dataset-expiration.md) e le eliminazioni degli ID (dati a livello di riga) utilizzando le identità primarie tramite l&#39;[endpoint workorder](./api/workorder.md). Puoi anche gestire [scadenze set di dati](./ui/dataset-expiration.md) e [eliminazioni record](./ui/record-delete.md) tramite l&#39;interfaccia utente di Platform. Per ulteriori informazioni, consulta la documentazione collegata. Il ciclo di vita dei dati non supporta l’eliminazione in batch.

## [!UICONTROL Ciclo di vita dati] area di lavoro interfaccia utente {#ui}

L&#39;area di lavoro [!UICONTROL Ciclo di vita dei dati] nell&#39;interfaccia utente di Platform consente di configurare e pianificare le operazioni del ciclo di vita dei dati, per garantire che i record vengano mantenuti come previsto.

Per i passaggi dettagliati sulla gestione delle attività del ciclo di vita dei dati nell&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente del ciclo di vita dei dati](./ui/overview.md).

## API di igiene dei dati {#api}

L&#39;interfaccia utente del [!UICONTROL ciclo di vita dei dati] è basata sull&#39;API di igiene dei dati, i cui endpoint sono disponibili per l&#39;utilizzo diretto se si preferisce automatizzare le attività del ciclo di vita dei dati. Per ulteriori informazioni, consulta la [Guida dell&#39;API di igiene dei dati](./api/overview.md).

## Timeline e trasparenza

[Le richieste di eliminazione dei record](./ui/record-delete.md) e di scadenza dei set di dati hanno ciascuno una propria timeline di elaborazione e forniscono aggiornamenti di trasparenza nei punti chiave dei rispettivi flussi di lavoro.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

Di seguito è riportato un evento che si verifica quando viene creata una [richiesta di scadenza del set di dati](./ui/dataset-expiration.md):

| Fase | Ora dopo la scadenza pianificata | Descrizione |
| --- | --- | --- |
| Richiesta inviata | 0 ore | Un amministratore di dati o un analista della privacy invia una richiesta affinché un set di dati scada in un determinato momento. La richiesta è visibile nell&#39;[!UICONTROL interfaccia utente del ciclo di vita dei dati] dopo l&#39;invio e rimane in sospeso fino alla scadenza pianificata, dopo la quale verrà eseguita. |
| Set di dati eliminato | 1 ora | Il set di dati viene eliminato dalla [pagina di inventario del set di dati](../catalog/datasets/user-guide.md) nell&#39;interfaccia utente. I dati all’interno del data lake vengono eliminati solo in modo non permanente e rimangono tali fino alla fine del processo, dopo di che verranno eliminati in modo definitivo. |
| Conteggio profili aggiornato | 30 ore | A seconda del contenuto del set di dati da eliminare, alcuni profili possono essere rimossi dal sistema se tutti gli attributi dei loro componenti sono associati a tale set di dati. 30 ore dopo l&#39;eliminazione del set di dati, eventuali modifiche risultanti nei conteggi complessivi dei profili vengono riportate in [widget dashboard](../dashboards/guides/profiles.md#profile-count-trend) e altri report. |
| Tipi di pubblico aggiornati | 48 ore | Una volta aggiornati tutti i profili interessati, tutti i [tipi di pubblico](../segmentation/home.md) correlati vengono aggiornati per riflettere le nuove dimensioni. A seconda del set di dati rimosso e degli attributi su cui stai effettuando la segmentazione, la dimensione di ciascun pubblico potrebbe aumentare o diminuire a seguito dell’eliminazione. |
| Percorsi e destinazioni aggiornati | 50 ore | [Percorsi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagne](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html) e [destinazioni](../destinations/home.md) vengono aggiornati in base alle modifiche nei segmenti correlati. |
| Eliminazione definitiva completata | 15 giorni | Tutti i dati relativi al set di dati vengono eliminati dal data lake. Lo stato [ del processo del ciclo di vita dei dati](./ui/browse.md#view-details) che ha eliminato il set di dati viene aggiornato di conseguenza. |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Passaggi successivi

Questo documento fornisce una panoramica delle funzionalità del ciclo di vita dei dati di Platform. Per iniziare a effettuare richieste di igiene dei dati nell&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente](./ui/overview.md). Per informazioni su come creare processi del ciclo di vita dei dati a livello di programmazione, consulta la [guida dell&#39;API di igiene dei dati](./api/overview.md)
