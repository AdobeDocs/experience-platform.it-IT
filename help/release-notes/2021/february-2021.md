---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2021
description: Note sulla versione di febbraio 2021 per Adobe Experience Platform.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 24 febbraio 2021**

Nuove funzioni in Adobe Experience Platform:

- [Dashboard (Beta)](#dashboards)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Dashboard (Beta) {#dashboards}

Adobe Experience Platform fornisce diverse dashboard attraverso le quali è possibile visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Dashboard per profili, segmenti, destinazioni e utilizzo licenze (Beta) | **Nota: La funzionalità del dashboard è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.**<br/><br/> Le dashboard forniscono rapporti predefiniti sui dati dell’organizzazione e sono integrate direttamente nel flusso di lavoro dell’addetto al marketing all’interno di Platform. Queste dashboard sono disponibili senza la necessità di ulteriore supporto IT o il tempo e lo sforzo necessari per esportare ed elaborare i dati con una progettazione e un&#39;implementazione aggiuntive per il data warehouse. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilizza l’apprendimento automatico e l’intelligenza artificiale per creare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace consente di fare previsioni utilizzando i contenuti e le risorse di dati nelle soluzioni Adobe.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Notebook JupyterLab EDA | Il notebook di Python per l&#39;analisi dei dati esplorativi (EDA) è ora disponibile in Jupyterlab. Questo notebook è stato progettato per aiutarti a scoprire i pattern dei dati, controllare l’integrità dei dati e riepilogare i dati pertinenti per i modelli predittivi. Guarda l’esercitazione su [esplorazione di dati basati sul web per modelli predittivi](../../data-science-workspace/jupyterlab/eda-notebook.md) per ulteriori informazioni. |

Per informazioni più generali su Data Science Workspace, consulta [Panoramica di Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

In Adobe Experience Platform, i dati vengono acquisiti da un’ampia varietà di sorgenti, analizzati all’interno di Experience Platform, e attivati in un’ampia varietà di destinazioni. Platform facilita il processo di tracciamento di questo flusso di dati potenzialmente non lineare grazie alla trasparenza dei flussi di dati.

I flussi di dati sono una rappresentazione dei processi di dati che consentono di spostare i dati in Platform. Questi flussi di dati sono configurati tra diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono quindi utilizzati da [!DNL Identity Service] e [!DNL Real-time Customer Profile] prima di essere infine attivato su [!DNL Destinations].

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Nuovo dashboard di monitoraggio | È ora possibile utilizzare il dashboard di monitoraggio per la trasparenza cross-service e informazioni fruibili per l’inserimento dei dati di origine. Il nuovo dashboard di monitoraggio fornisce una visualizzazione completa dei dati elaborati da [!DNL Data Lake] a [!DNL Identity Service] e [!DNL Profile], e al contempo monitorare i tassi di acquisizione, i successi e gli errori. Guarda l’esercitazione su [monitoraggio dei flussi di dati sorgente nell’interfaccia utente](../../dataflows/ui/monitor-sources.md) per ulteriori informazioni. |

Per informazioni più generali sui flussi di dati, consulta [panoramica dei dataflows](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | La [!DNL LinkedIn Matched Audiences] la connessione consente di attivare i tipi di pubblico nella [!DNL LinkedIn] piattaforma sociale. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base della [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare il potere delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che offre informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Interfaccia utente di ricerca aggiornata | Sono ora disponibili funzionalità di ricerca migliorate nel [!UICONTROL Sfoglia] nella scheda [!UICONTROL Schemi] area di lavoro e finestra di dialogo per la selezione del gruppo di campi dello schema [!DNL Schema Editor].<br><br>Durante la ricerca di un termine in precedenza, i risultati includevano solo risorse XDM il cui nome corrisponde alla query di ricerca. Ora, oltre alle risorse il cui nome corrisponde alla query, verranno incluse anche le risorse contenenti attributi singoli che corrispondono al termine. Ciò ti consente di cercare le risorse XDM in base agli attributi che contengono anziché in base al nome della risorsa.<br><br>Vedi i documenti su [esplorazione delle risorse XDM](../../xdm/ui/explore.md) e [gestione degli schemi](../../xdm/ui/resources/schemas.md) nell’interfaccia utente di per ulteriori informazioni. |

Per informazioni più generali su XDM, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni singolo cliente sembri avere più &quot;identità&quot;.

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una visione migliore del cliente e del suo comportamento attraverso il collegamento delle identità tra dispositivi e sistemi, per offrire in tempo reale esperienze digitali personali di impatto.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Visualizzatore grafico di identità | Il visualizzatore del grafico delle identità consente di convalidare e visualizzare le identità unite nell’interfaccia utente, per migliorare il debug e la trasparenza. Consulta la sezione [documento visualizzatore grafico identità](../../identity-service/ui/identity-graph-viewer.md) per ulteriori informazioni. |

Per informazioni più generali su [!DNL Identity Service], fare riferimento alla [Panoramica del servizio Identity](../../identity-service/home.md).

## Real-time Customer Profile {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account actionable con marca temporale per ogni interazione con il cliente.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Attributi calcolati (alfa) | ***Nota: Questa funzionalità è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.*** <br/><br/>Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Puoi quindi utilizzare gli aggregati in segmentazione, attivazione e personalizzazione. Alcuni esempi di queste funzioni includono conteggio, somma, media, min, max, true/false. Gli attributi calcolati sono attualmente disponibili solo tramite API. Per ulteriori informazioni, consulta la sezione [panoramica degli attributi calcolati](../../profile/computed-attributes/overview.md). |

Per ulteriori informazioni sul profilo cliente in tempo reale, compresi tutorial e best practice per l’utilizzo di [!DNL Profile] dati, si prega di iniziare leggendo il [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove fonti**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Google PubSub] | È ora possibile connettersi [!DNL Google PubSub] a [!DNL Experience Platform] utilizzando [!DNL Flow Service] API o interfaccia utente. Consulta la sezione [[!DNL Google PubSub] panoramica del connettore](../../sources/connectors/cloud-storage/google-pubsub.md) per ulteriori informazioni. |
| [!DNL Oracle Object Storage] | È ora possibile connettersi [!DNL Oracle Object Storage] a [!DNL Experience Platform] utilizzando [!DNL Flow Service] API o interfaccia utente. Consulta la sezione [[!DNL Oracle Object Storage] panoramica del connettore](../../sources/connectors/cloud-storage/oracle-object-storage.md) per ulteriori informazioni. |

Per informazioni più generali sulle fonti, consulta la [panoramica di origini](../../sources/home.md).
