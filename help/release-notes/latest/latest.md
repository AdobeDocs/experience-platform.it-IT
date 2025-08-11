---
title: Note sulla versione di Adobe Experience Platform di luglio 2025
description: Note sulla versione di Adobe Experience Platform di luglio 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: ht
source-wordcount: '1574'
ht-degree: 100%

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

**Data di rilascio: 29 luglio 2025**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Capacità](#capacity)
- [Destinazioni](#destinations)
- [Acquisizione dati](#data-ingestion)
- [Real-Time CDP B2B Edition](#b2b)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)


## Capacità {#capacity}

>[!AVAILABILITY]
>
>Questa funzione sarà disponibile per l’uso in base all’area geografica. Per gli utenti nelle Americhe, sarà disponibile a partire dall’11 agosto. Per gli utenti in Europa, sarà disponibile a partire dal 25 agosto. Per gli utenti in Asia, sarà disponibile a partire dall’8 settembre.

La funzione Capacità fornisce una visione completa dei [guardrail](../../rtcdp/guardrails/overview.md) dell’organizzazione e offre consigli su come risolvere le potenziali violazioni di capacità allocando le capacità a livello di sandbox. Con questa versione, è possibile visualizzare la capacità sia per l’acquisizione che per la segmentazione in streaming.

Per ulteriori informazioni, consulta la [panoramica sulla capacità](../../landing/license-usage-and-guardrails/capacity.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Disponibilità limitata della connessione [Google Customer Match + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) | Dopo essere stata brevemente disponibile per tutta la clientela a giugno, Adobe ha ripristinato la disponibilità limitata di questa integrazione. Attualmente, l’accesso a questa destinazione è limitato alla clientela già abilitata, mentre Adobe e Google si impegnano per risolvere i problemi di implementazione. Se hai interesse per l’utilizzo di questa integrazione una volta ripreso il rollout più ampio, contatta il tuo rappresentante Adobe per esprimere le tue intenzioni. |
| Aggiornamento interno di [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) | A partire dal 31 luglio 2025 nel catalogo delle destinazioni, puoi visualizzare due schede [!DNL The Trade Desk] affiancate. Questo è dovuto a un aggiornamento interno del servizio destinazioni. <br><br>Il connettore di destinazione [!DNL The Trade Desk] esistente è stato ridenominato in **[!UICONTROL (obsoleto) The Trade Desk]** e una nuova scheda con il nome **[!UICONTROL The Trade Desk]** è ora disponibile. Utilizza la nuova connessione **[!UICONTROL The Trade Desk]** nel catalogo per i nuovi flussi di dati di attivazione. <br><br>Se sono presenti flussi di dati attivi nella destinazione **[!UICONTROL (obsoleto) The Trade Desk]**, questi verranno aggiornati automaticamente e non sarà quindi richiesta alcuna azione da parte tua. <br><br>Se stai creando flussi di dati tramite [API Flow Service ](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare l’[!DNL flow spec ID] e l’[!DNL connection spec ID] ai seguenti valori:<ul><li>Flow spec ID: `86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>Connection spec ID: `1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nomi account e descrizioni per le connessioni di destinazione | È ora possibile [aggiungere nomi e descrizioni di account](/help/destinations/ui/connect-destination.md) durante la connessione alle destinazioni, consentendo una migliore gestione delle destinazioni con più account. |
| Informazioni sullo stream di dati migliorate per le destinazioni Edge | Le informazioni nella barra a destra per destinazioni [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) e [Personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md) sono state migliorate per mostrare il nome dello stream di dati, offrendo una visibilità più chiara nelle configurazioni dello stream di dati associato e contribuendo a ridurre la confusione durante la revisione dei flussi di dati esistenti. Il selettore **[!UICONTROL ID dello stream di dati]** nella schermata di configurazione della destinazione è stato aggiornato a **[!UICONTROL Stream di dati]** per una maggiore chiarezza nell’interfaccia utente. |
| Visibilità delle azioni di marketing nella selezione della destinazione | Le azioni di marketing vengono ora mostrate nella barra a destra della scheda **[[!UICONTROL Sfoglia]](/help/destinations/ui/destinations-workspace.md#browse)** nell’area di lavoro Destinazioni e nella pagina **[[!UICONTROL Esecuzioni flusso di dati]](/help/dataflows/ui/monitor-destinations.md)**, fornendo visibilità immediata sulle modifiche delle azioni di marketing senza dover passare alla pagina di visualizzazione. Questo miglioramento migliora l’esperienza utente rendendo più semplice verificare le configurazioni delle azioni di marketing durante la configurazione della destinazione. |
| [!BADGE Versione Beta limitata]{type=Informative} Modificare le azioni di marketing per le destinazioni | Ora è possibile [modificare le azioni di marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) per le destinazioni esistenti. Per il momento, questa funzione è in versione Beta limitata. Per richiedere l’accesso, contatta il tuo rappresentante Adobe. |
| [!BADGE Versione Beta limitata]{type=Informative} Modificare le destinazioni | Ora è possibile [modificare la configurazione della destinazione](/help/destinations/ui/edit-destination.md) dopo averla creata. Per il momento, questa funzione è in versione Beta limitata. Per richiedere l’accesso, contatta il tuo rappresentante Adobe. |

**Correzioni**

| Problema | Descrizione |
| --- | --- |
| Funzionalità di scorrimento delle categorie | È stato risolto un problema che impediva lo scorrimento corretto del menu laterale delle categorie nel catalogo delle destinazioni e delle origini al passaggio del mouse, migliorando l’usabilità della navigazione per gli utenti che sfogliano le categorie di destinazione. |

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Acquisizione dati {#ingestion}

Experience Platform fornisce un framework completo per l’acquisizione dei dati che supporta l’acquisizione di dati in batch e in streaming da varie origini.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per il monitoraggio dell’acquisizione del profilo di streaming | È ora disponibile il monitoraggio in tempo reale per l’acquisizione dei profili di streaming, che fornisce trasparenza in termini di velocità effettiva, latenza e metriche di qualità dei dati. In questo modo è possibile inviare avvisi proattivi e ottenere informazioni utili per aiutare i data engineer a identificare le violazioni della capacità e i problemi di acquisizione. Per ulteriori informazioni, consulta la guida al [monitoraggio dell’acquisizione del profilo di streaming](../../dataflows/ui/monitor-streaming-profile.md). |

Per ulteriori informazioni, consulta la [panoramica sull’acquisizione dei dati](../../ingestion/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B Edition fornisce funzionalità complete di gestione dei dati della clientela B2B, consentendo alle organizzazioni di creare profili cliente unificati, creare tipi di pubblico B2B sofisticati e attivare i dati su vari canali di marketing.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento dell’architettura B2B | Experience Platform sta effettuando l’aggiornamento a una nuova architettura B2B che introduce miglioramenti significativi per i tipi di pubblico con più entità e attributi B2B. Questo aggiornamento consolida il supporto dei criteri di unione, migliora l’accuratezza del conteggio del pubblico e migliora le funzionalità di risoluzione delle entità. Consulta la [panoramica sull’aggiornamento dell’architettura di Real-Time CDP B2B Edition](../../rtcdp/b2b-architecture-upgrade.md) per un raggruppamento completo delle modifiche. |
| Consolidamento dei criteri di unione per tipi di pubblico con più entità | I tipi di pubblico con più entità e attributi B2B ora supportano un solo criterio di unione, ovvero il criterio di unione predefinito, anziché più criteri di unione. Questa modifica garantisce una composizione coerente del pubblico e semplifica la gestione della logica di unione. Per ulteriori informazioni, consulta la [panoramica sui criteri di unione](../../profile/merge-policies/overview.md). |
| Conteggi di pubblico migliorati per le entità B2B | Le stime delle dimensioni del pubblico per i tipi di pubblico con entità B2B come Account e Opportunità ora sono esatte, in base ai risultati della segmentazione in tempo reale. Questo miglioramento fornisce stime più accurate e affidabili per i tipi di pubblico che coinvolgono relazioni B2B complesse. |
| Istantanee dell’account per l’appartenenza al pubblico | I dettagli dell’appartenenza al pubblico ora sono inclusi per le entità account nelle esportazioni di istantanee, consentendo l’accesso allo stato del pubblico a livello di account, alle marche temporali e agli indicatori di appartenenza. Questo porta alla parità di funzioni tra i modelli di profilo (Persona) e segmentazione dell’account. |
| Modifiche agli strumenti della sandbox per tipi di pubblico con più entità | L’importazione di tipi di pubblico con più entità con entità B2B ed eventi esperienza esportati prima della migrazione non è più supportata. Questi tipi di pubblico non supereranno la convalida di importazione e non potranno essere convertiti automaticamente nella nuova architettura. I tipi di pubblico devono essere esportati nuovamente dopo la migrazione prima di essere importati nelle sandbox di destinazione. Per ulteriori informazioni, consulta la [guida agli oggetti supportati per gli strumenti sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Obsolescenze delle API dell’entità B2B | Le operazioni di ricerca API [!DNL Profile Access] per le entità B2B (relazione account-persona, relazione persona-opportunità, campagna, membro della campagna, elenco di marketing e membri elenco di marketing) sono ora obsolete. Inoltre, le operazioni di eliminazione API [!DNL Profile Access] per entità B2B (account, relazione account-persona, opportunità, relazione persona opportunità, campagna, membro della campagna, elenco di marketing e membri elenco di marketing) sono anch’esse obsolete. Per ulteriori informazioni, consulta la [guida all’endpoint API delle entità](../../profile/api/entities.md). |
| Aggiornamenti allo spazio dei nomi identità per la risoluzione delle entità | Le entità Account e Opportunità ora utilizzano l’unione basata sulla precedenza temporale con spazi dei nomi identità specifici (`b2b_account` per Account, `b2b_opportunity` per Opportunità). Tutte le altre entità sono unificate con sovrapposizioni di identità primarie unite utilizzando l’unione basata sulla precedenza temporale. Per ulteriori informazioni sulla risoluzione delle entità, consulta la [guida all’endpoint API delle entità](../../profile/api/entities.md). |

Per ulteriori informazioni, consulta la [panoramica su Real-Time CDP B2B Edition](../../rtcdp/b2b-overview.md).

## Sandbox {#sandboxes}

Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere a sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Modifiche alle importazioni di tipi di pubblico con più entità | Gli strumenti sandbox sono stati aggiornati per supportare il nuovo aggiornamento dell’architettura B2B. I tipi di pubblico con più entità contenenti entità B2B ed eventi esperienza devono essere esportati di nuovo dopo l’aggiornamento dell’architettura prima di essere importati nelle sandbox di destinazione tramite gli strumenti sandbox. L’importazione delle versioni precedenti all’aggiornamento non supererà la convalida. Per ulteriori informazioni, consulta la [guida agli oggetti supportati per gli strumenti sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| API per pubblico esterno | Puoi utilizzare l’API dei tipi di pubblico esterni per importare in modo programmatico i tipi di pubblico generati esternamente in Adobe Experience Platform. Per ulteriori informazioni, consulta la [guida agli endpoint dei tipi di pubblico esterni](../../segmentation/api/external-audiences.md). |

Per ulteriori informazioni sulla segmentazione, consulta la [panoramica del Servizio di segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove origini**

| Origine | Descrizione |
| --- | --- |
| Supporto [!BADGE Beta]{type=Informative} per [!DNL Didomi] (SDK per lo streaming) | Utilizza l’origine [!DNL Didomi] per acquisire i dati di gestione del consenso e delle preferenze da [!DNL Didomi], supportando la conformità alle normative sulla privacy e alle strategie di marketing basate sul consenso. Per informazioni su come iniziare, consulta la [[!DNL Didomi] panoramica sull’origine](../../sources/connectors/consent-and-preferences/didomi.md). Per i passaggi relativi alla creazione di una connessione di origine, consulta la [[!DNL Didomi] guida alla connessione di origine](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md). |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per la modifica acquisizione dati in origini selezionate tramite l’API [!DNL Flow Service] | Ora è possibile creare flussi di dati che abilitano la modifica acquisizione dati per l’acquisizione incrementale utilizzando i connettori di origine. Questa funzionalità consente alla clientela di inserire il tipo di dati di modifica per l’acquisizione incrementale, migliorando l’aggiornamento dei dati e riducendo il sovraccarico di elaborazione. Per ulteriori informazioni, consulta la documentazione sull’[utilizzo dell’acquisizione dati di modifica per le origini](../../sources/tutorials/api/change-data-capture.md) |
| Supporto per l’eliminazione temporanea di record in [!DNL Salesforce] | L’origine [!DNL Salesforce] ora supporta l’inclusione di record eliminati temporaneamente tramite un parametro `includeDeletedObjects` facoltativo. Se impostato su true, la clientela può includere i record eliminati temporaneamente nelle rispettive query [!DNL Salesforce] e inserirli in Experience Platform. Per ulteriori informazioni, consulta la [[!DNL Salesforce] documentazione sulle origini.](../../sources/connectors/crm/salesforce.md) |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).
