---
title: Panoramica dell’igiene dei dati
description: Adobe Experience Platform Data Hygiene consente di gestire il ciclo di vita dei dati aggiornando o eliminando record obsoleti o imprecisi.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 70a2abcc4d6e27a89e77d68e7757e4876eaa4fc0
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# Igiene dei dati in Adobe Experience Platform

>[!IMPORTANT]
>
>L’igiene dei dati è attualmente disponibile solo per le organizzazioni che hanno acquistato **Scudo sanitario Adobe** o **Adobe Privacy e sicurezza scudo**.

Adobe Experience Platform fornisce un solido set di strumenti per gestire operazioni complesse e di grandi dimensioni sui dati al fine di orchestrare le esperienze dei consumatori. Man mano che i dati vengono acquisiti nel sistema nel tempo, diventa sempre più importante gestire gli archivi di dati in modo che i dati vengano utilizzati come previsto, vengono aggiornati quando è necessario correggere i dati errati e vengono eliminati quando i criteri organizzativi lo ritengono necessario.

Le funzionalità di igiene dei dati di Platform consentono di gestire i dati archiviati tramite:

* Pianificazione delle scadenze automatizzate dei set di dati
* Eliminazione di record singoli da uno o tutti i set di dati

>[!IMPORTANT]
>
>Le eliminazioni dei record sono intese per la pulizia, la rimozione di dati anonimi o la minimizzazione dei dati. Sono **not** da utilizzare per le richieste di diritti delle persone interessate (conformità) in relazione alle normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD). Per tutti i casi di utilizzo della conformità, utilizza [Adobe Experience Platform Privacy Service](../privacy-service/home.md) invece.

Queste attività possono essere eseguite utilizzando [[!UICONTROL Igiene dei dati] Area di lavoro dell&#39;interfaccia utente](#ui) o [API di igiene dei dati](#api). Quando un processo di igiene dei dati viene eseguito, il sistema fornisce aggiornamenti di trasparenza in ogni fase del processo. Vedi la sezione su [Tempistiche e trasparenza](#timelines-and-transparency) per ulteriori informazioni sulla rappresentazione di ciascun tipo di processo nel sistema.

## [!UICONTROL Igiene dei dati] Area di lavoro dell&#39;interfaccia utente {#ui}

La [!UICONTROL Igiene dei dati] Workspace nell’interfaccia utente di Platform consente di configurare e pianificare le operazioni di igiene dei dati, per garantire che i record vengano mantenuti come previsto.

Per passaggi dettagliati sulla gestione delle attività di igiene dei dati nell’interfaccia utente, consulta [Guida all’interfaccia utente per l’igiene dei dati](./ui/overview.md).

## API di igiene dei dati {#api}

La [!UICONTROL Igiene dei dati] L’interfaccia utente si basa sull’API di igiene dati, i cui endpoint sono disponibili per l’utilizzo diretto se preferisci automatizzare le attività di igiene dei dati. Consulta la sezione [Guida all’API per l’igiene dei dati](./api/overview.md) per ulteriori informazioni.

## Timeline e trasparenza

Le richieste di cancellazione dei record e di scadenza dei set di dati hanno ciascuna una propria timeline di elaborazione e forniscono aggiornamenti sulla trasparenza in punti chiave dei rispettivi flussi di lavoro. Per informazioni dettagliate su ciascun tipo di processo, fare riferimento alle sezioni seguenti.

### Scadenza set di dati {#dataset-expiration-transparency}

Quando un [richiesta di scadenza del set di dati](./ui/dataset-expiration.md) viene creato:

| Ambiente di staging | Ora dopo la scadenza pianificata | Descrizione |
| --- | --- | --- |
| Richiesta inviata | 0 ore | Un amministratore dei dati o un analista della privacy invia una richiesta per la scadenza di un set di dati in un dato momento. La richiesta è visibile nella [!UICONTROL Interfaccia utente di Data Hygiene] dopo l’invio e rimane in uno stato in sospeso fino al tempo di scadenza pianificato, dopo di che la richiesta verrà eseguita. |
| Set di dati eliminato | 1 ora | Il set di dati viene rilasciato dal [pagina di inventario dei set di dati](../catalog/datasets/user-guide.md) nell’interfaccia utente di . I dati all&#39;interno del data lake sono solo morbidi cancellati, e lo rimarranno fino alla fine del processo, dopo di che sarà duro cancellati. |
| Conteggio profili aggiornato | 30 ore | A seconda del contenuto del set di dati da eliminare, alcuni profili possono essere rimossi dal sistema se tutti gli attributi dei loro componenti sono legati a tale set di dati. 30 ore dopo l’eliminazione del set di dati, tutte le modifiche risultanti nei conteggi dei profili complessivi vengono riportate in [widget dashboard](../dashboards/guides/profiles.md#profile-count-trend) e altri rapporti. |
| Segmenti aggiornati | 48 ore | Una volta aggiornati tutti i profili interessati, tutti i relativi [segmenti](../segmentation/home.md) vengono aggiornati per riflettere le nuove dimensioni. A seconda del set di dati rimosso e degli attributi su cui stai eseguendo la segmentazione, la dimensione di ciascun segmento potrebbe aumentare o diminuire in seguito all’eliminazione. |
| Percorsi e destinazioni aggiornati | 50 ore | [Percorsi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagne](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)e [destinazioni](../destinations/home.md) vengono aggiornati in base alle modifiche nei segmenti correlati. |
| Eliminazione rigida completata | 14 giorni | Tutti i dati relativi al set di dati vengono eliminati dal data lake. La [stato del lavoro di igiene](./ui/browse.md#view-details) che ha eliminato il set di dati viene aggiornato per riflettere questa situazione. |

{style=&quot;table-layout:auto&quot;}

### Elimina record {#record-delete-transparency}

>[!IMPORTANT]
>
>Le cancellazioni record sono disponibili solo per le organizzazioni che hanno acquistato Adobe Healthcare Shield.

Quando un [richiesta di cancellazione record](./ui/record-delete.md) viene creato:

| Ambiente di staging | Tempo dopo l’invio della richiesta | Descrizione |
| --- | --- | --- |
| Richiesta inviata | 0 ore | Un amministratore dei dati o un analista della privacy invia una richiesta di cancellazione dei record. La richiesta è visibile nella [!UICONTROL Interfaccia utente di Data Hygiene] dopo l’invio. |
| Ricerca profilo aggiornata | 3 ore | La modifica dei conteggi dei profili causata dall’identità eliminata si riflette in [widget dashboard](../dashboards/guides/profiles.md#profile-count-trend) e altri rapporti. |
| Segmenti aggiornati | 24 ore | Una volta rimossi i profili, tutti i relativi [segmenti](../segmentation/home.md) vengono aggiornati per riflettere le nuove dimensioni. |
| Percorsi e destinazioni aggiornati | 26 ore | [Percorsi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagne](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)e [destinazioni](../destinations/home.md) vengono aggiornati in base alle modifiche nei segmenti correlati. |
| Record morbidi eliminati nel lago dati | 7 giorni | I dati vengono eliminati morbidi dal data lake. |
| Pulizia dati completata | 14 giorni | La [stato del lavoro di igiene](./ui/browse.md#view-details) aggiornamenti per indicare che il lavoro è stato completato, il che significa che l&#39;aspirazione dei dati è stata completata sul lago di dati e i relativi record sono stati duramente cancellati. |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Questo documento fornisce una panoramica delle funzionalità di igiene dei dati di Platform. Per iniziare a effettuare richieste di igiene dei dati nell’interfaccia utente, consulta [Guida all’interfaccia utente](./ui/overview.md). Per informazioni su come creare processi di igiene dei dati a livello di programmazione, consulta [Guida all’API per l’igiene dei dati](./api/overview.md)
