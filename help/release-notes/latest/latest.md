---
title: Note sulla versione di Adobe Experience Platform
description: ' note sulla versione del Experience Platform 9 dicembre 2020'
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: ae353e6dda3f92647c32ee8e731be5785d24e5cb
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 6%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 9 dicembre 2020**

Nuove funzioni in Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

I flussi di dati sono una rappresentazione dei processi di dati che consentono di spostare i dati tra piattaforme. Questi flussi di dati sono configurati tra diversi servizi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a Servizio identità e profilo e alle destinazioni.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Trasparenza per i flussi di dati | È possibile monitorare i flussi di dati per origini e destinazioni. Per ulteriori informazioni, consulta l’ [esercitazione sulle origini](../../dataflows/ui/monitor-sources.md) di monitoraggio o l’ [esercitazione sulle destinazioni](../../dataflows/ui/monitor-destinations.md)di monitoraggio. |

Per ulteriori informazioni sui flussi di dati, consulta la panoramica dei [flussi di dati](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per creare approfondimenti dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni  Adobe.

**Funzionalità chiave**

| Funzione | Descrizione |
| --- | ---|
| Aggiungi pacchetto Adobe Experience Platform Intelligence | L&#39;aggiunta del pacchetto Adobe Experience Platform Intelligence è un aggiornamento di Data Science Workspace che consente di accedere a funzionalità chiave aggiuntive, come: <li> Sperimentazione e valutazione basata sull’interfaccia utente.</li><li> Possibilità di implementare e rendere operativi modelli con formazione programmata e processi di deduzione.</li><li> Supporto per l&#39;apprendimento profondo nei modelli Tensorflow (GPU Compute).</li><li> Calcolo distribuito basato su Spark per la formazione e il punteggio rispetto a set di dati di grandi dimensioni (10MM + righe).</li><li>E altro</li> |

Per ulteriori informazioni sull&#39;aggiunta del pacchetto Adobe Experience Platform Intelligence, consulta la documentazione sull&#39;accesso e sulle funzioni [di](../../data-science-workspace/access-features-dsw.md)Data Science Workspace.

## [!DNL Sources] {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento dell&#39;account e dei dettagli di connessione per le origini di streaming | Ora puoi aggiornare i nomi, le descrizioni e le credenziali delle connessioni di streaming esistenti utilizzando l&#39; [!DNL Flow Service] API e l&#39;interfaccia utente. Per ulteriori informazioni, consultate l&#39;esercitazione sull&#39; [aggiornamento delle connessioni mediante l&#39;API](../../sources/tutorials/api/update.md) e la [modifica dei dettagli dell&#39;account tramite l&#39;interfaccia utente](../../sources/tutorials/ui/monitor.md). |
| Eliminare i flussi di dati | I flussi di dati in streaming che contengono errori o che non sono più necessari ora possono essere eliminati tramite l&#39; [!DNL Flow Service] API e l&#39;interfaccia utente. Per ulteriori informazioni, consultate l&#39;esercitazione sull&#39; [eliminazione dei flussi di dati tramite l&#39;API](../../sources/tutorials/api/delete-dataflows.md) e l&#39; [eliminazione dei flussi di dati tramite l&#39;interfaccia utente](../../sources/tutorials/ui/delete.md). |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).

