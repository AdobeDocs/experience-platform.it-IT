---
title: Note sulla versione di Adobe Experience Platform dicembre 2020
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

Nuove funzioni di Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

I flussi di dati sono una rappresentazione dei processi di dati che consentono di spostare i dati in Platform. Questi flussi di dati sono configurati tra servizi diversi, aiutando a spostare i dati dai connettori di origine ai set di dati di destinazione, al servizio Identity e Profile e alle destinazioni.

**Funzione chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Trasparenza per i flussi di dati | Puoi monitorare i flussi di dati per origini e destinazioni. Per ulteriori informazioni, leggere [tutorial sul monitoraggio delle origini](../../dataflows/ui/monitor-sources.md) o [tutorial sul monitoraggio delle destinazioni](../../dataflows/ui/monitor-destinations.md). |

Per ulteriori informazioni sui flussi di dati, consulta la sezione [panoramica dei flussi di dati](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni approfondite dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di effettuare previsioni utilizzando i contenuti e le risorse di dati delle soluzioni Adobe.

**Funzionalità chiave**

| Funzione | Descrizione |
| --- | ---|
| Componente aggiuntivo per pacchetto di Adobe Experience Platform Intelligence | Il componente aggiuntivo per il pacchetto di Adobe Experience Platform Intelligence è un aggiornamento di Data Science Workspace che sblocca ulteriori funzioni chiave come: <li> Sperimentazione e valutazione di modelli guidati dall’interfaccia utente.</li><li> Possibilità di implementare e rendere operativi i modelli con corsi di formazione pianificati e processi di inferenza.</li><li> Supporto per l’apprendimento profondo nei modelli Tensorflow (GPU Compute).</li><li> Calcolo distribuito basato su Spark per addestrare e valutare set di dati di grandi dimensioni (10 MM + righe).</li><li>E altro ancora</li> |

Per ulteriori informazioni sul componente aggiuntivo Adobe Experience Platform Intelligence, consulta la documentazione su [Accesso e funzioni di Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di configurare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzionalità chiave**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiorna i dettagli di account e connessione per le origini di streaming | È ora possibile aggiornare nomi, descrizioni e credenziali delle connessioni di streaming esistenti utilizzando [!DNL Flow Service] e l&#39;interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [aggiornamento delle connessioni tramite l’API](../../sources/tutorials/api/update.md) e [modifica dei dettagli account tramite l’interfaccia utente di](../../sources/tutorials/ui/monitor.md). |
| Elimina flussi di dati | I flussi di dati in streaming che contengono errori o sono diventati superflui ora possono essere eliminati utilizzando [!DNL Flow Service] e l&#39;interfaccia utente. Per ulteriori informazioni, consulta l’esercitazione su [eliminazione dei flussi di dati tramite l’API](../../sources/tutorials/api/delete-dataflows.md) e [eliminazione dei flussi di dati tramite l’interfaccia utente](../../sources/tutorials/ui/delete.md). |

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
