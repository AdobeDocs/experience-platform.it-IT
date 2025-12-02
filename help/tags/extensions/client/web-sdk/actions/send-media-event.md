---
title: Invia evento multimediale
description: Invia dati multimediali a Adobe Experience Platform Edge Network.
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Invia evento multimediale

L&#39;azione **[!UICONTROL Send media event]** invia l&#39;evento multimediale a un flusso di dati, che può quindi essere utilizzato da app e servizi come Adobe Experience Platform o Adobe Analytics. Questa azione è utile quando tieni traccia del contenuto multimediale in streaming sulla proprietà.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra la schermata Invia evento multimediale.](../assets/send-media-event.png)

Le opzioni disponibili dipendono da **[!UICONTROL Media event type]** selezionato. Tutti i tipi di evento multimediale richiedono **[!UICONTROL Player ID]**, che è il nome del lettore di contenuti.

Alcuni tipi di evento consentono di configurare altri campi. Se un tipo di evento multimediale non è elencato qui, l&#39;unico campo disponibile è [!UICONTROL Player ID]. I seguenti tipi di evento multimediale includono altri campi:

## [!UICONTROL Ad break start]

Consente di configurare i dettagli del pod pubblicitario.

* **[!UICONTROL Ad break name]**: nome descrittivo dell’interruzione pubblicitaria.
* **[!UICONTROL Ad break offset (seconds)]**: offset dell&#39;interruzione pubblicitaria all&#39;interno del contenuto, in secondi.
* **[!UICONTROL Ad break index]**: indice dell&#39;interruzione pubblicitaria all&#39;interno del contenuto, a partire da 1.

## [!UICONTROL Ad start]

Consente di configurare i dettagli pubblicitari.

* **[!UICONTROL Ad name]**: nome descrittivo dell&#39;annuncio.
* **[!UICONTROL Ad ID]**: ID dell&#39;annuncio. È supportato qualsiasi valore alfanumerico.
* **[!UICONTROL Ad length (seconds)]**: lunghezza dell&#39;annuncio video, in secondi.
* **[!UICONTROL Advertiser]**: azienda o marchio il cui prodotto è presentato nell&#39;annuncio.
* **[!UICONTROL Campaign ID]**: ID della campagna pubblicitaria.
* **[!UICONTROL Creative ID]**: ID della creatività dell&#39;annuncio.
* **[!UICONTROL Creative URL]**: URL della creatività dell&#39;annuncio.
* **[!UICONTROL Placement ID]**: ID di posizionamento dell&#39;annuncio.
* **[!UICONTROL Site ID]**: ID del sito dell&#39;annuncio.
* **[!UICONTROL Pod position]**: indice dell&#39;annuncio all&#39;interno dell&#39;interruzione pubblicitaria principale, a partire da 0.

Questo tipo di evento supporta anche la possibilità di fornire metadati personalizzati come parte del payload dell’evento multimediale.

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]**: oggetto [Quality of Experience](/help/xdm/data-types/qoe-data-details-collection.md) che specifica il bitrate, i fotogrammi saltati, i fotogrammi al secondo e il tempo di avvio.

## [!UICONTROL Chapter start]

Consente di configurare i dettagli del capitolo.

* **[!UICONTROL Chapter name]**: nome del capitolo o del segmento.
* **[!UICONTROL Chapter length]**: lunghezza del capitolo in secondi.
* **[!UICONTROL Chapter index]**: posizione del capitolo all&#39;interno del contenuto.
* **[!UICONTROL Chapter offset]**: offset del capitolo dall&#39;inizio del contenuto, in secondi.

Questo tipo di evento supporta anche la possibilità di fornire metadati personalizzati come parte del payload dell’evento multimediale.

## [!UICONTROL Error]

Consente di configurare i dettagli dell’errore.

* **[!UICONTROL Error name]**: nome dell&#39;errore.
* **[!UICONTROL Source]**: origine dell&#39;errore.

## [!UICONTROL Session start]

Consente di configurare i dettagli della sessione multimediale.

* **[!UICONTROL Handle media session automatically]**: casella di controllo che consente al Web SDK di inviare automaticamente i ping necessari. Puoi deselezionare questa casella se desideri inviare manualmente dei ping da solo.
* **[!UICONTROL Playhead]**: indicatore di riproduzione, in secondi.
* **[!UICONTROL Content type]**: tipo di contenuto. È supportato qualsiasi valore stringa; Adobe offre anche i seguenti predefiniti:
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]**: durata massima del contenuto utilizzato, in secondi. Per gli elementi multimediali live di durata sconosciuta, il valore predefinito è `86400`.
* **[!UICONTROL Content ID]**: ID contenuto.
* **[!UICONTROL Ad load type]**: tipo di annuncio caricato. Sono supportati i due valori seguenti:
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]**: album a cui appartiene la canzone.
* **[!UICONTROL Artist]**: artista della canzone.
* **[!UICONTROL Asset ID]**: identificatore univoco per il contenuto della risorsa multimediale. Questi ID sono in genere derivati da autorità di metadati come EIDR, TMS/Gracenote o Rovi. Questi identificatori possono provenire anche da altri sistemi proprietari o interni.
* **[!UICONTROL Author]**: nome dell&#39;autore del audiolibro.
* **[!UICONTROL Authorized]**: flag che determina se l&#39;utente ha eseguito l&#39;accesso tramite l&#39;autenticazione di Adobe.
* **[!UICONTROL Day part]**: ora del giorno in cui il contenuto è stato trasmesso o riprodotto. Qualsiasi valore stringa è supportato.
* **[!UICONTROL Episode]**: numero dell&#39;episodio.
* **[!UICONTROL Feed type]**: tipo di feed.
* **[!UICONTROL First air date]**: la data in cui il contenuto è andato in onda per la prima volta in televisione. Qualsiasi valore stringa è supportato. Tuttavia, Adobe consiglia di utilizzare il formato `YYYY-MM-DD`.
* **[!UICONTROL First digital date]**: la data in cui il contenuto è andato in onda per la prima volta su qualsiasi canale o piattaforma digitale. Qualsiasi valore stringa è supportato. Tuttavia, Adobe consiglia di utilizzare il formato `YYYY-MM-DD`.
* **[!UICONTROL Content name]**: nome descrittivo del contenuto.
* **[!UICONTROL Genre]**: tipo o raggruppamento di contenuti definiti dal produttore del contenuto. Questo campo supporta più valori, delimitati da una virgola.
* **[!UICONTROL Label]**: nome dell&#39;etichetta record.
* **[!UICONTROL Rating]**: valutazione come definita dalle linee guida TV per genitori.
* **[!UICONTROL MVPD]**: MVPD fornito dall&#39;autenticazione Adobe.
* **[!UICONTROL Network]**: nome della rete o del canale.
* **[!UICONTROL Originator]**: l&#39;autore del contenuto.
* **[!UICONTROL Publisher]**: l&#39;autore del contenuto audio.
* **[!UICONTROL Season]**: se lo spettacolo fa parte di una serie, il numero della stagione dello spettacolo.
* **[!UICONTROL Show]**: se lo spettacolo fa parte di una serie, il nome della serie.
* **[!UICONTROL Show type]**: tipo di presentazione. È supportato qualsiasi valore stringa; Adobe offre anche i seguenti predefiniti:
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]**: tipo di flusso.
* **[!UICONTROL Stream format]**: formato del flusso, ad esempio HD o SD.
* **[!UICONTROL Station]**: nome o ID della stazione radio.

Questo tipo di evento supporta anche la possibilità di fornire metadati personalizzati come parte del payload dell’evento multimediale. Consente inoltre sostituzioni nella configurazione dello stream di dati, consentendoti di controllare quali app e servizi ricevono i dati. Quando imposti una sostituzione della configurazione dello stream di dati sia in un singolo comando che all’interno delle impostazioni di configurazione dell’estensione tag, il singolo comando ha la precedenza. Per ulteriori informazioni, vedere [Override della configurazione Datastream](../configure/configuration-overrides.md).

## [!UICONTROL States update]

Consente di configurare i dettagli dell’aggiornamento dello stato. È possibile avviare o terminare i seguenti stati:

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

Sono disponibili i seguenti campi:

* **[!UICONTROL States started]**: menu a discesa che consente di indicare l&#39;avvio di uno stato. La selezione del pulsante **[!UICONTROL Add another state that started]** consente di avviare più stati nella stessa azione.
* **[!UICONTROL States ended]**: menu a discesa che consente di indicare la fine di uno stato. La selezione del pulsante **[!UICONTROL Add another state that ended]** consente di terminare più stati nella stessa azione.
