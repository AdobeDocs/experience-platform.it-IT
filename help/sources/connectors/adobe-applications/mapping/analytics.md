---
keywords: campi di mappatura di Analytics;mappatura di Analytics
solution: Experience Platform
title: Mappatura dei campi per il connettore Source di Adobe Analytics
description: Mappa i campi Adobe Analytics ai campi XDM utilizzando il connettore Source di Analytics.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 6cbd902c6a1159d062fb38bf124a09bb18ad1ba8
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 8%

---

# Mappature dei campi di Analytics

Adobe Experience Platform consente di acquisire dati da Adobe Analytics tramite l’origine Analytics. Alcuni dei dati acquisiti tramite ADC possono essere mappati direttamente dai campi di Analytics ai campi Experience Data Model (XDM), mentre altri dati richiedono trasformazioni e funzioni specifiche per essere mappati correttamente.

![](../images/analytics-data-experience-platform.png)

## Campi di mappatura diretta

I campi selezionati vengono mappati direttamente da Adobe Analytics a Experience Data Model (XDM).

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ---------- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | stringa | eVar di Analytics personalizzate. Ogni organizzazione può utilizzare le eVar in modo diverso. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | stringa | Proprietà personalizzate di Analytics. Ogni organizzazione può utilizzare prop in modo diverso. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | intero | ID del numero del browser. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | intero | Altezza del browser, in pixel. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | intero | Larghezza del browser, in pixel. |
| `m_campaign` | `marketing.trackingCode` | stringa | Variabile utilizzata nella dimensione Codice di tracciamento. |
| `m_channel` | `web.webPageDetails.siteSection` | stringa | Variabile utilizzata nella dimensione Sezioni del sito. |
| `m_domain` | `environment.domain` | stringa | Variabile utilizzata nella dimensione Dominio. Si basa sul provider di servizi Internet (ISP) dell&#39;utente. |
| `m_geo_city` | `placeContext.geo.city` | stringa | Il nome della città dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `m_geo_dma` | `placeContext.geo.dmaID` | intero | ID numerico dell’area demografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `m_geo_region` | `placeContext.geo.stateProvince` | stringa | Il nome dello stato o dell’area geografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `m_geo_zip` | `placeContext.geo.postalCode` | stringa | Il codice postale dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `m_keywords` | `search.keywords` | stringa | Variabile utilizzata nella dimensione Parola chiave. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | intero | L’ID numerico che rappresenta il sistema operativo del visitatore. Si basa sulla colonna user_agent. |
| `m_page_url` | `web.webPageDetails.URL` | stringa | URL dell’hit pagina. |
| `m_pagename` | `web.webPageDetails.pageViews.value` | stringa | È uguale a 1 nei risultati con un nome pagina. È simile alla metrica Visualizzazioni pagina di Adobe Analytics. |
| `m_referrer` | `web.webReferrer.URL` | stringa | URL della pagina precedente. |
| `m_search_page_num` | `search.pageDepth` | intero | Utilizzato dalla dimensione Classificazione di tutte le pagine di ricerca. Indica in quale pagina dei risultati di ricerca il sito è stato visualizzato prima che l’utente avesse fatto clic sul sito. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | stringa | Variabile di stato. |
| `m_user_server` | `web.webPageDetails.server` | stringa | Variabile utilizzata nella dimensione Server. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | stringa | Variabile utilizzata per popolare la dimensione Codice postale. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | stringa | Elenca tutte le lingue accettate, come indicato nell’intestazione HTTP Accept-Language. |
| `homepage` | `web.webPageDetails.isHomePage` | booleano | Non più utilizzato. Indica se l’URL corrente è la home page del browser. |
| `ipv6` | `environment.ipV6` | stringa |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | stringa | Versione di JavaScript supportata dal browser. |
| `user_agent` | `environment.browserDetails.userAgent` | stringa | Stringa dell’agente utente inviata nell’intestazione HTTP. |
| `mobileappid` | `application.name` | stringa | L&#39;ID dell&#39;app mobile, archiviato nel seguente formato: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | stringa | Nome del dispositivo mobile. In iOS, viene memorizzato come stringa di 2 cifre separate da virgola. Il primo numero rappresenta la generazione del dispositivo e il secondo rappresenta la famiglia di dispositivi. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | stringa | Utilizzato da Mobile Services. Rappresenta il punto di interesse. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | numero | Utilizzato da Mobile Services. Rappresenta la distanza del punto di interesse. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | numero | Raccolto dalla variabile di dati di contesto a.loc.acc. Indica la precisione del GPS in metri al momento della raccolta. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | stringa | Raccolto dalla variabile di dati di contesto a.loc.category. Descrive la categoria di un luogo specifico. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | stringa | Raccolto dalla variabile di dati di contesto a.loc.id. Identificatore per un dato punto di interesse. |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | stringa | Nome del video. |
| `videoad` | `advertising.adAssetReference._id` | stringa | Identificatore della risorsa dell’annuncio. |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | stringa | Il Tipo Di Contenuto Video. Viene automaticamente impostato su &quot;Video&quot; per tutte le visualizzazioni video. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | stringa | Il pod in cui si trova l’annuncio video. |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | intero | La posizione dell’annuncio video nel pod. |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | stringa | Nome del lettore video. |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | stringa | Canale video. |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | stringa | Nome del lettore di annunci video. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | stringa | Nome del capitolo Video |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | stringa | Il nome del video. |
| `videoadname` | `advertising.adAssetReference._dc.title` | stringa | Nome dell’annuncio video. |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | stringa | Presentazione video. |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | stringa | Stagione video. |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | stringa | Episodio video |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | stringa | Rete video. |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | stringa | Tipo di presentazione video. |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | stringa | Caricamenti di annunci video. |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | stringa | Tipo di feed video. |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | numero | Beacon principale di Mobile Services. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | numero | Beacon secondario di Mobile Services. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | stringa | Beacon UUID di Mobile Services. |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | stringa | ID sessione video. |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | array | Genere video. | {title (Oggetto), description (Oggetto), type (Oggetto), meta:xdmType (Oggetto), items (stringa), meta:xdmField (Oggetto)} |
| `mobileinstalls` | `application.firstLaunches` | Oggetto | Viene attivato alla prima esecuzione dopo l’installazione o la reinstallazione | {id (stringa), valore (numero)} |
| `mobileupgrades` | `application.upgrades` | Oggetto | Segnala il numero di aggiornamenti dell’app. Attiva alla prima esecuzione dopo l’aggiornamento o quando cambia il numero di versione. | {id (stringa), valore (numero)} |
| `mobilelaunches` | `application.launches` | Oggetto | Il numero di volte in cui l&#39;app è stata avviata. | {id (stringa), valore (numero)} |
| `mobilecrashes` | `application.crashes` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `mobilemessageclicks` | `directMarketing.clicks` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videotime` | `media.mediaTimed.timePlayed` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videostart` | `media.mediaTimed.impressions` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videocomplete` | `media.mediaTimed.completes` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoadstart` | `advertising.impressions` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoadcomplete` | `advertising.completes` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoadtime` | `advertising.timePlayed` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoplay` | `media.mediaTimed.starts` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Oggetto | Il tempo di avvio della qualità video. | {id (stringa), valore (numero)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Oggetto | Conteggio buffer qualità video | {id (stringa), valore (numero)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Oggetto | Tempo buffer qualità video | {id (stringa), valore (numero)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Oggetto | Conteggio modifiche qualità video | {id (stringa), valore (numero)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Oggetto | Bitrate medio della qualità video | {id (stringa), valore (numero)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Oggetto | Conteggio errori qualità video | {id (stringa), valore (numero)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoprogress10` | `media.mediaTimed.progress10` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoprogress25` | `media.mediaTimed.progress25` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoprogress50` | `media.mediaTimed.progress50` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoprogress75` | `media.mediaTimed.progress75` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoprogress95` | `media.mediaTimed.progress95` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videoresume` | `media.mediaTimed.resumes` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videopausecount` | `media.mediaTimed.pauses` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videopausetime` | `media.mediaTimed.pauseTime` | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | intero |

{style="table-layout:auto"}

## Campi con mappatura divisa

Questi campi hanno un&#39;unica origine, ma vengono mappati su **più** posizioni XDM.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | intero | ID numerico che rappresenta la risoluzione del monitoraggio. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | stringa | Versione del sistema operativo mobile. |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | intero | Lunghezza annuncio video. |

{style="table-layout:auto"}

## Campi di mappatura generati

È necessario trasformare i campi selezionati provenienti da ADC, che richiedono la generazione in XDM di una logica che va oltre una copia diretta da Adobe Analytics.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Oggetto | Proprietà personalizzate di Analytics, configurate come prop elenco. Contiene un elenco delimitato di valori. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Oggetto | Utilizzato dalle variabili gerarchiche. Contiene un elenco delimitato di valori. | {values (array), delimitatore (stringa)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Variabili elenco di Analytics personalizzate. Contiene un elenco delimitato di valori. | {value (stringa), key (stringa)} |
| `m_color` | `device.colorDepth` | intero | ID di profondità colore, basato sul valore della colonna c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | booleano | Variabile utilizzata nella dimensione Supporto cookie. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Oggetto | Eventi di e-commerce standard attivati sull’hit. | {id (stringa), valore (numero)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Oggetto | Eventi personalizzati attivati sull’hit. | {id (Oggetto), value (Oggetto)} |
| `m_geo_country` | `placeContext.geo.countryCode` | stringa | Abbreviazione del paese da cui proviene l’hit, basata sul PI. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | numero | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | numero | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | booleano | Flag che indica se Java™ è abilitato. |
| `m_latitude` | `placeContext.geo._schema.latitude` | numero | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | numero | <!-- MISSING --> |
| `m_page_event_var1` | `web.webInteraction.URL` | stringa | Variabile utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. Questa variabile contiene l’URL del collegamento di download, del collegamento di uscita o del collegamento personalizzato su cui è stato fatto clic. |
| `m_page_event_var2` | `web.webInteraction.name` | stringa | Variabile utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. Elenca il nome personalizzato del collegamento, se specificato. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | booleano | Variabile utilizzata per popolare la dimensione Pagine non trovate. Questa variabile deve essere vuota o contenere &quot;ErrorPage&quot;. |
| `m_pagename_no_url` | `web.webPageDetails.name` | numero | Nome della pagina (se impostato). Se non viene specificata alcuna pagina, questo valore viene lasciato vuoto. |
| `m_paid_search` | `search.isPaid` | booleano | Flag impostato se l’hit corrisponde al rilevamento di ricerche a pagamento. |
| `m_product_list` | `productListItems[].items` | array | L’elenco dei prodotti, trasmesso attraverso la variabile dei prodotti. | {SKU (stringa), quantità (numero intero), priceTotal (numero)} |
| `m_ref_type` | `web.webReferrer.type` | stringa | Un ID numerico che rappresenta il tipo di riferimento per l’hit.<br/>`1`: all&#39;interno del sito<br/>`2`: altri siti Web<br/>`3`: motori di ricerca<br/>`4`: disco rigido<br/>`5`: USENET<br/>`6`: digitato/contrassegnato con segnalibro (nessun referrer)<br/>`7`: e-mail<br/>`8`: nessun JavaScript<br/>`9`: social network |
| `m_search_engine` | `search.searchEngine` | stringa | L’ID numerico che rappresenta il motore di ricerca che ha indirizzato il visitatore al sito. |
| `post_currency` | `commerce.order.currencyCode` | stringa | Codice valuta utilizzato durante la transazione. |
| `post_cust_hit_time_gmt` | `timestamp` | stringa | Viene utilizzato solo nei set di dati abilitati per le marche temporali. Timestamp inviato con l’hit, in base all’ora UNIX®. |
| `post_cust_visid` | `identityMap` | oggetto | L’ID visitatore del cliente. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | booleano | L’ID visitatore del cliente. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | stringa | L’ID visitatore del cliente. |
| `post_visid_high` + `visid_low` | `identityMap` | oggetto | Un identificatore univoco per una visita. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | stringa | Un identificatore univoco per una visita. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | booleano | Utilizzato con `visid_low` per identificare in modo univoco una visita. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | stringa | Utilizzato con `visid_low` per identificare in modo univoco una visita. |
| `post_visid_low` | `identityMap` | oggetto | Utilizzato con visid_high per identificare in modo univoco una visita. |
| `hit_time_gmt` | `receivedTimestamp` | stringa | La marca temporale dell’hit, in base all’ora UNIX®. |
| `hitid_high` + `hitid_low` | `_id` | stringa | Un identificatore univoco per identificare un hit. |
| `hitid_low` | `_id` | stringa | Utilizzato con hitid_high per identificare in modo univoco un hit. |
| `ip` | `environment.ipV4` | stringa | L’indirizzo IP, in base all’intestazione HTTP della richiesta di immagine. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | booleano | Versione di JavaScript utilizzata. |
| `mcvisid_high` + `mcvisid_low` | identityMap | oggetto | L’ID visitatore Experience Cloud. |
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | stringa | L’ID Experience Cloud (ECID) è noto anche come MCID e talvolta viene utilizzato negli spazi dei nomi. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | booleano | L’ID Experience Cloud (ECID) è noto anche come MCID e talvolta viene utilizzato negli spazi dei nomi. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | stringa | L’ID Experience Cloud (ECID) è noto anche come MCID e talvolta viene utilizzato negli spazi dei nomi. |
| `mcvisid_low` | `identityMap` | oggetto | L’ID visitatore Experience Cloud. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | stringa | Hit Stitching ID. Il campo di analisi sdid_high e sdid_low è l’ID di dati supplementare utilizzato per unire due (o più) hit in arrivo. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | stringa | Prossimità beacon di Mobile Services. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | intero | Il nome del capitolo video. |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | intero | La lunghezza del video. |

{style="table-layout:auto"}

## Campi di mappatura avanzati

I campi di selezione (noti come &quot;valori post&quot;) contengono dati dopo che Adobe ha regolato i loro valori utilizzando le Regole di elaborazione, le regole VISTA e le tabelle di ricerca. La maggior parte dei valori post ha una controparte pre-elaborata. L’organizzazione può decidere se utilizzare il campo pre-elaborato, il campo post-elaborato o entrambi.

Per ulteriori informazioni sull&#39;esecuzione di queste trasformazioni tramite Query Service, vedere [Funzioni definite dall&#39;Adobe](/help/query-service/sql/adobe-defined-functions.md) nella guida utente di Query Service.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ---------- |
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | stringa | eVar di Analytics personalizzate. Ogni organizzazione può utilizzare le eVar in modo diverso. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | stringa | Proprietà personalizzate di Analytics. Ogni organizzazione può utilizzare prop in modo diverso. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | intero | Altezza del browser, in pixel. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | intero | Larghezza del browser, in pixel. |
| `post_campaign` | `marketing.trackingCode` | stringa | Variabile utilizzata nella dimensione Codice di tracciamento. |
| `post_channel` | `web.webPageDetails.siteSection` | stringa | Variabile utilizzata nella dimensione Sezioni del sito. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | stringa | ID visitatore personalizzato, se impostato. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | stringa | L’URL della prima pagina raggiunta dal visitatore. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | stringa | Variabile utilizzata nella dimensione Pagina di ingresso originale. Il nome della pagina di ingresso del visitatore. |
| `post_keywords` | `search.keywords` | stringa | Parole chiave raccolte per l’hit. |
| `post_page_url` | `web.webPageDetails.URL` | stringa | URL dell’hit pagina. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | stringa | È uguale a 1 nei risultati con un nome pagina. È simile alla metrica Visualizzazioni pagina di Adobe Analytics. |
| `post_purchaseid` | `commerce.order.purchaseID` | stringa | Variabile utilizzata per identificare in modo univoco gli acquisti. |
| `post_referrer` | `web.webReferrer.URL` | stringa | URL della pagina precedente. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | stringa | Variabile di stato. |
| `post_user_server` | `web.webPageDetails.server` | stringa | Variabile utilizzata nella dimensione Server. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | stringa | Variabile utilizzata per popolare la dimensione Codice postale. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | intero | ID numerico del browser. |
| `domain` | `environment.domain` | stringa | Variabile utilizzata nella dimensione Dominio. Si basa sul provider di servizi Internet (ISP) dell&#39;utente. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | stringa | Il primo URL di riferimento per il visitatore. |
| `geo_city` | `placeContext.geo.city` | stringa | Il nome della città dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `geo_dma` | `placeContext.geo.dmaID` | intero | ID numerico dell’area demografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `geo_region` | `placeContext.geo.stateProvince` | stringa | Il nome dello stato o dell’area geografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `geo_zip` | `placeContext.geo.postalCode` | stringa | Il codice postale dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | intero | L’ID numerico che rappresenta il sistema operativo del visitatore. Si basa sulla colonna user_agent. |
| `search_page_num` | `search.pageDepth` | intero | Questa variabile viene utilizzata dalla dimensione Classificazione di tutte le pagine di ricerca e indica quale pagina di risultati di ricerca ha il sito | è apparso su prima che l’utente facesse clic sul sito. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | stringa | Variabile utilizzata nella dimensione Parole chiave di ricerca. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | intero | Variabile utilizzata nella dimensione Numero di visite. Inizia da 1 e viene incrementato ogni volta che inizia una nuova visita (per utente). |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | intero | Variabile utilizzata nella dimensione Profondità di hit. Questo valore aumenta di 1 per ogni hit generato dall’utente e viene ripristinato dopo ogni visita. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | stringa | Il primo referrer della visita. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | intero | Nome della prima pagina della visita. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Oggetto | Proprietà personalizzate di Analytics, configurate come prop elenco. Contiene un elenco delimitato di valori. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Oggetto | Utilizzato dalle variabili della gerarchia e contiene un elenco delimitato di valori. | {values (array), delimitatore (stringa)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Elenco di valori di variabile. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. | {value (stringa), key (stringa)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | booleano | Variabile utilizzata nella dimensione Supporto cookie. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Oggetto | Eventi di e-commerce standard attivati sull’hit. | {id (stringa), valore (numero)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Oggetto | Eventi personalizzati attivati sull’hit. | {id (Oggetto), value (Oggetto)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | booleano | Flag che indica se Java™ è abilitato. |
| `post_latitude` | `placeContext.geo._schema.latitude` | numero | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | numero | <!-- MISSING --> |
| `post_page_event` | `web.webInteraction.type` | stringa | Tipo di hit inviato nella richiesta di immagine (hit standard, collegamento di download, collegamento di uscita o collegamento personalizzato su cui è stato fatto clic). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | numero | È uguale a 1 se l’hit è un clic di collegamento. È simile alla metrica Eventi pagina in Adobe Analytics. |
| `post_page_event_var1` | `web.webInteraction.URL` | stringa | Questa variabile viene utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. Si tratta dell’URL del collegamento di download, del collegamento di uscita o del collegamento personalizzato in cui è stato fatto clic. |
| `post_page_event_var2` | `web.webInteraction.name` | stringa | Questa variabile viene utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. È il nome personalizzato del collegamento. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | booleano | Viene utilizzato per popolare la dimensione Pagine non trovate. Questa variabile deve essere vuota o contenere &quot;ErrorPage&quot; |
| `post_pagename_no_url` | `web.webPageDetails.name` | numero | Nome della pagina (se impostato). Se non viene specificata alcuna pagina, questo valore viene lasciato vuoto. |
| `post_product_list` | `productListItems[].items` | array | L’elenco dei prodotti, trasmesso attraverso la variabile dei prodotti. | {SKU (stringa), quantità (numero intero), priceTotal (numero)} |
| `post_search_engine` | `search.searchEngine` | stringa | L’ID numerico che rappresenta il motore di ricerca che ha indirizzato il visitatore al sito. |
| `mvvar1_instances` | `.list.items[]` | Oggetto | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. |
| `mvvar2_instances` | `.list.items[]` | Oggetto | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. |
| `mvvar3_instances` | `.list.items[]` | Oggetto | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. |
| `color` | `device.colorDepth` | intero | ID profondità colore, in base al valore della colonna c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | stringa | ID numerico che rappresenta il tipo di referrer del primo referrer del visitatore. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | intero | Marca temporale del primo hit del visitatore in tempo UNIX®. |
| `geo_country` | `placeContext.geo.countryCode` | stringa | Abbreviazione del paese da cui proviene l’hit, basata su IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | numero | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | numero | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | booleano | Flag impostato se l’hit corrisponde al rilevamento di ricerche a pagamento. |
| `ref_type` | `web.webReferrer.type` | stringa | Un ID numerico che rappresenta il tipo di riferimento per l’hit. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | booleano | Un flag (1=a pagamento, 0=non a pagamento) che indica se il primo hit della visita proviene da un hit di ricerca a pagamento. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | stringa | ID numerico che rappresenta il tipo di referrer del primo referrer della visita. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | stringa | ID numerico del primo motore di ricerca della visita. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | intero | Timestamp del primo hit della visita in tempo UNIX®. |

{style="table-layout:auto"}