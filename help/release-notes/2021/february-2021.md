---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2021
description: Note sulla versione di Adobe Experience Platform di febbraio 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 22%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 24 febbraio 2021**

Nuove funzioni di Adobe Experience Platform:

- [Dashboard di (Beta)](#dashboards)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Dashboard di (Beta) {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso i quali è possibile visualizzare informazioni importanti sui dati dell&#39;organizzazione, acquisite durante le istantanee giornaliere.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Profili, segmenti, destinazioni e dashboard di utilizzo delle licenze (Beta) | **Nota: la funzionalità del dashboard è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.**<br/><br/> I dashboard forniscono rapporti predefiniti sui dati dell’organizzazione e sono incorporati direttamente nel flusso di lavoro degli addetti al marketing all’interno di Platform. Queste dashboard sono disponibili senza la necessità di ulteriore supporto IT o il tempo e l’impegno altrimenti necessari per esportare ed elaborare i dati con una progettazione e un’implementazione aggiuntive di data warehousing. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di effettuare previsioni utilizzando i contenuti e le risorse di dati delle soluzioni Adobe.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Notebook JupyterLab EDA | Il notebook Python per l’analisi dei dati esplorativi (EDA) è ora disponibile in Jupyterlab. Questo notebook è progettato per assistere l&#39;utente nell&#39;individuazione di pattern nei dati, nel controllo della integrità dei dati e nel riepilogo dei dati rilevanti per i modelli predittivi. Per ulteriori informazioni, consulta il tutorial su [esplorazione dei dati basati sul web per i modelli predittivi](../../data-science-workspace/jupyterlab/eda-notebook.md). |

Per informazioni più generali su Data Science Workspace, consulta la [Panoramica di Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

In Adobe Experience Platform, i dati vengono acquisiti da un’ampia varietà di fonti, analizzati all’interno di Experience Platform e attivati in un’ampia varietà di destinazioni. Platform semplifica il processo di tracciamento di questo flusso di dati potenzialmente non lineare fornendo trasparenza con i flussi di dati.

I flussi di dati sono una rappresentazione dei processi di dati che spostano i dati in Platform. Questi flussi di dati sono configurati in servizi diversi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono utilizzati da [!DNL Identity Service] e [!DNL Real-Time Customer Profile] prima di essere infine attivati in [!DNL Destinations].

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Nuovo dashboard di monitoraggio | Ora puoi utilizzare il dashboard di monitoraggio per garantire trasparenza tra i servizi e informazioni fruibili per l’inserimento dei dati sorgente. Il nuovo dashboard di monitoraggio fornisce una visualizzazione completa dei dati elaborati da [!DNL Data Lake] a [!DNL Identity Service] e a [!DNL Profile], consentendo al contempo di monitorare i tassi di acquisizione, i successi e gli errori. Per ulteriori informazioni, consulta l&#39;esercitazione sul monitoraggio dei flussi di dati di origine [ nell&#39;interfaccia utente](../../dataflows/ui/monitor-sources.md). |

Per informazioni più generali sui flussi di dati, consulta la [panoramica sui flussi di dati](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | La connessione [!DNL LinkedIn Matched Audiences] consente di attivare i tipi di pubblico nella piattaforma social [!DNL LinkedIn]. |

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull&#39;esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che fornisce informazioni in modo più veloce e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Interfaccia utente di ricerca aggiornata | Le funzionalità di ricerca migliorate sono ora disponibili nella scheda [!UICONTROL Sfoglia] nell&#39;area di lavoro [!UICONTROL Schemi] e nella finestra di dialogo per la selezione del gruppo di campi dello schema in [!DNL Schema Editor].<br><br>Quando si cerca un termine in precedenza, i risultati includerebbero solo risorse XDM il cui nome corrisponde alla query di ricerca. Ora, oltre alle risorse il cui nome corrisponde alla query, verranno incluse anche le risorse contenenti i singoli attributi che corrispondono al termine. Questo consente di cercare le risorse XDM in base agli attributi in esse contenuti, anziché in base al nome della risorsa.<br><br>Per ulteriori informazioni, consulta i documenti relativi a [esplorazione delle risorse XDM](../../xdm/ui/explore.md) e [gestione degli schemi](../../xdm/ui/resources/schemas.md) nell&#39;interfaccia utente. |

Per ulteriori informazioni generali su XDM, consulta la [Panoramica del sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Questo è reso più difficile quando i dati del cliente sono frammentati tra sistemi diversi, facendo apparire ogni singolo cliente con più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una migliore visualizzazione dei clienti e del loro comportamento collegando le identità tra dispositivi e sistemi, consentendo di fornire esperienze digitali personali e di impatto in tempo reale.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Visualizzatore del grafico delle identità | Il visualizzatore del grafo delle identità consente di convalidare e visualizzare le identità unite nell’interfaccia utente, migliorando il debug e la trasparenza. Per ulteriori informazioni, vedere il documento [visualizzatore grafico delle identità](../../identity-service/features/identity-graph-viewer.md). |

Per ulteriori informazioni generali su [!DNL Identity Service], consulta [Panoramica del servizio Identity](../../identity-service/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Attributi calcolati (Alpha) | ***Nota: questa funzionalità è attualmente in formato alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.*** <br/><br/>Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Puoi quindi utilizzare gli aggregati in segmentazione, attivazione e personalizzazione. Alcuni esempi di queste funzioni includono count, sum, average, min, max, true/false. Gli attributi calcolati sono attualmente disponibili solo tramite API. |

Per ulteriori informazioni su Real-Time Customer Profile, inclusi tutorial e best practice per l&#39;utilizzo dei dati di [!DNL Profile], leggere la [Panoramica sul profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove origini**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Google PubSub] | È ora possibile connettere [!DNL Google PubSub] a [!DNL Experience Platform] utilizzando l&#39;API [!DNL Flow Service] o l&#39;interfaccia utente. Per ulteriori informazioni, vedere [[!DNL Google PubSub] panoramica del connettore](../../sources/connectors/cloud-storage/google-pubsub.md). |
| [!DNL Oracle Object Storage] | È ora possibile connettere [!DNL Oracle Object Storage] a [!DNL Experience Platform] utilizzando l&#39;API [!DNL Flow Service] o l&#39;interfaccia utente. Per ulteriori informazioni, vedere [[!DNL Oracle Object Storage] panoramica del connettore](../../sources/connectors/cloud-storage/oracle-object-storage.md). |

Per informazioni più generali sulle origini, consulta la [panoramica delle origini](../../sources/home.md).
