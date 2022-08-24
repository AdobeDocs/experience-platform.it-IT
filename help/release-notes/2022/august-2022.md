---
title: Note sulla versione di Adobe Experience Platform - Agosto 2022
description: Note sulla versione di agosto 2022 per Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: f458b3f204e961f849782f26a1563a67d6ea4b60
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 6%

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

I servizi AI/ML consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi d’uso della customer experience. Questo consente agli analisti di marketing di impostare modelli specifici per le esigenze aziendali utilizzando configurazioni a livello di business senza la necessità di disporre di competenze scientifiche in materia di dati.

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per la privacy | <ul><li> Attribution AI supporta ora la definizione dei ruoli utente e dei criteri di accesso per la gestione [permissions](../../../help/access-control/abac/ui/permissions.md) per funzioni e oggetti all’interno di un’applicazione di prodotto. </li><li>Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività.</li><li> Attraverso [controllo dell&#39;accesso basato sugli attributi](../../access-control/abac/overview.md), gli amministratori possono controllare l’accesso a oggetti e/o funzionalità specifici in base a determinati attributi, che possono essere metadati aggiunti a un oggetto, ad esempio le etichette.Gli amministratori possono inoltre definire ruoli utente che hanno accesso solo a campi e dati specifici corrispondenti a tali campi.</li><li>[Igiene dei dati](../../../help/hygiene/home.md) le funzionalità di Attribution AI ti consentono di utilizzare solo dati aggiornati per ulteriore formazione e valutazione. Allo stesso modo, quando si richiede di eliminare i dati, Attribution AI rifiuta di utilizzare i dati eliminati.</li><li>Attribution AI sfrutta i set di dati di Platform. Per facilitare la conformità ai requisiti RGPD, puoi utilizzare Adobe Experience Platform Privacy Service per configurare i protocolli per soddisfare le richieste dei clienti di accedere e cancellare i loro dati dal data lake, dal servizio Identity e dal profilo cliente in tempo reale. Tutti i dati sono crittografati in transito e a riposo.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Nota**: Le Attribution AI non saranno disponibili con i clienti esistenti di Healthcare Shield o Privacy Shield fino a nuovo avviso.

Per ulteriori informazioni sulle Attribution AI, consulta la sezione [Attribution AI](../../intelligent-services/attribution-ai/overview.md) panoramica.

### Customer AI

Customer AI disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su scala.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per la privacy | <ul><li> Customer AI supporta ora la definizione di ruoli utente e di criteri di accesso da gestire [permissions](../../../help/access-control/abac/ui/permissions.md) per funzioni e oggetti all’interno di un’applicazione di prodotto. </li><li>Le risorse del registro di controllo vengono registrate automaticamente quando si verifica l’attività.</li><li> Attraverso [controllo dell&#39;accesso basato sugli attributi](../../access-control/abac/overview.md), gli amministratori possono controllare l’accesso a oggetti e/o funzionalità specifici in base a determinati attributi. Questi attributi possono essere metadati aggiunti a un oggetto, ad esempio etichette. Gli amministratori possono inoltre definire ruoli utente con accesso solo a campi e dati specifici corrispondenti a tali campi.</li><li>[Igiene dei dati](../../../help/hygiene/home.md) Le funzionalità di Customer AI consentono di utilizzare solo dati aggiornati per ulteriori formazione e valutazioni. Allo stesso modo, quando richiedi di eliminare i dati, Customer AI rifiuta di utilizzare i dati eliminati.</li><li>Customer AI sfrutta i set di dati di Platform. Per facilitare la conformità ai requisiti RGPD, puoi utilizzare Adobe Experience Platform Privacy Service per configurare i protocolli per soddisfare le richieste dei clienti di accedere e cancellare i loro dati dal data lake, dal servizio Identity e dal profilo cliente in tempo reale. Tutti i dati sono crittografati in transito e a riposo.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Nota**: Customer AI non sarà disponibile con i clienti esistenti di Healthcare Shield o Privacy Shield fino a nuovo avviso.

Per ulteriori informazioni su Customer AI, consulta la sezione [Customer AI](../../intelligent-services/customer-ai/overview.md) panoramica.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fornisce più [!DNL dashboards] attraverso cui puoi visualizzare informazioni importanti sui dati dell’organizzazione, come acquisiti durante le istantanee giornaliere.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget attivazioni pianificate | La [!UICONTROL Attivazioni pianificate] widget fornisce una visualizzazione tabularizzata delle destinazioni attivate più di recente. Per ogni segmento, include il nome, la piattaforma di destinazione e la data di inizio e di fine dell’attivazione. Questo widget consente di scoprire subito dove e quando il pubblico viene attivato e rende più trasparenti le attivazioni duplicate o non necessarie. Queste informazioni accumulate evidenziano anche dove sono state escluse eventuali attivazioni. |

Per ulteriori informazioni su [!DNL Dashboards], vedi [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’acquisizione di record con avvisi | In Preparazione dati gli avvisi (errori non critici) verranno localizzati nei campi e il resto della riga potrà essere acquisito. Tutti gli errori di trasformazione della mappatura vengono ora segnalati come avvisi e le righe parzialmente ingerite vengono considerate di successo, con un avviso.  Il monitoraggio è supportato anche nei record con avvisi e dettagli diagnostici. L’acquisizione parziale di record con avvisi è attualmente disponibile solo per i dati in streaming. Consulta la documentazione su [acquisizione di record con avvisi](../../sources/tutorials/ui/monitor-streaming.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni [!DNL Data Prep], vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

<!--

**New or updated features**

| Feature | Description |
| ----------- | ----------- |
|  ||

{style="table-layout:auto"}

-->

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) è una piattaforma di esecuzione delle vendite con i dati di interazione tra buyer e venditori B2B più diffusi al mondo e importanti investimenti in tecnologie di intelligenza artificiale proprietaria per tradurre i dati di vendita in informazioni. [!DNL Outreach] consente alle organizzazioni di automatizzare l&#39;impegno di vendita e di agire sulla base dell&#39;intelligenza dei ricavi per migliorare l&#39;efficienza, la prevedibilità e la crescita. |

{style=&quot;table-layout:auto&quot;}

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Schema globale | [[!UICONTROL Schema di entità AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Descrive le entità denormalizzate per Adobe Journey Optimizer. |
| Classe | [[!UICONTROL Entità di esecuzione AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Descrive le entità di esecuzione Adobe Journey Optimizer da utilizzare nella segmentazione. |
| Gruppo di campi | [[!UICONTROL Oggetti di lavoro Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Gruppo di campi wrapper che fa riferimento a tutti i gruppi di campi specifici dell’oggetto di livello inferiore per Adobe Workfront. |

{style=&quot;table-layout:auto&quot;}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Campi comuni evento evento passaggio Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Sono state aggiunte due nuove proprietà: `origTimeStamp` e `experienceID`. |
| Gruppo di campi | [[!UICONTROL Dettagli di appartenenza al segmento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Oltre a [!UICONTROL Profilo individuale XDM], questo gruppo di campi può ora essere utilizzato anche negli schemi in base alla classe Business Account XDM. |
| Gruppo di campi | (Multipli) | Diversi gruppi di campi relativi alle attività Marketo B2B sono stati aggiornati allo stato stabile. Vedi quanto segue [richiesta pull](https://github.com/adobe/xdm/pull/1593/files) per i dettagli. |
| Gruppo di campi | (Multipli) | Sono stati aggiornati diversi gruppi di campi correlati al meteo per correggere gli errori che si verificavano per `uvIndex` e `sunsetTime`. Vedi quanto segue [richiesta pull](https://github.com/adobe/xdm/pull/1602/files) per i dettagli. |
| Tipo di dati | [[!UICONTROL Voce dell’elenco dei prodotti]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Una nuova proprietà `productImageUrl` è stato aggiunto. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dei dati QE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Una nuova proprietà `framesPerSecond` è stato aggiunto. |
| Tipo di dati | [[!UICONTROL Informazioni sulla sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` è stato rinominato come `appVersion`. `meta:enum` e `description` Sono stati inoltre aggiornati i campi . |
| Tipi di dati e gruppi di campi | (Multipli) | Diversi tipi di dati multimediali e gruppi di campi dispongono di nuovi campi e descrizioni aggiornate. Vedi quanto segue [richiesta pull](https://github.com/adobe/xdm/pull/1582/files) per i dettagli. |
| (Tutto) | (Multipli) | Tutti gli oggetti dello schema che contengono un `enum` contiene ora anche un `meta:enum` campo per indicare i valori di visualizzazione per ciascun vincolo. Vedi quanto segue [richiesta pull](https://github.com/adobe/xdm/pull/1601/files) per i dettagli. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

| Funzione | Descrizione |
| ------- | ----------- |
| Limite rigido dei criteri di unione | Platform applicherà ora un limite rigido di **cinque** unione di criteri per sandbox. Se la sandbox dispone attualmente di più di cinque criteri di unione, verrà **not** è possibile creare nuovi criteri di unione fino a quando la sandbox non dispone di meno di cinque criteri di unione. |
| Pulizia attributo edge del profilo orfano | Per tutte le organizzazioni, il servizio di profilo ora rimuove quotidianamente gli attributi edge rimanenti dell’area di attività dell’utente per fornire una rappresentazione più accurata dei profili nel sistema. Questa pulizia si verifica dopo l’eliminazione di tutti i frammenti di profilo per un determinato profilo e dovrebbe influenzare i profili che vengono uniti dai set di dati in cui `com_adobe_aep_profile_region_dataset` è contrassegnato come `true`. Questo può mostrare un calo nella metrica &quot;Pubblico di riferimento&quot; nel dashboard dell’utilizzo della licenza e può mostrare un calo nella metrica &quot;Conteggio profili&quot; nel dashboard del profilo, poiché queste metriche includevano frammenti di attributi di margine residuo prima di questa versione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sul Profilo del cliente in tempo reale, compresi tutorial e best practice per l’utilizzo dei dati del profilo, consulta la sezione [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per 4000 segmenti | Tutte le organizzazioni con Platform ora possono supportare fino a 4000 definizioni di segmenti. Per ulteriori informazioni su come questa modifica influisce sulle API dei processi di segmento, consulta la sezione [guida all’endpoint del processo del segmento](../../segmentation/api/segment-jobs.md) |

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale delle origini self-service (SDK batch) | Sviluppa, testa e integra la tua origine dati basata su API REST per acquisire dati batch in Experience Platform utilizzando specifiche sorgente facili da configurare. Con l&#39;SDK di Origini puoi: <ul><li>Configura una nuova origine per il catalogo di Experience Platform.</li><li>Definisci le specifiche dell’origine, incluse le informazioni relative ai tipi di autenticazione supportati, alla pianificazione e al modo in cui vengono recuperati i dati delle risorse.</li><li>Crea la documentazione rivolta all’utente per la nuova sorgente.</li></ul> Per ulteriori informazioni, consulta la documentazione su [Sorgenti self-service (SDK batch)](../../sources/sources-sdk/overview.md). |
| Disponibilità generale [!DNL Google BigQuery] source | Utilizza la [!DNL Google BigQuery] sorgente per acquisire i dati dal [!DNL Google BigQuery] data warehouse ad Experience Platform. Per ulteriori informazioni, consulta la documentazione sul [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] sorgente (Beta) | Utilizza la [!DNL Teradata Vantage] da origine a acquisizione di dati da ambienti multi-cloud ibridi ad Experience Platform. Per ulteriori informazioni, consulta la documentazione sul [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Supporto tra aree geografiche per l’origine Adobe Analytics | È ora possibile acquisire suite di rapporti da qualsiasi regione (Stati Uniti, Regno Unito o Singapore). Le suite di rapporti devono essere mappate nella stessa organizzazione dell’istanza Sandbox di Experience Platform in cui viene creata la connessione sorgente. Per ulteriori informazioni, consulta la guida su [creazione di una connessione sorgente Adobe Analytics nell’interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
