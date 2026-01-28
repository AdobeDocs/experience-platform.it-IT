---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2026
description: Note sulla versione di Adobe Experience Platform di gennaio 2026.
source-git-commit: 54be4d5c309f60e6c3e2a96ab1fea700cc79a608
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 22%

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

**Data di rilascio: mercoledì 27 gennaio 2026**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

<!-- - [Agent Orchestrator](#agent-orchestrator) -->

- [Destinazioni](#destinations)
- [Profilo cliente in tempo reale](#real-time-customer-profile)
- [Schemi](#schemas)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

<!-- ## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator enables you to build and deploy AI-powered agents that can automate workflows and interact with customers across multiple channels.

**New or updated features**

| Feature | Description |
| --- | --- |
| Trial motion for Adobe Experience Platform Agents | **Select customers now have access to Adobe Experience Platform Agents for a complimentary trial**, enabling them to explore and interact with these Agents through the AI Assistant interface powered by Adobe Experience Platform Agent Orchestrator. The trial offers hands-on experience with AI Agents that operate within the context of customers' existing Experience Cloud products and environments, allowing teams to evaluate value before committing to a full purchase. Adobe Experience Platform Agents are guided by user input and oversight and respect existing product-level access controls, ensuring users can only perform actions or view data for which they are authorized within the underlying Experience Cloud applications.|

{style="table-layout:auto"}

For more information, see the [Agent Orchestrator documentation](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). -->

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Connettore [destinazione Kevel](/help/destinations/catalog/advertising/kevel.md) ora disponibile | La destinazione di streaming [!DNL Kevel] per Adobe Experience Platform consente ai clienti di attivare i tipi di pubblico di Adobe direttamente nelle API UserDB e Segment Management di [!DNL Kevel] per supportare il targeting in tempo reale al momento della decisione dell&#39;annuncio. [[!DNL Kevel]](https://www.kevel.com/) fornisce la tecnologia basata sull&#39;intelligenza artificiale e la guida di esperti che aiutano i leader di settore innovativi a lanciare, scalare e avere successo nel settore dei media retail. Retail Media Cloud di [!DNL Kevel] offre formati di annunci mirati, attribuibili e personalizzabili per la pubblicità nel sito e fuori dal sito. |
| [Connettore di destinazione di Exchange indice](/help/destinations/catalog/advertising/index-exchange.md) ora disponibile | Utilizza questo connettore di destinazione per esportare segmenti di pubblico da Adobe Experience Platform direttamente nella piattaforma di pubblicità programmatica di [!DNL Index Exchange]. [!DNL Index] è una piattaforma pubblicitaria globale lato offerta che consente ai proprietari di contenuti multimediali di massimizzare il valore dei contenuti su ogni schermo. Con oltre 20 anni di leadership nel settore, [!DNL Index] mette in contatto i marchi più grandi del mondo con i più importanti produttori di esperienze per offrire esperienze consumer di alta qualità. |
| Supporto di endpoint regionali per connessioni Braze | Tutti gli [endpoint specifici per area geografica](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) supportati da [!DNL Braze] sono ora disponibili per la selezione durante il flusso di configurazione di destinazione. Chiedi al tuo rappresentante [!DNL Braze] quale istanza endpoint utilizzare. |
| Supporto per la pianificazione settimanale e mensile per [onboarding Liveramp](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | Ora puoi configurare le pianificazioni di esportazione settimanali e mensili per la destinazione di onboarding Liveramp. <br> Questa versione verrà implementata gradualmente e verrà completata entro il 30 gennaio. |
| Esperienza di attivazione migliorata per [le destinazioni Trade Desk](../../destinations/catalog/advertising/tradedesk.md) e [Microsoft Bing](../../destinations/catalog/advertising/bing.md) | Le destinazioni Trade Desk e Microsoft Bing ora includono mappature obbligatorie predefinite per un’esperienza di attivazione ottimizzata.  <br> Questa versione verrà implementata gradualmente e verrà completata entro il 30 gennaio. |
| Supporto della crittografia AES256 per [destinazioni Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) | Ora puoi configurare la crittografia AES256 per le esportazioni Amazon S3. Sono disponibili due opzioni: <ul><li>**[!UICONTROL Default]**: se non hai criteri personalizzati applicati ai bucket, i dati verranno crittografati quando arriveranno in S3 con l&#39;algoritmo AES256. Tuttavia, se hai applicato criteri personalizzati, Experience Platform li rispetterà e Amazon S3 continuerà ad applicare qualsiasi criterio di crittografia personalizzato configurato.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform aggiunge l&#39;intestazione `s3:x-amz-server-side-encryption": "AES256` nell&#39;esportazione e i dati verranno crittografati quando arriveranno in S3 con l&#39;algoritmo AES256.</li></ul>  <br> Questa versione verrà implementata gradualmente e verrà completata entro il 30 gennaio. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Limiti di guardrail aggiornati per [destinazioni Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Il numero massimo di tipi di pubblico che è possibile mappare su una singola destinazione di Adobe Target è stato aumentato da 50 a 250. Questo allinea Adobe Target al limite di pubblico standard per altre destinazioni, fornendo maggiore flessibilità per i flussi di lavoro di attivazione del pubblico. Ora puoi attivare più tipi di pubblico nelle destinazioni di Adobe Target senza dover creare più flussi di dati. |
| [Modifica destinazioni](/help/destinations/ui/edit-destination.md) e [modifica azioni di marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) disponibilità generale | L’opzione per modificare le destinazioni e le azioni di marketing è ora disponibile per tutti gli utenti. |
| Attiva/disattiva i nomi visualizzati dei campi nel [passaggio](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) di mappatura | Quando mappi i campi dello schema su una destinazione, ora puoi alternare tra la visualizzazione del nome completo del campo XDM e la visualizzazione del solo nome visualizzato. <br> ![Registrazione dello schermo con il nome visualizzato attivato.](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Profilo cliente in tempo reale {#real-time-customer-profile}

Real-Time Customer Profile consente di visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Applicazione della capacità di streaming](/help/landing/license-usage-and-guardrails/capacity.md) | Experience Platform ora applica capacità di throughput in streaming per Real-Time Customer Profile e Identity Service. Quando i clienti superano la capacità di streaming contrattuale, i dati vengono messi in coda ed elaborati in modalità first in first out. In questo modo è possibile garantire prestazioni di sistema prevedibili e impedire che le violazioni della capacità influiscano sulla qualità dell’acquisizione dei dati. Note importanti: <ul><li>Gli upsert di streaming non saranno disponibili nel data lake quando viene superata la capacità</li><li>Questa implementazione non si applica ai clienti con licenze Adobe Journey Optimizer</li><li>I dati in coda verranno elaborati in sequenza una volta che la capacità sarà disponibile.</li></ul> Per ulteriori informazioni, leggere la [panoramica della capacità](/help/landing/license-usage-and-guardrails/capacity.md). |
| Ricerca entità obsoleta | L’utilizzo dell’API di ricerca delle entità per gli eventi esperienza è ora obsoleto per tutti i clienti Real-Time CDP Prime. Questa impostazione deprecata consente di allineare Real-Time CDP alle funzionalità di gestione delle licenze. I clienti Real-Time CDP Ultimate che intendono utilizzare questa funzionalità possono contattare l’Assistenza clienti Adobe per riattivarla.  Per ulteriori informazioni, consulta la [guida delle entità API](/help/profile/api/entities.md). |
| Monitorare lo stato del processo di acquisizione del profilo | Ora puoi monitorare la percentuale di avanzamento a livello di processo per il flusso di dati di acquisizione profilo in batch. Questa funzione fornisce visibilità in tempo reale sull’avanzamento corrente dei processi di acquisizione batch, inclusi i punti di controllo critici che indicano se l’acquisizione è pronta per la segmentazione dei clienti e le ricerche Adobe Journey Optimizer. Per le acquisizioni di grandi dimensioni che possono richiedere diverse ore, questa trasparenza dell&#39;avanzamento consente di capire se il processo procede normalmente o incontra problemi, riducendo l&#39;incertezza durante l&#39;elaborazione dei dati.Per ulteriori informazioni, leggere la [guida dei profili di monitoraggio](/help/dataflows/ui/monitor-profiles.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [[!DNL Real-Time Customer Profile] panoramica](../../profile/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Aggiornamento della scadenza dei dati del pubblico esterno | I tipi di pubblico esterni (come i caricamenti CSV) ora supportano la funzionalità di aggiornamento forzato per le impostazioni di scadenza dei dati. Questa funzione consente agli utenti di aggiornare manualmente la scadenza dei dati per i tipi di pubblico esterni, fornendo un maggiore controllo sulla gestione del ciclo di vita del pubblico. Ciò è particolarmente utile per i tipi di pubblico che devono persistere oltre il periodo di scadenza iniziale dei dati o richiedere una riattivazione senza ricaricare i dati. Per ulteriori informazioni su questa funzione, leggere la [Panoramica di Audience Portal](../../segmentation/ui/audience-portal.md#audience-summary). |

Per ulteriori informazioni, consulta la [[!DNL Segmentation Service] panoramica](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| Origine [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2 | È ora disponibile un nuovo connettore di origine [!DNL Oracle Eloqua], che sostituisce il [connettore obsoleto](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Questo connettore aggiornato offre funzionalità avanzate e maggiore affidabilità per l&#39;acquisizione di dati da [!DNL Oracle Eloqua] in Experience Platform. I clienti che utilizzano il connettore esistente devono effettuare la migrazione alla nuova implementazione, in quanto le connessioni esistenti non funzioneranno più. Il nuovo connettore supporta tutti i passaggi di configurazione e configurazione necessari per connettersi a [!DNL Oracle Eloqua] e acquisire i dati di automazione marketing. |
| Origine [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2 | È ora disponibile un nuovo connettore di origine [!DNL Salesforce Marketing Cloud], che sostituisce il [connettore obsoleto](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Questo connettore aggiornato offre prestazioni migliorate e funzionalità aggiuntive per l&#39;acquisizione di dati da [!DNL Salesforce Marketing Cloud] in Experience Platform. I clienti che utilizzano il connettore esistente devono passare alla nuova implementazione. Il nuovo connettore include istruzioni di configurazione complete per la connessione a [!DNL Salesforce Marketing Cloud] e l&#39;acquisizione dei dati di automazione marketing. |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

