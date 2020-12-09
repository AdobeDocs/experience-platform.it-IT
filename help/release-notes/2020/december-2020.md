---
title: Note sulla versione di Adobe Experience Platform
description: ' note sulla versione del Experience Platform 9 dicembre 2020'
doc-type: release notes
last-update: December 9, 2020
author: ens60013
translation-type: tm+mt
source-git-commit: 25c162f50f0a66d77eb638dbf87893af3c543ddc
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 10%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 9 dicembre 2020**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento dell&#39;account e dei dettagli di connessione per le origini di streaming | Ora puoi aggiornare i nomi, le descrizioni e le credenziali delle connessioni di streaming esistenti utilizzando l&#39; [!DNL Flow Service] API e l&#39;interfaccia utente. Per ulteriori informazioni, consultate l&#39;esercitazione sull&#39; [aggiornamento delle connessioni mediante l&#39;API](../../sources/tutorials/api/update.md) e la [modifica dei dettagli dell&#39;account tramite l&#39;interfaccia utente](../../sources/tutorials/ui/monitor.md). |
| Eliminare i flussi di dati | I flussi di dati in streaming che contengono errori o che non sono più necessari ora possono essere eliminati tramite l&#39; [!DNL Flow Service] API e l&#39;interfaccia utente. Per ulteriori informazioni, consultate l&#39;esercitazione sull&#39; [eliminazione dei flussi di dati tramite l&#39;API](../../sources/tutorials/api/delete-dataflows.md) e l&#39; [eliminazione dei flussi di dati tramite l&#39;interfaccia utente](../../sources/tutorials/ui/delete.md). |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).