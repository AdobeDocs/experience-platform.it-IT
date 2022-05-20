---
title: Note sulla versione di Adobe Experience Platform Dicembre 2020
description: Note sulla versione di dicembre 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 8%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 9 dicembre 2020**

Nuove funzioni in Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

I flussi di dati sono una rappresentazione dei processi di dati che consentono di spostare i dati in Platform. Questi flussi di dati sono configurati su diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, a Identity e Profile Service e alle destinazioni.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Trasparenza per i flussi di dati | Puoi monitorare i flussi di dati per sorgenti e destinazioni. Per ulteriori informazioni, leggere il [esercitazione sul monitoraggio delle origini](../../dataflows/ui/monitor-sources.md) o [esercitazione sulle destinazioni di monitoraggio](../../dataflows/ui/monitor-destinations.md). |

Per ulteriori informazioni sui flussi di dati, consulta la sezione [panoramica dei dataflows](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse di dati nelle soluzioni Adobe.

**Funzionalità chiave**

| Funzione | Descrizione |
| --- | ---|
| Aggiungi pacchetto Adobe Experience Platform Intelligence | L’aggiunta al pacchetto Adobe Experience Platform Intelligence è un aggiornamento di Data Science Workspace che sblocca ulteriori funzioni chiave come: <li> Sperimentazione e valutazione dei modelli basati sull’interfaccia utente.</li><li> Possibilità di implementare e gestire modelli con formazione programmata e processi di deduzione.</li><li> Supporto per l&#39;apprendimento profondo nei modelli di flusso di tensione (GPU Compute).</li><li> Calcolo distribuito basato su scintilla per addestrare e valutare in base a set di dati di grandi dimensioni (10MM + righe).</li><li>E altro ancora</li> |

Per ulteriori informazioni sull&#39;aggiunta del pacchetto Adobe Experience Platform Intelligence, consulta la documentazione su [Accesso e funzioni di Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiorna account e dettagli di connessione per le origini streaming | Ora puoi aggiornare i nomi, le descrizioni e le credenziali delle connessioni di streaming esistenti utilizzando [!DNL Flow Service] API e interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [aggiornamento delle connessioni tramite API](../../sources/tutorials/api/update.md) e [modifica dei dettagli dell’account tramite l’interfaccia utente](../../sources/tutorials/ui/monitor.md). |
| Eliminare i flussi di dati | I flussi di dati in streaming contenenti errori o diventati non necessari ora possono essere eliminati utilizzando [!DNL Flow Service] API e interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [eliminazione dei flussi di dati tramite l’API](../../sources/tutorials/api/delete-dataflows.md) e [eliminazione dei flussi di dati tramite l’interfaccia utente](../../sources/tutorials/ui/delete.md). |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
