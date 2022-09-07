---
keywords: Experience Platform;home;argomenti popolari;campi di mappatura di Analytics;mappatura di Analytics
solution: Experience Platform
title: Campi di mappatura per il connettore sorgente Adobe Analytics
topic-legacy: overview
description: Adobe Experience Platform consente di acquisire i dati di Adobe Analytics tramite l’origine Analytics. Alcuni dei dati acquisiti tramite ADC possono essere mappati direttamente dai campi di Analytics ai campi Experience Data Model (XDM), mentre altri dati richiedono trasformazioni e funzioni specifiche per essere mappati correttamente.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '3431'
ht-degree: 7%

---

# Mappature dei campi di Analytics

Adobe Experience Platform consente di acquisire i dati di Adobe Analytics tramite l’origine Analytics. Alcuni dei dati acquisiti tramite ADC possono essere mappati direttamente dai campi di Analytics ai campi Experience Data Model (XDM), mentre altri dati richiedono trasformazioni e funzioni specifiche per essere mappati correttamente.

![](../images/analytics-data-experience-platform.png)

## Campi di mappatura diretta

I campi selezionati sono mappati direttamente da Adobe Analytics a Experience Data Model (XDM).

La tabella seguente include colonne che mostrano il nome del campo Analytics (*Campo Analytics*), il campo XDM corrispondente (*Campo XDM*) e il relativo tipo (*Tipo XDM*), nonché una descrizione del campo (*Descrizione*).

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | stringa | Una variabile personalizzata che può variare da 1 a 250. Ciascuna organizzazione utilizza queste eVar personalizzate in modo diverso. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.prop.prop75 | stringa | Variabili di traffico personalizzate, che possono variare da 1 a 75. |
| m_browser | _experience.analytics.environment.browserID | numero intero | ID numero del browser. |
| m_browser_height | environment.browserDetails.viewportHeight | numero intero | Altezza del browser, in pixel. |
| m_browser_width | environment.browserDetails.viewportWidth | numero intero | Larghezza del browser, in pixel. |
| m_campaign | marketing.trackingCode | stringa | Variabile utilizzata nella dimensione Codice di tracciamento. |
| m_channel | web.webPageDetails.siteSection | stringa | Variabile utilizzata nella dimensione Sezioni del sito. |
| m_domain | environment.domain | stringa | Variabile utilizzata nella dimensione Domain. Questo sarà basato sul provider di servizi Internet (ISP) dell&#39;utente. |
| m_geo_city | placeContext.geo.city | stringa | Nome della città dell&#39;hit. Questo si basa sull’indirizzo IP dell’hit. |
| m_geo_dma | placeContext.geo.dmaID | numero intero | ID numerico dell&#39;area demografica per l&#39;hit. Questo si basa sull’indirizzo IP dell’hit. |
| m_geo_region | placeContext.geo.stateProvince | stringa | Nome dello stato o della regione dell&#39;hit. Questo si basa sull’indirizzo IP dell’hit. |
| m_geo_zip | placeContext.geo.postalCode | stringa | Il codice ZIP dell’hit. Questo si basa sull’indirizzo IP dell’hit. |
| m_keywords | search.keywords | stringa | Variabile utilizzata nella dimensione Parola chiave. |
| m_os | _experience.analytics.environment.operationSystemID | numero intero | L&#39;ID numerico che rappresenta il sistema operativo del visitatore. Si basa sulla colonna user_agent . |
| m_page_url | web.webPageDetails.URL | stringa | URL dell&#39;hit pagina. |
| m_pagename_no_url | web.webPageDetails.</span>name | stringa | Variabile utilizzata per compilare la dimensione Pagine. |
| m_referrer | web.webReferrer.URL | stringa | URL della pagina precedente. |
| m_search_page_num | search.pageDepth | numero intero | Utilizzato dalla dimensione Classifica pagina di ricerca. Indica in quale pagina dei risultati di ricerca il sito è stato visualizzato prima che l’utente avesse fatto clic sul sito. |
| m_state | _experience.analytics.customDimensions.stateProvince | stringa | Variabile di stato. |
| m_user_server | web.webPageDetails.server | stringa | Variabile utilizzata nella dimensione Server. |
| m_zip | _experience.analytics.customDimensions.postalCode | stringa | Variabile utilizzata per popolare la dimensione Codice postale. |
| accept_language | environment.browserDetails.acceptLanguage | stringa | Elenca tutte le lingue accettate, come indicato nell&#39;intestazione HTTP Accept-Language. |
| homepage | web.webPageDetails.isHomePage | booleano | Non più utilizzato. Indica se l’URL corrente è la home page del browser. |
| ipv6 | environment.ipV6 | stringa |
| j_jscript | environment.browserDetails.javaScriptVersion | stringa | Versione di JavaScript supportata dal browser. |
| user_agent | environment.browserDetails.userAgent | stringa | Stringa dell&#39;agente utente inviata nell&#39;intestazione HTTP. |
| mobileappid | applicazione.</span>name | stringa | L&#39;ID dell&#39;app mobile, memorizzato nel seguente formato: `[AppName][BundleVersion]`. |
| dispositivo mobile | device.model | stringa | Nome del dispositivo mobile. In iOS, viene memorizzato come stringa di 2 cifre separate da virgola. Il primo numero rappresenta la generazione del dispositivo e il secondo numero rappresenta la famiglia di dispositivi. |
| puntiniere | placeContext.POIinteraction.POIDetail.</span>name | stringa | Utilizzato da mobile services. Rappresenta il punto di interesse. |
| puntofinterestdistanza | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | numero | Utilizzato da mobile services. Rappresenta la distanza del punto di interesse. |
| mobile segnaposto precisione | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | numero | Raccolto dalla variabile di dati di contesto a.loc.acc. Indica la precisione del GPS in metri al momento della raccolta. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | stringa | Raccolto dalla variabile di dati di contesto a.loc.category. Descrive la categoria di un luogo specifico. |
| mobileplacid | placeContext.POIinteraction.POIDetail.POIID | stringa | Raccolto dalla variabile di dati di contesto a.loc.id. Identificatore per un dato punto di interesse. |
| video | media.mediaTimed.primaryAssetReference._id | stringa | Nome del video. |
| video | advertising.adAssetReference._id | stringa | Identificatore della risorsa dell’annuncio. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | stringa | Tipo Di Contenuto Video. Questa opzione viene impostata automaticamente su &quot;Video&quot; per tutte le visualizzazioni video. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | stringa | Il pod in cui si trova l’annuncio video. |
| videoadinpod | advertising.adAssetViewDetails.index | numero intero | La posizione dell’annuncio video nel pod. |
| videoplayname | media.mediaTimed.primaryAssetViewDetails.playerName | stringa | Nome del lettore video. |
| canale video | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | stringa | Il canale video. |
| videoadplayername | advertising.adAssetViewDetails.playerName | stringa | Il nome del lettore Video Ad. |
| videocapitolo | media.mediaTimed.mediaChapter.chapterAssetReference._id | stringa | Nome del capitolo video |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | stringa | Nome del video. |
| videoadname | advertising.adAssetReference._dc.title | stringa | Nome dell&#39;annuncio video. |
| video | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | stringa | Video. |
| videoconferenza | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | stringa | Video Stagione. |
| video episodio | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | stringa | episodio video. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | stringa | Rete video. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | stringa | Tipo di presentazione video. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | stringa | Caricamenti degli annunci video. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | stringa | Tipo di feed video. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | numero | beacon principale di Mobile Services. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | numero | beacon secondario di Mobile Services. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | stringa | UUID beacon di Mobile Services. |
| videosess ionid | media.mediaTimed.primaryAssetViewDetails._id | stringa | ID sessione video. |
| videogame | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | array | Genere video. | {title (Oggetto), description (Oggetto), tipo (Oggetto), meta:xdmType (Oggetto), elementi (stringa), meta:xdmField (Oggetto)} |
| mobileinstalls | application.firstLaunches | Oggetto | Viene attivato alla prima esecuzione dopo l&#39;installazione o reinstallazione | {id (stringa), valore (numero)} |
| dispositivi mobili | application.upgrades | Oggetto | Segnala il numero di aggiornamenti dell’app. Attiva alla prima esecuzione dopo l&#39;aggiornamento o ogni volta che cambia il numero di versione. | {id (stringa), valore (numero)} |
| mobilelaunches | application.launches | Oggetto | Il numero di volte in cui l’app è stata avviata. | {id (stringa), valore (numero)} |
| manifestazioni | application.crashes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| mobilemessageclicks | directMarketing.clicks | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| mobilesegnaposto | placeContext.POIinteraction.poiEntries | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| mobilesegnaposto exit | placeContext.POIinteraction.poiExits | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| tempo video | media.mediaTimed.timePlayed | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videostart | media.mediaTimed.impressions | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| video | media.mediaTimed.completes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| video segmentevisualizzazioni | media.mediaTimed.mediaSegmentViews | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| avvio video | advertising.impressions | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoadcomplete | advertising.completes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoconferenza | advertising.timePlayed | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoconferenza | media.mediaTimed.mediaChapter.timePlayed | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| video | media.mediaTimed.starts | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Oggetto | Tempo di avvio della qualità video. | {id (stringa), valore (numero)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Oggetto | Conteggio buffer qualità video | {id (stringa), valore (numero)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Oggetto | Tempo buffer qualità video | {id (stringa), valore (numero)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Oggetto | Conteggio dei cambiamenti nella qualità video | {id (stringa), valore (numero)} |
| videoqoebitratemedia | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Oggetto | Bit rate medio della qualità video | {id (stringa), valore (numero)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Oggetto | Numero di errori nella qualità video | {id (stringa), valore (numero)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| video-progress10 | media.mediaTimed.progress10 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| video-progress25 | media.mediaTimed.progress25 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| video-progress50 | media.mediaTimed.progress50 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| video progress75 | media.mediaTimed.progress75 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| video progress95 | media.mediaTimed.progress95 | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoresume | media.mediaTimed.resumes | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videopausecount | media.mediaTimed.pauses | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videopausetime | media.mediaTimed.pauseTime | Oggetto | <!-- MISSING --> | {id (stringa), valore (numero)} |
| videoseconssincelastic | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | numero intero |

{style=&quot;table-layout:auto&quot;}

## Campi di mappatura suddivisi

Questi campi hanno una singola origine, ma mappano a **multiplo** Posizioni XDM.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | numero intero | ID numerico che rappresenta la risoluzione del monitoraggio. |
| mobileosversion | environment.operationSystem, environment.operationsSystemVersion | stringa | Versione del sistema operativo mobile. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | numero intero | Lunghezza dell&#39;annuncio video. |

{style=&quot;table-layout:auto&quot;}

## Campi di mappatura generati

Per generare in XDM, è necessario trasformare i campi selezionati provenienti da ADC e richiede logica oltre una copia diretta da Adobe Analytics.

La tabella seguente include colonne che mostrano il nome del campo Analytics (*Campo Analytics*), il campo XDM corrispondente (*Campo XDM*) e il relativo tipo (*Tipo XDM*), nonché una descrizione del campo (*Descrizione*).

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Oggetto | Variabili di traffico personalizzate, comprese tra 1 e 75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.Hierarchies.hier1 - _experience.analytics.customDimensions.Hierarchies.hier5 | Oggetto | Utilizzato da variabili gerarchiche. Contiene un | elenco delimitato di valori. | {valori (matrice), delimitatore (stringa)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list.list3.list[] | array | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione | {valore (stringa), chiave (stringa)} |
| m_color | device.colorDepth | numero intero | L&#39;ID della profondità colore, basato sul valore della colonna c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | booleano | Variabile utilizzata nella dimensione Supporto cookie. |
| m_event_list | commerce.purchased, commerce.productViews, commerce.productListAperture, commerce.checkout, commerce.productListAdd, commerce.productListRemovals, commerce.productListViews | Oggetto | Eventi di e-commerce standard attivati sull’hit. | {id (stringa), valore (numero)} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event20 , _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event30 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 01to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Oggetto | Eventi personalizzati attivati sull&#39;hit. | {id (oggetto), valore (oggetto)} |
| m_geo_country | placeContext.geo.countryCode | stringa | Abbreviazione del paese da cui proviene l’hit, basato sul PI. |
| m_geo_latitude | placeContext.geo._schema.latitude | numero | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | numero | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | booleano | Flag che indica se Java è abilitato. |
| m_latitude | placeContext.geo._schema.latitude | numero | <!-- MISSING --> |
| m_longitude | placeContext.geo._schema.longitude | numero | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | stringa | Variabile utilizzata solo nelle richieste di immagini di tracciamento dei collegamenti. Questa variabile contiene l’URL del collegamento di download, del collegamento di uscita o del collegamento personalizzato su cui è stato fatto clic. |
| m_page_event_var2 | web.webInteraction.name | stringa | Variabile utilizzata solo nelle richieste di immagini di tracciamento dei collegamenti. In questo modo viene elencato il nome personalizzato del collegamento, se specificato. |
| m_page_type | web.webPageDetails.isErrorPage | booleano | Variabile utilizzata per compilare la dimensione Pagine non trovate. Questa variabile deve essere vuota o contenere &quot;ErrorPage&quot;. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | numero | Nome della pagina (se impostato). Se non viene specificata alcuna pagina, questo valore viene lasciato vuoto. |
| m_paid_search | search.isPaid | booleano | Flag impostato se l&#39;hit corrisponde al rilevamento di ricerca a pagamento. |
| m_product_list | productListItems[].items | array | L’elenco dei prodotti, come trasmesso attraverso la variabile dei prodotti. | {SKU (stringa), quantità (numero intero), prezzoTotale (numero)} |
| m_ref_type | web.webReferrer.type | stringa | Un ID numerico che rappresenta il tipo di riferimento per l&#39;hit. 1 significa all&#39;interno del tuo sito, 2 significa altri siti web, 3 significa motori di ricerca, 4 significa disco rigido, 5 significa USENET, 6 significa Digitato/Segnalibro (nessun referrer), 7 significa e-mail, 8 significa No JavaScript, e 9 significa Social Networks. |
| m_search_engine | search.searchEngine | stringa | L&#39;ID numerico che rappresenta il motore di ricerca che ha indirizzato il visitatore al sito. |
| post_currency | commerce.order.currencyCode | stringa | Codice valuta utilizzato durante la transazione. |
| post_cust_hit_time_gmt | timestamp | stringa | Viene utilizzato solo nei set di dati abilitati per le marche temporali. Si tratta della marca temporale inviata con , in base all’ora Unix. |
| post_cust_visid | identityMap | oggetto | ID visitatore del cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | booleano | ID visitatore del cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | stringa | ID visitatore del cliente. |
| post_visid_high + visid_low | identityMap | oggetto | Identificatore univoco per una visita. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | stringa | Identificatore univoco per una visita. |
| post_visid_high | endUserIDs._experience.aaid.primary | booleano | Utilizzato in combinazione con visid_low per identificare in modo univoco una visita. |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | stringa | Utilizzato in combinazione con visid_low per identificare in modo univoco una visita. |
| post_visid_low | identityMap | oggetto | Utilizzato in combinazione con visid_high per identificare in modo univoco una visita. |
| hit_time_gmt | ReceivedTimestamp | stringa | La marca temporale dell’hit, in base al tempo Unix. |
| hitid_high + hitid_low | _id | stringa | Identificatore univoco per identificare un hit. |
| hitid_low | _id | stringa | Utilizzato in combinazione con hitid_high per identificare in modo univoco un hit. |
| ip | environment.ipV4 | stringa | Indirizzo IP, basato sull&#39;intestazione HTTP della richiesta di immagine. |
| j_jscript | environment.browserDetails.javaScriptEnabled | booleano | Versione di JavaScript utilizzata. |
| mcvisid_high + mcvisid_low | identityMap | oggetto | ID visitatore Experience Cloud. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | stringa | L’ID Experience Cloud (ECID) è noto anche come MCID e a volte viene utilizzato nei namespace. |
| mcvisid_high | endUserIDs._experience.mcid.primary | booleano | L’ID Experience Cloud (ECID) è noto anche come MCID e a volte viene utilizzato nei namespace. |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | stringa | L’ID Experience Cloud (ECID) è noto anche come MCID e a volte viene utilizzato nei namespace. |
| mcvisid_low | identityMap | oggetto | ID visitatore Experience Cloud. |
| sdid_high + sdid_low | _experience.target.supplementalDataID | stringa | ID unione hit. Il campo di analisi sdid_high e sdid_low è l’ID di dati supplementare utilizzato per unire due (o più) hit in arrivo. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | stringa | Prossimità del beacon di Mobile Services. |
| videocapitolo | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | numero intero | Nome del capitolo video. |
| lunghezza di video | media.mediaTimed.primaryAssetReference._xmpDM.duration | numero intero | Lunghezza del video. |

{style=&quot;table-layout:auto&quot;}

## Campi di mappatura avanzati

Per poter essere mappati correttamente dai campi Adobe Analytics a Experience Data Model (XDM), alcuni campi selezionati (noti come &quot;postvalues&quot;) richiedono trasformazioni più avanzate. L’esecuzione di queste trasformazioni avanzate comporta l’utilizzo di Adobe Experience Platform Query Service e di funzioni precompilate (chiamate funzioni definite da Adobe) per la sessionizzazione, l’attribuzione e la deduplicazione.

Per ulteriori informazioni sull’esecuzione di queste trasformazioni tramite Query Service, visita la [Funzioni definite dall&#39;Adobe](../../../../query-service/sql/adobe-defined-functions.md) documentazione.

La tabella seguente include colonne che mostrano il nome del campo Analytics (*Campo Analytics*), il campo XDM corrispondente (*Campo XDM*) e il relativo tipo (*Tipo XDM*), nonché una descrizione del campo (*Descrizione*).

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Campo Analytics | Campo XDM | Tipo XDM | Descrizione |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | stringa | Una variabile personalizzata che può variare da 1 a 250. Ciascuna organizzazione utilizza queste eVar personalizzate in modo diverso. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.prop.prop75 | stringa | Variabili di traffico personalizzate, che possono variare da 1 a 75. |
| post_browser_height | environment.browserDetails.viewportHeight | numero intero | Altezza del browser, in pixel. |
| post_browser_width | environment.browserDetails.viewportWidth | numero intero | Larghezza del browser, in pixel. |
| post_campaign | marketing.trackingCode | stringa | Variabile utilizzata nella dimensione Codice di tracciamento. |
| post_channel | web.webPageDetails.siteSection | stringa | Variabile utilizzata nella dimensione Sezioni del sito. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | stringa | L&#39;ID visitatore personalizzato, se impostato. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | stringa | URL della prima pagina raggiunta dal visitatore. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | stringa | Variabile utilizzata nella dimensione Originale della pagina di ingresso. Il nome della pagina della pagina di ingresso del visitatore. |
| post_keywords | search.keywords | stringa | Le parole chiave raccolte per l’hit. |
| post_page_url | web.webPageDetails.URL | stringa | URL dell&#39;hit pagina. |
| post_pagename_no_url | web.webPageDetails.name | stringa | Variabile utilizzata per compilare la dimensione Pagine. |
| post_purchaseid | commerce.order.purchaseID | stringa | Variabile utilizzata per identificare in modo univoco gli acquisti. |
| post_referrer | web.webReferrer.URL | stringa | URL della pagina precedente. |
| post_state | _experience.analytics.customDimensions.stateProvince | stringa | Variabile di stato. |
| post_user_server | web.webPageDetails.server | stringa | Variabile utilizzata nella dimensione Server. |
| post_zip | _experience.analytics.customDimensions.postalCode | stringa | Variabile utilizzata per popolare la dimensione Codice postale. |
| browser | _experience.analytics.environment.browserID | numero intero | ID numerico del browser. |
| dominio | environment.domain | stringa | Variabile utilizzata nella dimensione Domain. Questo sarà basato sul provider di servizi Internet (ISP) dell&#39;utente. |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | stringa | Il primo URL di riferimento per il visitatore. |
| geo_city | placeContext.geo.city | stringa | Nome della città dell&#39;hit. Questo si basa sull’indirizzo IP dell’hit. |
| geo_dma | placeContext.geo.dmaID | numero intero | ID numerico dell&#39;area demografica per l&#39;hit. Questo si basa sull’indirizzo IP dell’hit. |
| area geografica | placeContext.geo.stateProvince | stringa | Nome dello stato o della regione dell&#39;hit. Questo si basa sull’indirizzo IP dell’hit. |
| geo_zip | placeContext.geo.postalCode | stringa | Il codice ZIP dell’hit. Questo si basa sull’indirizzo IP dell’hit. |
| os | _experience.analytics.environment.operationSystemID | numero intero | L&#39;ID numerico che rappresenta il sistema operativo del visitatore. Si basa sulla colonna user_agent . |
| search_page_num | search.pageDepth | numero intero | Questa variabile viene utilizzata dalla dimensione Classifica tutte le pagine di ricerca e indica quale pagina di risultati di ricerca del sito | è apparso il prima che l’utente facesse clic sul sito. |
| visit_keywords | _experience.analytics.session.search.keywords | stringa | Variabile utilizzata nella dimensione Parole chiave di ricerca. |
| visit_num | _experience.analytics.session.num | numero intero | Variabile utilizzata nella dimensione Numero visita. Questo inizia a 1 e viene incrementato ogni volta che inizia una nuova visita (per utente). |
| visit_page_num | _experience.analytics.session.depth | numero intero | Variabile utilizzata nella dimensione Profondità di hit. Questo valore aumenta di 1 per ogni hit generato dall’utente e viene reimpostato dopo ogni visita. |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | stringa | Il primo referente della visita. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | numero intero | Nome pagina della visita. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Oggetto | Variabili di traffico personalizzate da 1 a 75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.Hierarchies.hier1 - _experience.analytics.customDimensions.Hierarchies.hier5 | Oggetto | Utilizzato da variabili gerarchiche e contiene un elenco delimitato di valori. | {valori (matrice), delimitatore (stringa)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list.list3.list[] | array | Elenco di valori variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. | {valore (stringa), chiave (stringa)} |
| post_cookies | environment.browserDetails.cookiesEnabled | booleano | Variabile utilizzata nella dimensione Supporto cookie. |
| post_event_list | commerce.purchased, commerce.productViews, commerce.productListAperture, commerce.checkout, commerce.productListAdd, commerce.productListRemovals, commerce.productListViews | Oggetto | Eventi di e-commerce standard attivati sull’hit. | {id (stringa), valore (numero)} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event20 , _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event30 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 01to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Oggetto | Eventi personalizzati attivati sull&#39;hit. | {id (oggetto), valore (oggetto)} |
| post_java_enabled | environment.browserDetails.javaEnabled | booleano | Flag che indica se Java è abilitato. |
| post_latitude | placeContext.geo._schema.latitude | numero | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | numero | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | stringa | Tipo di hit inviato nella richiesta di immagine (hit standard, collegamento per il download, collegamento di uscita o collegamento personalizzato cliccato). |
| post_page_event | web.webInteraction.linkClicks.value | numero | Tipo di hit inviato nella richiesta di immagine (hit standard, collegamento per il download, collegamento di uscita o collegamento personalizzato cliccato). |
| post_page_event_var1 | web.webInteraction.URL | stringa | Questa variabile viene utilizzata solo nelle richieste di immagini di tracciamento dei collegamenti. Questo è l’URL del collegamento di download, del collegamento di uscita o del collegamento personalizzato su cui hai fatto clic. |
| post_page_event_var2 | web.webInteraction.name | stringa | Questa variabile viene utilizzata solo nelle richieste di immagini di tracciamento dei collegamenti. Questo sarà il nome personalizzato del collegamento. |
| post_page_type | web.webPageDetails.isErrorPage | booleano | Viene utilizzato per compilare la dimensione Pagine non trovate. Questa variabile deve essere vuota o contenere &quot;ErrorPage&quot; |
| post_pagename_no_url | web.webPageDetails.pageViews.value | numero | Nome della pagina (se impostato). Se non viene specificata alcuna pagina, questo valore viene lasciato vuoto. |
| post_product_list | productListItems[].items | array | L’elenco dei prodotti, come trasmesso attraverso la variabile dei prodotti. | {SKU (stringa), quantità (numero intero), prezzoTotale (numero)} |
| post_search_engine | search.searchEngine | stringa | L&#39;ID numerico che rappresenta il motore di ricerca che ha indirizzato il visitatore al sito. |
| mvvar1_instances | .list.items[] | Oggetto | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. |
| mvvar2_instances | .list.items[] | Oggetto | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. |
|  | mvvar3_instances | .list.items[] | Oggetto | Elenco dei valori delle variabili. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. |
| color | device.colorDepth | numero intero | ID profondità colore, in base al valore della colonna c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | stringa | L&#39;ID numerico che rappresenta il tipo di referente del primo referente del visitatore. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | numero intero | Timestamp del primo hit del visitatore in tempo Unix. |
| geo_country | placeContext.geo.countryCode | stringa | Abbreviazione del paese da cui proviene l&#39;hit, basata su IP. |
| geo_latitude | placeContext.geo._schema.latitude | numero | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | numero | <!-- MISSING --> |
| paid_search | search.isPaid | booleano | Flag impostato se l&#39;hit corrisponde al rilevamento di ricerca a pagamento. |
| ref_type | web.webReferrer.type | stringa | Un ID numerico che rappresenta il tipo di riferimento per l&#39;hit. |
| visit_paid_search | _experience.analytics.session.search.isPaid | booleano | Flag (1=paid, 0=not paid) che indica se il primo hit della visita proviene da un hit di ricerca a pagamento. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | stringa | ID numerico che rappresenta il tipo di referente del primo referente della visita. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | stringa | ID numerico del primo motore di ricerca della visita. |
| visit_start_time_gmt | _experience.analytics.session.timestamp | numero intero | Timestamp del primo hit della visita in tempo Unix. |

{style=&quot;table-layout:auto&quot;}