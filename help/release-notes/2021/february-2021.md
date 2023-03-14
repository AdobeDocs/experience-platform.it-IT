---
title: Note sulla versione di Adobe Experience Platform, febbraio 2021
description: Note sulla versione di febbraio 2021 per Adobe Experience Platform.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 24 febbraio 2021**

Nuove funzioni di Adobe Experience Platform:

- [Dashboard (Beta)](#dashboards)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Dashboard (Beta) {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso i quali è possibile visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Profili, segmenti, destinazioni e dashboard di utilizzo della licenza (Beta) | **Nota: la funzionalità dashboard è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.**<br/><br/> Le dashboard forniscono rapporti predefiniti sui dati dell’organizzazione e sono integrate direttamente nel flusso di lavoro degli addetti al marketing all’interno di Platform. Queste dashboard sono disponibili senza la necessità di ulteriore supporto IT o il tempo e l’impegno altrimenti necessari per esportare ed elaborare i dati con una progettazione e un’implementazione aggiuntive di data warehousing. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni approfondite dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di effettuare previsioni utilizzando i contenuti e le risorse di dati delle soluzioni Adobe.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Notebook JupyterLab EDA | Il notebook Python per l’analisi dei dati esplorativi (EDA) è ora disponibile in Jupyterlab. Questo notebook è progettato per assistere l&#39;utente nell&#39;individuazione di pattern nei dati, nel controllo della integrità dei dati e nel riepilogo dei dati rilevanti per i modelli predittivi. Guarda il tutorial su [esplorazione di dati basati sul web per modelli predittivi](../../data-science-workspace/jupyterlab/eda-notebook.md) per ulteriori informazioni. |

Per informazioni più generali su Data Science Workspace, consulta [Panoramica di Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

In Adobe Experience Platform, i dati vengono acquisiti da un’ampia varietà di fonti, analizzati all’interno di Experience Platform e attivati in un’ampia varietà di destinazioni. Platform semplifica il processo di tracciamento di questo flusso di dati potenzialmente non lineare fornendo trasparenza con i flussi di dati.

I flussi di dati sono una rappresentazione dei processi di dati che consentono di spostare i dati in Platform. Questi flussi di dati sono configurati tra servizi diversi, aiutando a spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono quindi utilizzati da [!DNL Identity Service] e [!DNL Real-Time Customer Profile] prima di essere infine attivato in [!DNL Destinations].

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Nuovo dashboard di monitoraggio | Ora puoi utilizzare il dashboard di monitoraggio per garantire trasparenza tra i servizi e informazioni fruibili per l’inserimento dei dati sorgente. Il nuovo dashboard di monitoraggio fornisce una panoramica completa dei dati elaborati da [!DNL Data Lake] a [!DNL Identity Service] e a [!DNL Profile], consentendo al contempo di monitorare i tassi di acquisizione, i successi e gli errori. Guarda il tutorial su [monitoraggio dei flussi di dati di origine nell’interfaccia utente](../../dataflows/ui/monitor-sources.md) per ulteriori informazioni. |

Per informazioni più generali sui flussi di dati, consulta [panoramica dei flussi di dati](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | Il [!DNL LinkedIn Matched Audiences] connessione consente di attivare i tipi di pubblico in [!DNL LinkedIn] piattaforma social network. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che fornisce informazioni in modo più veloce e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Interfaccia utente di ricerca aggiornata | Le funzionalità di ricerca migliorate sono ora disponibili nel [!UICONTROL Sfoglia] scheda in [!UICONTROL Schemi] area di lavoro e la finestra di dialogo per la selezione del gruppo di campi dello schema [!DNL Schema Editor].<br><br>Durante la ricerca di un termine precedente, i risultati includerebbero solo risorse XDM il cui nome corrisponde alla query di ricerca. Ora, oltre alle risorse il cui nome corrisponde alla query, verranno incluse anche le risorse contenenti i singoli attributi che corrispondono al termine. Questo consente di cercare le risorse XDM in base agli attributi in esse contenuti, anziché in base al nome della risorsa.<br><br>Consulta i documenti su [esplorazione delle risorse XDM](../../xdm/ui/explore.md) e [gestione degli schemi](../../xdm/ui/resources/schemas.md) nell’interfaccia utente di per ulteriori informazioni. |

Per informazioni più generali su XDM, consulta [Panoramica del sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Questo è reso più difficile quando i dati del cliente sono frammentati tra sistemi diversi, facendo apparire ogni singolo cliente con più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] ti consente di avere una visione migliore del cliente e del suo comportamento collegando le identità tra dispositivi e sistemi, consentendoti di fornire esperienze digitali personali e di impatto in tempo reale.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Visualizzatore del grafico delle identità | Il visualizzatore del grafo delle identità consente di convalidare e visualizzare le identità unite nell’interfaccia utente, migliorando il debug e la trasparenza. Consulta la [documento visualizzatore grafo identità](../../identity-service/ui/identity-graph-viewer.md) per ulteriori informazioni. |

Per informazioni più generali su [!DNL Identity Service], fare riferimento a [Panoramica del servizio Identity](../../identity-service/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di offrire ai tuoi clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Real-Time Customer Profile puoi visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, del sistema CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Attributi calcolati (alfa) | ***Nota: questa funzionalità è attualmente in formato alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.*** <br/><br/>Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento negli attributi a livello di profilo. Puoi quindi utilizzare gli aggregati in segmentazione, attivazione e personalizzazione. Alcuni esempi di queste funzioni includono count, sum, average, min, max, true/false. Gli attributi calcolati sono attualmente disponibili solo tramite API. Per ulteriori informazioni, vedere [panoramica degli attributi calcolati](../../profile/computed-attributes/overview.md). |

Per ulteriori informazioni su Real-Time Customer Profile, inclusi tutorial e best practice per l’utilizzo di [!DNL Profile] , per iniziare leggi il [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove sorgenti**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Google PubSub] | Ora puoi connetterti [!DNL Google PubSub] a [!DNL Experience Platform] utilizzando [!DNL Flow Service] o l&#39;interfaccia utente. Consulta la [[!DNL Google PubSub] panoramica del connettore](../../sources/connectors/cloud-storage/google-pubsub.md) per ulteriori informazioni. |
| [!DNL Oracle Object Storage] | Ora puoi connetterti [!DNL Oracle Object Storage] a [!DNL Experience Platform] utilizzando [!DNL Flow Service] o l&#39;interfaccia utente. Consulta la [[!DNL Oracle Object Storage] panoramica del connettore](../../sources/connectors/cloud-storage/oracle-object-storage.md) per ulteriori informazioni. |

Per informazioni più generali sulle fonti, fare riferimento a [panoramica sulle origini](../../sources/home.md).
