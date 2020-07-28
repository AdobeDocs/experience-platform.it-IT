---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' campi di mappatura Analytics'
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '3328'
ht-degree: 3%

---


#  campi di mappatura Analytics

 Adobe Experience Platform consente di acquisire  dati Adobe Analytics tramite il connettore dati  Analytics (ADC). Alcuni dei dati acquisiti tramite ADC possono essere mappati direttamente  campi Analytics ai campi Experience Data Model (XDM), mentre altri dati richiedono trasformazioni e funzioni specifiche per essere mappati correttamente.

![](../images/analytics-data-experience-platform.png)

## Campi di mappatura diretta

Alcuni campi sono mappati direttamente da  Adobe Analytics a Experience Data Model (XDM).

La tabella seguente include colonne che mostrano il nome del campo  Analytics (*campo* Analytics), il campo XDM corrispondente (campo ** XDM) e il relativo tipo (tipo ** XDM), nonché una descrizione del campo (*Descrizione*).

>[!NOTE]
>
>Scorrere a sinistra/destra per visualizzare il contenuto completo della tabella.

|  campo Analytics | Campo XDM | XDM, tipo | Descrizione |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars. eVar1 - _experience.analytics.customDimensions.eVars. eVar250 | string | Variabile personalizzata che può essere compresa tra 1 e 250. Ciascuna organizzazione utilizzerà queste eVar personalizzate in modo diverso. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.prop.prop1 - _experience.analytics.customDimensions.prop.prop75 | string | Variabili di traffico personalizzate, che possono essere comprese tra 1 e 75. |
| m_browser | _experience.analytics.environment.browserID | integer | Numero ID del browser. |
| m_browser_height | environment.browserDetails.viewportHeight | integer | L’altezza del browser, in pixel. |
| m_browser_width | environment.browserDetails.viewportWidth | integer | Larghezza del browser, in pixel. |
| m_campaign | marketing.trackingCode | string | Variabile utilizzata nella dimensione Codice di tracciamento. |
| m_channel | web.webPageDetails.siteSection | string | Variabile utilizzata nella dimensione Sezioni del sito. |
| m_domain | environment.domain | string | Variabile utilizzata nella dimensione Dominio. Questo sarà basato sul provider di servizi Internet (ISP) dell&#39;utente. |
| m_geo_city | placeContext.geo.city | string | Il nome della città dell&#39;hit. Questo è basato sull&#39;indirizzo IP dell&#39;hit. |
| m_geo_dma | placeContext.geo.dmaID | integer | ID numerico dell&#39;area demografica per l&#39;hit. Questo è basato sull&#39;indirizzo IP dell&#39;hit. |
| m_geo_region | placeContext.geo.stateProvince | string | Nome dello stato o della regione dell’hit. Questo è basato sull&#39;indirizzo IP dell&#39;hit. |
| m_geo_zip | placeContext.geo.postalCode | string | Il codice ZIP dell’hit. Questo è basato sull&#39;indirizzo IP dell&#39;hit. |
| m_keywords | search.keywords | string | Variabile utilizzata nella dimensione Parola chiave. |
| m_os | _experience.analytics.environment.operationSystemID | integer | L&#39;ID numerico che rappresenta il sistema operativo del visitatore. Si basa sulla colonna user_agent. |
| m_page_url | web.webPageDetails.URL | string | URL dell’hit di pagina. |
| m_pagename_no_url | web.webPageDetails.</span>nome | string | Variabile utilizzata per compilare la dimensione Pagine. |
| m_referrer | web.webReferrer.URL | string | URL pagina della pagina precedente. |
| m_search_page_num | search.pageDepth | integer | Utilizzata dalla dimensione Classifica pagina di ricerca. Indica in quale pagina di risultati di ricerca il sito è stato visualizzato prima che l’utente facesse clic sul sito. |
| m_state | _experience.analytics.customDimensions.stateProvince | string | Variabile di stato. |
| m_user_server | web.webPageDetails.server | string | Variabile utilizzata nella dimensione Server. |
| m_zip | _experience.analytics.customDimensions.postalCode | string | Variabile utilizzata per compilare la dimensione Codice postale. |
| accept_language | environment.browserDetails.acceptLanguage | string | Elenca tutte le lingue accettate, come indicato nell&#39;intestazione HTTP Accept-Language. |
| homepage | web.webPageDetails.isHomePage | booleano | Non più utilizzato. Indicato se l’URL corrente è la home page del browser. |
| ipv6 | environment.ipV6 | string |
| j_jscript | environment.browserDetails.javaScriptVersion | string | La versione di JavaScript supportata dal browser. |
| user_agent | environment.browserDetails.userAgent | string | Stringa agente utente inviata nell’intestazione HTTP. |
| mobileappid | applicazione.</span>nome | string | L&#39;ID app mobile, memorizzato nel seguente formato: `[AppName][BundleVersion]`. |
| mobiledevice | device.model | string | Nome del dispositivo mobile. Su iOS, viene memorizzato come stringa di 2 cifre separate da virgola. Il primo numero rappresenta la generazione del dispositivo e il secondo numero rappresenta la famiglia di dispositivi. |
| puntiniere | placeContext.POIinteraction.POIDetail.</span>nome | string | Utilizzato dai servizi mobili. Rappresenta il punto di interesse. |
| puntofinterestdistanze | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | numero | Utilizzato dai servizi mobili. Rappresenta la distanza del punto di interesse. |
| mobilesegnaposto | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | numero | Raccolte dalla variabile di dati contestuali a.loc.acc. Indica la precisione del GPS in metri al momento della raccolta. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | string | Raccolti dalla variabile di dati contestuali a.loc.category. Descrive la categoria di un luogo specifico. |
| mobilesegnaposto | placeContext.POIinteraction.POIDetail.POIID | string | Raccolte dalla variabile di dati contestuali a.loc.id. Identificatore per un dato punto di interesse. |
| video | media.mediaTimed.primaryAssetReference._id | string | Nome del video. |
| videoad | advertising.adAssetReference._id | string | Identificatore della risorsa annuncio. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | string | Il Tipo Di Contenuto Video. Viene automaticamente impostato su &quot;Video&quot; per tutte le viste video. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | string | Il contenitore in cui si trova l&#39;annuncio video. |
| videoadinpod | advertising.adAssetViewDetails.index | integer | La posizione in cui si trova il video annuncio nel contenitore. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | string | Nome del lettore video. |
| videocanale | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | string | Il canale video. |
| videoadplayername | advertising.adAssetViewDetails.playerName | string | Il nome del lettore Video Ad. |
| videocapitolo | media.mediaTimed.mediaChapter.chapterAssetReference._id | string | Nome del capitolo Video |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | string | Il nome del video. |
| videoadname | advertising.adAssetReference._dc.title | string | Il nome dell&#39;annuncio video. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | string | Video show. |
| videoconferenza | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | string | Stagione Video. |
| videoepisodio | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | string | episodio video. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | string | Rete video. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | string | Tipo di visualizzazione video. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | string | Caricamenti annuncio video. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | string | Tipo di feed video. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | numero | beacon principale Mobile Services. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | numero | beacon minore di Mobile Services. |
| mobilebeaconuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | string | UUID beacon Mobile Services. |
| videosess ionid | media.mediaTimed.primaryAssetViewDetails._id | string | ID sessione video. |
| videogenere | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | array | Genere video. | {title (Object), descrizione (Object), tipo (Object), meta:xdmType (Object), elementi (string), meta:xdmField (Object)} |
| mobileinstalls | application.firstLaunches | Oggetto | Viene attivato alla prima esecuzione dopo l&#39;installazione o reinstallazione | {id (stringa), value (numero)} |
| mobileupgrade | application.upgrades | Oggetto | Segnala il numero di aggiornamenti dell&#39;app. Viene attivato alla prima esecuzione dopo l’aggiornamento o in qualsiasi momento il numero di versione cambi. | {id (stringa), value (numero)} |
| mobilelaunches | application.launches | Oggetto | Il numero di volte in cui l&#39;app è stata avviata. | {id (stringa), value (numero)} |
| mobilecrash | application.crashes | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| mobilemessagecick | directMarketing.clicks | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| mobilesegnaposto | placeContext.POIinteraction.poiEntries | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| mobilesegnaposto exit | placeContext.POIinteraction.poiExits | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videotime | media.mediaTimed.timePlayed | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videostart | media.mediaTimed.impressions | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videocomplete | media.mediaTimed.completes | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videosegmentazioni | media.mediaTimed.mediaSegmentViews | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoadstart | advertising.impressions | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoadcomplete | advertising.completes | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoadtime | advertising.timePlayed | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videogioco | media.mediaTimed.starts | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Oggetto | Tempo di avvio della qualità video. | {id (stringa), value (numero)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Oggetto | Conteggio buffer qualità video | {id (stringa), value (numero)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Oggetto | Tempo buffer qualità video | {id (stringa), value (numero)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Oggetto | Conteggio modifiche qualità video | {id (stringa), value (numero)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Oggetto | Bitrate medio della qualità video | {id (stringa), value (numero)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Oggetto | Conteggio errori qualità video | {id (stringa), value (numero)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoprogress10 | media.mediaTimed.progress10 | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoprogress25 | media.mediaTimed.progress25 | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoprogress50 | media.mediaTimed.progress50 | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoprogress75 | media.mediaTimed.progress75 | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoprogress95 | media.mediaTimed.progress95 | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videoresume | media.mediaTimed.resumes | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videopausecount | media.mediaTimed.pauses | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videopausetime | media.mediaTimed.pauseTime | Oggetto | <!-- MISSING --> | {id (stringa), value (numero)} |
| videodistincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | integer |

## Dividi campi di mappatura

Questi campi hanno una singola origine, ma vengono mappati su **più** posizioni XDM.

|  campo Analytics | Campo XDM | XDM, tipo | Descrizione |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | integer | ID numerico che rappresenta la risoluzione del monitor. |
| mobileosversion | environment.operationSystem, environment.operationSystemVersion | string | Versione del sistema operativo mobile. |
| videoadlength | advertising.adAssetReference._xmpDM.durata | integer | Lunghezza annuncio video. |

## Campi di mappatura generati

Per generare in XDM, è necessario trasformare i campi selezionati provenienti da ADC, che richiedono logica oltre una copia diretta da  Adobe Analytics.

La tabella seguente include colonne che mostrano il nome del campo  Analytics (*campo* Analytics), il campo XDM corrispondente (campo ** XDM) e il relativo tipo (tipo ** XDM), nonché una descrizione del campo (*Descrizione*).

>[!NOTE]
>
>Scorrere a sinistra/destra per visualizzare il contenuto completo della tabella.

|  campo Analytics | Campo XDM | XDM, tipo | Descrizione |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprop.prop1 - _experience.analytics.customDimensions.listprop.prop75 | Oggetto | Variabili di traffico personalizzate, comprese tra 1 e 75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchy.hier1 - _experience.analytics.customDimensions.hierarchy.hier5 | Oggetto | Utilizzata dalle variabili della gerarchia. Contiene un | elenco delimitato di valori. | {values (array), delimiter (stringa)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | array | Elenco di valori variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell&#39;implementazione | {value (stringa), key (stringa)} |
| m_color | device.colorDepth | integer | L’ID della profondità colore, che si basa sul valore della colonna c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | booleano | Variabile utilizzata nella dimensione Cookie Support. |
| m_event_list | commerce.purchase, commerce.productViews, commerce.productListOpen, commerce.checkout, commerce.productListAdd, commerce.productListRemovals, commerce.productListViews | Oggetto | Eventi di commercio standard attivati sull&#39;hit. | {id (stringa), value (numero)} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event20 , _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event30 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 Da 01a800.event701 - _experience.analytics.event701a800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801a900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Oggetto | Eventi personalizzati attivati sull’hit. | {id (Object), value (Object)} |
| m_geo_country | placeContext.geo.countryCode | string | Abbreviazione del paese da cui proveniva l’hit, che si basa sul PI. |
| m_geo_latitude | placeContext.geo._schema.latitude | numero | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | numero | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | booleano | Flag che indica se Java è abilitato. |
| m_latitude | placeContext.geo._schema.latitude | numero | <!-- MISSING --> |
| m_longitude | placeContext.geo._schema.longitude | numero | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | string | Variabile utilizzata solo nelle richieste di tracciamento dei collegamenti per immagini. Questa variabile contiene l’URL del collegamento di download, del collegamento di uscita o del collegamento personalizzato su cui è stato fatto clic. |
| m_page_event_var2 | web.webInteraction.name | string | Variabile utilizzata solo nelle richieste di tracciamento dei collegamenti per immagini. In questo modo viene riportato il nome personalizzato del collegamento, se specificato. |
| m_page_type | web.webPageDetails.isErrorPage | booleano | Variabile utilizzata per compilare la dimensione Pagine non trovate. Questa variabile deve essere vuota o contenere &quot;ErrorPage&quot;. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | numero | Il nome della pagina (se impostato). Se non viene specificata alcuna pagina, questo valore viene lasciato vuoto. |
| m_paid_search | search.isPaid | booleano | Flag impostato se l’hit corrisponde al rilevamento della ricerca a pagamento. |
| m_product_list | productListItems[].items | array | L&#39;elenco dei prodotti, come trasmesso attraverso la variabile &quot;products&quot;. | {SKU (stringa), quantità (numero intero), prezzoTotale (numero)} |
| m_ref_type | web.webReferrer.type | string | Un ID numerico che rappresenta il tipo di riferimento per l&#39;hit. 1 significa all&#39;interno del sito, 2 significa altri siti Web, 3 significa motori di ricerca, 4 significa disco rigido, 5 significa USENET, 6 significa Typed/Bookmarked (nessun referrer), 7 significa email, 8 significa No JavaScript, 9 significa Social Network. |
| m_search_Engine | search.searchEngine | string | L&#39;ID numerico che rappresenta il motore di ricerca che ha indirizzato il visitatore al sito. |
| post_currency | commerce.order.currencyCode | string | Codice valuta utilizzato durante la transazione. |
| post_cust_hit_time_gmt | timestamp | string | Viene utilizzato solo nei set di dati con marca temporale abilitata. Indica la marca temporale inviata insieme alla marca, in base all&#39;ora Unix. |
| post_cust_visid | identityMap | object | L’ID visitatore del cliente. |
| post_cust_visid | endUserIDs._experience.acustomomid.Primary | booleano | L’ID visitatore del cliente. |
| post_cust_visid | endUserIDs._experience.acustom.namespace.code | string | L’ID visitatore del cliente. |
| post_visid_high + visid_low | identityMap | object | Un identificatore univoco per una visita. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | string | Un identificatore univoco per una visita. |
| post_visid_high | endUserIDs._experience.aaid.Primary | booleano | Utilizzata insieme a visid_low per identificare in modo univoco una visita. |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | string | Utilizzata insieme a visid_low per identificare in modo univoco una visita. |
| post_visid_low | identityMap | object | Utilizzata insieme a visid_high per identificare in modo univoco una visita. |
| hit_time_gmt | ReceivedTimestamp | string | Il timestamp dell’hit, in base all’ora Unix. |
| hitid_high + hitid_low | _id | string | Identificatore univoco per identificare un hit. |
| hitid_low | _id | string | Utilizzata insieme a hitid_high per identificare in modo univoco un hit. |
| ip | environment.ipV4 | string | Indirizzo IP, basato sull’intestazione HTTP della richiesta di immagine. |
| j_jscript | environment.browserDetails.javaScriptEnabled | booleano | Versione di JavaScript utilizzata. |
| mcvisid_high + mcvisid_low | identityMap | object | L’ID visitatore  Experience Cloud. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | string | L’ID visitatore  Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.Primary | booleano | L’ID visitatore  Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | string | L’ID visitatore  Experience Cloud. |
| mcvisid_low | identityMap | object | L’ID visitatore  Experience Cloud. |
| sdid_high + sdid_low | _experience.target.supplementareDataID | string | Hit Stitching ID. Il campo di analisi sdid_high e sdid_low è l’ID di dati supplementare utilizzato per unire due (o più) hit in entrata. |
| mobilebeaconprossimità | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | string | Prossimità del beacon Mobile Services. |
| videocapitolo | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.durata | integer | Nome del capitolo video. |
| lunghezza video | media.mediaTimed.primaryAssetReference._xmpDM.durata | integer | Lunghezza del video. |

## Campi di mappatura avanzati

Per poter mappare correttamente i campi di Adobe Analytics  a Experience Data Model (XDM) è necessario disporre di trasformazioni più avanzate. L&#39;esecuzione di queste trasformazioni avanzate implica l&#39;uso di Adobe Experience Platfrom Query Service e di funzioni preconfigurate (denominate funzioni  definite dal Adobe) per la sessionizzazione, l&#39;attribuzione e la deduplicazione.

Per ulteriori informazioni sull&#39;esecuzione di queste trasformazioni tramite il servizio Query Service, consultare la documentazione relativa alle funzioni [definite dal Adobe](../../../../query-service/sql/adobe-defined-functions.md) .

La tabella seguente include colonne che mostrano il nome del campo  Analytics (*campo* Analytics), il campo XDM corrispondente (campo ** XDM) e il relativo tipo (tipo ** XDM), nonché una descrizione del campo (*Descrizione*).

>[!NOTE]
>
>Scorrere a sinistra/destra per visualizzare il contenuto completo della tabella.

|  campo Analytics | Campo XDM | XDM, tipo | Descrizione |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars. eVar1 - _experience.analytics.customDimensions.eVars. eVar250 | string | Variabile personalizzata che può essere compresa tra 1 e 250. Ciascuna organizzazione utilizzerà queste eVar personalizzate in modo diverso. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.prop.prop1 - _experience.analytics.customDimensions.prop.prop75 | string | Variabili di traffico personalizzate, che possono essere comprese tra 1 e 75. |
| post_browser_height | environment.browserDetails.viewportHeight | integer | L’altezza del browser, in pixel. |
| post_browser_width | environment.browserDetails.viewportWidth | integer | Larghezza del browser, in pixel. |
| post_campaign | marketing.trackingCode | string | Variabile utilizzata nella dimensione Codice di tracciamento. |
| post_channel | web.webPageDetails.siteSection | string | Variabile utilizzata nella dimensione Sezioni del sito. |
| post_cust_visid | endUserIDs._experience.acustomid.id | string | L’ID visitatore personalizzato, se impostato. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | string | URL della prima pagina raggiunta dal visitatore. |
| post_first_hit_page | _experience.analytics.endUser.firstWeb.webPageDetails.name | string | Variabile utilizzata nella dimensione Originale pagina di immissione. Il nome della pagina della pagina di immissione del visitatore. |
| post_keywords | search.keywords | string | Le parole chiave raccolte per l’hit. |
| post_page_url | web.webPageDetails.URL | string | URL dell’hit di pagina. |
| post_pagename_no_url | web.webPageDetails.name | string | Variabile utilizzata per compilare la dimensione Pagine. |
| post_purchaseid | commerce.order.purchaseID | string | Variabile utilizzata per identificare in modo univoco gli acquisti. |
| post_referrer | web.webReferrer.URL | string | URL della pagina precedente. |
| post_state | _experience.analytics.customDimensions.stateProvince | string | Variabile di stato. |
| post_user_server | web.webPageDetails.server | string | Variabile utilizzata nella dimensione Server. |
| post_zip | _experience.analytics.customDimensions.postalCode | string | Variabile utilizzata per compilare la dimensione Codice postale. |
| browser | _experience.analytics.environment.browserID | integer | ID numerico del browser. |
| domain | environment.domain | string | Variabile utilizzata nella dimensione Dominio. Questo sarà basato sul provider di servizi Internet (ISP) dell&#39;utente. |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | string | Il primo URL di provenienza del visitatore. |
| geo_city | placeContext.geo.city | string | Il nome della città dell&#39;hit. Questo è basato sull&#39;indirizzo IP dell&#39;hit. |
| geo_dma | placeContext.geo.dmaID | integer | ID numerico dell&#39;area demografica per l&#39;hit. Questo è basato sull&#39;indirizzo IP dell&#39;hit. |
| geo_region | placeContext.geo.stateProvince | string | Nome dello stato o della regione dell’hit. Questo è basato sull&#39;indirizzo IP dell&#39;hit. |
| geo_zip | placeContext.geo.postalCode | string | Il codice ZIP dell’hit. Questo è basato sull&#39;indirizzo IP dell&#39;hit. |
| os | _experience.analytics.environment.operationSystemID | integer | L&#39;ID numerico che rappresenta il sistema operativo del visitatore. Si basa sulla colonna user_agent. |
| search_page_num | search.pageDepth | integer | Questa variabile viene utilizzata dalla dimensione All Search Page Rank e indica quale pagina di risultati di ricerca del sito | veniva visualizzato prima che l’utente facesse clic sul sito. |
| visit_keywords | _experience.analytics.session.search.keywords | string | Variabile utilizzata nella dimensione Cerca parole chiave. |
| visit_num | _experience.analytics.session.num | integer | Variabile utilizzata nella dimensione Numero visita. Questo inizia da 1 e viene incrementato ogni volta che inizia una nuova visita (per utente). |
| visit_page_num | _experience.analytics.session.profondità | integer | Variabile utilizzata nella dimensione Profondità hit. Questo valore aumenta di 1 per ogni hit generato dall’utente e viene ripristinato dopo ogni visita. |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | string | Il primo referente della visita. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | integer | Il nome della prima pagina della visita. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprop.prop1 - _experience.analytics.customDimensions.listprop.prop75 | Oggetto | Variabili di traffico personalizzate 1-75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchy.hier1 - _experience.analytics.customDimensions.hierarchy.hier5 | Oggetto | Utilizzato dalle variabili della gerarchia e contiene un elenco delimitato di valori. | {values (array), delimiter (stringa)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | array | Un elenco di valori variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell&#39;implementazione. | {value (stringa), key (stringa)} |
| post_cookies | environment.browserDetails.cookiesEnabled | booleano | Variabile utilizzata nella dimensione Cookie Support. |
| post_event_list | commerce.purchase, commerce.productViews, commerce.productListOpen, commerce.checkout, commerce.productListAdd, commerce.productListRemovals, commerce.productListViews | Oggetto | Eventi di commercio standard attivati sull&#39;hit. | {id (stringa), value (numero)} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event20 , _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event30 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 Da 01a800.event701 - _experience.analytics.event701a800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801a900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Oggetto | Eventi personalizzati attivati sull’hit. | {id (Object), value (Object)} |
| post_java_enabled | environment.browserDetails.javaEnabled | booleano | Flag che indica se Java è abilitato. |
| post_latitude | placeContext.geo._schema.latitude | numero | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | numero | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | string | Tipo di hit inviato nella richiesta di immagine (hit standard, collegamento di download, collegamento di uscita o collegamento personalizzato su cui è fatto clic). |
| post_page_event | web.webInteraction.linkClicks.value | numero | Tipo di hit inviato nella richiesta di immagine (hit standard, collegamento di download, collegamento di uscita o collegamento personalizzato su cui è fatto clic). |
| post_page_event_var1 | web.webInteraction.URL | string | Questa variabile viene utilizzata solo nelle richieste di tracciamento dei collegamenti per le immagini. Si tratta dell’URL del collegamento di download, del collegamento di uscita o del collegamento personalizzato su cui è stato fatto clic. |
| post_page_event_var2 | web.webInteraction.name | string | Questa variabile viene utilizzata solo nelle richieste di tracciamento dei collegamenti per le immagini. Questo sarà il nome personalizzato del collegamento. |
| post_page_type | web.webPageDetails.isErrorPage | booleano | Viene utilizzato per compilare la dimensione Pagine non trovate. Questa variabile deve essere vuota o contenere &quot;ErrorPage&quot; |
| post_pagename_no_url | web.webPageDetails.pageViews.value | numero | Il nome della pagina (se impostato). Se non viene specificata alcuna pagina, questo valore viene lasciato vuoto. |
| post_product_list | productListItems[].items | array | L&#39;elenco dei prodotti, come trasmesso attraverso la variabile &quot;products&quot;. | {SKU (stringa), quantità (numero intero), prezzoTotale (numero)} |
| post_search_Engine | search.searchEngine | string | L&#39;ID numerico che rappresenta il motore di ricerca che ha indirizzato il visitatore al sito. |
| mvvar1_instance | .list.items[] | Oggetto | Elenco di valori variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell&#39;implementazione. |
| mvvar2_instance | .list.items[] | Oggetto | Elenco di valori variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell&#39;implementazione. |
|  | mvvar3_instance | .list.items[] | Oggetto | Elenco di valori variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell&#39;implementazione. |
| color | device.colorDepth | integer | ID profondità colore, in base al valore della colonna c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | string | L&#39;ID numerico che rappresenta il tipo di referente del primo referente del visitatore. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | integer | Timestamp del primo hit del visitatore in Unix time. |
| geo_country | placeContext.geo.countryCode | string | Abbreviazione del paese da cui l&#39;hit è venuto, basato su IP. |
| geo_latitude | placeContext.geo._schema.latitude | numero | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | numero | <!-- MISSING --> |
| paid_search | search.isPaid | booleano | Flag impostato se l’hit corrisponde al rilevamento della ricerca a pagamento. |
| ref_type | web.webReferrer.type | string | Un ID numerico che rappresenta il tipo di riferimento per l&#39;hit. |
| visit_paid_search | _experience.analytics.session.search.isPaid | booleano | Flag (1=paid, 0=not paid) che indica se il primo hit della visita proveniva da un hit di ricerca a pagamento. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | string | ID numerico che rappresenta il tipo di referente del primo referente della visita. |
| visit_search_Engine | _experience.analytics.session.search.searchEngine | string | ID numerico del primo motore di ricerca della visita. |
| visit_start_time_gmt | _experience.analytics.session.timestamp | integer | Timestamp del primo hit della visita in Unix. |
