---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' note sulla versione del Experience Platform 10 agosto 2020'
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 89531ad458bd41720090ef2c429376af4460d7c0
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 7%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 12 agosto 2020**

Note aggiornate sulla versione per  Experience Platform

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per liberare informazioni dai dati. Integrato in Adobe Experience Platform, [!DNL Data Science Workspace] consente di fare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni  Adobe.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti delle VM [!DNL JupyterLab] | È stata migliorata la stabilità delle [!DNL JupyterLab notebook] macchine virtuali con esecuzione prolungata. |

Per ulteriori informazioni su [!DNL JupyterLab]questo argomento, consultate la guida [[!DNL JupyterLab] utente](../../data-science-workspace/jupyterlab/overview.md).

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Monitoraggio dell&#39;esecuzione dei flussi | Gli utenti possono monitorare tutte le esecuzioni del flusso e visualizzare una visualizzazione dettagliata di ciascuna esecuzione, incluso lo stato di completamento, la durata dell&#39;esecuzione, l&#39;elenco dei file elaborati, gli errori e le metriche. Per ulteriori informazioni, consulta il documento [sui flussi di dati](../../sources/tutorials/ui/monitor.md) di monitoraggio. |
| Aggiornamento account | Gli utenti possono aggiornare le credenziali, il nome e la descrizione di qualsiasi account esistente per fornire informazioni più significative e correggere eventuali errori che potrebbero essere stati creati. |
| Notifiche di esecuzione del flusso | Gli utenti possono iscriversi agli eventi e registrare i webhooks per ricevere notifiche in tempo reale sullo stato, le metriche e gli errori relativi alle esecuzioni di flusso. |
| Miglioramenti al catalogo dell&#39;interfaccia utente | Aggiornamenti alla schermata del catalogo origini per consentire un accesso più semplice alle azioni principali degli oggetti selezionati. |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).
