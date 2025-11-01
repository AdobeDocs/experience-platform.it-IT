---
title: Mappatura dei campi per il connettore Source di Adobe Analytics
description: Mappa i campi Adobe Analytics ai campi XDM utilizzando il connettore Source di Analytics.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '3832'
ht-degree: 5%

---

# Mappature dei campi di Analytics

Adobe Experience Platform consente di acquisire dati da Adobe Analytics tramite l’origine Analytics. Alcuni dei dati acquisiti tramite ADC possono essere mappati direttamente dai campi di Analytics ai campi Experience Data Model (XDM), mentre altri dati richiedono trasformazioni e funzioni specifiche per essere mappati correttamente.

![Illustrazione del percorso di dati di Adobe Analytics da Analytics ad Experience Platform.](../images/analytics-data-experience-platform.png)

## Parametri per contenuti multimediali in streaming

Leggi la tabella seguente per informazioni sui parametri dei contenuti multimediali in streaming.

| Feed dati | Percorso campo XDM | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| `videoname` | `mediaReporting.sessionDetails.friendlyName` | stringa | Il nome descrittivo (leggibile dall’uomo) del video. |
| `videoaudioauthor` | `mediaReporting.sessionDetails.author` | stringa | Nome dell’autore del contenuto multimediale. |
| `videoaudioartist` | `mediaReporting.sessionDetails.artist` | stringa | Nome dell&#39;artista o del gruppo dell&#39;album che esegue la registrazione musicale o il video. |
| `videoaudioalbum` | `mediaReporting.sessionDetails.album` | stringa | Il nome dell&#39;album a cui appartiene la registrazione musicale o il video. |
| `videolength` | `mediaReporting.sessionDetails.length` | intero | Durata o runtime del video. |
| `videoshowtype` | `mediaReporting.sessionDetails.showType` | stringa |  |
| `video` | `mediaReporting.sessionDetails.name` | stringa | ID del video. |
| `videoshow` | `mediaReporting.sessionDetails.show` | stringa | Nome del programma o della serie. Il nome del programma o della serie è necessario solo se lo spettacolo fa parte di una serie. |
| `videostreamtype` | mediaReporting.sessionDetails.streamType | stringa | Il tipo di contenuti multimediali in streaming, ad esempio &quot;video&quot; o &quot;audio&quot;. |
| `videoseason` | `mediaReporting.sessionDetails.season` | stringa | Il numero di stagione a cui appartiene lo spettacolo. Questo valore è necessario solo se la presentazione fa parte di una serie. |
| `videoepisode` | `mediaReporting.sessionDetails.episode` | stringa | Numero dell’episodio. |
| `videogenre` | `mediaReporting.sessionDetails.genreList[]` | stringa[] | Il genere del video. |
| `videosessionid` | `mediaReporting.sessionDetails.ID` | stringa | Identificatore di un’istanza di un flusso di contenuto univoco per una singola riproduzione. |
| `videoplayername` | `mediaReporting.sessionDetails.playerName` | stringa | Nome del lettore video. |
| `videochannel` | `mediaReporting.sessionDetails.channel` | stringa | Il canale di distribuzione da cui è stato riprodotto il contenuto. |
| `videocontenttype` | `mediaReporting.sessionDetails.contentType` | stringa | Tipo di consegna del flusso utilizzato per il contenuto. Viene automaticamente impostato su &quot;Video&quot; per tutte le visualizzazioni video. I valori consigliati includono: VOD, Live, Linear, UGC, DVOD, Radio, Podcast, Audiook e Song. |
| `videonetwork` | `mediaReporting.sessionDetails.network` | stringa | Il nome della rete o del canale. |
| `videofeedtype` | `mediaReporting.sessionDetails.feed` | stringa | Tipo di feed. Può rappresentare dati effettivi relativi al feed, ad esempio &quot;East HD&quot; o &quot;SD&quot;, oppure la sorgente del feed, ad esempio un URL. |
| `videosegment` | `mediaReporting.sessionDetails.segment` | stringa |  |
| `videostart` | `mediaReporting.sessionDetails.isViewed` | booleano | Valore booleano che indica se il video è stato avviato o meno. Ciò si verifica una volta che l’utente seleziona il pulsante di riproduzione e conta anche in presenza di annunci pre-roll, buffering, errori e così via. |
| `videoplay` | `mediaReporting.sessionDetails.isPlayed` | booleano | Valore booleano che indica se il primo fotogramma del file multimediale è stato avviato. Se l’utente abbandona durante gli annunci o il tempo di buffering, l’avvio del contenuto non è idoneo. |
| `videotime` | `mediaReporting.sessionDetails.timePlayed` | intero | Durata (in secondi) di tutti gli eventi di `type=PLAY` sul contenuto principale. |
| `videocomplete` | `mediaReporting.sessionDetails.isCompleted` | booleano | Valore booleano che indica se una risorsa multimediale a tempo è stata guardata fino al completamento. Questo valore non significa necessariamente che il visualizzatore abbia guardato l’intero video, perché non tiene conto del fatto che potrebbe ignorare tutto. |
| `videototaltime` | `mediaReporting.sessionDetails.totalTimePlayed` | intero | La quantità totale di tempo trascorso da un utente su una specifica risorsa multimediale a tempo, incluso il tempo trascorso a guardare gli annunci. |
| `videouniquetimeplayed` | `mediaReporting.sessionDetails.uniqueTimePlayed` | intero | La somma degli intervalli univoci visualizzati da un utente su una risorsa multimediale a tempo. In altre parole, la lunghezza degli intervalli di riproduzione visualizzati più volte viene conteggiata una sola volta. |
| `videoaverageminuteaudience` | `mediaReporting.sessionDetails.averageMinuteAudience` | numero | Tempo medio di contenuto trascorso per un elemento multimediale specifico. In altre parole, il tempo totale di contenuto trascorso diviso per la lunghezza di tutte le sessioni di riproduzione. |
| `videoprogress10` | `mediaReporting.sessionDetails.hasProgress10` | booleano | Valore booleano che indica se l’indicatore di riproduzione di un determinato video ha superato l’indicatore del 10% della lunghezza totale del video. L’indicatore viene conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| `videoprogress25` | `mediaReporting.sessionDetails.hasProgress25` | booleano | Valore booleano che indica se l’indicatore di riproduzione di un determinato video ha superato l’indicatore del 25% della lunghezza totale del video. L’indicatore viene conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| `videoprogress50` | `mediaReporting.sessionDetails.hasProgress50` | booleano | Valore booleano che indica se l’indicatore di riproduzione di un determinato video ha superato l’indicatore del 50% della lunghezza totale del video. L’indicatore viene conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| `videoprogress75` | `mediaReporting.sessionDetails.hasProgress75` | booleano | Valore booleano che indica se l’indicatore di riproduzione di un determinato video ha superato l’indicatore del 75% della lunghezza totale del video. L’indicatore viene conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| `videoprogress95` | `mediaReporting.sessionDetails.hasProgress95` | booleano | Valore booleano che indica se l’indicatore di riproduzione di un determinato video ha superato l’indicatore del 95% della lunghezza totale del video. L’indicatore viene conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| `videopause` | `mediaReporting.sessionDetails.hasPauseImpactedStreams` | booleano | Valore booleano che indica se si sono verificate una o più pause durante la riproduzione di un singolo elemento multimediale. |
| `videopausecount` | `mediaReporting.sessionDetails.pauseCount` | intero | Il numero di periodi di pausa che si sono verificati durante la riproduzione. |
| `videopausetime` | `mediaReporting.sessionDetails.pauseTime` | intero | Durata totale (in secondi) della sospensione della riproduzione da parte di un utente. |
| `videomvpd` | `mediaReporting.sessionDetails.mvpd` | stringa | Un identificatore MVPD fornito tramite l’autenticazione Adobe. |
| `videoauthorized` | `mediaReporting.sessionDetails.authorized` | stringa | Definisce che l’utente è stato autorizzato tramite l’autenticazione Adobe. |
| `videodaypart` | `mediaReporting.sessionDetails.dayPart` | Definisce l’ora del giorno in cui il contenuto è stato trasmesso o riprodotto. |  |
| `videoresume` | `mediaReporting.sessionDetails.hasResume` | booleano | Valore booleano che contrassegna ogni riproduzione ripresa dopo più di 30 minuti di buffer, pausa o interruzione. |
| `videosegmentviews` | `mediaReporting.sessionDetails.hasSegmentView` | booleano | Valore booleano che indica che è stato visualizzato almeno un frame. Non è necessario che questo fotogramma sia il primo. |
| `videoaudiolabel` | `mediaReporting.sessionDetails.label` | stringa | Nome dell&#39;etichetta discografica. |
| `videoaudiostation` | `mediaReporting.sessionDetails.station` | stringa | La stazione radio o il nome su cui viene riprodotto l&#39;audio. |
| `videoaudiopublisher` | `mediaReporting.sessionDetails.publisher` | stringa | Nome dell&#39;autore del contenuto audio. |
| `videosecondssincelastcall` | `mediaReporting.sessionDetails.secondsSinceLastCall` | numero | Indica il tempo (in secondi) trascorso tra l’ultima interazione nota di un utente e il momento in cui la sessione è stata chiusa. |
| `videoadload` | `mediaReporting.sessionDetails.adLoad` | stringa | Il tipo di annuncio caricato come definito dalla rappresentazione interna. |

{style="table-layout:auto"}

## Parametri di Advertising

Leggi la tabella seguente per informazioni sui parametri pubblicitari.

| Feed dati | Percorso campo XDM | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| `videoad` | `mediaReporting.advertisingDetails.name` | stringa | Nome dell’annuncio. Nella generazione rapporti, &quot;Nome annuncio&quot; è la classificazione e &quot;Nome annuncio (variabile)&quot; è l’eVar. |
| `videoadinpod` | `mediaReporting.advertisingDetails.podPosition` | intero | L’indice dell’annuncio all’interno dell’inizio dell’annuncio principale. Ad esempio, il primo annuncio ha indice 0 e il secondo 1. |
| `videoadlength` | `mediaReporting.advertisingDetails.length` | intero | La lunghezza dell’annuncio video, misurata in secondi. |
| `videoadplayername` | `mediaReporting.advertisingDetails.playerName` | stringa | Nome del lettore utilizzato per il rendering dell’annuncio. |
| `videoadpod` | `mediaReporting.advertisingPodDetails.ID` | stringa | ID dell’interruzione pubblicitaria. |
| `videoadname` | `mediaReporting.advertisingDetails.friendlyName` | stringa | Il nome descrittivo (leggibile dall’uomo) dell’interruzione pubblicitaria. |
| `videoadadvertiser` | `mediaReporting.advertisingDetails.advertiser` | stringa | Azienda o marchio il cui prodotto è presentato nell’annuncio. |
| `videoadcampaign` | `mediaReporting.advertisingDetails.campaignID` | stringa | ID della campagna pubblicitaria. |
| `videoadstart` | `mediaReporting.advertisingDetails.isStarted` | booleano | Valore booleano che indica se l’annuncio è stato avviato o meno. |
| `videoadcomplete` | `mediaReporting.advertisingDetails.isCompleted` | booleano | Valore booleano che indica se l’era stata completata o meno. |
| `videoadtime` | `mediaReporting.advertisingDetails.timePlayed` | intero | La quantità totale di tempo, misurata in secondi, trascorso a guardare l’annuncio. |

{style="table-layout:auto"}

## Parametri del capitolo

Per informazioni sui parametri dei capitoli, leggere la tabella seguente.

| Feed dati | Percorso campo XDM | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| `videochapter` | `mediaReporting.chapterDetails.ID` | stringa | ID del capitolo generato automaticamente. |
| `videochapterstart` | `mediaReporting.chapterDetails.isStarted` | booleano | Valore booleano che indica se il capitolo è stato avviato o meno. |
| `videochaptercomplete` | `mediaReporting.chapterDetails.isCompleted` | booleano | Valore booleano che indica se il capitolo è stato completato o meno. |
| `videochaptertime` | `mediaReporting.chapterDetails.timePlayed` | intero | Il tempo, misurato in secondi, trascorso sul capitolo. |

{style="table-layout:auto"}

## Parametri dello stato del lettore

Leggi la tabella seguente per informazioni sui parametri dello stato del lettore.

| Feed dati | Percorso campo XDM | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| `videostatefullscreen` | `mediaReporting.states[].isSet` | booleano | Valore booleano che indica se lo stato del video è impostato o meno su schermo intero. |
| `videostatefullscreencount` | `mediaReporting.states[].count` | intero | Il numero di volte in cui uno stato video è stato impostato su schermo intero. |
| `videostatefullscreentime` | `mediaReporting.states[].time` | intero | La durata totale di quando lo stato del video è stato impostato su schermo intero. |
| `videostateclosedcaptioning` | `mediaReporting.states[].isSet` | booleano | Valore booleano che indica se i sottotitoli sono abilitati o meno. |
| `videostateclosedcaptioningcount` | `mediaReporting.states[].count` | intero | Il numero di volte in cui sono stati abilitati i sottotitoli. |
| `videostateclosedcaptioningtime` | `mediaReporting.states[].time` | intero | Durata totale dell&#39;abilitazione dei sottotitoli. |
| `videostatemute` | `mediaReporting.states[].isSet` | booleano | Valore booleano che indica se lo stato del video è stato impostato o meno su Disattiva audio. |
| `videostatemutecount` | `mediaReporting.states[].count` | intero | Il numero di volte in cui un video è stato disattivato. |
| `videostatemutetime` | `mediaReporting.states[].time` | intero | La durata totale del video in muto. |
| `videostatepictureinpicture` | `mediaReporting.states[].isSet` | booleano | Valore booleano che indica se è abilitata o meno la modalità immagine nell’immagine. |
| `videostatepictureinpicturecount` | `mediaReporting.states[].count` | intero | Il numero di volte in cui è attivata la modalità immagine nell&#39;immagine (picture-in-picture). |
| `videostatepictureinpicturetime` | `mediaReporting.states[].time` | intero | La durata totale di quando è stata abilitata la modalità picture-in-picture. |
| `videostateinfocus` | `mediaReporting.states[].isSet` | booleano | Valore booleano che indica se la modalità in focus è abilitata o meno |
| `videostateinfocuscount` | `mediaReporting.states[].count` | intero | Il numero di volte in cui è stata abilitata la modalità nell’immagine. |
| `videostateinfocustime` | `mediaReporting.states[].time` | intero | La durata totale di quando è stata abilitata la modalità in focus. |

{style="table-layout:auto"}

## Parametri di qualità

Per informazioni sui parametri di qualità, leggi la tabella seguente.

| Feed dati | Percorso campo XDM | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| `videoqoebitrateaverage` | `mediaReporting.qoeDataDetails.bitrateAverage` | numero | Il bitrate medio (in kbps, numero intero). Questa metrica viene calcolata come media ponderata di tutti i valori di bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione. |
| `videoqoebitratechange` | `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | booleano | Valore booleano che indica il numero di flussi in cui si sono verificate le modifiche del bitrate. Questa metrica è impostata su true solo se durante una sessione di riproduzione si è verificato almeno un evento di modifica del bitrate. |
| `videoqoebitratechangecountevar` | `mediaReporting.qoeDataDetails.bitrateChangeCount` | intero |  |
| `videoqoebitrateaverageevar` | `mediaReporting.qoeDataDetails.bitrateAverageBucket` | stringa | Il numero di modifiche del bitrate. Questo valore viene calcolato come somma di tutti gli eventi di modifica del bitrate che si sono verificati durante una sessione di riproduzione. |
| `videoqoetimetostartevar` | `mediaReporting.qoeDataDetails.timeToStart` | intero | La durata, misurata in secondi, tra il caricamento del video e l’avvio del video. |
| `videoqoedroppedframes` | `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | booleano | Valore booleano che indica il numero di flussi in cui i fotogrammi sono stati eliminati. Questa metrica è impostata su true solo se durante una sessione di riproduzione è stato eliminato almeno un fotogramma. |
| `videoqoedroppedframecountevar` | `mediaReporting.qoeDataDetails.droppedFrames` | intero | Il numero di fotogrammi persi durante la riproduzione del contenuto principale. |
| `videoqoebuffercountevar` | `mediaReporting.qoeDataDetails.bufferCount` | intero | Numero di eventi del buffer. Questa metrica viene calcolata come conteggio dei diversi stati del buffer che si sono verificati durante una sessione di riproduzione. Si tratta del numero di volte in cui il lettore entra in uno stato di buffer da altri stati, ad esempio riproduzione o pausa. |
| `videoqoebuffertimeevar` | `mediaReporting.qoeDataDetails.bufferTime` | intero | La quantità totale di tempo, misurata in secondi, trascorso il buffering. Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. |
| `videoqoebuffer` | `mediaReporting.qoeDataDetails.hasBufferImpactedStreams` | booleano | Valore booleano che indica il numero di flussi interessati dal buffering. Questa metrica è impostata su true solo se si è verificato almeno un evento buffer durante una sessione di riproduzione. |
| `videoqoeerror` | `mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | booleano | Valore booleano che indica il numero di flussi in cui si è verificato un evento di errore. Ad esempio, se è stato chiamato un trackError durante la sessione di riproduzione e è stata generata una chiamata heartbeat type=error. Questa metrica è impostata su true solo se si è verificato almeno un errore durante la riproduzione. |
| `videoerrorcountevar` | `mediaReporting.qoeDataDetails.errorCount` | intero | Il numero di errori che si sono verificati. Questo valore viene calcolato come somma di tutti gli eventi di errore che si sono verificati durante una sessione di riproduzione. |
| `videoqoeplayersdkerrors` | `mediaReporting.qoeDataDetails.playerSdkErrors` | matrice di stringa | Gli ID di errore univoci generati dal lettore SDK. Devi fornire i codici di errore o gli ID al momento dell’implementazione tramite API di errore fornite. |
| `videoqoeextneralerrors` | `mediaReporting.qoeDataDetails.externalErrors` | matrice di stringa | ID di errore univoci da qualsiasi origine esterna, ad esempio errori CDN. Devi fornire i codici di errore o gli ID al momento dell’implementazione tramite API di errore fornite. |
| `videoqoedropbeforestart` | `mediaReporting.qoeDataDetails.isDroppedBeforeStart` | booleano | ID di errore univoci generati da Media SDK durante la riproduzione. |

{style="table-layout:auto"}

## Campi obsoleti

Leggi questa sezione per informazioni sui campi di mappatura Analytics obsoleti.

### Campi di mappatura diretta

+++Seleziona per visualizzare una tabella dei campi di mappatura diretta obsoleti

| Feed dati | Campo XDM | Tipo XDM | Descrizione |
| --- | --- | --- | --- |
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
| `ipv6` | `environment.ipV6` | stringa |  |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | stringa | Versione di JavaScript supportata dal browser. |
| `user_agent` | `environment.browserDetails.userAgent` | stringa | Stringa dell’agente utente inviata nell’intestazione HTTP. |
| `mobileappid` | `application.name` | stringa | L&#39;ID dell&#39;app mobile, archiviato nel seguente formato: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | stringa | Nome del dispositivo mobile. In iOS, viene memorizzato come stringa di 2 cifre separate da virgola. Il primo numero rappresenta la generazione del dispositivo e il secondo rappresenta la famiglia di dispositivi. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | stringa | Utilizzato da Mobile Services. Rappresenta il punto di interesse. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | numero | Utilizzato da Mobile Services. Rappresenta la distanza del punto di interesse. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | numero | Raccolto dalla variabile di dati di contesto a.loc.acc. Indica la precisione del GPS in metri al momento della raccolta. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | stringa | Raccolto dalla variabile di dati di contesto a.loc.category. Descrive la categoria di un luogo specifico. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | stringa | Raccolto dalla variabile di dati di contesto a.loc.id. Identificatore per un dato punto di interesse. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | stringa | |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | numero | Beacon principale di Mobile Services. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | numero | Beacon secondario di Mobile Services. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | stringa | Beacon UUID di Mobile Services. |
| `mobileinstalls` | `application.firstLaunches` | Oggetto | Attivazione alla prima esecuzione dopo l&#39;installazione o la reinstallazione di `{id (string), value (number)}` |
| `mobileupgrades` | `application.upgrades` | Oggetto | Segnala il numero di aggiornamenti dell’app. Attiva alla prima esecuzione dopo l’aggiornamento o quando cambia il numero di versione. `{id (string), value (number)}` |
| `mobilelaunches` | `application.launches` | Oggetto | Il numero di volte in cui l&#39;app è stata avviata.  `{id (string), value (number)}` |
| `mobilecrashes` | `application.crashes` | Oggetto | `{id (string), value (number)}` |
| `mobilemessageclicks` | `directMarketing.clicks` | Oggetto | `{id (string), value (number)}` |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Oggetto | `{id (string), value (number)}` |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Oggetto | `{id (string), value (number)}` |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Oggetto | Il tempo di avvio della qualità video. `{id (string), value (number)}` |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Oggetto | `{id (string), value (number)}` |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Oggetto | Conteggio buffer qualità video `{id (string), value (number)}` |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Oggetto | Tempo buffer qualità video `{id (string), value (number)}` |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Oggetto | Conteggio modifiche qualità video `{id (string), value (number)}` |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Oggetto | Bitrate medio della qualità video `{id (string), value (number)}` |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Oggetto | Conteggio errori qualità video `{id (string), value (number)}` |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Oggetto | `{id (string), value (number)}` |

{style="table-layout:auto"}

+++

## Campi di mappatura generati

È necessario trasformare i campi selezionati provenienti da ADC, che richiedono la generazione in XDM di una logica che va oltre una copia diretta da Adobe Analytics.

+++Seleziona questa opzione per visualizzare una tabella dei campi di mappatura generati obsoleti

| Feed dati | Campo XDM | Tipo XDM | Descrizione |
| --- | --- | --- | --- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Oggetto | Proprietà personalizzate di Analytics, configurate come prop elenco. Contiene un elenco delimitato di valori. `{}` |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Oggetto | Utilizzato dalle variabili gerarchiche. Contiene un elenco delimitato di valori. `{values (array), delimiter (string)}` |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Variabili elenco di Analytics personalizzate. Contiene un elenco delimitato di valori.  `{value (string), key (string)}` |
| `m_color` | `device.colorDepth` | intero | ID di profondità colore, basato sul valore della colonna c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | booleano | Variabile utilizzata nella dimensione Supporto cookie. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Oggetto | Eventi di e-commerce standard attivati sull’hit. `{id (string), value (number)}` |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Oggetto | Eventi personalizzati attivati sull’hit. `{id (Object), value (Object)}` |
| `m_geo_country` | `placeContext.geo.countryCode` | stringa | Abbreviazione del paese da cui proviene l’hit, basata sul PI. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | numero | |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | numero | |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | booleano | Flag che indica se Java™ è abilitato. |
| `m_latitude` | `placeContext.geo._schema.latitude` | numero | |
| `m_longitude` | `placeContext.geo._schema.longitude` | numero | |
| `m_page_event_var1` | `web.webInteraction.URL` | stringa | Variabile utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. Questa variabile contiene l’URL del collegamento di download, del collegamento di uscita o del collegamento personalizzato su cui è stato fatto clic. |
| `m_page_event_var2` | `web.webInteraction.name` | stringa | Variabile utilizzata solo nelle richieste di immagini per il tracciamento dei collegamenti. Elenca il nome personalizzato del collegamento, se specificato. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | booleano | Variabile utilizzata per popolare la dimensione Pagine non trovate. Questa variabile deve essere vuota o contenere &quot;ErrorPage&quot;. |
| `m_pagename_no_url` | `web.webPageDetails.name` | numero | Nome della pagina (se impostato). Se non viene specificata alcuna pagina, questo valore viene lasciato vuoto. |
| `m_paid_search` | `search.isPaid` | booleano | Flag impostato se l’hit corrisponde al rilevamento di ricerche a pagamento. |
| `m_product_list` | `productListItems[].items` | array | L’elenco dei prodotti, trasmesso attraverso la variabile dei prodotti. `{SKU (string), quantity (integer), priceTotal (number)}` |
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
| `mcvisid_high` + `mcvisid_low` | identityMap | oggetto | L’ID visitatore di Experience Cloud. |
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | stringa | L’Experience Cloud ID (ECID) è noto anche come MCID e talvolta viene utilizzato negli spazi dei nomi. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | booleano | L’Experience Cloud ID (ECID) è noto anche come MCID e talvolta viene utilizzato negli spazi dei nomi. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | stringa | L’Experience Cloud ID (ECID) è noto anche come MCID e talvolta viene utilizzato negli spazi dei nomi. |
| `mcvisid_low` | `identityMap` | oggetto | L’ID visitatore di Experience Cloud. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | stringa | Hit Stitching ID. Il campo di analisi sdid_high e sdid_low è l’ID di dati supplementare utilizzato per unire due (o più) hit in arrivo. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | stringa | Prossimità beacon di Mobile Services. |

{style="table-layout:auto"}

+++

## Campi con mappatura divisa

Questi campi hanno un&#39;unica origine, ma vengono mappati su **più** posizioni XDM.

+++Seleziona questa opzione per visualizzare una tabella dei campi di mappatura di suddivisione obsoleti

| Feed dati | Campo XDM | Tipo XDM | Descrizione |
| --- | --- | --- | --- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | intero | ID numerico che rappresenta la risoluzione del monitoraggio. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | stringa | Versione del sistema operativo mobile. |

{style="table-layout:auto"}

+++

## Campi di mappatura avanzati

I campi di selezione (noti come &quot;valori di post&quot;) contengono dati dopo che Adobe ne ha regolato i valori utilizzando le Regole di elaborazione, le regole VISTA e le tabelle di ricerca. La maggior parte dei valori post ha una controparte pre-elaborata.

Il connettore di origine di Analytics invia dati preelaborati in un set di dati in Experience Platform. Puoi trasformare questi dati nella controparte post-elaborata utilizzando le trasformazioni. Per ulteriori informazioni sull&#39;esecuzione di queste trasformazioni tramite Query Service, vedere [Funzioni definite da Adobe](/help/query-service/sql/adobe-defined-functions.md) nella guida utente di Query Service.

Per ulteriori informazioni sull&#39;esecuzione di queste trasformazioni tramite Query Service, vedere [Funzioni definite da Adobe](/help/query-service/sql/adobe-defined-functions.md) nella guida utente di Query Service.

+++Seleziona questa opzione per visualizzare una tabella dei campi di mappatura avanzata obsoleti

| Feed dati | Campo XDM | Tipo XDM | Descrizione |
| — | — | — | — ||
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | stringa | eVar di Analytics personalizzate. Ogni organizzazione può utilizzare le eVar in modo diverso. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | stringa | Proprietà personalizzate di Analytics. Ogni organizzazione può utilizzare prop in modo diverso. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | numero intero | Altezza del browser, in pixel. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | numero intero | Larghezza del browser, in pixel. |
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
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | stringa |  Variabile di stato. |
| `post_user_server` | `web.webPageDetails.server` | stringa | Variabile utilizzata nella dimensione Server. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | stringa | Variabile utilizzata per popolare la dimensione Codice postale. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | numero intero | ID numerico del browser. |
| `domain` | `environment.domain` | stringa | Variabile utilizzata nella dimensione Dominio. Si basa sul provider di servizi Internet (ISP) dell&#39;utente. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | stringa | Il primo URL di riferimento per il visitatore. |
| `geo_city` | `placeContext.geo.city` | stringa | Il nome della città dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `geo_dma` | `placeContext.geo.dmaID` | numero intero | ID numerico dell’area demografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `geo_region` | `placeContext.geo.stateProvince` | stringa | Il nome dello stato o dell’area geografica dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `geo_zip` | `placeContext.geo.postalCode` | stringa | Il codice postale dell’hit. Si basa sull’indirizzo IP dell’hit. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | numero intero | L’ID numerico che rappresenta il sistema operativo del visitatore. Si basa sulla colonna user_agent. |
| `search_page_num` | `search.pageDepth` | numero intero | Questa variabile viene utilizzata dalla dimensione Classificazione di tutte le pagine di ricerca e indica quale pagina di risultati di ricerca ha il sito | è apparso su prima che l’utente facesse clic sul sito. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | stringa | Variabile utilizzata nella dimensione Parole chiave di ricerca. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | numero intero | Variabile utilizzata nella dimensione Numero di visite. Inizia da 1 e viene incrementato ogni volta che inizia una nuova visita (per utente). |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | numero intero | Variabile utilizzata nella dimensione Profondità di hit. Questo valore aumenta di 1 per ogni hit generato dall’utente e viene ripristinato dopo ogni visita. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | stringa | Il primo referrer della visita. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | numero intero | Nome della prima pagina della visita. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Oggetto | Proprietà personalizzate di Analytics, configurate come prop elenco. Contiene un elenco delimitato di valori. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Oggetto | Utilizzato dalle variabili della gerarchia e contiene un elenco delimitato di valori. | {values (array), delimitatore (stringa)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Elenco di valori di variabile. Contiene un elenco delimitato di valori personalizzati, a seconda dell’implementazione. | {value (stringa), key (stringa)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | booleano | Variabile utilizzata nella dimensione Supporto cookie. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Oggetto | Eventi di e-commerce standard attivati sull’hit. | {id (stringa), valore (numero)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Oggetto | Eventi personalizzati attivati sull’hit.| {id (Oggetto), value (Oggetto)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | booleano | Flag che indica se Java™ è abilitato. |
| `post_latitude` | `placeContext.geo._schema.latitude` | numero |   |
| `post_longitude` | `placeContext.geo._schema.longitude` | numero |   |
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
| `color` | `device.colorDepth` | numero intero | ID profondità colore, in base al valore della colonna c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | stringa | ID numerico che rappresenta il tipo di referrer del primo referrer del visitatore. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | numero intero | Marca temporale del primo hit del visitatore in tempo UNIX®. |
| `geo_country` | `placeContext.geo.countryCode` | stringa | Abbreviazione del paese da cui proviene l’hit, basata su IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | numero |  |
| `geo_longitude` | `placeContext.geo._schema.longitude` | numero |  |
| `paid_search` | `search.isPaid` | booleano | Flag impostato se l’hit corrisponde al rilevamento di ricerche a pagamento. |
| `ref_type` | `web.webReferrer.type` | stringa | Un ID numerico che rappresenta il tipo di riferimento per l’hit. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | booleano | Un flag (1=a pagamento, 0=non a pagamento) che indica se il primo hit della visita proviene da un hit di ricerca a pagamento. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | stringa | ID numerico che rappresenta il tipo di referrer del primo referrer della visita. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | stringa | ID numerico del primo motore di ricerca della visita. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | numero intero | Timestamp del primo hit della visita in tempo UNIX®. |

+++
