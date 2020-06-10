---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione della piattaforma Experience - 10 giugno 2020
doc-type: release notes
last-update: June 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: b6cfdf56c20065bdc3e8a9fedf6007ddd74eaeaa
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 6%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 10 giugno 2020**

Aggiornamenti alle funzionalità esistenti in Adobe Experience Platform:

- [Area di lavoro Data Science](#dsw)
- [Origini](#sources)

## Area di lavoro Data Science {#dsw}

Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per liberare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace ti aiuta a fare previsioni utilizzando i tuoi contenuti e le risorse di dati nelle soluzioni Adobe.

Data Science Workspace ha lavorato su nuovi modi per consentire esperienze e previsioni migliori attraverso l&#39;uso dell&#39;apprendimento automatico in tempo reale. L&#39;apprendimento automatico in tempo reale consente di creare, testare e implementare modelli di machine learning personalizzati o importati in formati di modelli interoperabili standard di settore per l&#39;assegnazione di punteggi/attivazione in tempo reale tramite un endpoint API.

Tenere presente che l&#39;apprendimento automatico in tempo reale è in alfa e in fase di sviluppo.

| Funzione | Descrizione |
|--- | ---|
| JupyterLab Lancio del codice ML in tempo reale | JupyterLab Launcher ora include un notebook Python per l&#39;apprendimento automatico in tempo reale (Alpha). |

Per ulteriori informazioni sull&#39;alfa Real-time Machine Learning, vedere la panoramica [sull&#39;apprendimento automatico in tempo](../../data-science-workspace/real-time-machine-learning/home.md)reale.

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e allo stesso tempo di strutturarli, etichettarli e ottimizzarli tramite i servizi della piattaforma. È possibile acquisire dati da origini diverse, come applicazioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto aggiuntivo per API e interfaccia utente per i sistemi di storage cloud | Nuovo connettore sorgente per Apache HDFS |
| Supporto aggiuntivo per API e interfaccia utente per i database | Nuovo connettore sorgente per Couchbase. |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).
