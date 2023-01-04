---
title: Note sulla versione di Adobe Experience Platform - Aprile 2022
description: Le note sulla versione di aprile 2022 per Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2916'
ht-degree: 7%

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

Platform fornisce diverse dashboard attraverso le quali puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

Le dashboard forniscono opzioni di reporting preconfigurate per i dati dell’organizzazione e sono integrate direttamente nel flusso di lavoro dell’addetto al marketing all’interno di Platform. Queste dashboard sono disponibili senza la necessità di ulteriore supporto IT o il tempo e lo sforzo necessari per esportare ed elaborare i dati con una progettazione e un&#39;implementazione aggiuntive per il data warehouse.

I seguenti widget sono disponibili tramite la libreria Widget sulle rispettive dashboard. Per ulteriori informazioni, consulta la documentazione . [come aggiungere widget tramite la libreria Widget](../../dashboards/customize/widget-library.md).

**Nuovi widget**

| Widget | Dashboard di | Descrizione |
| ------ | --------- | ----------- |
| [!UICONTROL Profili tendenza aggiunta] | Profili | Questo widget utilizza un grafico a linee per illustrare il numero totale di profili uniti aggiunti quotidianamente all’archivio profili negli ultimi 30 giorni, 90 giorni o 12 mesi. |
| [!UICONTROL Tipi di pubblico mappati sullo stato di destinazione] | Profili | Questo widget visualizza il numero totale di tipi di pubblico mappati e non mappati in un’unica metrica e utilizza un grafico ad anello per illustrare la differenza proporzionale tra i loro totali. |
| [!UICONTROL Dimensione del pubblico] | Profili | Questo widget fornisce una tabella a due colonne in cui sono elencati fino a 20 segmenti e il numero totale di tipi di pubblico contenuti in ciascun segmento. L’elenco dipende dal criterio di unione applicato e ordinato da alto a basso in base al numero totale di tipi di pubblico. |
| [!UICONTROL Tendenza al conteggio dei profili] | Profili | Questo widget utilizza un grafico a linee per illustrare la tendenza nel numero totale di profili contenuti nel sistema nel tempo. I dati possono essere visualizzati in 30 giorni, 90 giorni e 12 mesi. |
| [!UICONTROL Singoli profili di identità per identità] | Profili | Questo widget utilizza un grafico a barre per illustrare il numero totale di profili identificati con un solo identificatore univoco. Il widget supporta fino a cinque delle identità più comuni. |
| [!UICONTROL Stato della destinazione] | Destinazioni | Questo widget visualizza il numero totale di destinazioni abilitate come una singola metrica e utilizza un grafico ad anello per illustrare la differenza proporzionale tra destinazioni abilitate e disabilitate. |
| [!UICONTROL Destinazioni attive per piattaforma di destinazione] | Destinazioni | Questo widget utilizza una tabella a due colonne per visualizzare un elenco di piattaforme di destinazione attive e il numero totale di destinazioni attive per ciascuna piattaforma di destinazione. |
| [!UICONTROL Tipi di pubblico attivati per tutte le destinazioni] | Destinazioni | Questo widget fornisce il numero totale di tipi di pubblico attivati in tutte le destinazioni in un’unica metrica. |
| [!UICONTROL Ordine di attivazione del pubblico] | Segmenti | Questo widget fornisce una tabella a tre colonne in cui sono elencati il nome della destinazione, la piattaforma e la data di attivazione del pubblico. |
| [!UICONTROL Tendenza delle dimensioni del pubblico] | Segmenti | Questo widget fornisce un’illustrazione grafico a linee per il numero totale di profili che soddisfano i criteri di qualsiasi definizione di segmento per periodi di 30 giorni, 90 giorni e 12 mesi. |
| [!UICONTROL Tendenza al cambiamento della dimensione del pubblico] | Segmenti | Questo widget fornisce un grafico a linee che illustra la differenza nel numero totale di profili qualificati per un dato segmento tra le istantanee giornaliere più recenti. Il periodo di analisi delle tendenze può essere visualizzato in 30 giorni, 90 giorni e 12 mesi. |
| [!UICONTROL Tendenza delle dimensioni del pubblico in base all’identità] | Segmenti | Questo widget illustra la tendenza delle dimensioni del pubblico per un particolare segmento in base a un tipo di identità selezionato. Il periodo di analisi delle tendenze può essere visualizzato in 30 giorni, 90 giorni e 12 mesi. |

**Nuove funzioni** {#new-features}

| Funzione | Dashboard di | Descrizione |
| ------- | --------- | ----------- |
| Pulizia dell’appartenenza al segmento di profilo orfano | Profili e utilizzo della licenza | Il Servizio profili ora rimuove quotidianamente i membri del segmento rimasti per fornire una rappresentazione più precisa dei profili nel sistema. Questa pulizia si verifica dopo l’eliminazione di tutti i frammenti di profilo per un determinato profilo. Questo può mostrare un calo nella metrica &quot;Pubblico di riferimento&quot; nel dashboard dell’utilizzo della licenza e può mostrare un calo nella metrica &quot;Conteggio profili&quot; nel dashboard Profilo, dal momento che queste metriche includevano frammenti di segmento di avanzo prima di questa versione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni, consulta la documentazione . [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md)e [[!DNL Segments]](../../dashboards/guides/segments.md) dashboard.

## Flussi di dati {#dataflows}

In Platform, i dati vengono acquisiti da diverse sorgenti, analizzati all’interno del sistema e attivati in un’ampia gamma di destinazioni. Platform facilita il processo di tracciamento di questo flusso di dati potenzialmente non lineare grazie alla trasparenza dei flussi di dati.

I flussi di dati sono una rappresentazione dei processi che spostano i dati in Platform. Questi flussi di dati sono configurati tra diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono quindi utilizzati dal servizio Identity e dal profilo cliente in tempo reale prima di essere infine attivati nelle destinazioni.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Dashboard dei segmenti | Ora puoi utilizzare il dashboard di monitoraggio per monitorare i flussi di dati per i segmenti. Per ulteriori informazioni, consulta la guida su [monitoraggio dei segmenti nell’interfaccia utente](../../dataflows/ui/monitor-segments.md) |

Per informazioni più generali sui flussi di dati, consulta [panoramica dei dataflows](../../dataflows/home.md). Per ulteriori informazioni sulla segmentazione, consulta la sezione [panoramica sulla segmentazione](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l&#39;origine Adobe Analytics | L’origine Adobe Analytics ora supporta le funzioni di preparazione dei dati, che consentono di mappare i dati della suite di rapporti di Analytics su uno schema XDM di destinazione durante la creazione di un flusso di dati. Guarda l’esercitazione su [creazione di una connessione sorgente Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) per ulteriori informazioni. |
| Supporto per l&#39;importazione di regole di mappatura esistenti | Ora puoi importare le regole di mappatura da un flusso di dati esistente per accelerare le configurazioni del flusso di dati e limitare gli errori. Guarda l’esercitazione su [importazione di regole di mappatura esistenti](../../data-prep/ui/mapping.md) per ulteriori informazioni. |

Per ulteriori informazioni su [!DNL Data Prep], vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ----------- | ----------- |
| Connettori di destinazione aziendali avanzati | Sono ora disponibili in genere tre connettori di destinazione aziendali: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)e [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> La disponibilità generale dei connettori di destinazione aziendali include tutte le funzionalità offerte in precedenza nella fase Beta e altro ancora: <ul><li>Nuove funzionalità di autenticazione, tra cui [Firma di accesso condiviso negli hub eventi di Azure](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) e altro [tipi di autenticazione](../../destinations/catalog/streaming/http-destination.md#authentication-information) (token portatori, OAuth 2) nella destinazione API HTTP;</li><li>[Backfill dei dati del profilo storico](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (invio di profili storici qualificati per il segmento quando è stato attivato per la prima volta);</li><li>Le metriche delle esecuzioni dei flussi di dati sono ora supportate per queste destinazioni;</li><li>[Metadati dei segmenti aggiuntivi](../../destinations/catalog/streaming/http-destination.md#destination-details) inclusi nel payload dei dati, compresi i nomi dei segmenti e le marche temporali dei segmenti;</li><li>Supporto per [indirizzi IP statici](/help/destinations/catalog/streaming/ip-address-allow-list.md) per i clienti che devono inserire nell&#39;elenco Consentiti Experience Platform.</li></ul> |
| Avvisi contestuali per i flussi di dati di destinazione | Ora puoi [effettuare la sottoscrizione agli avvisi](../../destinations/ui/alerts.md) durante la creazione di un flusso di dati di destinazione, per ricevere messaggi di avviso relativi allo stato, al successo o all’errore dell’esecuzione del flusso di dati. Puoi scegliere di ricevere avvisi nell’interfaccia utente di Experience Platform o tramite e-mail. |

### Processo di rilascio per i connettori di destinazione aziendali avanzati {#release-process-enterprise-destinations}

Per le destinazioni Amazon Kinesis, Azure Event Hubs e HTTP API, durante il processo di rilascio (a partire dal 27 aprile), vedrai sia la precedente scheda di destinazione Beta, sia la nuova scheda di destinazione generalmente disponibile (GA) nel catalogo delle destinazioni. Eventuali flussi di dati configurati dai clienti che utilizzano le destinazioni beta verranno migrati nei successivi due giorni alla versione GA della stessa destinazione. La migrazione dovrebbe essere completata entro la fine del giorno di venerdì 29 aprile. Le destinazioni Beta continueranno a essere visibili durante questa breve finestra e saranno etichettate come **Obsoleto**.

Se utilizzi queste destinazioni nella fase Beta, tieni presente quanto segue:

- Se in precedenza era presente in Beta con una qualsiasi delle 3 destinazioni, non è necessaria alcuna azione. Tutti i flussi di dati configurati come parte di Beta continueranno a funzionare e verranno migrati alla versione GA.
- Se desideri impostare queste destinazioni a partire dal 27 aprile, effettua questa operazione con la nuova versione GA delle destinazioni.
- Le schede beta contrassegnate come obsolete verranno rimosse al termine dell’operazione di rilascio, stimato entro la fine del giorno venerdì 29 aprile. Il team di progettazione di Experience Platform sta monitorando da vicino l&#39;esito di un&#39;operazione di rilascio riuscita.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [!DNL Criteo] | Collegare e attivare i dati al [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) piattaforma pubblicitaria. |
| [!DNL Sendgrid] | Collegare e attivare i dati al [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) piattaforma per le e-mail transazionali e di marketing. |

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Aggiunta o rimozione di singoli campi standard per uno schema | L’interfaccia utente dell’Editor di schema ora consente di aggiungere parti di gruppi di campi standard agli schemi, fornendo maggiore flessibilità per i campi che si sceglie di includere senza dover creare risorse personalizzate da zero.<br><br>È ora inoltre possibile definire campi personalizzati ad hoc direttamente all’interno della struttura dello schema e assegnarli a un gruppo di campi personalizzato nuovo o esistente senza dover prima creare o modificare il gruppo di campi.<br><br>Consulta la guida su [creazione e modifica di schemi nell’interfaccia utente](../../xdm/ui/resources/schemas.md) per ulteriori informazioni su questi nuovi flussi di lavoro. |

{style=&quot;table-layout:auto&quot;}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Schema globale | [[!UICONTROL Richiesta di funzionamento dell&#39;igiene dei dati]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Acquisisce i dettagli di una richiesta di pulizia dei dati per eliminare o modificare i record in un set di dati o sandbox specifico. |
| Descrittore | [[!UICONTROL Descrittore di granularità della serie temporale]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indica la granularità delle serie temporali e dei dati di riepilogo. Quando viene applicato a uno schema, la proprietà `timestamp` è la prima marca temporale in un periodo di questa granularità. |
| Classe | [[!UICONTROL Metriche di riepilogo XDM]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Fornisce metriche pre-riepilogate con dimensioni di raggruppamento, ad esempio i risultati di un SQL SELECT con un GROUP BY. |
| Gruppo di campi | [[!UICONTROL Mappa dei risultati della valutazione delle politiche di consenso]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | Acquisisce il risultato della valutazione dei criteri di consenso per un singolo utente. |
| Gruppo di campi | [[!UICONTROL Ricerca nel sito]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Acquisisce informazioni correlate alla ricerca del sito quali query di ricerca, filtri e ordine. |
| Gruppo di campi | [[!UICONTROL Unisci lead]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Acquisisce i dettagli di un evento in cui vengono uniti due o più lead. |
| Gruppo di campi | [[!UICONTROL Invia e-mail]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Acquisisce i dettagli di un evento in cui viene inviato un messaggio e-mail a un destinatario. |
| Gruppo di campi | [[!UICONTROL Unione di campi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Acquisisce i valori calcolati attraverso il processo di unione delle identità per un evento. |
| Gruppo di campi | [[!UICONTROL Dettagli Destinatario Secondario Per L&#39;Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Un gruppo di campi Adobe Journey Optimizer che acquisisce i dettagli di un destinatario secondario per un controllo di audit. |
| Gruppo di campi | [[!UICONTROL Dettagli sulle relazioni personali dell&#39;account aziendale XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Acquisisce i dettagli relativi a una relazione account-persona. |
| Gruppo di campi | [[!UICONTROL Dettagli persona account]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Acquisisce i dettagli relativi a una relazione account-persona. |
| Tipo di dati | [[!UICONTROL Carrello]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Acquisisce informazioni su un carrello acquisti per e-commerce. |
| Tipo di dati | [[!UICONTROL Spedizione]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Acquisisce le informazioni di spedizione per uno o più prodotti. |
| Tipo di dati | [[!UICONTROL Ricerca nel sito]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | Acquisisce informazioni sulle attività di ricerca nel sito. |
| Estensione (Workfront) | [[!UICONTROL Attributi delle attività operative]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Acquisisce i dettagli relativi a un&#39;attività operativa. |
| Estensione (Workfront) | [[!UICONTROL Attributi del Portfolio di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Acquisisce i dettagli relativi a un portafoglio di lavoro. |
| Estensione (Workfront) | [[!UICONTROL Attributi del programma di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Acquisisce i dettagli relativi a un programma di lavoro. |
| Estensione (Workfront) | [[!UICONTROL Attributi del progetto di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Acquisisce i dettagli relativi a un progetto di lavoro. |

{style=&quot;table-layout:auto&quot;}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione aggiornamento |
| --- | --- | --- |
| Schema globale | [[!UICONTROL Destinazioni ]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nuovi valori enum per `destinationCategory`. |
| Descrittore | [[!UICONTROL Descrittore di nome descrittivo]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | È stato aggiunto il supporto per la rimozione dei valori suggeriti (`meta:enum`) non necessarie nei campi standard. |
| Gruppo di campi | [[!UICONTROL Processo di accesso utente]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` campo aggiunto. |
| Tipo di dati | [[!UICONTROL Commercio]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Sono stati aggiunti diversi campi relativi al carrello. |
| Tipo di dati | [[!UICONTROL Voce dell’elenco dei prodotti]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Nuovi campi aggiunti per le opzioni selezionate e l’importo dello sconto. |
| Estensione (Intelligent Services) | [[!UICONTROL Ottimizzazione dei tempi di invio di JourneyAI Intelligent Services]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Ottimizza il formato di archiviazione per i punteggi del tempo di invio. |
| Estensione (Workfront) | [[!UICONTROL Evento di modifica Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Diversi campi sono stati sostituiti da un `workfront:customData` campo per campi modulo personalizzati. |
| Estensione (Workfront) | [[!UICONTROL Attributi attività di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Sono stati aggiunti diversi campi. |
| Estensione (Workfront) | [[!UICONTROL Oggetto di lavoro]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nuovi campi per il tipo di oggetto principale e i campi modulo personalizzati. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

I servizi AI/ML consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi d’uso della customer experience. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science.

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per set di dati multipli | La funzione Set di dati multipli supporta ora tutti i set di dati Experience Event e la selezione di Identity Map come identità. I clienti possono selezionare la mappa di identità ed eventuali ID associati, purché nei set di dati sia presente uno spazio dei nomi di identità comune. Attribution AI supporta i seguenti schemi: Adobe Analytics, Evento Di Esperienza, Evento Di Esperienza Del Consumatore. Per ulteriori informazioni sul supporto di più set di dati in Attribution AI, consulta la sezione [Guida utente di Attribution AI](../../intelligent-services/attribution-ai/user-guide.md). |

Per ulteriori informazioni su [!DNL Intelligent Services], vedi [[!DNL Intelligent Services] panoramica](../../intelligent-services/home.md).

### Customer AI

Customer AI disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di machine learning né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per set di dati multipli | La funzione Set di dati multipli supporta ora tutti i set di dati Experience Event e la selezione di Identity Map come identità. I clienti possono selezionare la mappa di identità ed eventuali ID associati, purché nei set di dati sia presente uno spazio dei nomi di identità comune. Customer AI supporta i seguenti schemi: Adobe Analytics, Experience Event, Consumer Experience Event e lo schema Adobe Audience Manager. Per ulteriori informazioni sul supporto di più set di dati in Customer AI, consulta [Guida utente di Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Nuove metriche di valutazione del modello in Customer AI | I nuovi grafici Gain in Customer AI consentono agli esperti di marketing di determinare le dimensioni del gruppo di destinazione in base ai loro obiettivi di budget e ROI. I nuovi grafici di incremento misurano la qualità del modello, fornendo una migliore visibilità nell’incremento che otterrebbero con il targeting casuale. Per ulteriori informazioni, consulta la sezione [scoprire informazioni approfondite con Customer AI](../../intelligent-services/customer-ai/user-guide/discover-insights.md) documento. |

Per ulteriori informazioni su [!DNL Intelligent Services], vedi [[!DNL Intelligent Services] panoramica](../../intelligent-services/home.md).

## Edizione B2B di Real-Time Customer Data Platform {#B2B}

Basato su Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition è progettato appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Riunisce i dati provenienti da più sorgenti e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli esperti di marketing di eseguire il targeting preciso di tipi di pubblico specifici e coinvolgerli in tutti i canali disponibili.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per `isDeleted` funzionalità | Tutto [!DNL Marketo] set di dati eccetto `Activities` ora supporta `isDeleted` mappatura. La nuova mappatura viene aggiunta automaticamente ai flussi di dati B2B esistenti. È possibile utilizzare `isDeleted` mappatura per filtrare i record eliminati in modo che i dati nella [!DNL Data Lake] è coerente con i dati di origine. Consulta la sezione [[!DNL Marketo] guida alla mappatura dei campi](../../sources/connectors/adobe-applications/mapping/marketo.md) per ulteriori informazioni su `isDeleted`. |

Per ulteriori informazioni su Real-time Customer Data Platform B2B Edition, consulta la sezione [Panoramica B2B](../../rtcdp/b2b-overview.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per [!DNL OneTrust Integration] | Ora puoi utilizzare la [!DNL OneTrust Integration] sorgente per acquisire i dati di consenso e preferenze dal tuo [!DNL OneTrust] a Platform. Consulta la documentazione su [creazione di un [!DNL OneTrust Integration] connessione sorgente](../../sources/connectors/consent-and-preferences/onetrust.md) per ulteriori informazioni. |
| Supporto per [!DNL Square] | Ora puoi utilizzare la [!DNL Square] origine per acquisire i dati di pagamento dal [!DNL Square] a Platform. |
| Supporto per l&#39;eliminazione dei flussi di dati Attributi del cliente | È ora possibile eliminare i flussi di dati creati con il connettore di origine Attributi del cliente. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
