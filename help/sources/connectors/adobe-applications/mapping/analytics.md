---
keywords: Experience Platform;home;argomenti popolari;campi di mappatura di Analytics;mappatura di Analytics
solution: Experience Platform
title: Campi di mappatura per il connettore di origine di Adobe Analytics
description: Adobe Experience Platform consente di acquisire dati da Adobe Analytics tramite l’origine Analytics. Alcuni dei dati acquisiti tramite ADC possono essere mappati direttamente dai campi di Analytics ai campi Experience Data Model (XDM), mentre altri dati richiedono trasformazioni e funzioni specifiche per essere mappati correttamente.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '3419'
ht-degree: 13%

---

# Mappature dei campi di Analytics

Adobe Experience Platform consente di acquisire dati da Adobe Analytics tramite l’origine Analytics. Alcuni dei dati acquisiti tramite ADC possono essere mappati direttamente dai campi di Analytics ai campi Experience Data Model (XDM), mentre altri dati richiedono trasformazioni e funzioni specifiche per essere mappati correttamente.

![](../images/analytics-data-experience-platform.png)

## Campi di mappatura diretta

I campi selezionati vengono mappati direttamente da Adobe Analytics a Experience Data Model (XDM).

La tabella seguente include colonne che mostrano il nome del campo Analytics (*Campo Analytics*), il campo XDM corrispondente (*Campo XDM*) e il relativo tipo (*Tipo XDM*), nonché una descrizione del campo (*Descrizione*).

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Una variabile personalizzata, che può essere compresa tra 1 e 250. Ciascuna organizzazione utilizzerà queste eVar personalizzate in modo diverso. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variabili di traffico personalizzate, che possono essere comprese tra 1 e 75. |
| m_browser | _experience.analytics.environment.browserID | numero intero | ID del numero del browser. |
| m_browser_height | environment.browserDetails.viewportHeight | numero intero | Altezza del browser, in pixel. |
| m_browser_width | environment.browserDetails.viewportWidth | numero intero | Larghezza del browser, in pixel. |
| m_campaign | marketing.trackingCode | string | Variabile utilizzata nella dimensione Codice di tracciamento. |
| m_channel | web.webPageDetails.siteSection | string | Variabile utilizzata nella dimensione Sezioni del sito. |
| m_domain | environment.domain | string | Variabile utilizzata nella dimensione Dominio. Il provider sarà il provider di servizi Internet (ISP) dell&#39;utente. |
| m_geo_city | placeContext.geo.city | string | Il nome della città dell’hit. Si basa sull’indirizzo IP dell’hit. |
| m_geo_dma | placeContext.geo.dmaID | numero intero | ID numerico dell’area demografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| m_geo_region | placeContext.geo.stateProvince | string | Il nome dello stato o dell’area geografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| m_geo_zip | placeContext.geo.postalCode | string | Il codice postale dell’hit. Si basa sull’indirizzo IP dell’hit. |
| m_parole chiave | search.keywords | string | Variabile utilizzata nella dimensione Parola chiave. |
| m_os | _experience.analytics.environment.operatingSystemID | numero intero | L’ID numerico che rappresenta il sistema operativo del visitatore. Si basa sulla colonna user_agent. |
| m_page_url | web.webPageDetails.URL | string | URL dell’hit pagina. |
| m_pagename_no_url | web.webPageDetails.</span>name | string | Variabile utilizzata per popolare la dimensione Pagine. |
| m_referrer | web.webReferrer.URL | string | URL della pagina precedente. |
| m_search_page_num | search.pageDepth | numero intero | Utilizzato dalla dimensione Classificazione di tutte le pagine di ricerca. Indica in quale pagina dei risultati di ricerca il sito è stato visualizzato prima che l’utente avesse fatto clic sul sito. |
| m_state | _experience.analytics.customDimensions.stateProvince | string | Variabile di stato. |
| m_user_server | web.webPageDetails.server | string | Variabile utilizzata nella dimensione Server. |
| m_zip | _experience.analytics.customDimensions.postalCode | string | Variabile utilizzata per popolare la dimensione Codice postale. |
| accept_language | environment.browserDetails.acceptLanguage | string | Elenca tutte le lingue accettate, come indicato nell’intestazione HTTP Accept-Language. |
| homepage | web.webPageDetails.isHomePage | booleano | Non più utilizzato. Indica se l’URL corrente è la home page del browser. |
| ipv6 | environment.ipV6 | string |
| j_jscript | environment.browserDetails.javaScriptVersion | string | La versione di JavaScript supportata dal browser. |
| user_agent | environment.browserDetails.userAgent | string | Stringa dell’agente utente inviata nell’intestazione HTTP. |
| mobileappid | applicazione.</span>name | string | L’ID dell’app mobile, memorizzato nel seguente formato: `[AppName][BundleVersion]`. |
| dispositivo mobile | device.model | string | Nome del dispositivo mobile. In iOS, viene memorizzato come stringa di 2 cifre separate da virgola. Il primo numero rappresenta la generazione del dispositivo e il secondo rappresenta la famiglia di dispositivi. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | string | Utilizzato da Mobile Services. Rappresenta il punto di interesse. |
| pointofinterestDISTANCE | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | number | Utilizzato da Mobile Services. Rappresenta la distanza del punto di interesse. |
| mobileplaceprecision | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | number | Raccolto dalla variabile di dati di contesto a.loc.acc. Indica la precisione del GPS in metri al momento della raccolta. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | string | Raccolto dalla variabile di dati di contesto a.loc.category. Descrive la categoria di un luogo specifico. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | string | Raccolto dalla variabile di dati di contesto a.loc.id. Identificatore per un dato punto di interesse. |
| video | media.mediaTimed.primaryAssetReference._id | string |  il nome del video. |
| videoad | advertising.adAssetReference._id | string | Identificatore della risorsa dell’annuncio. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | string | Il Tipo Di Contenuto Video. Viene automaticamente impostato su &quot;Video&quot; per tutte le visualizzazioni video. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | string | Il pod in cui si trova l’annuncio video. |
| videoadinpod | advertising.adAssetViewDetails.index | numero intero | La posizione dell’annuncio video nel pod. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | string | Nome del lettore video. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | string | Canale video. |
| videoadplayername | advertising.adAssetViewDetails.playerName | string | Nome del lettore di annunci video. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | string | Nome del capitolo Video |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | string | Il nome del video. |
| videoadname | advertising.adAssetReference._dc.title | string | Nome dell’annuncio video. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | string | Presentazione video. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | string | Stagione video. |
| videoepisodio | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | string | Episodio video. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | string | Rete video. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | string | Tipo di presentazione video. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | string | Caricamenti di annunci video. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | string | Tipo di feed video. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | number | Beacon principale di Mobile Services. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | number | Beacon secondario di Mobile Services. |
| mobilebeaconuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | string | UUID del beacon di Mobile Services. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | string | ID sessione video. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | array | Genere video. | {title (Oggetto), description (Oggetto), type (Oggetto), meta:xdmType (Oggetto), items (stringa), meta:xdmField (Oggetto)} |
| mobileinstalls | application.firstLaunches | Oggetto | Viene attivato alla prima esecuzione dopo l’installazione o la reinstallazione | {id (stringa), valore (numero)} |
| mobileupgrade | application.upgrades | Oggetto | Segnala il numero di aggiornamenti dell’app. Attiva alla prima esecuzione dopo l’aggiornamento o quando cambia il numero di versione. | {id (stringa), valore (numero)} |
| mobilelaunches | application.launches | Oggetto | Il numero di volte in cui l&#39;app è stata avviata. | {id (stringa), valore (numero)} |
| eruzioni cutanee | application.crashes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| mobilemessageclicks | directMarketing.clicks | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videotime | media.mediaTimed.timePlayed | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videostart | media.mediaTimed.impressions | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videocomplete | media.mediaTimed.completes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoadstart | advertising.impressions | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoadcomplete | advertising.completes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoadtime | advertising.timePlayed | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoplay | media.mediaTimed.starts | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Oggetto | Il tempo di avvio della qualità video. | {id (stringa), valore (numero)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Oggetto | Conteggio buffer qualità video | {id (stringa), valore (numero)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Oggetto | Tempo buffer qualità video | {id (stringa), valore (numero)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Oggetto | Conteggio dei cambiamenti nella qualità video | {id (stringa), valore (numero)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Oggetto | Bit rate medio della qualità video | {id (stringa), valore (numero)} |
| videoqoerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Oggetto | Conteggio errori nella qualità video | {id (stringa), valore (numero)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoprogress10 | media.mediaTimed.progress10 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoprogress25 | media.mediaTimed.progress25 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoprogress50 | media.mediaTimed.progress50 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoprogress75 | media.mediaTimed.progress75 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoprogress95 | media.mediaTimed.progress95 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoresume | media.mediaTimed.resumes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videopausecount | media.mediaTimed.pauses | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videopausetime | media.mediaTimed.pauseTime | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videosecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | numero intero |

{style="table-layout:auto"}

## Dividi campi di mappatura

Questi campi hanno un’unica origine, ma vengono mappati su **multiplo** Posizioni XDM.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | numero intero | ID numerico che rappresenta la risoluzione del monitoraggio. |
| mobileosversion | environment.operatingSystem, environment.operatingSystemVersion | string | Versione del sistema operativo mobile. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | numero intero | Lunghezza annuncio video. |

{style="table-layout:auto"}

## Campi di mappatura generati

Per poter essere generati in XDM, alcuni campi provenienti da ADC devono essere trasformati, richiedendo una logica che vada oltre una copia diretta da Adobe Analytics.

La tabella seguente include colonne che mostrano il nome del campo Analytics (*Campo Analytics*), il campo XDM corrispondente (*Campo XDM*) e il relativo tipo (*Tipo XDM*), nonché una descrizione del campo (*Descrizione*).

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Oggetto | Variabili di traffico personalizzate comprese tra 1 e 75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | Oggetto | Utilizzato da variabili gerarchiche. Contiene un | elenco delimitato di valori. | {values (array), delimitatore (stringa)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.LISTS.list1.list[] - _experience.analytics.customDimensions.LISTS.list3.list[] | array | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione | {value (stringa), key (stringa)} |
| m_color | device.colorDepth | numero intero | ID di profondità colore, basato sul valore della colonna c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | booleano | Variabile utilizzata nella dimensione Supporto cookie. |
| m_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | Oggetto | Eventi di e-commerce standard attivati sull’hit. | {id (stringa), valore (numero)} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to30 .event300, _experience.analytics.event301to400.event301 - _experience.analytics.event301to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event701 - _experience.analytics.event701to800.event800, experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Oggetto | Eventi personalizzati attivati sull’hit. | {id (Oggetto), value (Oggetto)} |
| m_geo_country | placeContext.geo.countryCode | string | Abbreviazione del paese da cui proviene l’hit, basata sul PI. |
| m_geo_latitude | placeContext.geo._schema.latitude | number | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | number | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | booleano | Flag che indica se Java è abilitato. |
| m_latitude | placeContext.geo._schema.latitude | number | <!-- MISSING --> |
| m_longitudine | placeContext.geo._schema.longitude | number | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | string | Variabile utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. Questa variabile contiene l’URL del collegamento di download, del collegamento di uscita o del collegamento personalizzato su cui è stato fatto clic. |
| m_page_event_var2 | web.webInteraction.name | string | Variabile utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. Elenca il nome personalizzato del collegamento, se specificato. |
| m_page_type | web.webPageDetails.isErrorPage | booleano | Variabile utilizzata per popolare la dimensione Pagine non trovate. Questa variabile deve essere vuota o contenere &quot;ErrorPage&quot;. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | number | Nome della pagina (se impostato). Se non viene specificata alcuna pagina, questo valore viene lasciato vuoto. |
| m_paid_search | search.isPaid | booleano | Flag impostato se l’hit corrisponde al rilevamento di ricerche a pagamento. |
| m_product_list | productListItems[].items | array | L’elenco dei prodotti, trasmesso attraverso la variabile dei prodotti. | {SKU (stringa), quantità (numero intero), priceTotal (numero)} |
| m_ref_type | web.webReferrer.type | string | Un ID numerico che rappresenta il tipo di riferimento per l’hit. 1 significa all&#39;interno del sito, 2 significa altri siti Web, 3 significa motori di ricerca, 4 significa disco rigido, 5 significa USENET, 6 significa Digitato/Contrassegnato con segnalibro (nessun referrer), 7 significa e-mail, 8 significa Nessun JavaScript e 9 significa Social Network. |
| m_search_engine | search.searchEngine | string | L’ID numerico che rappresenta il motore di ricerca che ha indirizzato il visitatore al sito. |
| post_currency | commerce.order.currencyCode | string | Codice valuta utilizzato durante la transazione. |
| post_cust_hit_time_gmt | timestamp | string | Viene utilizzato solo nei set di dati abilitati per le marche temporali. Questa è la marca temporale inviata con l’IT, in base all’ora Unix. |
| post_cust_visid | identityMap | oggetto | L’ID visitatore del cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | booleano | L’ID visitatore del cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | string | L’ID visitatore del cliente. |
| post_visid_high + visid_low | identityMap | oggetto | Un identificatore univoco per una visita. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | string | Un identificatore univoco per una visita. |
| post_visid_high | endUserIDs._experience.aaid.primary | booleano | Utilizzato insieme a visid_low per identificare in modo univoco una visita. |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | string | Utilizzato insieme a visid_low per identificare in modo univoco una visita. |
| post_visid_low | identityMap | oggetto | Utilizzato insieme a visid_high per identificare in modo univoco una visita. |
| hit_time_gmt | receivedTimestamp | string | La marca temporale dell’hit, in base all’ora Unix. |
| hitid_high + hitid_low | _id | string | Un identificatore univoco per identificare un hit. |
| hitid_low | _id | string | Utilizzato insieme a hitid_high per identificare in modo univoco un hit. |
| ip | environment.ipV4 | string | L’indirizzo IP, in base all’intestazione HTTP della richiesta di immagine. |
| j_jscript | environment.browserDetails.javaScriptEnabled | booleano | Versione di JavaScript utilizzata. |
| mcvisid_high + mcvisid_low | identityMap | oggetto | L’ID visitatore Experience Cloud. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | string | L’ID Experience Cloud (ECID) è noto anche come MCID e talvolta viene utilizzato negli spazi dei nomi. |
| mcvisid_high | endUserIDs._experience.mcid.primary | booleano | L’ID Experience Cloud (ECID) è noto anche come MCID e talvolta viene utilizzato negli spazi dei nomi. |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | string | L’ID Experience Cloud (ECID) è noto anche come MCID e talvolta viene utilizzato negli spazi dei nomi. |
| mcvisid_low | identityMap | oggetto | L’ID visitatore Experience Cloud. |
| sdid_high + sdid_low | _experience.target.supplementalDataID | string | Hit Stitching ID. Il campo di analisi sdid_high e sdid_low è l’ID di dati supplementare utilizzato per unire due (o più) hit in arrivo. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | string | Prossimità beacon di Mobile Services. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | numero intero | Il nome del capitolo video. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | numero intero | La lunghezza del video. |

{style="table-layout:auto"}

## Campi di mappatura avanzati

I campi selezionati (noti come &quot;postvalues&quot;) richiedono trasformazioni più avanzate prima di poter essere mappati correttamente dai campi di Adobe Analytics all’Experience Data Model (XDM). L’esecuzione di queste trasformazioni avanzate comporta l’utilizzo di Adobe Experience Platform Query Service e di funzioni predefinite (chiamate funzioni definite da Adobe) per la sessionizzazione, l’attribuzione e la deduplicazione.

Per ulteriori informazioni sull’esecuzione di queste trasformazioni utilizzando Query Service, visita [Funzioni definite da Adobe](../../../../query-service/sql/adobe-defined-functions.md) documentazione.

La tabella seguente include colonne che mostrano il nome del campo Analytics (*Campo Analytics*), il campo XDM corrispondente (*Campo XDM*) e il relativo tipo (*Tipo XDM*), nonché una descrizione del campo (*Descrizione*).

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Una variabile personalizzata, che può essere compresa tra 1 e 250. Ciascuna organizzazione utilizzerà queste eVar personalizzate in modo diverso. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variabili di traffico personalizzate, che possono essere comprese tra 1 e 75. |
| post_browser_height | environment.browserDetails.viewportHeight | numero intero | Altezza del browser, in pixel. |
| post_browser_width | environment.browserDetails.viewportWidth | numero intero | Larghezza del browser, in pixel. |
| post_campaign | marketing.trackingCode | string | Variabile utilizzata nella dimensione Codice di tracciamento. |
| post_channel | web.webPageDetails.siteSection | string | Variabile utilizzata nella dimensione Sezioni del sito. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | string | ID visitatore personalizzato, se impostato. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | string | L’URL della prima pagina raggiunta dal visitatore. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | string | Variabile utilizzata nella dimensione Pagina di ingresso originale. Il nome della pagina di ingresso del visitatore. |
| post_keywords | search.keywords | string | Parole chiave raccolte per l’hit. |
| post_page_url | web.webPageDetails.URL | string | URL dell’hit pagina. |
| post_pagename_no_url | web.webPageDetails.name | string | Variabile utilizzata per popolare la dimensione Pagine. |
| post_purchaseid | commerce.order.purchaseID | string | Variabile utilizzata per identificare in modo univoco gli acquisti. |
| post_referrer | web.webReferrer.URL | string | URL della pagina precedente. |
| post_state | _experience.analytics.customDimensions.stateProvince | string | Variabile di stato. |
| post_user_server | web.webPageDetails.server | string | Variabile utilizzata nella dimensione Server. |
| post_zip | _experience.analytics.customDimensions.postalCode | string | Variabile utilizzata per popolare la dimensione Codice postale. |
| browser | _experience.analytics.environment.browserID | numero intero | ID numerico del browser. |
| dominio | environment.domain | string | Variabile utilizzata nella dimensione Dominio. Il provider sarà il provider di servizi Internet (ISP) dell&#39;utente. |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | string | Il primo URL di riferimento per il visitatore. |
| geo_city | placeContext.geo.city | string | Il nome della città dell’hit. Si basa sull’indirizzo IP dell’hit. |
| geo_dma | placeContext.geo.dmaID | numero intero | ID numerico dell’area demografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| area_geografica | placeContext.geo.stateProvince | string | Il nome dello stato o dell’area geografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| geo_zip | placeContext.geo.postalCode | string | Il codice postale dell’hit. Si basa sull’indirizzo IP dell’hit. |
| sistema operativo | _experience.analytics.environment.operatingSystemID | numero intero | L’ID numerico che rappresenta il sistema operativo del visitatore. Si basa sulla colonna user_agent. |
| search_page_num | search.pageDepth | numero intero | Questa variabile viene utilizzata dalla dimensione Classificazione di tutte le pagine di ricerca e indica quale pagina di risultati di ricerca ha il sito | è apparso su prima che l’utente facesse clic sul sito. |
| visit_keywords | _experience.analytics.session.search.keywords | string | Variabile utilizzata nella dimensione Parole chiave di ricerca. |
| visit_num | _experience.analytics.session.num | numero intero | Variabile utilizzata nella dimensione Numero di visite. Inizia da 1 e viene incrementato ogni volta che inizia una nuova visita (per utente). |
| visit_page_num | _experience.analytics.session.depth | numero intero | Variabile utilizzata nella dimensione Profondità di hit. Questo valore aumenta di 1 per ogni hit generato dall’utente e viene ripristinato dopo ogni visita. |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | string | Il primo referrer della visita. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | numero intero | Nome della prima pagina della visita. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Oggetto | Variabili di traffico personalizzate da 1 a 75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | Oggetto | Utilizzato dalle variabili della gerarchia e contiene un elenco delimitato di valori. | {values (array), delimitatore (stringa)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.LISTS.list1.list[] - _experience.analytics.customDimensions.LISTS.list3.list[] | array | Elenco di valori di variabile. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. | {value (stringa), key (stringa)} |
| post_cookies | environment.browserDetails.cookiesEnabled | booleano | Variabile utilizzata nella dimensione Supporto cookie. |
| post_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | Oggetto | Eventi di e-commerce standard attivati sull’hit. | {id (stringa), valore (numero)} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to30 .event300, _experience.analytics.event301to400.event301 - _experience.analytics.event301to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event701 - _experience.analytics.event701to800.event800, experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Oggetto | Eventi personalizzati attivati sull’hit. | {id (Oggetto), value (Oggetto)} |
| post_java_enabled | environment.browserDetails.javaEnabled | booleano | Flag che indica se Java è abilitato. |
| post_latitude | placeContext.geo._schema.latitude | number | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | number | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | string | Tipo di hit inviato nella richiesta di immagine (hit standard, collegamento di download, collegamento di uscita o collegamento personalizzato su cui è stato fatto clic). |
| post_page_event | web.webInteraction.linkClicks.value | number | Tipo di hit inviato nella richiesta di immagine (hit standard, collegamento di download, collegamento di uscita o collegamento personalizzato su cui è stato fatto clic). |
| post_page_event_var1 | web.webInteraction.URL | string | Questa variabile viene utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. Questo è l’URL del collegamento di download, del collegamento di uscita o del collegamento personalizzato in cui è stato fatto clic. |
| post_page_event_var2 | web.webInteraction.name | string | Questa variabile viene utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. Questo sarà il nome personalizzato del collegamento. |
| post_page_type | web.webPageDetails.isErrorPage | booleano | Viene utilizzato per popolare la dimensione Pagine non trovate. Questa variabile deve essere vuota o contenere &quot;ErrorPage&quot; |
| post_pagename_no_url | web.webPageDetails.pageViews.value | number | Nome della pagina (se impostato). Se non viene specificata alcuna pagina, questo valore viene lasciato vuoto. |
| post_product_list | productListItems[].items | array | L’elenco dei prodotti, trasmesso attraverso la variabile dei prodotti. | {SKU (stringa), quantità (numero intero), priceTotal (numero)} |
| post_search_engine | search.searchEngine | string | L’ID numerico che rappresenta il motore di ricerca che ha indirizzato il visitatore al sito. |
| mvvar1_instances | .list.items[] | Oggetto | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. |
| mvvar2_instances | .list.items[] | Oggetto | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. |
|  | mvvar3_instances | .list.items[] | Oggetto | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. |
| colore | device.colorDepth | numero intero | ID profondità colore, in base al valore della colonna c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | string | ID numerico che rappresenta il tipo di referrer del primo referrer del visitatore. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | numero intero | Marca temporale del primo hit del visitatore in tempo Unix. |
| geo_country | placeContext.geo.countryCode | string | Abbreviazione del paese da cui proviene l’hit, basata su IP. |
| geo_latitude | placeContext.geo._schema.latitude | number | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | number | <!-- MISSING --> |
| paid_search | search.isPaid | booleano | Flag impostato se l’hit corrisponde al rilevamento di ricerche a pagamento. |
| ref_type | web.webReferrer.type | string | Un ID numerico che rappresenta il tipo di riferimento per l’hit. |
| visit_paid_search | _experience.analytics.session.search.isPaid | booleano | Un flag (1=a pagamento, 0=non a pagamento) che indica se il primo hit della visita proviene da un hit di ricerca a pagamento. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | string | ID numerico che rappresenta il tipo di referrer del primo referrer della visita. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | string | ID numerico del primo motore di ricerca della visita. |
| visit_start_time_gmt | _experience.analytics.session.timestamp | numero intero | Timestamp del primo hit della visita in tempo Unix. |

{style="table-layout:auto"}