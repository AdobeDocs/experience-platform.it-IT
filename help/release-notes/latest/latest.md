---
title: Note sulla versione di Adobe Experience Platform
description: ' note sulla versione del Experience Platform per il 24 febbraio 2021.'
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: a2470d44512821996a2d5ee44722cb24990d1054
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 7%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 24 febbraio 2021**

Nuove funzioni in Adobe Experience Platform:

- [(Beta) Dashboard](#dashboards)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta) Dashboard {#dashboards}

Adobe Experience Platform fornisce diverse dashboard attraverso le quali potete visualizzare informazioni importanti sui dati aziendali, come acquisito durante le istantanee giornaliere.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Dashboard per profili, segmenti, destinazioni e utilizzo licenze (Beta) | **Nota: La funzionalità del dashboard è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.**<br/><br/> I dashboard consentono di generare report out-of-the-box sui dati aziendali e sono integrati direttamente nel flusso di lavoro di marketing all&#39;interno di Platform (Piattaforma). Queste dashboard sono disponibili senza bisogno di ulteriore supporto IT e senza il tempo e lo sforzo altrimenti necessari per esportare ed elaborare i dati con un&#39;ulteriore progettazione e implementazione del data warehouse. |

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

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con il profilo cliente in tempo reale, puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Attributi calcolati (alfa) | ***Nota: Questa funzionalità è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.*** <br/><br/>Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Potete quindi utilizzare gli aggregati per segmentazione, attivazione e personalizzazione. Alcuni esempi di queste funzioni includono conteggio, somma, media, min, max, true/false. Gli attributi calcolati sono attualmente disponibili solo tramite API. Per ulteriori informazioni, vedere la [panoramica degli attributi calcolati](../../profile/computed-attributes/overview.md). |

Per ulteriori informazioni sul profilo cliente in tempo reale, comprese esercitazioni e best practice per l&#39;utilizzo dei dati [!DNL Profile], si prega di iniziare leggendo la [panoramica sul profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne consentendo al contempo di strutturare, etichettare e migliorare tali dati tramite i servizi Piattaforma. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

 Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove origini**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Google PubSub] | È ora possibile connettersi a [!DNL Google PubSub] [!DNL Experience Platform] utilizzando l&#39;API [!DNL Flow Service] o l&#39;interfaccia utente. Per ulteriori informazioni, vedere la [[!DNL Google PubSub] panoramica del connettore](../../sources/connectors/cloud-storage/google-pubsub.md). |
| [!DNL Oracle Object Storage] | È ora possibile connettersi a [!DNL Oracle Object Storage] [!DNL Experience Platform] utilizzando l&#39;API [!DNL Flow Service] o l&#39;interfaccia utente. Per ulteriori informazioni, vedere la [[!DNL Oracle Object Storage] panoramica del connettore](../../sources/connectors/cloud-storage/oracle-object-storage.md). |

Per informazioni più generali sulle origini, fare riferimento alla [panoramica delle origini](../../sources/home.md).
