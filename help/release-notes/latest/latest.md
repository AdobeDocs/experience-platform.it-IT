---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione della piattaforma Experience 13 maggio 2020
doc-type: release notes
last-update: May 13, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 0eca2f6e50024ec43c025dd75c34ca876d71c3f2
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 6%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 13 maggio 2020**

Aggiornamenti alle funzionalità esistenti in Adobe Experience Platform:

- [Note sulla versione di Adobe Experience Platform](#adobe-experience-platform-release-notes)
   - [Aggiornamenti dell&#39;interfaccia utente {#ux}](#user-interface-updates-ux)
   - [Area di lavoro Data Science {#dsw}](#data-science-workspace-dsw)
   - [Destinazioni {#destinations}](#destinations-destinations)
   - [SDK Web per la piattaforma Experience e la rete Edge per la piattaforma Experience {#edge}](#experience-platform-web-sdk-and-experience-platform-edge-network-edge)
   - [Origini {#sources}](#sources-sources)

## Aggiornamenti dell&#39;interfaccia utente {#ux}

Adobe Experience Platform sta rilasciando aggiornamenti al dominio e alla barra di intestazione per migliorare la tua esperienza e unificarsi con altre applicazioni Experience Cloud.

- Un passaggio più semplice tra le organizzazioni o verso un’altra applicazione
- Miglioramento dell’aiuto degli utenti, inclusi gli articoli in evidenza e la documentazione pertinente al contesto nel menu Aiuto
- Possibilità di fornire feedback sulla piattaforma Experience e sui biglietti di supporto per i file

L&#39;introduzione della nuova esperienza è graduale. Potete visualizzare l&#39;esperienza all&#39;indirizzo [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

## Area di lavoro Data Science {#dsw}

Data Science Workspace utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per liberare informazioni dai tuoi dati. Integrato in Adobe Experience Platform, Data Science Workspace ti aiuta a fare previsioni utilizzando i tuoi contenuti e le risorse di dati nelle soluzioni Adobe. Uno dei modi in cui Data Science Workspace ottiene questo risultato è attraverso l&#39;uso di JupyterLab. JupyterLab è un&#39;interfaccia utente basata sul Web per <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> ed è strettamente integrata in Adobe Experience Platform. Fornisce un ambiente di sviluppo interattivo che consente agli scienziati dei dati di lavorare con notebook, codice e dati Jupyter.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| JupyterLab Launcher | JupyterLab Launcher ora include avviatori per i notebook Spark 2.4. Gli avviatori dei notebook Spark 2.3 ora sono contrassegnati come obsoleti e impostati per essere rimossi in una versione successiva. |
| Spark 2.4 | Le nuove ricette Scala (Spark) e PySpark ora utilizzano Spark 2.4. |
| Kernel | I notebook Scala (Spark) ora vengono creati tramite il kernel Scala. I notebook PySpark sono ora creati tramite il kernel Python. Il kernel Spark e PySpark sono obsoleti e sono impostati per essere rimossi in una release successiva. |
| Ricette | Le nuove ricette PySpark e Spark ora seguono il flusso di lavoro Docker simile alle ricette Python e R. |

Per ulteriori informazioni sulla migrazione dei notebook e delle ricette per utilizzare Spark 2.4, consulta la guida [alla migrazione dei](../../data-science-workspace/recipe-notebook-migration.md)notebook. Per ulteriori informazioni generali su Data Science Workspace, consulta la documentazione [](../../data-science-workspace/home.md)di panoramica.

## Destinazioni {#destinations}

In [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni preconfigurate con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Adobe Real-time CDP ora supporta l&#39;attivazione dei dati per lo streaming delle destinazioni di archiviazione cloud, consentendo di esportare i dati e gli eventi del pubblico in queste destinazioni in formato JSON. Puoi quindi descrivere la logica di business sopra questi eventi nelle tue destinazioni. Per ulteriori informazioni, vedere di seguito:

>[!NOTE]
>
>Le destinazioni [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs] le destinazioni in Adobe Real-time CDP sono attualmente in versione beta. La documentazione e la funzionalità sono soggette a modifiche.

| Documentazione | Descrizione |
|--- | ---|
| [(Beta) Destinazione Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) | In questo articolo viene illustrato come creare una connessione in uscita in tempo reale allo [!DNL Amazon Kinesis] storage per lo streaming dei dati da Adobe Experience Platform. |
| [(Beta) Destinazione degli hub eventi di Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md) | In questo articolo viene illustrato come creare una connessione in uscita in tempo reale allo [!DNL Azure Event Hubs] storage per lo streaming dei dati da Adobe Experience Platform. |
| [Esercitazione API - Connessione alle destinazioni di streaming e attivazione dei dati](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md) | Questa esercitazione illustra come utilizzare le chiamate API per connettersi ai dati della piattaforma Adobe Experience, creare una connessione a una destinazione di archiviazione cloud in streaming (hub eventi Amazon Kinesis o Azure), creare un flusso di dati per la nuova destinazione creata e attivare i dati per la nuova destinazione creata. |

Per ulteriori informazioni, consulta la panoramica [](/help/rtcdp/destinations/destinations-overview.md)Destinazioni.

## SDK Web per la piattaforma Experience e la rete Edge per la piattaforma Experience {#edge}

L’SDK per la piattaforma Web Experience Platform e l’Experience Platform Edge Network consentono agli utenti di inviare dati ad Adobe Experience Platform e ad altre soluzioni Adobe in tempo reale per i dispositivi e i browser degli utenti finali. L’elenco più recente dei casi di utilizzo è riportato nella roadmap [](https://github.com/adobe/alloy/projects/5) pubblica, che viene aggiornata spesso.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Supporto per ECID | L’SDK supporta l’ECID in dotazione senza ulteriori librerie o informazioni da installare |
| Interfaccia utente di configurazione | Per gestire le impostazioni ID di configurazione con la nuova interfaccia utente di configurazione edge in Launch, è necessario che sia presente una whitelist per accedere a |
| Adobe Experience Platform Web SDK Mixin | Un mixin da usare con l’SDK Web della piattaforma Experience che include tutti i campi supportati. |
| Controlli per il consenso al corso | Fornisce alle aziende i controlli relativi all’opzione di rifiuto e di iscrizione all’SDK Web per la piattaforma Experience |
| Supporto per il debug lato client nella nuova estensione Experience Cloud Debugger | Consulta le richieste dell’SDK per Web della piattaforma Experience e le tracce Edge per vedere in che modo i dati scorrono nel sistema. |
| Adobe Analytics | Invia i dati alle suite di rapporti di Analytics tramite la configurazione edge. XDM viene appiattito nei dati contestuali e supporta l&#39;assegnazione di tag a più suite |
| Adobe Target | Supporto per Adobe Target. Compositore VEC, composer basato su modulo, A/B, XT, Automated Personalization (Personalizzazione automatizzata), MVT |
| Supporto di Adobe Audience Manager | Supporto per le sincronizzazioni ID di Audience Manager, le destinazioni URL e le destinazioni dei cookie |
| `synceIdnetity` | Rinominato `setCustomersIds` per `syncIdentity` renderlo più chiaro |
| Generatore di oggetti XDM | Nell&#39;estensione del lancio è ora possibile creare oggetti XDM come elementi dati |

Per ulteriori informazioni su Platform Web SDK e Edge Network, consulta la [documentazione](../../edge/home.md).

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e allo stesso tempo di strutturarli, etichettarli e ottimizzarli tramite i servizi della piattaforma. È possibile acquisire dati da origini diverse, come applicazioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto aggiuntivo per API e interfaccia utente per i sistemi di storage cloud | Nuovi connettori di origine per Azure File Storage. |
| Supporto aggiuntivo per API e interfaccia utente per i database | Nuovi connettori di origine per Azure Data Explorer, IBM DB2 e Oracle DB. |

**Problemi noti**

- None

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).