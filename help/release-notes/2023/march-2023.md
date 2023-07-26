---
title: Note sulla versione di Adobe Experience Platform - Marzo 2023
description: Note sulla versione di Adobe Experience Platform di marzo 2023.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '2206'
ht-degree: 100%

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

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate** {#dashboards-new-updated-features}

| Funzione | Descrizione |
| --- | --- |
| Dashboard definite dall’utente | Ora puoi **campionare i valori di attributo** prima di aggiungere un attributo a un widget nel compositore widget della dashboard definito dall’utente. Durante la creazione di un widget, sono disponibili alcuni valori campione per i singoli attributi della colonna di attributi.<br>Ora puoi **scambiare gli assi X e Y** sul widget con il pulsante scambia asse. Questo consente di risparmiare tempo e offre un’esperienza più ergonomica quando si aggiungono attributi ai widget. In questo modo si evita la necessità di trovare nuovamente entrambi gli attributi dal pannello attributi.<br>Ora puoi **modificare la posizione e il titolo della legenda** nei widget. Una volta che una legenda è presente in un widget, è possibile riposizionarla in qualsiasi punto del grafico e rinominare il titolo della legenda, allo stesso modo delle etichette degli assi e il titolo del widget. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuovo flusso di lavoro con avvio rapido per l’API Conversions di Meta (Beta) | Accedi ai nuovi flussi di lavoro di avvio rapido nella “Guida introduttiva” dalla schermata iniziale della Raccolta dati. Il [flusso di lavoro di avvio rapido per l’API Conversions di Meta](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=it#quick-start) consente alla clientela di raccogliere e inoltrare rapidamente a Meta i dati dell’evento lato server per le conversioni di annunci in alcuni semplici passaggi. |
| Nuovo flusso di lavoro di avvio rapido per l’SDK Mobile (Beta) | Accedi ai nuovi flussi di lavoro di avvio rapido nella “Guida introduttiva” dalla schermata iniziale della Raccolta dati. Il [flusso di lavoro di avvio rapido per l’SDK Mobile](https://developer.adobe.com/client-sdks/documentation/) consente di implementare rapidamente l’SDK Mobile e di convalidare gli eventi mobili di base in pochi semplici passaggi. |
| Estensione [!DNL Braze] per l’inoltro degli eventi | L’estensione [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) per l’inoltro degli eventi consente di sfruttare i dati acquisiti nella rete Edge di Adobe Experience Platform e di inviarli a [!DNL Braze] in forma di eventi lato server che utilizzano le API User Track di [!DNL Braze]. |
| Estensione [!DNL Epsilon] per l’inoltro degli eventi | L’estensione [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html?lang=it) consente di sfruttare l’inoltro degli eventi per acquisire informazioni sugli eventi nella rete Edge di Adobe Experience Platform e inviarle a [!DNL Epsilon] utilizzando l’API dell’evento di [!DNL Epsilon]. |
| Estensione [!DNL Mixpanel] per l’inoltro degli eventi | L’estensione [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=it) consente ai clienti di sfruttare l’inoltro degli eventi per acquisire informazioni sugli eventi nella rete Edge di Adobe Experience Platform e inviarle a Mixpanel utilizzando l’API Track Events. |

{style="table-layout:auto"}

## Preparazione dei dati {#data-prep}

La preparazione dei dati consente ai data engineer di mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale del filtro per i dati di Adobe Analytics | Ora puoi utilizzare le funzionalità di preparazione dei dati per applicare regole e condizioni per filtrare i dati di analisi prima di acquisirli nel profilo cliente in tempo reale. Per ulteriori informazioni, consulta la guida sul [filtro dei dati di Analytics per l’acquisizione del profilo](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nuove funzioni per la codifica e la decodifica delle stringhe URL | <ul><li>La funzione `get_url_encoded` accetta un URL come input e sostituisce o codifica i caratteri speciali con caratteri ASCII.</li><li>La funzione `get_url_decoded` accetta un URL come input e decodifica i caratteri ASCII in caratteri speciali.</li></ul> Per ulteriori informazioni, consulta la [Guida alle funzioni della preparazione dei dati](../../data-prep/functions.md). Per un elenco completo dei caratteri riservati e dei caratteri codificati corrispondenti, consulta la guida sui [caratteri speciali](../../data-prep/functions.md#special-characters). |

Per ulteriori informazioni sulla preparazione dei dati, consulta [Panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni** {#new-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] connessione GA](../../destinations/catalog/personalization/adobe-commerce.md) | Il connettore di destinazione [!DNL Adobe Commerce] (ora generalmente disponibile) consente di selezionare uno o più tipi di pubblico Real-Time CDP da attivare nell’account [!DNL Adobe Commerce] per offrire agli acquirenti un’esperienza dinamica e personalizzata. |
| [[!DNL Snap Inc] connessione GA](../../destinations/catalog/advertising/snap-inc.md) | Il connettore di destinazione [!DNL Snap Inc] (ora generalmente disponibile) consente ai marketer di importare i segmenti utente creati in Experience Platform in [!DNL Snapchat Ads] e utilizzarli per eseguire il targeting dei loro annunci. |
| [Connessione Eloqua Oracle (API)](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Utilizza la connessione [!DNL Oracle Eloqua] basata su API per pianificare ed eseguire campagne offrendo un’esperienza personalizzata per i potenziali clienti in [!DNL Oracle Eloqua]. |
|  [!DNL Amazon Ads] connessione](../../destinations/catalog/advertising/amazon-ads.md)[(Beta) | L’integrazione di [!DNL Amazon Ads] con Adobe Experience Platform fornisce integrazione diretta con i prodotti di [!DNL Amazon Ads], tra cui [!DNL Amazon DSP (ADSP)]. Utilizzando la destinazione [!DNL Amazon Ads] in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l’attivazione su [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] connessione](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (precedentemente Bizible) offre ai marketer approfondimenti sulle iniziative di marketing più efficaci per aumentare i ricavi e ottimizzare il ritorno sull’investimento per l’azienda. La destinazione consente il flusso di dati business-to-business (B2B) da Adobe Experience Platform a [!DNL Marketo Measure]. La scheda è disponibile solo per la clientela di [!DNL Marketo Measure Ultimate]. |
| [Connessione TikTok](../../destinations/catalog/social/tiktok.md) | Crea tipi di pubblico personalizzati su TikTok con i tuoi dati per il targeting con le campagne pubblicitarie. |
| [Connessione Zendesk](../../destinations/catalog/crm/zendesk.md) | Utilizza questa destinazione per creare e aggiornare le identità all’interno di un segmento come contatti in [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Nuova autorizzazione di controllo degli accessi per le destinazioni: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | La nuova autorizzazione consente agli utenti di attivare i segmenti nelle destinazioni esistenti, senza visualizzare il [passaggio di mappatura](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Gli utenti possono aggiungere e rimuovere segmenti nei flussi di lavoro di attivazione, ma non possono aggiungere o rimuovere gli attributi o le identità mappate. |

{style="table-layout:auto"}

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

Stiamo rilasciando una correzione di bug per la crittografia PGP/GPG nelle destinazioni basate su file per Real-time CDP. Con questa modifica, le destinazioni esistenti basate su file che attualmente utilizzano la crittografia genereranno un nome file con un’estensione diversa da quella precedente.

- Estensione corrente quando si utilizza la crittografia: `filename.csv`
- Estensione futura quando si utilizza la crittografia: `filename.csv.gpg`

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Consiglio da CSV a schema | Ora puoi caricare i file locali per creare schemi generati dall’apprendimento automatico che eliminano la necessità di creare manualmente uno schema. Dall’area di lavoro [!UICONTROL Origini], carica un file CSV di esempio e gli algoritmi di apprendimento automatico di Adobe ti suggeriranno uno schema basato sui campi di destinazione. Per ulteriori informazioni, consulta la [documentazione](../../ingestion/tutorials/map-csv/recommendations.md).” |

{style="table-layout:auto"}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Elemento offerta]](https://github.com/adobe/xdm/pull/1678/files) | Classe che rappresenta un’offerta. |
| Classe | [[!UICONTROL Elemento decisione]](https://github.com/adobe/xdm/pull/1678/files) | Un elemento che può essere soggetto a decisioning. L’output di un processo di decisioning è uno o più elementi decisionali. |
| Classe | [[!UICONTROL Timeout del server della sessione multimediale]](https://github.com/adobe/xdm/pull/1676/files) | Indica il tempo, in secondi, trascorso tra l’ultima interazione nota dell’utente e il momento in cui la sessione è stata chiusa. |
| Gruppo di campi | [[!UICONTROL Attributi calcolati del profilo XDM]](https://github.com/adobe/xdm/pull/1686/files) | Questo aggiunge attributi calcolati dai servizi interni di Adobe ai dati della clientela in arrivo. La clientela non deve utilizzarlo per acquisire i dati. |
| Tipo di dati | [[!UICONTROL Elemento rimborso]](https://github.com/adobe/xdm/pull/1685/files) | Indica se un rimborso è associato a un ordine e ne definisce il tipo, l’importo e la valuta associata. |
| Tipo di dati | [[!UICONTROL Dati categoria]](https://github.com/adobe/xdm/pull/1677/files) | Questo nuovo tipo di dati rappresenta la categoria di un prodotto. |
| Schema | [[!UICONTROL Campi di classificazione di Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | È stato creato un nuovo schema XDM per i set di dati di classificazione di Target. Contiene un set di campi di metadati che classificano le attività ed esperienze di Target. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Dettagli del componente di contenuto]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` è stato rimosso dai [!UICONTROL Dettagli del componente di contenuto] |
| Gruppo di campi | [[!UICONTROL Tag di entità AJO]](https://github.com/adobe/xdm/pull/1672/files) | Sono stati aggiunti tag di entità AJO ai [!UICONTROL Campi entità AJO] che corrispondono a un percorso o a una campagna |
| Gruppo di campi | (Multiplo) | Sono stati aggiunti diversi campi per i [[!UICONTROL Campi comuni dell’evento passaggio di Journey Orchestration]](https://github.com/adobe/xdm/pull/1671/files) |
| Gruppo di campi | (Multiplo) | [Sono stati aggiunti diversi tipi di evento XDM per il [!UICONTROL Reporting sui file multimediali]](https://github.com/adobe/xdm/pull/1670/files). |
| Gruppo di campi | [!UICONTROL Evento modifica di Workfront] | Sono stati aggiunti i gruppi di campo `Full Record` e `Accessor Employee Ids`. |
| Tipo di dati | [[!UICONTROL Elemento dell’elenco prodotti]](https://github.com/adobe/xdm/pull/1685/files) | L’[!UICONTROL Importo del rimborso] è stato aggiunto per indicare l’importo rimborsato per l’elemento, se presente. |
| Tipo di dati | [[!UICONTROL Ordine ]](https://github.com/adobe/xdm/pull/1685/files) | L’[!UICONTROL Elenco rimborsi] è stato aggiunto all’elenco dei rimborsi per questo ordine. |
| Tipo di dati | [[!UICONTROL Elemento elenco prodotti ]](https://github.com/adobe/xdm/pull/1677/files) | Le categorie di prodotti sono state aggiunte all’elenco dei dati delle categorie di questo prodotto. |
| Tipo di dati | [!UICONTROL Informazioni sui dettagli della sessione] | È stato aggiunto il campo stringa `pev3` che [indica il tipo di flusso multimediale utilizzato per il reporting](https://github.com/adobe/xdm/pull/1676/files). È stata aggiunta anche la proprietà `pccr` che indica se si è verificato un reindirizzamento. |
| Tipo di dati | [!UICONTROL Elenco richieste] | Fornisce le [proprietà dell’elenco richieste](https://github.com/adobe/xdm/pull/1675/files). Includono nome, ID e descrizione. |
| Tipo di dati | [!UICONTROL Commerce] | Il tipo di dati [Commerce è stato aggiornato](https://github.com/adobe/xdm/pull/1675/files) per includere `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals` e `requisitionList`. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [Panoramica sul sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

Il Servizio query consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal data lake e acquisire i risultati della query sotto forma di nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o da acquisire nel profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Controllo degli accessi basato su attributi nell’archivio accelerato | Utilizza il controllo degli accessi basato su attributi con Data Distiller per definire il controllo degli accessi su tutti i set di dati nell’archivio accelerato. Questo consente di controllare l’accesso ai modelli di dati personalizzati creati dagli utenti e memorizzati in un archivio accelerato per abilitare le dashboard personalizzate. |

{style="table-layout:auto"}

Per ulteriori informazioni sul Servizio query, consulta la [Panoramica sul servizio query](../../query-service/home.md).

## Edizione B2B di Real-Time Customer Data Platform {#b2b}

L’Edizione B2B di Real-Time CDP, basata su Real-Time Customer Data Platform (Real-Time CDP), è creata appositamente per i marketer che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono ai marketer di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Bugfix | Per fornire una rappresentazione più precisa dei profili nel sistema, il sistema non include più i profili interni nel conteggio totale dei profili o nella metrica del pubblico indirizzabile per l’edizione B2B di Real-time Customer Data Platform. A partire da oggi, potrebbe verificarsi un unico calo nel conteggio totale dei profili/metrica del pubblico indirizzabile. Nessuno dato è stato cancellato, si tratta semplicemente di una modifica al conteggio. Per eventuali dubbi, contatta il rappresentante Adobe |

{style="table-layout:auto"}

Per ulteriori informazioni sull’edizione B2B di Real-Time CDP, consulta la [Panoramica sull’edizione B2B di Real-Time CDP](../../rtcdp/overview.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Metriche del profilo | Per ottenere una rappresentazione più precisa delle metriche del profilo, vengono combinate le metriche di raggruppamento delle appartenenze e di abbandono e ora sono calcolate in un periodo di 24 ore. Ulteriori informazioni sono disponibili nella [Guida all’interfaccia utente di segmentazione](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità in versione beta di [!DNL Chatlio] | L’origine [!DNL Chatlio] è ora disponibile in versione beta. Utilizza l’origine [!DNL Chatlio] per trasmettere i dati degli eventi [!DNL Chatlio] ad Experience Platform. Per ulteriori informazioni, consulta la [[!DNL Chatlio] panoramica](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilità in versione beta di [!DNL Customer.io] | L’origine [!DNL Customer.io] è ora disponibile in versione beta. Utilizza l’origine [!DNL Customer.io] per trasmettere i dati degli eventi cliente ad Experience Platform. Per ulteriori informazioni, consulta la [[!DNL Customer.io] panoramica](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilità in versione beta di [!DNL Pendo] | L’origine [!DNL Pendo] è ora disponibile in versione beta. Utilizza l’origine [!DNL Pendo] per trasmettere i dati di analisi dei prodotti ad Experience Platform. Per ulteriori informazioni, consulta la [[!DNL Pendo] panoramica](../../sources/connectors/analytics/pendo-webhook.md). |
| Supporto per flussi di dati di bozza | Ora puoi utilizzare l’API del servizio Flow per impostare i flussi di dati su uno stato di bozza. I flussi di dati nella bozza possono essere successivamente aggiornati e pubblicati con nuove informazioni. Per ulteriori informazioni, consulta la guida sull’[impostazione dei flussi di dati di origine come bozze](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sources/home.md).
