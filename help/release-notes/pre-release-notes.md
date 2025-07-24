---
title: Note pre-release di Experience Platform
description: Un’anteprima delle ultime note sulla versione di Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 7e91181f71b84fdaf04a39e003cbbd415827e282
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 22%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: mercoledì 29 luglio 2025**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Destinazioni](#destinations)
- [Acquisizione dei dati](#ingestion)
- [Query Service](#query-service)
- [Edizione B2B di Real-Time CDP](#b2b)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Consolidamento delle schede di destinazione Marketo | Le schede di destinazione Marketo V2 e Marketo Engage Person Sync sono state consolidate in un’unica scheda di destinazione unificata. Questo consolidamento semplifica il processo di selezione della destinazione e offre un’esperienza più semplice per le integrazioni Marketo. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Informazioni sullo stream di dati migliorate per le destinazioni edge | Le informazioni migliorate nella barra a destra per le destinazioni Adobe Target e Custom Personalization ora visualizzano il nome dello stream di dati, fornendo una visibilità più chiara nelle configurazioni dello stream di dati associato e riducendo la confusione durante l’esame dei flussi di dati esistenti. Il selettore **[!UICONTROL ID Datastream]** nella schermata di configurazione di destinazione è stato aggiornato a **[!UICONTROL Datastream]** per una maggiore chiarezza nell&#39;interfaccia utente. |
| Visibilità delle azioni di marketing nella selezione della destinazione | Le azioni di marketing vengono ora visualizzate nella barra a destra della scheda **[!UICONTROL Sfoglia]** di destinazione e nella pagina **[!UICONTROL Il flusso di dati viene eseguito]**, fornendo una visibilità immediata delle modifiche apportate alle azioni di marketing senza dover passare alla pagina di visualizzazione. Questo miglioramento migliora l’esperienza utente rendendo più semplice verificare le configurazioni delle azioni di marketing durante la configurazione della destinazione. |
| (Versione beta limitata) Modifica le azioni di marketing per le destinazioni | Ora puoi modificare le azioni di marketing per le destinazioni esistenti. Questa funzionalità è in versione beta limitata. Per richiedere l’accesso, contatta il rappresentante Adobe. |
| (Versione beta limitata) Modifica destinazioni | Ora puoi modificare la configurazione di destinazione dopo averla creata. Questa funzionalità è in versione beta limitata. Per richiedere l’accesso, contatta il rappresentante Adobe. |
| Nomi account e descrizioni per le connessioni di destinazione | È ora possibile aggiungere nomi e descrizioni di account durante la connessione alle destinazioni, consentendo una migliore gestione delle destinazioni con più account. |

**Correzioni**

| Problema | Descrizione |
| --- | --- |
| Funzionalità di scorrimento delle categorie | È stato risolto un problema che impediva lo scorrimento corretto del menu laterale delle categorie nel catalogo delle destinazioni e delle origini al passaggio del mouse, migliorando l’usabilità della navigazione per gli utenti che navigavano nelle categorie di destinazione. |

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../destinations/home.md).

## Acquisizione dei dati {#ingestion}

Experience Platform fornisce un framework completo per l’acquisizione dei dati che supporta l’acquisizione di dati in batch e in streaming da varie sorgenti.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per il monitoraggio dell’acquisizione del profilo di streaming | È ora disponibile il monitoraggio in tempo reale per l’acquisizione dei profili di streaming, che fornisce trasparenza in termini di velocità effettiva, latenza e metriche di qualità dei dati. In questo modo è possibile inviare avvisi proattivi e ottenere informazioni utili per aiutare i data engineer a identificare le violazioni della capacità e i problemi di acquisizione. |

Per ulteriori informazioni, consulta la [panoramica sull&#39;acquisizione dei dati](../ingestion/home.md).

## Query Service {#query-service}

Adobe Experience Platform Query Service fornisce una solida interfaccia SQL per l’analisi e l’esplorazione dei dati su tutta la piattaforma.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Gestione delle sessioni migliorata | Data Distiller ora include funzionalità avanzate di gestione delle sessioni, che forniscono un migliore controllo sulle sessioni degli utenti e un migliore monitoraggio delle prestazioni negli ambienti di sviluppo e produzione. |
| Supporto per le restrizioni di carattere per le password senza scadenza delle credenziali | Data Distiller ora supporta le credenziali senza scadenza con restrizioni specifiche per i caratteri. Sebbene le password richiedano almeno un numero, una lettera minuscola, una lettera maiuscola e un carattere speciale, il simbolo del dollaro ($) non è supportato. I caratteri speciali consigliati includono `!, @, #, ^, or &`. |
| Miglioramento della coerenza delle prestazioni negli ambienti | Le prestazioni di Data Distiller sono ora coerenti tra le sandbox di sviluppo e di produzione, con risorse di back-end simili disponibili in entrambi gli ambienti. Le ore di calcolo utilizzate possono variare in base al volume di dati e alle risorse di calcolo back-end disponibili al momento dell’elaborazione. |

Per ulteriori informazioni, leggere la [Panoramica di Query Service](../query-service/home.md).

## Edizione B2B di Real-Time CDP {#b2b}

Real-Time CDP B2B edition fornisce funzionalità complete di gestione dei dati dei clienti B2B, consentendo alle organizzazioni di creare profili cliente unificati, creare tipi di pubblico B2B sofisticati e attivare i dati su vari canali di marketing.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento dell’architettura B2B | Experience Platform sta effettuando l’aggiornamento a una nuova architettura B2B che introduce miglioramenti significativi per i tipi di pubblico multientità con attributi B2B. Questo aggiornamento consolida il supporto dei criteri di unione, migliora l’accuratezza del conteggio del pubblico e migliora le funzionalità di risoluzione delle entità. |
| Criterio di unione Consolidamento per più entità di pubblico | I tipi di pubblico con più entità con attributi B2B ora supportano un solo criterio di unione, ovvero il criterio di unione predefinito, anziché più criteri di unione. Questa modifica garantisce una composizione coerente del pubblico e semplifica la gestione della logica di unione. |
| Aggiornamenti ai vincoli di pubblico dell’account | I tipi di pubblico dell&#39;account non hanno più i vincoli precedenti di un intervallo di lookback di 30 giorni per gli eventi di esperienza, le restrizioni di entità personalizzate o le limitazioni sull&#39;utilizzo di `inSegment` eventi. Questi aggiornamenti forniscono maggiore flessibilità nella creazione di definizioni di pubblico B2B complesse. |
| Conteggi avanzati dei tipi di pubblico per le entità B2B | Le stime delle dimensioni del pubblico per i tipi di pubblico con entità B2B come Account e Opportunità sono ora esatte, in base ai risultati della segmentazione in tempo reale. Questo miglioramento fornisce stime più accurate e affidabili per i tipi di pubblico che coinvolgono relazioni B2B complesse. |
| Snapshot dell’account per l’iscrizione al pubblico | I dettagli di iscrizione al pubblico sono ora inclusi per le entità account nelle esportazioni di istantanee, consentendo l’accesso allo stato del pubblico a livello di account, alle marche temporali e agli indicatori di iscrizione. Questo porta alla parità delle funzioni tra i modelli di profilo (Persona) e segmentazione dell’account. |
| Modifiche agli strumenti della sandbox per tipi di pubblico con più entità | L’importazione di tipi di pubblico con più entità con entità B2B ed eventi di esperienza esportati prima della migrazione non è più supportata. Questi tipi di pubblico non supereranno la convalida di importazione e non potranno essere convertiti automaticamente nella nuova architettura. I tipi di pubblico devono essere riesportati dopo la migrazione prima di essere importati nelle sandbox di destinazione. |
| API dell’entità B2B obsolete | La creazione di tipi di pubblico tramite API per entità B2B (account, opportunità, relazione account-persona, relazione opportunità-persona, campagna, membro della campagna, elenco di marketing e membro dell’elenco di marketing) è ora obsoleta. Inoltre, anche le operazioni di ricerca ed eliminazione dell’API di accesso al profilo per queste entità B2B sono diventate obsolete. |
| Aggiornamenti allo spazio dei nomi delle identità per la risoluzione delle entità | Le entità account e opportunità ora utilizzano l&#39;unione basata sulla precedenza temporale con spazi dei nomi di identità specifici (`b2b_account` per l&#39;account, `b2b_opportunity` per l&#39;opportunità). Tutte le altre entità sono unificate con sovrapposizioni di identità primarie unite utilizzando l’unione basata sulla precedenza temporale. |

Per ulteriori informazioni, leggere la [panoramica di Real-Time CDP B2B edition](../rtcdp/b2b-overview.md).

## Sandbox {#sandboxes}

Experience Platform è stato sviluppato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere a sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Modifiche alle importazioni di tipi di pubblico con più entità | Gli strumenti sandbox sono stati aggiornati per supportare il nuovo aggiornamento dell’architettura B2B. I tipi di pubblico con più entità contenenti entità B2B ed eventi esperienza devono essere riesportati dopo l’aggiornamento dell’architettura prima di essere importati nelle sandbox di destinazione tramite gli strumenti sandbox. L’importazione delle versioni precedenti all’aggiornamento non riuscirà la convalida. |

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../sandboxes/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| API per pubblico esterno | Puoi utilizzare l’API dei tipi di pubblico esterni per importare in modo programmatico i tipi di pubblico generati esternamente in Adobe Experience Platform. |

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove origini**

| Origine | Descrizione |
| --- | --- |
| Supporto per [!DNL Didomi] (Streaming SDK) | Il connettore di origine [!DNL Didomi] consente di acquisire i dati di gestione del consenso dalla piattaforma di [!DNL Didomi], supportando la conformità alle normative sulla privacy e alle strategie di marketing basate sul consenso. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l&#39;acquisizione di dati di modifica in origini selezionate | Ora puoi creare flussi di dati che abilitano l’acquisizione di dati di modifica per l’acquisizione incrementale utilizzando i connettori di origine. Questa funzionalità consente ai clienti di inserire il tipo di dati Change per l’acquisizione incrementale, migliorando l’aggiornamento dei dati e riducendo il sovraccarico di elaborazione. |
| Supporto per l&#39;eliminazione temporanea di record in [!DNL Salesforce] | L&#39;origine [!DNL Salesforce] ora supporta l&#39;inclusione di record eliminati tramite un parametro `includeDeletedObjects` facoltativo. Se impostato su true, i clienti possono includere record eliminati soft nelle query [!DNL Salesforce] e inserire tali record in Experience Platform. |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../sources/home.md).
