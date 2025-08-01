---
title: Note sulla versione di Adobe Experience Platform di luglio 2025
description: Note sulla versione di Adobe Experience Platform di luglio 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 23%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: mercoledì 29 luglio 2025**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Capacità](#capacity)
- [Destinazioni](#destinations)
- [Acquisizione dei dati](#data-ingestion)
- [Edizione B2B di Real-Time CDP](#b2b)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)


## Capacità {#capacity}

>[!AVAILABILITY]
>
>Questa funzione sarà disponibile per l’uso in base alla tua area geografica. Per gli utenti delle Americhe, sarà disponibile a partire dall’11 agosto. Per gli utenti in Europa, sarà disponibile a partire dal 25 agosto. Per gli utenti in Asia, questo sarà disponibile a partire dall’8 settembre.

Capacity fornisce una visione completa delle [protezioni](../../rtcdp/guardrails/overview.md) della tua organizzazione e fornisce consigli su come risolvere le potenziali violazioni di capacità allocando le capacità a livello di sandbox. Con questa versione, puoi visualizzare la capacità sia per l’acquisizione in streaming che per la segmentazione in streaming.

Per ulteriori informazioni, leggere la [Panoramica capacità](../../landing/license-usage-and-guardrails/capacity.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Disponibilità limitata della connessione [Google Customer Match + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) | Dopo essere stata brevemente disponibile per tutti i clienti a giugno, Adobe ha ripristinato la disponibilità limitata di questa integrazione. Attualmente, l’accesso a questa destinazione è limitato ai clienti che sono già abilitati, mentre Adobe e Google lavorano per risolvere i problemi di implementazione. Se ti interessa utilizzare questa integrazione una volta ripreso il rollout più ampio, contatta il tuo rappresentante Adobe per esprimere le tue intenzioni. |
| [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) aggiornamento interno | A partire dal venerdì 31 luglio 2025 nel catalogo delle destinazioni, puoi visualizzare due schede [!DNL The Trade Desk] affiancate. Questo è dovuto a un aggiornamento interno del servizio destinazioni. <br><br>Il connettore di destinazione [!DNL The Trade Desk] esistente è stato rinominato in **[!UICONTROL (obsoleto) The Trade Desk]** e una nuova scheda con il nome **[!UICONTROL The Trade Desk]** è ora disponibile. Utilizza la nuova connessione **[!UICONTROL Trade Desk]** nel catalogo per i nuovi flussi di dati di attivazione. <br><br>Se sono presenti flussi di dati attivi per la destinazione **[!UICONTROL (obsoleto) Trade Desk]**, questi verranno aggiornati automaticamente, pertanto non è richiesta alcuna azione da parte dell&#39;utente. <br><br>Se si creano flussi di dati tramite l&#39;API [Servizio flusso](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare [!DNL flow spec ID] e [!DNL connection spec ID] ai valori seguenti:<ul><li>Flow spec ID: `86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>Connection spec ID: `1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nomi account e descrizioni per le connessioni di destinazione | È ora possibile [aggiungere nomi e descrizioni di account](/help/destinations/ui/connect-destination.md) durante la connessione alle destinazioni, consentendo una migliore gestione delle destinazioni con più account. |
| Informazioni sullo stream di dati migliorate per le destinazioni edge | Le informazioni nella barra a destra per [destinazioni Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) e [destinazioni Personalization](/help/destinations/catalog/personalization/custom-personalization.md) personalizzate sono state migliorate per visualizzare il nome dello stream di dati, offrendo una visibilità più chiara nelle configurazioni dello stream di dati associato e contribuendo a ridurre la confusione durante la revisione dei flussi di dati esistenti. Il selettore **[!UICONTROL ID Datastream]** nella schermata di configurazione di destinazione è stato aggiornato a **[!UICONTROL Datastream]** per una maggiore chiarezza nell&#39;interfaccia utente. |
| Visibilità delle azioni di marketing nella selezione della destinazione | Le azioni di marketing vengono ora visualizzate nella barra a destra della scheda **[[!UICONTROL Sfoglia]](/help/destinations/ui/destinations-workspace.md#browse)** nell&#39;area di lavoro Destinazioni e nella pagina **[[!UICONTROL Il flusso di dati viene eseguito]](/help/dataflows/ui/monitor-destinations.md)**, fornendo visibilità immediata sulle modifiche delle azioni di marketing senza dover passare alla pagina di visualizzazione. Questo miglioramento migliora l’esperienza utente rendendo più semplice verificare le configurazioni delle azioni di marketing durante la configurazione della destinazione. |
| [!BADGE Versione beta limitata]{type=Informative} Modifica azioni di marketing per le destinazioni | È ora possibile [modificare le azioni di marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) per le destinazioni esistenti. Questa funzione è attualmente in versione beta limitata. Per richiedere l’accesso, contatta il tuo rappresentante Adobe. |
| [!BADGE Versione beta limitata]{type=Informative} Modificare le destinazioni | È ora possibile [modificare la configurazione di destinazione](/help/destinations/ui/edit-destination.md) dopo averla creata. Questa funzione è attualmente in versione beta limitata. Per richiedere l’accesso, contatta il tuo rappresentante Adobe. |

**Correzioni**

| Problema | Descrizione |
| --- | --- |
| Funzionalità di scorrimento delle categorie | È stato risolto un problema che impediva lo scorrimento corretto del menu laterale delle categorie nel catalogo delle destinazioni e delle origini al passaggio del mouse, migliorando l’usabilità della navigazione per gli utenti che navigavano nelle categorie di destinazione. |

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Acquisizione dei dati {#ingestion}

Experience Platform fornisce un framework completo per l’acquisizione dei dati che supporta l’acquisizione di dati in batch e in streaming da varie sorgenti.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per il monitoraggio dell’acquisizione del profilo di streaming | È ora disponibile il monitoraggio in tempo reale per l’acquisizione dei profili di streaming, che fornisce trasparenza in termini di velocità effettiva, latenza e metriche di qualità dei dati. In questo modo è possibile inviare avvisi proattivi e ottenere informazioni utili per aiutare i data engineer a identificare le violazioni della capacità e i problemi di acquisizione. Per ulteriori informazioni, consulta la guida sul [monitoraggio dell&#39;acquisizione del profilo di streaming](../../dataflows/ui/monitor-streaming-profile.md). |

Per ulteriori informazioni, consulta la [panoramica sull&#39;acquisizione dei dati](../../ingestion/home.md).

## Edizione B2B di Real-Time CDP {#b2b}

Real-Time CDP B2B edition fornisce funzionalità complete di gestione dei dati dei clienti B2B, consentendo alle organizzazioni di creare profili cliente unificati, creare tipi di pubblico B2B sofisticati e attivare i dati su vari canali di marketing.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento dell’architettura B2B | Experience Platform sta effettuando l’aggiornamento a una nuova architettura B2B che introduce miglioramenti significativi per i tipi di pubblico multientità con attributi B2B. Questo aggiornamento consolida il supporto dei criteri di unione, migliora l’accuratezza del conteggio del pubblico e migliora le funzionalità di risoluzione delle entità. Leggi la [Panoramica sull&#39;aggiornamento dell&#39;architettura di Real-Time CDP B2B edition](../../rtcdp/b2b-architecture-upgrade.md) per una suddivisione completa delle modifiche. |
| Consolidamento dei criteri di unione per tipi di pubblico con più entità | I tipi di pubblico con più entità con attributi B2B ora supportano un solo criterio di unione, ovvero il criterio di unione predefinito, anziché più criteri di unione. Questa modifica garantisce una composizione coerente del pubblico e semplifica la gestione della logica di unione. Per ulteriori informazioni, leggere la [panoramica dei criteri di unione](../../profile/merge-policies/overview.md). |
| Conteggi avanzati dei tipi di pubblico per le entità B2B | Le stime delle dimensioni del pubblico per i tipi di pubblico con entità B2B come Account e Opportunità sono ora esatte, in base ai risultati della segmentazione in tempo reale. Questo miglioramento fornisce stime più accurate e affidabili per i tipi di pubblico che coinvolgono relazioni B2B complesse. |
| Snapshot dell’account per l’iscrizione al pubblico | I dettagli di iscrizione al pubblico sono ora inclusi per le entità account nelle esportazioni di istantanee, consentendo l’accesso allo stato del pubblico a livello di account, alle marche temporali e agli indicatori di iscrizione. Questo porta alla parità delle funzioni tra i modelli di profilo (Persona) e segmentazione dell’account. |
| Modifiche agli strumenti della sandbox per tipi di pubblico con più entità | L’importazione di tipi di pubblico con più entità con entità B2B ed eventi di esperienza esportati prima della migrazione non è più supportata. Questi tipi di pubblico non supereranno la convalida di importazione e non potranno essere convertiti automaticamente nella nuova architettura. I tipi di pubblico devono essere riesportati dopo la migrazione prima di essere importati nelle sandbox di destinazione. Per ulteriori informazioni, leggere la [guida sugli oggetti supportati per gli strumenti sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| API dell’entità B2B obsolete | Le operazioni di ricerca API [!DNL Profile Access] per le entità B2B (relazione account-persona, relazione persona-opportunità, campagna, membro della campagna, elenco di marketing e membri elenco di marketing) sono ora obsolete. Inoltre, [!DNL Profile Access] operazioni di eliminazione API per entità B2B (account, relazione account-persona, opportunità, relazione persona opportunità, campagna, membro della campagna, elenco di marketing e membri elenco di marketing) sono anch&#39;esse obsolete. Per ulteriori informazioni, consulta la guida dell&#39;API dell&#39;endpoint [entities](../../profile/api/entities.md). |
| Aggiornamenti allo spazio dei nomi delle identità per la risoluzione delle entità | Le entità account e opportunità ora utilizzano l&#39;unione basata sulla precedenza temporale con spazi dei nomi di identità specifici (`b2b_account` per l&#39;account, `b2b_opportunity` per l&#39;opportunità). Tutte le altre entità sono unificate con sovrapposizioni di identità primarie unite utilizzando l’unione basata sulla precedenza temporale. Per ulteriori informazioni sulla risoluzione delle entità, leggere la guida dell&#39;API dell&#39;endpoint [entities](../../profile/api/entities.md). |

Per ulteriori informazioni, leggere la [panoramica di Real-Time CDP B2B edition](../../rtcdp/b2b-overview.md).

## Sandbox {#sandboxes}

Experience Platform è stato sviluppato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere a sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Modifiche alle importazioni di tipi di pubblico con più entità | Gli strumenti sandbox sono stati aggiornati per supportare il nuovo aggiornamento dell’architettura B2B. I tipi di pubblico con più entità contenenti entità B2B ed eventi esperienza devono essere riesportati dopo l’aggiornamento dell’architettura prima di essere importati nelle sandbox di destinazione tramite gli strumenti sandbox. L’importazione delle versioni precedenti all’aggiornamento non riuscirà la convalida. Per ulteriori informazioni, leggere la [guida sugli oggetti supportati per gli strumenti sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| API per pubblico esterno | Puoi utilizzare l’API dei tipi di pubblico esterni per importare in modo programmatico i tipi di pubblico generati esternamente in Adobe Experience Platform. Per ulteriori informazioni, consulta la [guida dell&#39;endpoint per tipi di pubblico esterni](../../segmentation/api/external-audiences.md). |

Per ulteriori informazioni sulla segmentazione, leggere la [Panoramica del servizio di segmentazione](../../segmentation/home.md)

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove origini**

| Origine | Descrizione |
| --- | --- |
| Supporto di [!BADGE Beta]{type=Informative} per [!DNL Didomi] (Streaming SDK) | Utilizza l&#39;origine [!DNL Didomi] per acquisire i dati di gestione del consenso e delle preferenze da [!DNL Didomi], supportando la conformità alle normative sulla privacy e alle strategie di marketing basate sul consenso. Per informazioni su come eseguire la configurazione, leggere la [[!DNL Didomi] panoramica origine](../../sources/connectors/consent-and-preferences/didomi.md). Per i passaggi relativi alla creazione di una connessione di origine, leggere la [[!DNL Didomi] guida alla connessione di origine](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md). |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l&#39;acquisizione di dati di modifica in origini selezionate tramite l&#39;API [!DNL Flow Service] | Ora puoi creare flussi di dati che abilitano l’acquisizione di dati di modifica per l’acquisizione incrementale utilizzando i connettori di origine. Questa funzionalità consente ai clienti di inserire il tipo di dati Change per l’acquisizione incrementale, migliorando l’aggiornamento dei dati e riducendo il sovraccarico di elaborazione. Per ulteriori informazioni, leggere la documentazione su [utilizzo dell&#39;acquisizione dati di modifica per le origini](../../sources/tutorials/api/change-data-capture.md) |
| Supporto per l&#39;eliminazione temporanea di record in [!DNL Salesforce] | L&#39;origine [!DNL Salesforce] ora supporta l&#39;inclusione di record eliminati tramite un parametro `includeDeletedObjects` facoltativo. Se impostato su true, i clienti possono includere record eliminati soft nelle query [!DNL Salesforce] e inserire tali record in Experience Platform. Per ulteriori informazioni, consulta la [[!DNL Salesforce] documentazione sulle origini.](../../sources/connectors/crm/salesforce.md) |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).
