---
title: Note sulla versione di Adobe Experience Platform - Agosto 2022
description: Note sulla versione di agosto 2022 per Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: 3069bdb3592ac1cd3fd7fe4f7f9234d5be56547d
workflow-type: tm+mt
source-wordcount: '1999'
ht-degree: 26%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 24 agosto 2022**

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
| Supporto per la privacy | <ul><li> Attribution AI ora supporta la definizione di ruoli utente e criteri di accesso per gestire [autorizzazioni](../../../help/access-control/abac/ui/permissions.md) per funzionalità e oggetti all&#39;interno di un&#39;applicazione di prodotto. </li><li>Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività.</li><li> Tramite il controllo dell&#39;accesso basato su [attributi](../../access-control/abac/overview.md), gli amministratori possono controllare l&#39;accesso a oggetti e/o funzionalità specifici in base a determinati attributi, che possono essere metadati aggiunti a un oggetto, ad esempio le etichette. Gli amministratori possono inoltre definire ruoli utente con accesso solo a campi e dati specifici corrispondenti a tali campi.</li><li>Attribution AI sfrutta i set di dati di Platform. Per supportare le richieste di diritti dei consumatori che un brand può ricevere, i brand devono utilizzare Platform Privacy Service per inviare ai consumatori le richieste di accesso e cancellazione per rimuovere i propri dati attraverso il data lake, il servizio Identity e il profilo cliente in tempo reale.  </li><li>Tutti i set di dati utilizzati per l’input/output dei modelli seguiranno le linee guida di Platform. Platform Data Encryption si applica ai dati in transito e a riposo. Per ulteriori informazioni sulla [crittografia dei dati](../../../help/landing/governance-privacy-security/encryption.md), consulta la documentazione.</li></ul> |

{style="table-layout:auto"}

**Nota**: l&#39;Attribution AI non sarà disponibile con i clienti esistenti di Healthcare Shield fino a nuovo avviso.

Per ulteriori informazioni sull&#39;Attribution AI, vedere la panoramica dell&#39;[Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### IA per l’analisi dei clienti

IA per l’analisi dei clienti disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su larga scala.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per la privacy | <ul><li> IA per l&#39;analisi dei clienti ora supporta la definizione di ruoli utente e criteri di accesso per gestire [autorizzazioni](../../../help/access-control/abac/ui/permissions.md) per funzionalità e oggetti all&#39;interno di un&#39;applicazione di prodotto. </li><li>Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività.</li><li> Tramite il controllo dell&#39;accesso basato su [attributi](../../access-control/abac/overview.md), gli amministratori possono controllare l&#39;accesso a oggetti e/o funzionalità specifici in base a determinati attributi. Questi attributi possono essere metadati aggiunti a un oggetto, ad esempio le etichette. Gli amministratori possono inoltre definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.</li><li>IA per l’analisi dei clienti sfrutta i set di dati di Platform. Per supportare le richieste di diritti dei consumatori che un brand può ricevere, i brand devono utilizzare Platform Privacy Service per inviare ai consumatori le richieste di accesso e cancellazione per rimuovere i propri dati attraverso il data lake, il servizio Identity e il profilo cliente in tempo reale. </li><li>Tutti i set di dati utilizzati per l’input/output dei modelli seguiranno le linee guida di Platform. Platform Data Encryption si applica ai dati in transito e a riposo. Per ulteriori informazioni sulla [crittografia dei dati](../../../help/landing/governance-privacy-security/encryption.md), consulta la documentazione.</li></ul> |

{style="table-layout:auto"}

**Nota**: IA per l&#39;analisi dei clienti non sarà disponibile con i clienti esistenti di Healthcare Shield fino a nuovo avviso.

Per ulteriori informazioni su Customer AI, consulta la panoramica di [Customer AI](../../intelligent-services/customer-ai/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fornisce più [!DNL dashboards] tramite i quali è possibile visualizzare informazioni importanti sui dati dell&#39;organizzazione acquisiti durante le istantanee giornaliere.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget attivazioni pianificate | Il widget [!UICONTROL Attivazioni pianificate] fornisce una visualizzazione in forma di tabella delle destinazioni attivate più di recente. Per ogni segmento, include il nome, la piattaforma di destinazione e la data di inizio e di fine dell’attivazione. Questo widget consente di scoprire subito dove e quando il pubblico viene attivato e rende più trasparenti le attivazioni duplicate o non necessarie. Queste informazioni accumulate evidenziano anche dove sono state escluse eventuali attivazioni. |

Per ulteriori informazioni su [!DNL Dashboards], vedere la [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’acquisizione di record con avvisi | La preparazione dati localizza ora gli avvisi (errori non critici) nei campi e consente di acquisire il resto della riga. Tutti gli errori di trasformazione dei mapper ora vengono segnalati come avvisi e le righe parzialmente acquisite vengono considerate riuscite, con un avviso.  Il monitoraggio è supportato anche nei record con avvertenze e dettagli di diagnostica. L’acquisizione parziale di record con avvertenze è attualmente disponibile solo per i dati in streaming. Per ulteriori informazioni, consulta la documentazione su [acquisizione di record con avvisi](../../sources/tutorials/ui/monitor-streaming.md). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Data Prep], vedere la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| (Beta) Supporto della personalizzazione basata su attributi per le destinazioni di personalizzazione | Con la versione beta della personalizzazione basata su attributi, nel [catalogo di destinazione](../../destinations/catalog/overview.md) verranno visualizzate due nuove schede: <ul><li>**[!UICONTROL Adobe Target V2]**: questo connettore è attualmente in versione beta ed è disponibile solo per un numero selezionato di clienti. Oltre alla funzionalità fornita dalla scheda di Adobe Target V1, il connettore di Target V2 aggiunge un [passaggio di mappatura](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) al flusso di lavoro di attivazione, che consente di mappare gli attributi del profilo ad Adobe Target, abilitando la personalizzazione della stessa pagina basata su attributi e della pagina successiva.</li><li>**[!UICONTROL Personalization personalizzato con attributi]**: il connettore è attualmente in versione beta ed è disponibile solo per un numero selezionato di clienti. Oltre alla funzionalità fornita da **[!UICONTROL Personalization personalizzato]**, il connettore **[!UICONTROL Personalization personalizzato con attributi]** aggiunge un [passaggio di mappatura](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes) facoltativo al flusso di lavoro di attivazione, che consente di mappare gli attributi del profilo alla destinazione di personalizzazione personalizzata, abilitando la personalizzazione della stessa pagina e della pagina successiva basata su attributi.</li></ul> Gli attributi del profilo <br> possono contenere dati sensibili. Per proteggere questi dati, la destinazione **[!UICONTROL Personalization personalizzato con attributi]** richiede l&#39;utilizzo dell&#39;[Edge Network Server API](../../server-api/overview.md) per la raccolta dati. Inoltre, tutte le chiamate API server devono essere effettuate in un [contesto autenticato](../../server-api/authentication.md). |

{style="table-layout:auto"}

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) è una piattaforma di esecuzione delle vendite con i dati di interazione più B2B tra acquirenti e venditori al mondo e investimenti significativi in tecnologie di intelligenza artificiale proprietarie per tradurre i dati di vendita in informazioni. [!DNL Outreach] consente alle organizzazioni di automatizzare il coinvolgimento nelle vendite e di agire sulla base delle informazioni sui ricavi per migliorare l&#39;efficienza, la prevedibilità e la crescita. |

{style="table-layout:auto"}

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Classe di entità AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-class.schema.json) | Classe basata su record per la creazione di schemi di ricerca per Adobe Journey Optimizer. |
| Gruppo di campi | [[!UICONTROL Oggetti di lavoro di Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Un gruppo di campi wrapper che fa riferimento a tutti i gruppi di campi specifici dell’oggetto di livello inferiore per Adobe Workfront. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Campi comuni evento passaggio Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Sono state aggiunte due nuove proprietà: `origTimeStamp` e `experienceID`. |
| Gruppo di campi | [[!UICONTROL Dettagli sull’appartenenza a segmento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Oltre al [!UICONTROL Profilo individuale XDM], questo gruppo di campi ora può essere utilizzato anche in schemi basati sulla classe XDM Business Account. |
| Gruppo di campi | (Multiplo) | Diversi gruppi di campi relativi alle attività B2B di Marketo sono stati aggiornati a uno stato stabile. Per ulteriori informazioni, consulta la [richiesta pull](https://github.com/adobe/xdm/pull/1593/files) seguente. |
| Gruppo di campi | (Multiplo) | Diversi gruppi di campi correlati al meteo sono stati aggiornati per correggere gli errori che si verificavano per `uvIndex` e `sunsetTime`. Per ulteriori informazioni, consulta la [richiesta pull](https://github.com/adobe/xdm/pull/1602/files) seguente. |
| Tipo di dati | [[!UICONTROL Elemento dell’elenco prodotti]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | È stata aggiunta una nuova proprietà `productImageUrl`. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dei dati QoE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | È stata aggiunta una nuova proprietà `framesPerSecond`. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` è stato rinominato come `appVersion`. Sono stati aggiornati anche `meta:enum` e `description` campi. |
| Tipi di dati e gruppi di campi | (Multiplo) | Diversi tipi di dati multimediali e gruppi di campi dispongono di nuovi campi e descrizioni aggiornate. Per ulteriori informazioni, consulta la [richiesta pull](https://github.com/adobe/xdm/pull/1582/files) seguente. |
| (Tutti) | (Multiplo) | Tutti gli oggetti dello schema che contengono un campo `enum` ora contengono anche un campo `meta:enum` corrispondente per indicare i valori di visualizzazione per ciascun vincolo. Per ulteriori informazioni, consulta la [richiesta pull](https://github.com/adobe/xdm/pull/1601/files) seguente. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [Panoramica sul sistema XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Limite rigido dei criteri di unione | Platform applicherà ora un limite massimo di **cinque** criteri di unione per sandbox. Se la sandbox dispone attualmente di più di cinque criteri di unione, **non** potrà creare nuovi criteri di unione fino a quando la sandbox non avrà meno di cinque criteri di unione. |
| Pulizia attributi edge profilo orfano | Per tutte le organizzazioni, il servizio Profilo ora rimuove gli attributi edge rimanenti dell’area di attività dell’utente su base giornaliera per fornire una rappresentazione più accurata dei profili nel sistema. Questa pulizia si verifica dopo l&#39;eliminazione di tutti i frammenti di profilo per un determinato profilo e dovrebbe interessare i profili da unire dai set di dati in cui `com_adobe_aep_profile_region_dataset` è contrassegnato come `true`. Questo potrebbe mostrare un calo della metrica &quot;Pubblico indirizzabile&quot; nel dashboard di utilizzo della licenza e un calo della metrica &quot;Conteggio profili&quot; nel dashboard Profilo, poiché queste metriche includevano frammenti di attributi edge rimasti prima di questa versione. |

{style="table-layout:auto"}

Per ulteriori informazioni sul Profilo cliente in tempo reale, inclusi tutorial e best practice per l’utilizzo dei dati del profilo, inizia consultando la [Panoramica sul Profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per 4000 segmenti | Tutte le organizzazioni con Platform possono ora supportare fino a 4000 definizioni di segmenti. Per ulteriori informazioni su come questa modifica influisce sulle API del processo di segmentazione, consulta la [guida dell&#39;endpoint del processo di segmentazione](../../segmentation/api/segment-jobs.md) |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale di origini self-service (SDK batch) | Sviluppa, testa e integra l’origine dati REST basata su API per acquisire i dati batch in Experience Platform utilizzando specifiche di origine facili da configurare. Con l’SDK Sources puoi: <ul><li>Configura una nuova origine nel catalogo Experience Platform.</li><li>Definisci le specifiche per l’origine, incluse le informazioni relative ai tipi di autenticazione supportati, alla pianificazione e al modo in cui vengono recuperati i dati delle risorse.</li><li>Crea una documentazione rivolta all’utente per la nuova sorgente.</li></ul> Per ulteriori informazioni, consulta la documentazione su [Self-Serve Sources (Batch SDK)](../../sources/sources-sdk/overview.md). |
| Disponibilità generale dell&#39;origine [!DNL Google BigQuery] | Utilizza l&#39;origine [!DNL Google BigQuery] per acquisire i dati dal data warehouse [!DNL Google BigQuery] per l&#39;Experience Platform. Per ulteriori informazioni, consulta la documentazione sull&#39;[[!DNL Google BigQuery] origine](../../sources/connectors/databases/bigquery.md). |
| Origine [!DNL Teradata Vantage] (Beta) | Utilizza l&#39;origine [!DNL Teradata Vantage] per acquisire i dati dagli ambienti ibridi multi-cloud per l&#39;Experience Platform. Per ulteriori informazioni, consulta la documentazione sull&#39;[[!DNL Teradata Vantage] origine](../../sources/connectors/databases/teradata-vantage.md). |
| Supporto per aree geografiche diverse per origine Adobe Analytics | Ora puoi acquisire suite di rapporti da qualsiasi area geografica (Stati Uniti, Regno Unito o Singapore). Le suite di rapporti devono essere mappate sulla stessa organizzazione dell’istanza Sandbox di Experience Platform in cui viene creata la connessione di origine. Per ulteriori informazioni, leggere la guida sulla [creazione di una connessione di origine Adobe Analytics nell&#39;interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
