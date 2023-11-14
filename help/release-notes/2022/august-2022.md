---
title: Note sulla versione di Adobe Experience Platform - Agosto 2022
description: Note sulla versione di agosto 2022 per Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: 7f5a1d8e50ff030b2abe04b5155f28b8c8b6fbf9
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 27%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 24 agosto 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Profilo cliente in tempo reale](#profile)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

I servizi di intelligenza artificiale e machine learning consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi di utilizzo dell’esperienza del cliente. Questo consente agli analisti di marketing di impostare modelli specifici per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science.

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzata dai marketer per quantificare l’impatto di ogni punto di contatto di marketing lungo i percorsi della clientela.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per la privacy | <ul><li> Attribution AI ora supporta la definizione dei ruoli utente e dei criteri di accesso da gestire [autorizzazioni](../../../help/access-control/abac/ui/permissions.md) per funzioni e oggetti all’interno di un’applicazione di prodotto. </li><li>Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività.</li><li> Da a [controllo degli accessi basato su attributi](../../access-control/abac/overview.md), gli amministratori possono controllare l&#39;accesso a oggetti e/o funzionalità specifici in base a determinati attributi, che possono essere metadati aggiunti a un oggetto, ad esempio le etichette.Gli amministratori possono inoltre definire ruoli utente che hanno accesso solo a campi e dati specifici che corrispondono a tali campi.</li><li>Attribution AI sfrutta i set di dati di Platform. Per supportare le richieste di diritti dei consumatori che un brand può ricevere, i brand devono utilizzare Platform Privacy Service per inviare ai consumatori le richieste di accesso e cancellazione per rimuovere i propri dati attraverso il data lake, il servizio Identity e il profilo cliente in tempo reale.  </li><li>Tutti i set di dati utilizzati per l’input/output dei modelli seguiranno le linee guida di Platform. Platform Data Encryption si applica ai dati in transito e a riposo. Per ulteriori informazioni, consulta la documentazione di [crittografia dei dati](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**Nota**: l’Attribution AI non sarà disponibile con i clienti esistenti di Healthcare Shield fino a nuovo avviso.

Per ulteriori informazioni sull&#39;Attribution AI, vedere [Attribution AI](../../intelligent-services/attribution-ai/overview.md) panoramica.

### IA per l’analisi dei clienti

IA per l’analisi dei clienti disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su larga scala.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per la privacy | <ul><li> IA per l’analisi dei clienti ora supporta la definizione dei ruoli utente e dei criteri di accesso da gestire [autorizzazioni](../../../help/access-control/abac/ui/permissions.md) per funzioni e oggetti all’interno di un’applicazione di prodotto. </li><li>Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività.</li><li> Da a [controllo degli accessi basato su attributi](../../access-control/abac/overview.md), gli amministratori possono controllare l’accesso a oggetti e/o funzionalità specifici in base a determinati attributi. Questi attributi possono essere metadati aggiunti a un oggetto, ad esempio le etichette. Gli amministratori possono inoltre definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.</li><li>IA per l’analisi dei clienti sfrutta i set di dati di Platform. Per supportare le richieste di diritti dei consumatori che un brand può ricevere, i brand devono utilizzare Platform Privacy Service per inviare ai consumatori le richieste di accesso e cancellazione per rimuovere i propri dati attraverso il data lake, il servizio Identity e il profilo cliente in tempo reale. </li><li>Tutti i set di dati utilizzati per l’input/output dei modelli seguiranno le linee guida di Platform. Platform Data Encryption si applica ai dati in transito e a riposo. Per ulteriori informazioni, consulta la documentazione di [crittografia dei dati](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**Nota**: IA per l’analisi dei clienti non sarà disponibile con i clienti esistenti di Healthcare Shield fino a nuovo avviso.

Per ulteriori informazioni su Customer AI, consulta la sezione [IA per l’analisi dei clienti](../../intelligent-services/customer-ai/overview.md) panoramica.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform offre più [!DNL dashboards] attraverso cui è possibile visualizzare informazioni importanti sui dati dell&#39;organizzazione, acquisite durante le istantanee giornaliere.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget attivazioni pianificate | Il [!UICONTROL Attivazioni pianificate] Il widget fornisce una vista in forma di tabella delle destinazioni attivate più di recente. Per ogni segmento, include il nome, la piattaforma di destinazione e la data di inizio e di fine dell’attivazione. Questo widget consente di scoprire subito dove e quando il pubblico viene attivato e rende più trasparenti le attivazioni duplicate o non necessarie. Queste informazioni accumulate evidenziano anche dove sono state escluse eventuali attivazioni. |

Per ulteriori informazioni su [!DNL Dashboards], consultare il [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’acquisizione di record con avvisi | La preparazione dati localizza ora gli avvisi (errori non critici) nei campi e consente di acquisire il resto della riga. Tutti gli errori di trasformazione dei mapper ora vengono segnalati come avvisi e le righe parzialmente acquisite vengono considerate riuscite, con un avviso.  Il monitoraggio è supportato anche nei record con avvertenze e dettagli di diagnostica. L’acquisizione parziale di record con avvertenze è attualmente disponibile solo per i dati in streaming. Consulta la documentazione su [acquisizione di record con avvisi](../../sources/tutorials/ui/monitor-streaming.md) per ulteriori informazioni. |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Data Prep], vedere [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| (Beta) Supporto della personalizzazione basata su attributi per le destinazioni di personalizzazione | Con la versione beta della personalizzazione basata su attributi, vedrai due nuove schede in [catalogo di destinazione](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**: questo connettore è attualmente in versione beta e disponibile solo per un determinato numero di clienti. Oltre alle funzionalità fornite dalla scheda Adobe Target V1, il connettore Target V2 aggiunge una [passaggio di mappatura](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) al flusso di lavoro di attivazione, che consente di mappare gli attributi del profilo ad Adobe Target, abilitando la personalizzazione della stessa pagina e della pagina successiva basata su attributi.</li><li>**[!UICONTROL Personalizzazione Personalizzata Con Attributi]**: questo connettore è attualmente in versione beta e disponibile solo per un determinato numero di clienti. Oltre alle funzionalità fornite dal **[!UICONTROL Personalizzazione personalizzata]**, il **[!UICONTROL Personalizzazione Personalizzata Con Attributi]** il connettore aggiunge un [passaggio di mappatura](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes) al flusso di lavoro di attivazione, che consente di mappare gli attributi del profilo alla destinazione di personalizzazione personalizzata, abilitando la personalizzazione della stessa pagina e della pagina successiva basata su attributi.</li></ul> <br> Gli attributi del profilo possono contenere dati sensibili. Per proteggere questi dati, è necessario **[!UICONTROL Personalizzazione Personalizzata Con Attributi]** La destinazione richiede l&#39;utilizzo di [API server di rete Edge](../../server-api/overview.md) per la raccolta di dati. Inoltre, tutte le chiamate API server devono essere effettuate in un [contesto autenticato](../../server-api/authentication.md). |

{style="table-layout:auto"}

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) è una piattaforma di esecuzione delle vendite con i dati di interazione tra acquirenti e venditori B2B più diffusi al mondo e investimenti significativi in tecnologie di intelligenza artificiale proprietarie per tradurre i dati di vendita in informazioni. [!DNL Outreach] consente alle organizzazioni di automatizzare il coinvolgimento nelle vendite e di agire sulla base delle informazioni sui ricavi per migliorare l&#39;efficienza, la prevedibilità e la crescita. |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Classe entità AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Classe basata su record per la creazione di schemi di ricerca per Adobe Journey Optimizer. |
| Gruppo di campi | [[!UICONTROL Oggetti di lavoro Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Un gruppo di campi wrapper che fa riferimento a tutti i gruppi di campi specifici dell’oggetto di livello inferiore per Adobe Workfront. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Campi comuni evento passaggio Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Sono state aggiunte due nuove proprietà: `origTimeStamp` e `experienceID`. |
| Gruppo di campi | [[!UICONTROL Dettagli sull’appartenenza a segmento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Oltre a [!UICONTROL Profilo individuale XDM], questo gruppo di campi ora può essere utilizzato anche in schemi basati sulla classe XDM Business Account. |
| Gruppo di campi | (Multiplo) | Diversi gruppi di campi relativi alle attività B2B di Marketo sono stati aggiornati a uno stato stabile. Vedi quanto segue [richiesta pull](https://github.com/adobe/xdm/pull/1593/files) per i dettagli. |
| Gruppo di campi | (Multiplo) | Diversi gruppi di campi correlati al meteo sono stati aggiornati per correggere gli errori che si verificavano per `uvIndex` e `sunsetTime`. Vedi quanto segue [richiesta pull](https://github.com/adobe/xdm/pull/1602/files) per i dettagli. |
| Tipo di dati | [[!UICONTROL Elemento dell’elenco prodotti]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Una nuova proprietà `productImageUrl` è stato aggiunto. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dei dati QoE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Una nuova proprietà `framesPerSecond` è stato aggiunto. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` è stato rinominato come `appVersion`. `meta:enum` e `description` Anche i campi di sono stati aggiornati. |
| Tipi di dati e gruppi di campi | (Multiplo) | Diversi tipi di dati multimediali e gruppi di campi dispongono di nuovi campi e descrizioni aggiornate. Vedi quanto segue [richiesta pull](https://github.com/adobe/xdm/pull/1582/files) per i dettagli. |
| (Tutto) | (Multiplo) | Tutti gli oggetti dello schema che contengono un `enum` ora contiene anche un valore corrispondente `meta:enum` per indicare i valori visualizzati per ciascun vincolo. Vedi quanto segue [richiesta pull](https://github.com/adobe/xdm/pull/1601/files) per i dettagli. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [Panoramica sul sistema XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Limite rigido dei criteri di unione | Platform ora applica un limite massimo di **cinque** criteri di unione per sandbox. Se la sandbox dispone attualmente di più di cinque criteri di unione, **non** essere in grado di creare nuovi criteri di unione fino a quando la sandbox non avrà meno di cinque criteri di unione. |
| Pulizia attributi edge profilo orfano | Per tutte le organizzazioni, il servizio Profilo ora rimuove gli attributi edge rimanenti dell’area di attività dell’utente su base giornaliera per fornire una rappresentazione più accurata dei profili nel sistema. Questa pulizia si verifica dopo che tutti i frammenti di profilo per un determinato profilo sono stati eliminati e dovrebbe interessare i profili uniti da set di dati in cui `com_adobe_aep_profile_region_dataset` è contrassegnato come `true`. Questo potrebbe mostrare un calo della metrica &quot;Pubblico indirizzabile&quot; nel dashboard di utilizzo della licenza e un calo della metrica &quot;Conteggio profili&quot; nel dashboard Profilo, poiché queste metriche includevano frammenti di attributi edge rimasti prima di questa versione. |

{style="table-layout:auto"}

Per ulteriori informazioni sul Profilo cliente in tempo reale, inclusi tutorial e best practice per l’utilizzo dei dati del profilo, inizia consultando la [Panoramica sul Profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per 4000 segmenti | Tutte le organizzazioni con Platform possono ora supportare fino a 4000 definizioni di segmenti. Per ulteriori informazioni su come questa modifica influisce sulle API dei processi di segmentazione, leggi [guida dell’endpoint del processo di segmento](../../segmentation/api/segment-jobs.md) |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale di origini self-service (SDK batch) | Sviluppa, testa e integra l’origine dati REST basata su API per acquisire i dati batch in Experienci Platform utilizzando specifiche di origine facili da configurare. Con l’SDK Sources puoi: <ul><li>Configura una nuova origine nel catalogo Experienci Platform.</li><li>Definisci le specifiche per l’origine, incluse le informazioni relative ai tipi di autenticazione supportati, alla pianificazione e al modo in cui vengono recuperati i dati delle risorse.</li><li>Crea una documentazione rivolta all’utente per la nuova sorgente.</li></ul> Per ulteriori informazioni, consulta la documentazione su [Origini self-service (SDK batch)](../../sources/sources-sdk/overview.md). |
| Disponibilità generale di [!DNL Google BigQuery] sorgente | Utilizza il [!DNL Google BigQuery] origine per acquisire dati dal [!DNL Google BigQuery] data warehouse da Experience Platform. Per ulteriori informazioni, consulta la documentazione sul [[!DNL Google BigQuery] sorgente](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] sorgente (Beta) | Utilizza il [!DNL Teradata Vantage] origine per acquisire i dati da ambienti ibridi multi-cloud ad Experienci Platform. Per ulteriori informazioni, consulta la documentazione sul [[!DNL Teradata Vantage] sorgente](../../sources/connectors/databases/teradata-vantage.md). |
| Supporto per aree geografiche diverse per origine Adobe Analytics | È ora possibile acquisire suite di rapporti da qualsiasi area geografica (Stati Uniti, Regno Unito o Singapore). Le suite di rapporti devono essere mappate sulla stessa organizzazione dell’istanza Sandbox di Experience Platform in cui viene creata la connessione di origine. Per ulteriori informazioni, consulta la guida su [creazione di una connessione sorgente Adobe Analytics nell’interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
