---
title: Note sulla versione di Adobe Experience Platform - Aprile 2022
description: Note sulla versione di aprile 2022 per Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2904'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 aprile 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Flussi di dati](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Edizione B2B di Real-Time Customer Data Platform](#B2B)
- [Origini](#sources)

## [!DNL Dashboards] {#dashboards}

Platform fornisce più dashboard attraverso i quali è possibile visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

Le dashboard forniscono opzioni di reporting preconfigurate per i dati dell’organizzazione e sono integrate direttamente nel flusso di lavoro degli addetti al marketing in Platform. Queste dashboard sono disponibili senza la necessità di ulteriore supporto IT o il tempo e l’impegno altrimenti necessari per esportare ed elaborare i dati con una progettazione e un’implementazione aggiuntive di data warehousing.

I seguenti widget sono disponibili nella libreria Widget nei rispettivi dashboard. Consulta la documentazione per ulteriori informazioni su [come aggiungere widget tramite la libreria Widget](../../dashboards/customize/widget-library.md).

**Nuovi widget**

| Widget | Dashboard di | Descrizione |
| ------ | --------- | ----------- |
| [!UICONTROL Tendenza profili aggiunti] | Profili | Questo widget utilizza un grafico a linee per illustrare il numero totale di profili uniti che sono stati aggiunti quotidianamente all’archivio profili negli ultimi 30 giorni, 90 giorni o 12 mesi. |
| [!UICONTROL Tipi di pubblico mappati allo stato di destinazione] | Profili | Questo widget visualizza il numero totale di tipi di pubblico mappati e non mappati in una singola metrica e utilizza un grafico ad anello per illustrare la differenza proporzionale tra i totali. |
| [!UICONTROL Dimensione pubblico] | Profili | Questo widget fornisce una tabella a due colonne che elenca fino a 20 segmenti e il numero totale di tipi di pubblico contenuti in ciascun segmento. L’elenco dipende dal criterio di unione applicato e ordinato da alto a basso in base al numero totale di tipi di pubblico. |
| [!UICONTROL Tendenza conteggio profili] | Profili | Questo widget utilizza un grafico a linee per illustrare la tendenza nel numero totale di profili contenuti nel sistema nel tempo. I dati possono essere visualizzati in periodi di 30 giorni, 90 giorni e 12 mesi. |
| [!UICONTROL Profili di identità singola per identità] | Profili | Questo widget utilizza un grafico a barre per illustrare il numero totale di profili identificati con un solo identificatore univoco. Il widget supporta fino a cinque delle identità più comuni. |
| [!UICONTROL Stato della destinazione] | Destinazioni | Questo widget visualizza il numero totale di destinazioni abilitate come una singola metrica e utilizza un grafico ad anello per illustrare la differenza proporzionale tra le destinazioni abilitate e disabilitate. |
| [!UICONTROL Destinazioni attive per piattaforma di destinazione] | Destinazioni | Questo widget utilizza una tabella a due colonne per mostrare un elenco di piattaforme di destinazione attive e il numero totale di destinazioni attive per ogni piattaforma di destinazione. |
| [!UICONTROL Tipi di pubblico attivati su tutte le destinazioni] | Destinazioni | Questo widget fornisce in un’unica metrica il numero totale di tipi di pubblico attivati su tutte le destinazioni. |
| [!UICONTROL Ordine di attivazione pubblico] | Segmenti | Questo widget fornisce una tabella a tre colonne che elenca il nome della destinazione, la piattaforma e la data di attivazione del pubblico. |
| [!UICONTROL Tendenza dimensione pubblico] | Segmenti | Questo widget fornisce un’illustrazione del grafico a linee per il numero totale di profili che soddisfano i criteri di qualsiasi definizione di segmento per periodi di 30 giorni, 90 giorni e 12 mesi. |
| [!UICONTROL Tendenza di modifica della dimensione del pubblico] | Segmenti | Questo widget fornisce un grafico a linee che illustra la differenza nel numero totale di profili idonei per un dato segmento tra le istantanee giornaliere più recenti. Il periodo di analisi delle tendenze può essere visualizzato in periodi di 30 giorni, 90 giorni e 12 mesi. |
| [!UICONTROL Tendenza dimensione pubblico per identità] | Segmenti | Questo widget illustra la tendenza delle dimensioni del pubblico per un particolare segmento in base a un tipo di identità selezionato. Il periodo di analisi delle tendenze può essere visualizzato in periodi di 30 giorni, 90 giorni e 12 mesi. |

**Nuove funzioni** {#new-features}

| Funzione | Dashboard di | Descrizione |
| ------- | --------- | ----------- |
| Pulizia appartenenza a segmenti di profilo orfani | Profili e utilizzo delle licenze | Il Servizio profili ora rimuove i membri del segmento rimasti su base giornaliera per fornire una rappresentazione più accurata dei profili nel sistema. Questa pulizia si verifica dopo l’eliminazione di tutti i frammenti di profilo per un determinato profilo. Questo potrebbe mostrare un calo della metrica &quot;Pubblico indirizzabile&quot; nel dashboard di utilizzo della licenza e un calo della metrica &quot;Conteggio profili&quot; nel dashboard Profilo, poiché queste metriche includevano frammenti di segmenti rimanenti prima di questa versione. |

{style="table-layout:auto"}

Consulta la documentazione per ulteriori informazioni su [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md), e [[!DNL Segments]](../../dashboards/guides/segments.md) dashboard.

## Flussi di dati {#dataflows}

In Platform, i dati vengono acquisiti da diverse origini, analizzati all’interno del sistema e attivati in un’ampia varietà di destinazioni. Platform semplifica il processo di tracciamento di questo flusso di dati potenzialmente non lineare fornendo trasparenza con i flussi di dati.

I flussi di dati sono una rappresentazione dei processi che spostano i dati in Platform. Questi flussi di dati sono configurati tra servizi diversi, aiutando a spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono quindi utilizzati dal servizio Identity e dal profilo cliente in tempo reale prima di essere attivati nelle destinazioni.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Dashboard dei segmenti | Ora puoi utilizzare la dashboard di monitoraggio per monitorare i flussi di dati per i segmenti. Per ulteriori informazioni, consulta la guida su [monitoraggio dei segmenti nell’interfaccia utente](../../dataflows/ui/monitor-segments.md) |

Per informazioni più generali sui flussi di dati, consulta [panoramica dei flussi di dati](../../dataflows/home.md). Per ulteriori informazioni sulla segmentazione, consulta [panoramica sulla segmentazione](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per origine Adobe Analytics | L’origine di Adobe Analytics ora supporta le funzioni di preparazione dati, che consentono di mappare i dati della suite di rapporti di Analytics su uno schema XDM di destinazione durante la creazione di un flusso di dati. Guarda il tutorial su [creazione di una connessione sorgente Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) per ulteriori informazioni. |
| Supporto per l’importazione di regole di mappatura esistenti | Ora puoi importare le regole di mappatura da un flusso di dati esistente per accelerare le configurazioni del flusso di dati e limitare gli errori. Guarda il tutorial su [importazione delle regole di mappatura esistenti](../../data-prep/ui/mapping.md) per ulteriori informazioni. |

Per ulteriori informazioni su [!DNL Data Prep], consultare il [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| Connettori di destinazione Enterprise avanzati | Sono ora generalmente disponibili tre connettori di destinazione aziendali: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md), e [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> La disponibilità generale dei connettori di destinazione aziendali include tutte le funzionalità offerte in precedenza nella fase Beta e altro ancora: <ul><li>Nuove funzionalità di autenticazione, tra cui [Firma di accesso condiviso negli hub eventi di Azure](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) e altro ancora [tipi di autenticazione](../../destinations/catalog/streaming/http-destination.md#authentication-information) (token Bearer, OAuth 2) nella destinazione API HTTP;</li><li>[Backfill dei dati storici del profilo](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (invio di profili storici qualificati per il segmento quando è attivato per la prima volta);</li><li>Le metriche di esecuzione del flusso di dati sono ora supportate per queste destinazioni;</li><li>[Metadati aggiuntivi del segmento](../../destinations/catalog/streaming/http-destination.md#destination-details) inclusi nel payload dei dati, compresi i nomi dei segmenti e le marche temporali dei segmenti;</li><li>Supporto per [indirizzi IP statici](/help/destinations/catalog/streaming/ip-address-allow-list.md) per i clienti che devono Experience Platform di inserisce nell&#39;elenco Consentiti.</li></ul> |
| Avvisi contestuali per i flussi di dati di destinazione | Ora puoi [abbonati agli avvisi](../../destinations/ui/alerts.md) durante la creazione di un flusso di dati di destinazione, per ricevere messaggi di avviso relativi allo stato, al completamento o al fallimento dell’esecuzione del flusso di dati. Puoi scegliere di ricevere gli avvisi nell’interfaccia utente di Experience Platform o tramite e-mail. |

### Processo di rilascio per connettori di destinazione aziendali avanzati {#release-process-enterprise-destinations}

Per le destinazioni Amazon Kinesis, Azure Event Hub e HTTP API, durante il processo di rilascio (a partire dal 27 aprile), nel catalogo delle destinazioni verranno visualizzate sia la scheda di destinazione Beta precedente che la nuova scheda di destinazione generalmente disponibile (GA). Eventuali flussi di dati configurati dai clienti che utilizzano le destinazioni beta verranno migrati nei prossimi giorni alla versione GA della stessa destinazione. La migrazione dovrebbe concludersi entro la fine della giornata di venerdì 29 aprile. Le destinazioni Beta continueranno a essere visibili durante questo breve intervallo di tempo ed etichettate come **Obsoleto**.

Se hai utilizzato queste destinazioni nella fase Beta, tieni presente quanto segue:

- Se in precedenza è stato in versione beta con una qualsiasi delle 3 destinazioni, non è necessaria alcuna azione. Tutti i flussi di dati configurati come parte di Beta continueranno a essere funzionali e verranno migrati alla versione GA.
- Se desideri impostare queste destinazioni a partire dal 27 aprile, esegui questa operazione con la nuova versione GA delle destinazioni.
- Le schede beta contrassegnate come obsolete verranno rimosse una volta completata l’operazione di rilascio, stimata entro la fine della giornata di venerdì 29 aprile. Il team di progettazione Experience Platform sta monitorando attentamente la corretta esecuzione dell’operazione di rilascio.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [!DNL Criteo] | Connetti e attiva i dati a [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) piattaforma pubblicitaria. |
| [!DNL Sendgrid] | Connetti e attiva i dati a [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) piattaforma per e-mail transazionali e di marketing. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Aggiungere o rimuovere singoli campi standard per uno schema | L’interfaccia utente dell’Editor schema ora consente di aggiungere porzioni di gruppi di campi standard agli schemi, fornendo maggiore flessibilità per i campi che scegli di includere senza dover creare risorse personalizzate da zero.<br><br>Ora puoi anche definire campi personalizzati ad hoc direttamente all’interno della struttura dello schema e assegnarli a un gruppo di campi personalizzato nuovo o esistente senza dover prima creare o modificare il gruppo di campi.<br><br>Consulta la guida su [creazione e modifica di schemi nell’interfaccia utente](../../xdm/ui/resources/schemas.md) per ulteriori informazioni su questi nuovi flussi di lavoro. |

{style="table-layout:auto"}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Schema globale | [[!UICONTROL Richiesta operazione di igiene dei dati]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Acquisisce i dettagli di una richiesta di pulizia dati per eliminare o modificare record in un set di dati o una sandbox specifici. |
| Descrittore | [[!UICONTROL Descrittore di granularità della serie temporale]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indica la granularità delle serie temporali e dei dati di riepilogo. Quando applicato a uno schema, il valore di `timestamp` è il primo timestamp in un periodo di questa granularità. |
| Classe | [[!UICONTROL Metriche di riepilogo XDM]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Fornisce metriche preriepilogate con dimensioni di raggruppamento, ad esempio i risultati di SQL SELECT con GROUP BY. |
| Gruppo di campi | [[!UICONTROL Mappa dei risultati della valutazione dei criteri di consenso]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | Acquisisce il risultato della valutazione dei criteri di consenso per un individuo. |
| Gruppo di campi | [[!UICONTROL Ricerca nel sito]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Acquisisce informazioni relative alla ricerca del sito come query di ricerca, filtri e ordinamento. |
| Gruppo di campi | [[!UICONTROL Unisci lead]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Acquisisce i dettagli di un evento in cui vengono uniti due o più lead. |
| Gruppo di campi | [[!UICONTROL E-mail inviata]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Acquisisce i dettagli di un evento in cui un’e-mail viene inviata a un destinatario. |
| Gruppo di campi | [[!UICONTROL Campi di unione]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Acquisisce i valori calcolati attraverso il processo di unione delle identità per un evento. |
| Gruppo di campi | [[!UICONTROL Dettagli Destinatario Secondario Per Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Un gruppo di campi Adobe Journey Optimizer che acquisisce i dettagli di un destinatario secondario per un controllo di audit. |
| Gruppo di campi | [[!UICONTROL Dettagli della relazione della persona dell’account aziendale XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Acquisisce i dettagli relativi a una relazione account-persona. |
| Gruppo di campi | [[!UICONTROL Dettagli persona account]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Acquisisce i dettagli relativi a una relazione account-persona. |
| Tipo di dati | [[!UICONTROL Carrello]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Acquisisce informazioni su un carrello acquisti e-commerce. |
| Tipo di dati | [[!UICONTROL Spedizione]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Acquisisce le informazioni di spedizione per uno o più prodotti. |
| Tipo di dati | [[!UICONTROL Ricerca nel sito]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | Acquisisce informazioni sull’attività di ricerca del sito. |
| Estensione (Workfront) | [[!UICONTROL Attributi dei task operativi]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Acquisisce i dettagli relativi a un’attività operativa. |
| Estensione (Workfront) | [[!UICONTROL Attributi Portfolio di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Acquisisce i dettagli relativi a un portfolio di lavoro. |
| Estensione (Workfront) | [[!UICONTROL Attributi del programma di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Acquisisce i dettagli relativi a un programma di lavoro. |
| Estensione (Workfront) | [[!UICONTROL Attributi progetto di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Acquisisce i dettagli relativi a un progetto di lavoro. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione aggiornamento |
| --- | --- | --- |
| Schema globale | [[!UICONTROL Destinazioni ]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nuovi valori enum per `destinationCategory`. |
| Descrittore | [[!UICONTROL Descrittore del nome intuitivo]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | È stato aggiunto il supporto per la rimozione dei valori suggeriti (`meta:enum`) non necessari dai campi standard. |
| Gruppo di campi | [[!UICONTROL Processo di accesso utente]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` campo aggiunto. |
| Tipo di dati | [[!UICONTROL Commercio]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Sono stati aggiunti diversi campi relativi al carrello. |
| Tipo di dati | [[!UICONTROL Elemento dell’elenco prodotti]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Sono stati aggiunti nuovi campi per le opzioni selezionate e l’importo dello sconto. |
| Estensione (Intelligent Services) | [[!UICONTROL Ottimizzazione del tempo di invio di Intelligent Services JourneyAI]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Ottimizza il formato di archiviazione per i punteggi del tempo di invio. |
| Estensione (Workfront) | [[!UICONTROL Evento modifica Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Diversi campi sostituiti con un `workfront:customData` campo per campi modulo personalizzati. |
| Estensione (Workfront) | [[!UICONTROL Attributi attività di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Sono stati aggiunti diversi campi. |
| Estensione (Workfront) | [[!UICONTROL Oggetto di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nuovi campi per il tipo di oggetto padre e i campi modulo personalizzati. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta [Panoramica del sistema XDM](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

I servizi di intelligenza artificiale e machine learning consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi di utilizzo dell’esperienza del cliente. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science.

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per più set di dati | La funzione Set di dati multipli ora supporta tutti i set di dati Experience Event e la selezione di Identity Map come identità. I clienti possono selezionare Identity Map ed eventuali ID associati, purché sia presente uno spazio dei nomi di identità comune tra i set di dati. Attribution AI supporta i seguenti schemi: Adobe Analytics, Experience Event, Consumer Experience Event. Per ulteriori informazioni sul supporto di più set di dati in Attribution AI, consulta [Guida utente di Attribution AI](../../intelligent-services/attribution-ai/user-guide.md). |

Per ulteriori informazioni su [!DNL Intelligent Services], consultare il [[!DNL Intelligent Services] panoramica](../../intelligent-services/home.md).

### IA per l’analisi dei clienti

IA per l’analisi dei clienti disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su larga scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di machine learning né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per più set di dati | La funzione Set di dati multipli ora supporta tutti i set di dati Experience Event e la selezione di Identity Map come identità. I clienti possono selezionare Identity Map ed eventuali ID associati, purché sia presente uno spazio dei nomi di identità comune tra i set di dati. IA per l’analisi dei clienti supporta i seguenti schemi: Adobe Analytics, Experience Event, Consumer Experience Event e Adobe Audience Manager schema. Per ulteriori informazioni sul supporto di più set di dati in Customer AI, consulta [Guida utente di Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Nuove metriche di valutazione del modello in IA per l’analisi dei clienti | I nuovi grafici dei guadagni in IA per l’analisi dei clienti consentono agli addetti al marketing di determinare le dimensioni del gruppo di destinazione in base al budget e agli obiettivi di ROI. I nuovi grafici Lift misurano la qualità del modello, fornendo una migliore visibilità dell’incremento ottenuto rispetto al targeting casuale. Per ulteriori informazioni, vedere [scoprire informazioni con Customer AI](../../intelligent-services/customer-ai/user-guide/discover-insights.md) documento. |

Per ulteriori informazioni su [!DNL Intelligent Services], consultare il [[!DNL Intelligent Services] panoramica](../../intelligent-services/home.md).

## Edizione B2B di Real-Time Customer Data Platform {#B2B}

Basata su Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition è progettata appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli addetti al marketing di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per `isDeleted` funzionalità | Tutti [!DNL Marketo] set di dati eccetto `Activities` ora supporta `isDeleted` mappatura. La nuova mappatura viene aggiunta automaticamente ai flussi di dati B2B esistenti. È possibile utilizzare `isDeleted` mappatura per filtrare i record che sono stati eliminati in modo che i dati in [!DNL Data Lake] è coerente con i dati di origine. Consulta la [[!DNL Marketo] guida alla mappatura dei campi](../../sources/connectors/adobe-applications/mapping/marketo.md) per ulteriori informazioni su `isDeleted`. |

Per ulteriori informazioni sulla versione B2B di Real-time Customer Data Platform, consulta [Panoramica B2B](../../rtcdp/b2b-overview.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per [!DNL OneTrust Integration] | Ora puoi utilizzare la [!DNL OneTrust Integration] acquisire i dati di consenso e preferenze dal tuo [!DNL OneTrust] da un account a Platform. Consulta la documentazione su [creazione di [!DNL OneTrust Integration] connessione sorgente](../../sources/connectors/consent-and-preferences/onetrust.md) per ulteriori informazioni. |
| Supporto per [!DNL Square] | Ora puoi utilizzare la [!DNL Square] origine per acquisire i dati dei pagamenti dal tuo [!DNL Square] da un account a Platform. |
| Supporto per l’eliminazione dei flussi di dati Attributi del cliente | Ora puoi eliminare i flussi di dati creati con il connettore di origine Attributi del cliente. |

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
