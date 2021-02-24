---
title: Note sulla versione di Adobe Experience Platform
description: ' note sulla versione del Experience Platform per il 24 febbraio 2021.'
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 7142d13b144f34d92087affe101c5ccfcb52d90e
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 6%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 24 febbraio 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per creare approfondimenti dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni  Adobe.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Notebook JupyterLab EDA | Il notebook Python per l&#39;analisi dei dati esplorativi (EDA) è ora disponibile in Jupyterlab. Questo notebook è stato progettato per aiutarvi a scoprire i pattern dei dati, verificare l&#39;integrità dei dati e riepilogare i dati rilevanti per i modelli predittivi. Per ulteriori informazioni, vedere l&#39;esercitazione su [esplorazione di dati basati sul Web per modelli predittivi](../../data-science-workspace/jupyterlab/eda-notebook.md). |

Per ulteriori informazioni generali su Data Science Workspace, fare riferimento alla [panoramica di Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

In Adobe Experience Platform, i dati vengono acquisiti da un&#39;ampia varietà di fonti, analizzati all&#39;interno  Experience Platform, e attivati in un&#39;ampia gamma di destinazioni. La piattaforma semplifica il processo di tracciamento di questo flusso di dati potenzialmente non lineare fornendo trasparenza con i flussi di dati.

I flussi di dati sono una rappresentazione dei processi di dati che consentono di spostare i dati in Platform. Questi flussi di dati sono configurati tra diversi servizi, aiutando a spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono quindi utilizzati da [!DNL Identity Service] e [!DNL Real-time Customer Profile] prima di essere attivati in ultima istanza su [!DNL Destinations].

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Nuovo dashboard di monitoraggio | È ora possibile utilizzare il dashboard di monitoraggio per la trasparenza tra i servizi e per informazioni fruibili per l&#39;assimilazione dei dati di origine. Il nuovo dashboard di monitoraggio fornisce una visualizzazione completa dei dati elaborati da [!DNL Data Lake] a [!DNL Identity Service] e a [!DNL Profile], consentendo al contempo di monitorare i tassi di assimilazione, i successi e gli errori. Per ulteriori informazioni, consulta l&#39;esercitazione sui flussi di dati di origine [monitoraggio nell&#39;interfaccia utente](../../dataflows/ui/monitor-sources.md). |

Per informazioni più generali sui flussi di dati, fare riferimento alla [panoramica dei flussi di dati](../../dataflows/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che comunica con i servizi di Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza dei clienti possono essere incorporati in una rappresentazione comune, fornendo informazioni approfondite in modo più rapido e integrato. Puoi ricavare informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Interfaccia di ricerca aggiornata | Funzionalità di ricerca migliorate sono ora disponibili nella scheda [!UICONTROL Browse] nell&#39;area di lavoro [!UICONTROL Schemas] e nella finestra di dialogo di selezione del mixin in [!DNL Schema Editor].<br><br>Durante la ricerca di un termine in precedenza, i risultati includevano solo risorse XDM il cui nome corrisponde alla query di ricerca. Ora, oltre alle risorse il cui nome corrisponde alla query, verranno incluse anche le risorse contenenti attributi singoli che corrispondono al termine. Questo consente di cercare risorse XDM in base agli attributi che contengono anziché in base al nome della risorsa.<br><br>Per ulteriori informazioni, consulta i documenti  [sull’](../../xdm/ui/explore.md) esplorazione delle risorse XDM e sulla  [gestione ](../../xdm/ui/resources/schemas.md) degli schemi nell’interfaccia utente. |

Per ulteriori informazioni generali su XDM, fare riferimento alla [Panoramica del sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati del cliente sono frammentati in sistemi diversi, causando l&#39;apparenza di più &quot;identità&quot; per ogni singolo cliente.

Adobe Experience Platform [!DNL Identity Service] consente di acquisire una visione migliore del cliente e del suo comportamento collegando le identità tra dispositivi e sistemi, consentendo di offrire esperienze digitali personali e di forte impatto in tempo reale.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Visualizzatore grafico identità | Il visualizzatore per grafici di identità consente di convalidare e visualizzare le identità unite nell’interfaccia utente, per migliorare il debug e la trasparenza. Per ulteriori informazioni, vedere il documento del visualizzatore del grafico di identità [documento](../../identity-service/ui/identity-graph-viewer.md). |

Per ulteriori informazioni generali su [!DNL Identity Service], fare riferimento alla [Panoramica del servizio identità](../../identity-service/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne consentendo al contempo di strutturare, etichettare e migliorare tali dati tramite i servizi Piattaforma. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

 Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove origini**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Google PubSub] | È ora possibile connettersi a [!DNL Google PubSub] [!DNL Experience Platform] utilizzando l&#39;API [!DNL Flow Service] o l&#39;interfaccia utente. Per ulteriori informazioni, vedere la [[!DNL Google PubSub] panoramica del connettore](../../sources/connectors/cloud-storage/google-pubsub.md). |
| [!DNL Oracle Object Storage] | È ora possibile connettersi a [!DNL Oracle Object Storage] [!DNL Experience Platform] utilizzando l&#39;API [!DNL Flow Service] o l&#39;interfaccia utente. Per ulteriori informazioni, vedere la [[!DNL Oracle Object Storage] panoramica del connettore](../../sources/connectors/cloud-storage/oracle-object-storage.md). |

Per informazioni più generali sulle origini, fare riferimento alla [panoramica delle origini](../../sources/home.md).
