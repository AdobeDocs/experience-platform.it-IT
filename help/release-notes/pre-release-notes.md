---
title: Note pre-release di Experience Platform
description: Un’anteprima delle ultime note sulla versione di Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: d401707e263f09ccd8575f02a71d7e74899e02db
workflow-type: tm+mt
source-wordcount: '1395'
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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: gennaio 2026**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Destinazioni](#destinations)
- [Profilo cliente in tempo reale](#real-time-customer-profile)
- [Schemi](#schemas)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator consente di creare e distribuire agenti basati sull’intelligenza artificiale in grado di automatizzare i flussi di lavoro e interagire con i clienti su più canali.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Movimento di prova per Agent Orchestrator | Agent Orchestrator offre ora una mozione di prova che consente ai clienti di esplorare e testare il servizio prima di effettuare un acquisto completo. Questa opzione &quot;try-before-you-buy&quot; consente alle organizzazioni di valutare le funzionalità di Agent Orchestrator, incluse le competenze e le funzioni di orchestrazione, nel proprio ambiente. La versione di prova offre un’esperienza pratica nella creazione di agenti basati sull’intelligenza artificiale e nella comprensione di come possono essere integrati nei flussi di lavoro esistenti. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [documentazione di Agent Orchestrator](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Connettore di destinazione Kevel ora disponibile | [[!DNL Kevel]](https://www.kevel.com/) fornisce la tecnologia basata sull&#39;intelligenza artificiale e la guida di esperti che aiutano i leader di settore innovativi a lanciare, scalare e avere successo nel settore dei media retail. Retail Media Cloud di [!DNL Kevel] offre formati di annunci mirati, attribuibili e personalizzabili per la pubblicità nel sito e fuori dal sito. |
| Connettore di destinazione per Exchange indice ora disponibile | [!DNL Index] è una piattaforma pubblicitaria globale lato offerta che consente ai proprietari di contenuti multimediali di massimizzare il valore dei contenuti su ogni schermo. Con oltre 20 anni di leadership nel settore, [!DNL Index] mette in contatto i marchi più grandi del mondo con i più importanti produttori di esperienze per offrire esperienze consumer di alta qualità. |
| Supporto di endpoint regionali per connessioni Braze | Tutti gli [endpoint specifici per area geografica](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) supportati da [!DNL Braze] sono ora disponibili per la selezione durante il flusso di configurazione di destinazione. Chiedi al tuo rappresentante [!DNL Braze] quale istanza endpoint utilizzare. |
| Supporto di pianificazione settimanale e mensile per l’onboarding di Liveramp | Ora puoi configurare le pianificazioni di esportazione settimanali e mensili per la destinazione di onboarding Liveramp. |
| Supporto della crittografia AES256 per le destinazioni Amazon S3 | Ora puoi configurare la crittografia AES256 per le esportazioni Amazon S3. |
| Esperienza di attivazione migliorata per le destinazioni Trade Desk e Microsoft Bing | Le destinazioni Trade Desk e Microsoft Bing ora includono mappature obbligatorie predefinite per un’esperienza di attivazione ottimizzata. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Limiti di guardrail aggiornati per la destinazione Adobe Target | Il numero massimo di tipi di pubblico che è possibile mappare su una singola destinazione di Adobe Target è stato aumentato da 50 a 250. Questo allinea Adobe Target al limite di pubblico standard per altre destinazioni, fornendo maggiore flessibilità per i flussi di lavoro di attivazione del pubblico. Ora puoi attivare più tipi di pubblico nelle destinazioni di Adobe Target senza dover creare più flussi di dati. |
| [Modifica destinazioni](/help/destinations/ui/edit-destination.md) e [modifica azioni di marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) disponibilità generale | L’opzione per modificare le destinazioni e le azioni di marketing è ora disponibile per tutti gli utenti. |
| Attiva o disattiva i nomi visualizzati dei campi nel passaggio di mappatura | Quando mappi i campi dello schema su una destinazione, ora puoi alternare tra la visualizzazione del nome completo del campo XDM e la visualizzazione del solo nome visualizzato. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../destinations/home.md).

## Profilo cliente in tempo reale {#real-time-customer-profile}

Real-Time Customer Profile consente di visualizzare una visualizzazione olistica di ogni singolo cliente combinando dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Applicazione della capacità di streaming | Experience Platform ora applica capacità di throughput in streaming per Real-Time Customer Profile e Identity Service. Quando i clienti superano la capacità di streaming contrattuale, i dati vengono messi in coda ed elaborati in modalità first in first out. In questo modo è possibile garantire prestazioni di sistema prevedibili e impedire che le violazioni della capacità influiscano sulla qualità dell’acquisizione dei dati. Note importanti: gli upsert di streaming non saranno disponibili sul data lake quando viene superata la capacità. Questa implementazione non si applica ai clienti con licenze Adobe Journey Optimizer e i dati in coda verranno elaborati in sequenza una volta che la capacità diventa disponibile. |
| Accesso API obsoleto per Real-Time CDP Prime | L’accesso API per gli eventi esperienza è ora obsoleto per tutti i clienti Real-Time CDP Prime. Questa modifica influisce sulla possibilità di eseguire query sugli eventi esperienza direttamente tramite API. I clienti di Real-Time CDP Ultimate possono richiedere un’eccezione tramite un processo di eccezione formale per abilitare l’accesso API agli eventi di esperienza, se necessario per i loro casi d’uso. Questa funzione consente di ottimizzare le prestazioni del sistema e di allinearsi alle best practice per i modelli di accesso ai dati. |
| Monitorare l’esecuzione del flusso di dati | Ora puoi monitorare l’avanzamento e la preparazione del flusso di dati eseguito in Profilo. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [[!DNL Real-Time Customer Profile] panoramica](../profile/home.md).

## Schemi {#schemas}

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e quindi ottenere valore dai dati. Gli schemi sono composti da una classe base e da zero o più gruppi di campi schema.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Modernizzazione dell’inventario degli schemi con ricerca, filtro, tag e cartelle | La pagina di navigazione dello schema è stata modernizzata per fornire funzionalità organizzative e di individuazione avanzate. Le nuove funzioni includono opzioni avanzate di ricerca e filtro, supporto di tag e cartelle generati dall’utente per organizzare gli schemi e azioni in linea per semplificare i flussi di lavoro. I miglioramenti principali includono: colonne aggiornate (Nome, Classe, Set di dati, Identità, Relazioni, Abilita per profilo, Comportamento, Tipo di schema, Tag, Data di creazione, Ultima modifica), filtri avanzati (Mostra profili, Tipo di schema, Classe, Ha qualsiasi tag, Creato da, Data di creazione, Data di modifica, Ha identità primaria, Ha relazione, Spazio dei nomi dell’identità primaria), azioni in linea (Modifica, Elimina, Applica etichette, Crea set di dati per schemi non relazionali, Gestisci tag, Sposta in cartella, Aggiungi a pacchetto, Copia struttura JSON, Scarica file di esempio) e la possibilità di organizzare gli schemi utilizzando tag e cartelle. Questi miglioramenti forniscono una visibilità completa delle risorse dello schema e consentono una gestione più efficiente dello schema a livello di sandbox. |

Per ulteriori informazioni, consulta la [[!DNL Schemas] panoramica](../xdm/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Monitoraggio della segmentazione in streaming | Il monitoraggio in tempo reale per la segmentazione in streaming fornisce trasparenza in termini di tasso di valutazione, latenza e metriche di qualità dei dati a livello di sandbox, set di dati e pubblico. In questo modo è possibile inviare avvisi proattivi e ottenere informazioni utili per aiutare i data engineer a identificare le violazioni della capacità e i problemi di acquisizione. Le metriche di monitoraggio includono il tasso di valutazione, la latenza di acquisizione P95, nonché i record ricevuti, valutati, non riusciti e saltati. Le funzionalità View-by-DataSet e View-by-Audience forniscono una visibilità completa sui nuovi profili qualificati e non qualificati. |
| Aggiornamento TTL per pubblico esterno | I tipi di pubblico esterni (come i caricamenti CSV) ora supportano la funzionalità di aggiornamento forzato per le impostazioni Time-to-Live (TTL). Questa funzione consente agli utenti di aggiornare manualmente la scadenza TTL per i tipi di pubblico esterni, fornendo un maggiore controllo sulla gestione del ciclo di vita dei tipi di pubblico. Ciò è particolarmente utile per i tipi di pubblico che devono persistere oltre il periodo TTL iniziale o richiedere una riattivazione senza ricaricare i dati. |

Per ulteriori informazioni, consulta la [[!DNL Segmentation Service] panoramica](../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| Origine [!DNL Oracle Eloqua] V2 | È ora disponibile un nuovo connettore di origine [!DNL Oracle Eloqua] che sostituisce il connettore obsoleto. Questo connettore aggiornato offre funzionalità avanzate e maggiore affidabilità per l&#39;acquisizione di dati da [!DNL Oracle Eloqua] in Experience Platform. I clienti che utilizzano il connettore esistente devono effettuare la migrazione alla nuova implementazione, in quanto le connessioni esistenti non funzioneranno più. Il nuovo connettore supporta tutti i passaggi di configurazione e configurazione necessari per connettersi a [!DNL Oracle Eloqua] e acquisire i dati di automazione marketing. |
| Origine [!DNL Salesforce Marketing Cloud] V2 | È ora disponibile un nuovo connettore di origine [!DNL Salesforce Marketing Cloud] che sostituisce il connettore obsoleto. Questo connettore aggiornato offre prestazioni migliorate e funzionalità aggiuntive per l&#39;acquisizione di dati da [!DNL Salesforce Marketing Cloud] in Experience Platform. I clienti che utilizzano il connettore esistente devono passare alla nuova implementazione. Il nuovo connettore include istruzioni di configurazione complete per la connessione a [!DNL Salesforce Marketing Cloud] e l&#39;acquisizione dei dati di automazione marketing. |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../sources/home.md).

