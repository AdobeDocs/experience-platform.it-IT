---
title: Note sulla versione di Adobe Experience Platform, marzo 2023
description: Note sulla versione di marzo 2023 per Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2206'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 29 marzo 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Dashboard](#dashboards)
- [Raccolta dati](#data-collection)
- [Preparazione dei dati](#data-prep)
- [Destinazioni](#destinations)
- [Experience Data Model](#xdm)
- [Servizio query](#query-service)
- [Edizione B2B di Real-Time Customer Data Platform](#b2b)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Dashboard {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso i quali è possibile visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

**Funzioni nuove o aggiornate** {#dashboards-new-updated-features}

| Funzione | Descrizione |
| --- | --- |
| Dashboard definiti dall&#39;utente | Ora puoi **valori attributo di esempio** prima di aggiungere un attributo a un widget nel compositore widget dashboard definito dall&#39;utente. Durante la creazione di un widget, sono disponibili alcuni valori di esempio per i singoli attributi della colonna di attributi.<br>Ora puoi **scambiare gli assi X e Y** sul widget con il pulsante scambia asse. Questo consente di risparmiare tempo e offre un&#39;esperienza più ergonomica quando si aggiungono attributi ai widget. In questo modo si evita la necessità di trovare nuovamente entrambi gli attributi dal pannello attributi.<br> Ora puoi **modificare la posizione e il titolo della legenda** nei widget. Una volta che una legenda è presente in un widget, è possibile riposizionarla in qualsiasi punto del grafico e rinominare il titolo della legenda, come è possibile fare con le etichette degli assi e il titolo del widget. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, leggi [panoramica delle dashboard](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuovo flusso di lavoro con avvio rapido per l’API di conversione metadati (Beta) | Accedi ai nuovi flussi di lavoro di avvio rapido in &quot;Guida introduttiva&quot; dalla schermata iniziale di Data Collection. Il [flusso di lavoro di avvio rapido per l’API Meta Conversions](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) consente ai clienti di raccogliere e inoltrare rapidamente i dati dell’evento, lato server a Meta, per le conversioni di annunci in pochi semplici passaggi. |
| Nuovo flusso di lavoro di avvio rapido per Mobile SDK (Beta) | Accedi ai nuovi flussi di lavoro di avvio rapido in &quot;Guida introduttiva&quot; dalla schermata iniziale di Data Collection. Il [flusso di lavoro di avvio rapido per Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) consente di implementare rapidamente l’SDK di Mobile e di convalidare gli eventi mobili di base in pochi semplici passaggi. |
| [!DNL Braze] estensione di inoltro eventi | Il [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) l’estensione per l’inoltro degli eventi consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e di inviarli a [!DNL Braze] sotto forma di eventi lato server che utilizzano [!DNL Braze] API User Track. |
| [!DNL Epsilon] estensione di inoltro eventi | Il [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) consente di sfruttare l’inoltro degli eventi per acquisire informazioni sugli eventi in Adobe Experience Platform Edge Network e inviarle a [!DNL Epsilon] utilizzando [!DNL Epsilon] API evento. |
| [!DNL Mixpanel] estensione di inoltro eventi | Il [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) L’estensione consente ai clienti di sfruttare l’inoltro degli eventi per acquisire informazioni sugli eventi in Adobe Experience Platform Edge Network e inviarle a Mixpanel utilizzando l’API Track Events. |

{style="table-layout:auto"}

## Preparazione dei dati {#data-prep}

La preparazione dati consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale del filtro per i dati di Adobe Analytics | Ora puoi utilizzare le funzionalità di preparazione dati per applicare regole e condizioni per filtrare i dati di Analytics prima di acquisirli in Real-Time Customer Profile. Per ulteriori informazioni, consulta la guida su [filtraggio dei dati di Analytics per l’acquisizione del profilo](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nuove funzioni per la codifica e la decodifica delle stringhe URL | <ul><li>Il `get_url_encoded` La funzione accetta un URL come input e sostituisce o codifica caratteri speciali con caratteri ASCII.</li><li>Il `get_url_decoded` La funzione accetta un URL come input e decodifica i caratteri ASCII in caratteri speciali.</li></ul> Per ulteriori informazioni, leggere [Guida alle funzioni della preparazione dati](../../data-prep/functions.md). Per un elenco completo dei caratteri riservati e dei caratteri codificati corrispondenti, leggere la guida in linea [caratteri speciali](../../data-prep/functions.md#special-characters). |

Per ulteriori informazioni sulla preparazione dati, consulta [Panoramica sulla preparazione dati](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni** {#new-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] connessione GA](../../destinations/catalog/personalization/adobe-commerce.md) | Il [!DNL Adobe Commerce] il connettore di destinazione (ora generalmente disponibile) consente di selezionare uno o più tipi di pubblico Real-Time CDP da attivare nel [!DNL Adobe Commerce] per offrire agli acquirenti un&#39;esperienza dinamica e personalizzata. |
| [[!DNL Snap Inc] connessione GA](../../destinations/catalog/advertising/snap-inc.md) | Il [!DNL Snap Inc] il connettore di destinazione (ora generalmente disponibile) consente agli addetti al marketing di importare in i segmenti utente creati in Experience Platform [!DNL Snapchat Ads] e utilizzarli per eseguire il targeting dei loro annunci. |
| [(API) Connessione Eloqua Oracle](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Utilizzare la connessione basata su API per [!DNL Oracle Eloqua] pianificare ed eseguire campagne offrendo al tempo stesso un’esperienza cliente personalizzata per i potenziali clienti in [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] connessione](../../destinations/catalog/advertising/amazon-ads.md) | Il [!DNL Amazon Ads] integrazione con Adobe Experience Platform fornisce integrazione chiavi in mano a [!DNL Amazon Ads] prodotti, tra cui [!DNL Amazon DSP (ADSP)]. Utilizzo di [!DNL Amazon Ads] destinazione in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l’attivazione sul [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] connessione](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (precedentemente Bizible) offre agli esperti di marketing informazioni sulle attività di marketing più efficaci per incrementare le entrate e massimizzare il ritorno sull’investimento. La destinazione consente il flusso di dati business-to-business (B2B) da Adobe Experience Platform a [!DNL Marketo Measure]. La scheda è disponibile solo per [!DNL Marketo Measure Ultimate] clienti. |
| [Connessione TikTok](../../destinations/catalog/social/tiktok.md) | Crea tipi di pubblico personalizzati su TikTok con i tuoi dati per il targeting con le campagne pubblicitarie. |
| [Connessione Zendesk](../../destinations/catalog/crm/zendesk.md) | Utilizza questa destinazione per creare e aggiornare le identità all’interno di un segmento come contatti in [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Nuova autorizzazione di controllo degli accessi per le destinazioni: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | La nuova autorizzazione consente agli utenti di attivare i segmenti nelle destinazioni esistenti, senza visualizzare [passaggio di mappatura](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Gli utenti possono aggiungere e rimuovere segmenti nei flussi di lavoro di attivazione, ma non possono aggiungere o rimuovere attributi o identità mappati. |

{style="table-layout:auto"}

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

Stiamo rilasciando una correzione di bug per la crittografia PGP/GPG nelle destinazioni basate su file per Real-time CDP. Con questa modifica, le destinazioni esistenti basate su file che attualmente utilizzano la crittografia genereranno un nome file con un’estensione diversa da quella precedente.

- Estensione corrente quando si utilizza la crittografia: `filename.csv`
- Estensione futura quando si utilizza la crittografia: `filename.csv.gpg`

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Consigli da CSV a schema | Ora puoi caricare i file locali per creare schemi generati dall’apprendimento automatico che eliminano la necessità di creare manualmente uno schema. Dalla sezione [!UICONTROL Sorgenti] Workspace, carica un file CSV di esempio e gli algoritmi di machine learning di Adobe ti suggeriranno uno schema basato sui campi di destinazione. Per ulteriori informazioni, consulta la [documentazione](../../ingestion/tutorials/map-csv/recommendations.md) dello strumento.&quot; |

{style="table-layout:auto"}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Elemento offerta]](https://github.com/adobe/xdm/pull/1678/files) | Classe che rappresenta un’offerta. |
| Classe | [[!UICONTROL Elemento decisione]](https://github.com/adobe/xdm/pull/1678/files) | Un elemento che può essere soggetto a decisioni. L’output di un processo decisionale è uno o più elementi decisionali. |
| Classe | [[!UICONTROL Timeout del server della sessione multimediale]](https://github.com/adobe/xdm/pull/1676/files) | Indica il tempo, in secondi, trascorso tra l’ultima interazione nota dell’utente e il momento in cui la sessione è stata chiusa. |
| Gruppo di campi | [[!UICONTROL Attributi calcolati del profilo XDM]](https://github.com/adobe/xdm/pull/1686/files) | Questo aggiunge attributi calcolati dai servizi interni di Adobe ai dati dei clienti in arrivo. I clienti non devono utilizzarlo per acquisire i dati. |
| Tipo di dati | [[!UICONTROL Rimborso articolo]](https://github.com/adobe/xdm/pull/1685/files) | Indica se un rimborso è associato a un ordine e definisce il tipo di rimborso, l&#39;importo e la valuta associata. |
| Tipo di dati | [[!UICONTROL Dati categoria]](https://github.com/adobe/xdm/pull/1677/files) | Questo nuovo tipo di dati rappresenta la categoria di un prodotto. |
| Schema | [[!UICONTROL Campi di classificazione Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | È stato creato un nuovo schema XDM per i set di dati di classificazione di Target. Contiene un set di campi di metadati che classificano le attività ed esperienze Target. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Dettagli dei componenti di contenuto]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` è stato rimosso da [!UICONTROL Dettagli dei componenti di contenuto] |
| Gruppo di campi | [[!UICONTROL Tag di entità AJO]](https://github.com/adobe/xdm/pull/1672/files) | Sono stati aggiunti tag di entità AJO a [!UICONTROL Campi entità AJO], che corrispondono a un Percorso o a una campagna |
| Gruppo di campi | (Multiplo) | Sono stati aggiunti diversi campi per [[!UICONTROL Campi comuni evento passaggio Journey Orchestration]](https://github.com/adobe/xdm/pull/1671/files) |
| Gruppo di campi | (Multiplo) | [Sono stati aggiunti diversi tipi di evento XDM per [!UICONTROL Reporting sui contenuti multimediali]](https://github.com/adobe/xdm/pull/1670/files). |
| Gruppo di campi | [!UICONTROL Evento modifica Workfront] | Il `Full Record` e `Accessor Employee Ids` sono stati aggiunti gruppi di campi. |
| Tipo di dati | [[!UICONTROL Elemento dell’elenco prodotti]](https://github.com/adobe/xdm/pull/1685/files) | Il [!UICONTROL Importo rimborso] è stato aggiunto per indicare l&#39;importo rimborsato per l&#39;articolo, se presente. |
| Tipo di dati | [[!UICONTROL Ordine ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Elenco rimborsi] è stato aggiunto all&#39;elenco dei rimborsi per questo ordine. |
| Tipo di dati | [[!UICONTROL Elemento elenco prodotti ]](https://github.com/adobe/xdm/pull/1677/files) | Le categorie di prodotti sono state aggiunte all’elenco dei dati delle categorie di questo prodotto. |
| Tipo di dati | [!UICONTROL Informazioni sui dettagli della sessione] | È stata aggiunta la `pev3` campo stringa che [indica il tipo di flusso multimediale utilizzato per il reporting](https://github.com/adobe/xdm/pull/1676/files). È stata aggiunta anche la sezione `pccr` indica se si è verificato un reindirizzamento. |
| Tipo di dati | [!UICONTROL Elenco richieste] | Fornisce [proprietà elenco richieste di acquisto](https://github.com/adobe/xdm/pull/1675/files). Includono nome, ID e descrizione. |
| Tipo di dati | [!UICONTROL Commerce] | Il [Il tipo di dati Commerce è stato aggiornato](https://github.com/adobe/xdm/pull/1675/files) da includere `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`, e `requisitionList`. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta [Panoramica del sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal data lake e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire in Real-Time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Controllo dell’accesso basato su attributi nell’archivio accelerato | Utilizza il controllo degli accessi basato su attributi con Data Distiller per definire il controllo degli accessi su tutti i set di dati nell’archivio accelerato. Questo consente di controllare l’accesso ai modelli di dati personalizzati creati dagli utenti e memorizzati in un archivio accelerato per abilitare i dashboard personalizzati. |

{style="table-layout:auto"}

Per ulteriori informazioni su Query Services, consulta [Panoramica di Query Service](../../query-service/home.md).

## Edizione B2B di Real-Time Customer Data Platform {#b2b}

Basata su Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition è progettata appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli addetti al marketing di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Bugfix | Per fornire una rappresentazione più precisa dei profili nel sistema, il sistema non include più i profili interni nel conteggio totale dei profili o nella metrica del pubblico indirizzabile per la versione B2B di Real-time Customer Data Platform. A partire da oggi, potrebbe verificarsi un calo una tantum nel conteggio totale dei profili/metrica del pubblico indirizzabile. Nessuno dei dati è stato cancellato, si tratta semplicemente di una modifica al conteggio. Contatta il tuo responsabile Adobe per eventuali dubbi |

{style="table-layout:auto"}

Per ulteriori informazioni sulla versione B2B di Real-Time CDP, leggere [Panoramica dell’edizione B2B di Real-Time CDP](../../rtcdp/overview.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo commerciabile di persone all’interno della tua base clienti. I segmenti possono essere basati su dati record (ad esempio informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Metriche del profilo | Per ottenere una rappresentazione più precisa delle metriche del profilo, vengono combinate le metriche di suddivisione delle appartenenze e di abbandono e vengono ora calcolate in un periodo di 24 ore. Ulteriori informazioni sono disponibili nel [Guida all’interfaccia utente Segmentazione](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consultare il [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità beta di [!DNL Chatlio] | Il [!DNL Chatlio] Il codice sorgente è ora disponibile in versione beta. Utilizza il [!DNL Chatlio] origine per lo streaming [!DNL Chatlio] dati degli eventi di cui eseguire l’Experience Platform. Per ulteriori informazioni, leggere [[!DNL Chatlio] panoramica](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilità beta di [!DNL Customer.io] | Il [!DNL Customer.io] Il codice sorgente è ora disponibile in versione beta. Utilizza il [!DNL Customer.io] origine per inviare in streaming i dati degli eventi cliente ad Experience Platform. Per ulteriori informazioni, leggere [[!DNL Customer.io] panoramica](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilità beta di [!DNL Pendo] | Il [!DNL Pendo] Il codice sorgente è ora disponibile in versione beta. Utilizza il [!DNL Pendo] origine per lo streaming dei dati di analisi dei prodotti su Experience Platform. Per ulteriori informazioni, leggere [[!DNL Pendo] panoramica](../../sources/connectors/analytics/pendo-webhook.md). |
| Supporto per flussi di dati di bozza | Ora puoi utilizzare l’API del servizio Flusso per impostare i flussi di dati su uno stato di bozza. I flussi di dati redatti possono essere successivamente aggiornati e pubblicati con nuove informazioni. Per ulteriori informazioni, consulta la guida su [impostazione dei flussi di dati di origine come bozze](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere [panoramica sulle origini](../../sources/home.md).
