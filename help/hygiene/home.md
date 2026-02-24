---
title: Panoramica di Advanced Data Lifecycle Management
description: Advanced Data Lifecycle Management consente di gestire il ciclo di vita dei dati aggiornando o eliminando record obsoleti o imprecisi.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: fc71e61fd33fe216f8cd326b9df048958c07077a
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 2%

---

# Gestione avanzata del ciclo di vita dei dati in Adobe Experience Platform

Adobe Experience Platform fornisce un solido set di strumenti per gestire operazioni di dati complesse e di grandi dimensioni al fine di orchestrare le esperienze dei consumatori. Man mano che i dati vengono acquisiti nel sistema nel tempo, diventa sempre più importante gestire gli archivi di dati in modo che vengano utilizzati come previsto, vengano aggiornati quando i dati errati devono essere corretti e vengano eliminati quando le politiche organizzative lo ritengono necessario.

Queste attività possono essere eseguite utilizzando l&#39;area di lavoro dell&#39;interfaccia utente [[!UICONTROL Data Lifecycle]](#ui) o l&#39;API [Igiene dei dati](#api). Quando viene eseguito un processo del ciclo di vita dei dati, il sistema fornisce aggiornamenti di trasparenza in ogni fase del processo. Consulta la sezione su [timeline e trasparenza](#timelines-and-transparency) per ulteriori informazioni sulla rappresentazione di ogni tipo di processo nel sistema.

>[!NOTE]
>
>Advanced Data Lifecycle Management supporta le eliminazioni dei dataset tramite l&#39;[endpoint di scadenza del dataset](./api/dataset-expiration.md) e le eliminazioni degli ID (dati a livello di riga) utilizzando le identità primarie tramite l&#39;[endpoint workorder](./api/workorder.md). Puoi anche gestire [scadenze set di dati](./ui/dataset-expiration.md) e [eliminazioni record](./ui/record-delete.md) tramite l&#39;interfaccia utente di Experience Platform. Per ulteriori informazioni, consulta la documentazione collegata. Il ciclo di vita dei dati non supporta l’eliminazione in batch.

## Area di lavoro dell&#39;interfaccia utente [!UICONTROL Data Lifecycle] {#ui}

L&#39;area di lavoro [!UICONTROL Data Lifecycle] nell&#39;interfaccia utente di Experience Platform consente di configurare e pianificare le operazioni del ciclo di vita dei dati, garantendo la conservazione dei record come previsto.

Per i passaggi dettagliati sulla gestione delle attività del ciclo di vita dei dati nell&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente del ciclo di vita dei dati](./ui/overview.md).

## API di igiene dei dati {#api}

L&#39;interfaccia utente di [!UICONTROL Data Lifecycle] è basata sull&#39;API di igiene dei dati, i cui endpoint sono disponibili per l&#39;utilizzo diretto se si preferisce automatizzare le attività del ciclo di vita dei dati. Per ulteriori informazioni, consulta la [Guida dell&#39;API di igiene dei dati](./api/overview.md).

## Timeline e trasparenza {#timelines-and-transparency}

[Le richieste di eliminazione dei record](./ui/record-delete.md) e di scadenza dei set di dati hanno ciascuno una propria timeline di elaborazione e forniscono aggiornamenti di trasparenza nei punti chiave dei rispettivi flussi di lavoro.

>[!TIP]
>
>Per monitorare l&#39;utilizzo corrente rispetto ai limiti di quota, vedere la [Guida di riferimento alle quote](./api/quota.md).\
>Per le regole di adesione, i limiti mensili, le timeline di SLA e i criteri di gestione delle eccezioni, consulta la documentazione [Eliminazione record (UI)](./ui/record-delete.md#quotas) e [Ordine di lavoro (API)](./api/workorder.md#quotas).

Di seguito è riportato un evento che si verifica quando viene creata una [richiesta di scadenza del set di dati](./ui/dataset-expiration.md):

| Fase | Ora dopo la scadenza pianificata | Descrizione |
| --- | --- | --- |
| Richiesta inviata | 0 ore | Un amministratore di dati o un analista della privacy invia una richiesta affinché un set di dati scada in un determinato momento. La richiesta è visibile in [!UICONTROL Data Lifecycle UI] dopo l&#39;invio e rimane in uno stato in sospeso fino all&#39;ora di scadenza pianificata, dopo la quale verrà eseguita. |
| Set di dati eliminato dal data lake | 1 ora | Il set di dati viene eliminato dalla [pagina di inventario del set di dati](../catalog/datasets/user-guide.md) nell&#39;interfaccia utente. I dati all’interno del data lake vengono eliminati solo in modo non permanente e rimangono tali fino alla fine del processo, dopo di che verranno eliminati in modo definitivo. |
| Set di dati eliminato dal servizio profilo | 3 ore | Da questo momento in poi, le operazioni che includono segmentazione in batch e streaming, anteprima o stima, esportazione e accesso alle entità non leggeranno più i dati da questo set di dati. I dati all’interno del servizio profilo vengono eliminati solo temporaneamente e rimangono tali fino alla fine del processo, dopo di che verranno eliminati definitivamente. |
| Conteggio profili e pubblico aggiornati | 48 ore | Una volta aggiornati tutti i profili interessati, tutti i [tipi di pubblico](../segmentation/home.md) correlati vengono aggiornati per riflettere le nuove dimensioni. A seconda del set di dati rimosso e degli attributi su cui stai eseguendo la segmentazione, la dimensione di ciascun pubblico potrebbe aumentare o diminuire a causa dell’eliminazione. A questo punto, qualsiasi modifica risultante nei conteggi complessivi dei profili viene riportata in [widget del dashboard](../dashboards/guides/profiles.md#profile-count-trend) e altri report. |
| Percorsi e destinazioni aggiornati | 50 ore | [Percorsi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagne](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html) e [destinazioni](../destinations/home.md) vengono aggiornati in base alle modifiche nei segmenti correlati. |
| Eliminazione definitiva completata | 15 giorni | Tutti i dati relativi al set di dati vengono eliminati in modo rigido dal data lake e dal servizio profilo. Lo stato [ del processo del ciclo di vita dei dati](./ui/browse.md#view-details) che ha eliminato il set di dati viene aggiornato di conseguenza. |

{style="table-layout:auto"}

## Passaggi successivi

Questo documento fornisce una panoramica delle funzionalità del ciclo di vita dei dati di Experience Platform. Per iniziare a effettuare richieste di igiene dei dati nell&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente](./ui/overview.md). Per informazioni su come creare processi del ciclo di vita dei dati a livello di programmazione, consulta la [guida dell&#39;API di igiene dei dati](./api/overview.md)
