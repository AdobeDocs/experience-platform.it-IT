---
title: Note sulla versione di Adobe Experience Platform dicembre 2020
description: Note sulla versione di dicembre 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 11%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 9 dicembre 2020**

Nuove funzioni di Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

I flussi di dati sono una rappresentazione dei processi di dati che spostano i dati in Platform. Questi flussi di dati sono configurati tra servizi diversi, aiutando a spostare i dati dai connettori di origine ai set di dati di destinazione, al servizio Identity e Profile e alle destinazioni.

**Caratteristica chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Trasparenza per i flussi di dati | Puoi monitorare i flussi di dati per origini e destinazioni. Per ulteriori informazioni, leggere l&#39;[esercitazione sul monitoraggio delle origini](../../dataflows/ui/monitor-sources.md) o l&#39;[esercitazione sul monitoraggio delle destinazioni](../../dataflows/ui/monitor-destinations.md). |

Per ulteriori informazioni sui flussi di dati, leggere la [panoramica dei flussi di dati](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di effettuare previsioni utilizzando i contenuti e le risorse di dati delle soluzioni Adobe.

**Funzioni principali**

| Funzione | Descrizione |
| --- | ---|
| Componente aggiuntivo per pacchetto di Adobe Experience Platform Intelligence | Il componente aggiuntivo del pacchetto di Adobe Experience Platform Intelligence è un aggiornamento di Data Science Workspace che sblocca funzionalità chiave aggiuntive, quali: <li> Sperimentazione e valutazione di modelli guidati dall’interfaccia utente.</li><li> Possibilità di implementare e rendere operativi i modelli con corsi di formazione pianificati e processi di inferenza.</li><li> Supporto per l’apprendimento profondo nei modelli Tensorflow (GPU Compute).</li><li> Calcolo distribuito basato su Spark per addestrare e valutare set di dati di grandi dimensioni (10 MM + righe).</li><li>E altro ancora</li> |

Per ulteriori informazioni sull&#39;addon del pacchetto di Adobe Experience Platform Intelligence, vedere la documentazione relativa all&#39;accesso e alle funzionalità di [Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo consentire di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform]. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni principali**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiorna i dettagli di account e connessione per le origini di streaming | È ora possibile aggiornare i nomi, le descrizioni e le credenziali delle connessioni in streaming esistenti utilizzando l&#39;API [!DNL Flow Service] e l&#39;interfaccia utente. Per ulteriori informazioni, vedere l&#39;esercitazione sull&#39;[aggiornamento delle connessioni tramite l&#39;API](../../sources/tutorials/api/update.md) e la [modifica dei dettagli dell&#39;account tramite l&#39;interfaccia utente](../../sources/tutorials/ui/monitor.md). |
| Elimina flussi di dati | I flussi di dati in streaming che contengono errori o sono diventati superflui ora possono essere eliminati utilizzando l&#39;API [!DNL Flow Service] e l&#39;interfaccia utente. Per ulteriori informazioni, vedere l&#39;esercitazione su [eliminazione dei flussi di dati tramite API](../../sources/tutorials/api/delete-dataflows.md) e [eliminazione dei flussi di dati tramite l&#39;interfaccia utente](../../sources/tutorials/ui/delete.md). |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
