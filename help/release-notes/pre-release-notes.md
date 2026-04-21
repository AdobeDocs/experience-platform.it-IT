---
title: Note pre-release di Experience Platform
description: Un’anteprima delle ultime note sulla versione di Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5d1825bad97d3ec4beece416dc3e0fc9f6ca636d
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 20%

---

# Note preliminari su Adobe Experience Platform

>[!IMPORTANT]
>
>Questo documento è destinato ad essere **anteprima** delle note sulla versione per il mese corrente. Gli elementi da rilasciare sono soggetti a modifiche e possono essere aggiunti o rimossi nella versione finale.

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/latest)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: aprile 2026**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Servizio Query Service](#query-service)
- [Real-Time CDP](#rtcdp)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Corrispondenza cliente Microsoft Ads](../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Abbina i clienti per indirizzo e-mail e interagisci nuovamente con loro in [!DNL Microsoft Advertising Network], inclusi gli annunci Search&amp;Audience. Collega il tuo account [!DNL Microsoft Advertising] a Real-Time CDP per automatizzare la creazione e la gestione degli elenchi di corrispondenze dei clienti direttamente da Experience Platform. |
| [!BADGE Beta]{type=Informative} [Modifica pubblico personalizzato](../destinations/catalog/advertising/reddit-custom-audience.md) | Invia tipi di pubblico da Experience Platform a [!DNL Reddit Ads]. Connetti il tuo account [!DNL Reddit], mappa le identità e attiva i tipi di pubblico per raggiungere le persone che esplorano attivamente i loro interessi su [!DNL Reddit]. |
| [Amazon Ads v2](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2] è la destinazione corrente per tutte le nuove connessioni [!DNL Amazon Ads]. Se si dispone di una connessione [(Legacy) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md) esistente, questa continuerà a funzionare senza le modifiche necessarie. [!DNL Amazon Ads v2] si connette a [!DNL Ads Data Manager], che fornisce supporto per tipi di identità espansi, campi relativi all&#39;indirizzo e condivisione di dati tra i prodotti [!DNL Amazon Ads], migliorando il targeting e le percentuali di corrispondenza del pubblico rispetto a [(Legacy) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md). |
| [!DNL Rokt] | Utilizza [!DNL Rokt] per connettere il pubblico di Experience Platform a decisioni in tempo reale basate sull&#39;intelligenza artificiale, migliorando le prestazioni della campagna tramite targeting, eliminazione e personalizzazione più precisi. |

{style="table-layout:auto"}

**Correzioni e miglioramenti**

| Correzione | Descrizione |
| --- | --- |
| Supporto per il monitoraggio personalizzato di Personalization | Il dashboard di monitoraggio per le destinazioni ora supporta [!DNL Custom Personalization] destinazioni. La nota di limitazione che ha escluso [!DNL Custom Personalization] dal monitoraggio è stata rimossa. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati introdotti in Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Visibilità utilizzo schema gruppo di campi | Puoi visualizzare gli schemi che utilizzano un gruppo di campi dalla pagina dei dettagli ed esplorarli in una finestra di dialogo ordinabile con i metadati dello schema. Questo consente di valutare rapidamente le dipendenze e l’impatto senza uscire. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica del sistema XDM](../xdm/home.md).

## Servizio Query Service {#query-service}

Utilizzare Query Service per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake] con SQL standard. Unisci qualsiasi set di dati da [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o nell&#39;acquisizione in Real-Time Customer Profile.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Acceleratori Data Distiller | Esegui e pianifica modelli SQL con parametri gestiti da Adobe nell’interfaccia utente di Query Service per eseguire analisi comuni senza scrivere codice SQL. Questo consente di standardizzare i flussi di lavoro di analisi e riutilizzare una logica di query affidabile in tutta l’organizzazione. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica di Query Service](../query-service/home.md).

## Real-Time CDP {#rtcdp}

[!DNL Real-Time CDP] fornisce profili cliente unificati e actionable acquisendo, elaborando e attivando dati in più canali in tempo reale. Con Real-Time CDP, le organizzazioni possono collegare origini di dati esistenti, creare e attivare tipi di pubblico avanzati e garantire l’attivazione conforme alla privacy tra le destinazioni, il tutto dall’interno di Experience Platform. In questo modo esperti di marketing, analisti e team IT possono offrire esperienze altamente personalizzate e tempestive ai clienti attraverso campagne di marketing dirette e multicanale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Real-Time CDP MCP (Beta) | Utilizza Real-Time CDP MCP per inserire Real-Time CDP negli agenti di intelligenza artificiale e nei client compatibili con MCP, consentendo di interagire direttamente con gli strumenti Real-Time CDP tramite l’esperienza LLM nativa. Collegando un client compatibile con MCP (ad esempio Claude, ChatGPT, Claude Code, Codex, Cursor o VS Code) a `https://rtcdp-mcp.adobe.io/mcp`, è possibile utilizzare il linguaggio naturale per controllare il pubblico, la configurazione della destinazione e la cronologia dell&#39;esecuzione dell&#39;attivazione, senza scrivere chiamate REST API di Experience Platform o navigare in più flussi di lavoro dell&#39;interfaccia utente. Dopo aver completato l’accesso a Adobe basato su browser, potrai accedere in sola lettura a diversi strumenti, tra cui: <ul><li>Cerca tipi di pubblico esistenti</li><li>Anteprima iscrizione pubblico</li><li>Elenca tipi di destinazione</li><li>Elenca account configurati</li><li>Elenco delle destinazioni configurate</li><li>Elencare connessioni Source</li><li>Elenca connessioni di destinazione</li><li>Controlla esecuzioni di attivazione</li></ul>. Ogni richiesta richiede `imsOrgId` e `sandboxName` parametri per garantire che le azioni abbiano l&#39;ambito della tua organizzazione e sandbox. In questa versione di Beta non sono supportate le operazioni di scrittura. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [panoramica di Real-Time CDP](../rtcdp/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Express Copy | Utilizza la funzione Copia rapida per copiare gli oggetti in una sandbox di destinazione in un&#39;unica azione dall&#39;[interfaccia utente strumenti sandbox](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Gli oggetti dipendenti vengono rilevati automaticamente e vengono creati nella sandbox di destinazione o riutilizzati quando esistono già. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [panoramica sulle sandbox](../sandboxes/home.md).

## Servizio di segmentazione {#segmentation-service}

Utilizza il servizio di segmentazione per creare tipi di pubblico a partire dai dati dei clienti e gestirne l’intero ciclo di vita in Experience Platform.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Monitoraggio della segmentazione in streaming | Monitora la segmentazione in streaming con visibilità in tempo reale sul tasso di valutazione, la latenza di acquisizione e le metriche di qualità dei dati a livello di sandbox, set di dati e segmenti. Visualizzare le metriche, compresi il tasso di valutazione, la latenza di acquisizione P95, i record ricevuti, i record valutati, i record non riusciti e quelli saltati. Visualizza anche i nuovi profili qualificati e non qualificati per segmento. Utilizza queste informazioni per identificare le violazioni della capacità e i problemi di acquisizione prima che influiscano sui dati. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere la [Panoramica tipi di pubblico](../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| Disattivazione automatica del flusso di dati | I flussi di dati di acquisizione delle origini che si interrompono continuamente per 30 giorni vengono disattivati automaticamente, contribuendo a far emergere flussi di dati non integri e a ridurre le esecuzioni ripetute non riuscite. |
| [!DNL Delta Sharing] | È possibile utilizzare l&#39;origine [!DNL Delta Sharing] per inserire tabelle Delta in Experience Platform tramite un protocollo di condivisione dei dati protetto e aperto. Dopo aver configurato una connessione [!DNL Delta Sharing] e aver selezionato le condivisioni e le tabelle da acquisire, Platform inserisce automaticamente tali dati nei set di dati in modo da poterli utilizzare per l&#39;analisi, la segmentazione e l&#39;attivazione. |
| [!DNL Meta Ads] (Beta) | È possibile utilizzare il connettore di origine [!DNL Meta Ads] (Beta) nell&#39;area di lavoro Origini per eseguire l&#39;autenticazione in [!DNL Meta], selezionare gli account annuncio e pianificare l&#39;acquisizione dei dati relativi alle prestazioni e alla campagna [!DNL Meta Ads] nei set di dati di Experience Platform. |
| [!DNL Talon.One] | È ora possibile connettere Experience Platform a [!DNL Talon.One] utilizzando il nuovo batch [!DNL Talon.One] e le origini di streaming. Utilizza le nuove origini per acquisire i dati del profilo fedeltà e gli eventi di transazione e attività fedeltà in Experience Platform. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../sources/home.md).
