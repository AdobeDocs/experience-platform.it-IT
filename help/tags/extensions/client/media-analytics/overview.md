---
title: Panoramica dell’estensione Adobe Media Analytics for Audio and Video
description: Scopri l’estensione tag Adobe Media Analytics for Audio and Video in Adobe Experience Platform.
exl-id: 426cfd08-aead-4b35-824c-45494bca2fc8
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 98%

---

# Panoramica dell’estensione Adobe Media Analytics for Audio and Video

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Utilizza questa documentazione per avere maggiori informazioni sull&#39;installazione, la configurazione e l&#39;implementazione dell&#39;estensione Adobe Media Analytics for Audio and Video (estensione Media Analytics). Sono incluse le opzioni disponibili quando si utilizza questa estensione per generare una regola, insieme a esempi e collegamenti a campioni.

L&#39;estensione Media Analytics (MA) aggiunge l&#39;SDK principale JavaScript Media SDK (Media 2.x SDK). Questa estensione fornisce le funzionalità necessarie per aggiungere l’istanza di tracciamento `MediaHeartbeat` a un progetto o sito progetto di tag. L’estensione MA richiede due estensioni aggiuntive:

* [Estensione Analytics](../analytics/overview.md)
* [Estensione Experience Cloud ID](../id-service/overview.md)

>[!IMPORTANT]
>
>Il tracciamento audio richiede l’estensione Analytics v1.6 o una versione successiva.

Dopo aver incluso tutte e tre le estensioni precedentemente menzionate nel progetto di tag, puoi procedere in uno dei due modi seguenti:

* Utilizza le API `MediaHeartbeat` dalla Web app
* Includi, o genera, un&#39;estensione specifica per il lettore che mappa eventi specifici del lettore multimediale nelle API sull&#39;istanza tracker `MediaHeartbeat`. Questa istanza viene esposta tramite l&#39;estensione MA.

## Installa e configura l&#39;estensione MA

* **Installa:** per installare l‘estensione MA, apri la proprietà dell’estensione, seleziona **[!UICONTROL Estensioni > Catalogo]**, passa il puntatore del mouse sull’estensione **[!UICONTROL Adobe Media Analytics for Audio and Video]** e seleziona **[!UICONTROL Installa]**.

* **Configura:** per configurare l’estensione MA, apri la scheda [!UICONTROL Estensioni], passa il puntatore sull’estensione, quindi seleziona **[!UICONTROL Configura]**:

![Configurazione dell&#39;estensione MA](../../../images/ext-va-config.jpg)

### Opzioni di configurazione:

| Opzione | Descrizione |
| :--- | :--- |
| Tracking Server | Definisce il server per il monitoraggio degli heartbeat multimediali (diverso dal server di tracciamento Analytics) |
| Application Version | Versione dell&#39;app/SDK del lettore multimediale |
| Player Name | Nome del lettore multimediale in uso (ad esempio &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Channel | Proprietà nome canale |
| Online Video Provider | Nome della piattaforma video online attraverso la quale il contenuto è distribuito |
| Debug Logging | Attiva o disattiva la registrazione |
| Enable SSL | Attiva o disattiva l&#39;invio di ping su HTTPS |
| Export APIs to Window Object | Attivare o disattivare l&#39;esportazione delle API di Media Analytics all&#39;ambito globale |
| Variable Name | Una variabile utilizzata per esportare le API di Media Analytics sotto l&#39;oggetto `window` |

**Promemoria:** l&#39;estensione MA richiede le estensioni [Analytics](../analytics/overview.md) ed [Experience Cloud ID](../id-service/overview.md). Devi aggiungere queste estensioni alla proprietà dell&#39;estensione e configurarle.

## Utilizzo dell&#39;estensione MA

### Utilizzo da una pagina web/JS-app

L’estensione MA esporta le API MediaHeartbeat nell’oggetto finestra globale abilitando l’impostazione “Esporta API nell’oggetto finestra” nella pagina [!UICONTROL Configurazione]. Esporta le API sotto il nome della variabile configurato. Ad esempio, se il nome della variabile è configurato per essere `ADB` allora è possibile accedere a MediaHeartbeat tramite `window.ADB.MediaHeartbeat`.

>[!IMPORTANT]
>
>L’estensione MA esporta le API solo se `window["CONFIGURED_VARIABLE_NAME"]` non è definito e non sostituisce le variabili esistenti.

1. **Crea istanza MediaHeartbeat:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

   **Parametri:** un oggetto delegato valido che espone queste funzioni.

   | Metodo |  Descrizione   |
   | :--- | :--- |
   | `getQoSObject()` | Restituisce l&#39;istanza `theMediaObject` che contiene le informazioni QoS correnti. Questo metodo verrà chiamato più volte durante una sessione di riproduzione. L&#39;implementazione del lettore deve restituire sempre i dati QoS disponibili più di recente. |
   | `getCurrentPlaybackTime()` | Restituisce la posizione corrente dell&#39;indicatore di riproduzione. Per il tracciamento VOD, il valore è specificato in secondi dall&#39;inizio dell&#39;elemento multimediale. Per il tracciamento LIVE/LIVE, il valore viene specificato in secondi dall&#39;inizio del programma. |

   **Valore restituito:** una promessa che risolve con un&#39;istanza `MediaHeartbeat` o rifiuta con un messaggio di errore.

1. **Accesso a costanti MediaHeartbeat:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat`

   Questo espone tutte le costanti e i metodi statici dalla [`MediaHeartbeat`](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) classe.

   Ottieni il sample player qui: [MA Sample Player](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/2.x). Il sample player funge da riferimento per mostrare come utilizzare l’estensione MA per supportare Media Analytics direttamente da una Web app.

1. Crea l&#39;istanza di tracciamento MediaHeartbeat come segue:

   ```javascript
   var MediaHeartbeat = window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat;
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   };
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   };
   
   var self = this;
   MediaHeartbeat.getInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   ```

### Utilizzo da altre estensioni

L&#39;estensione MA espone i moduli condivisi `get-instance` e `media-heartbeat` ad altre estensioni. (Per ulteriori informazioni sui moduli condivisi, consulta la [documentazione Moduli condivisi](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Puoi accedere ai moduli condivisi solo da altre estensioni. In altre parole, una pagina web/JS-app non può accedere ai moduli condivisi, né utilizzare `turbine` (vedi il codice di esempio di seguito) all&#39;esterno di un&#39;estensione.

1. **Crea istanza MediaHeartbeat:** `get-instance` modulo condiviso

   **Parametri:**

   * Un oggetto delegato valido che espone queste funzioni:

      | Metodo |  Descrizione   |
      | :--- | :--- |
      | `getQoSObject()` | Restituisce l&#39;istanza `MediaObject` che contiene le informazioni QoS correnti. Questo metodo verrà chiamato più volte durante una sessione di riproduzione. L&#39;implementazione del lettore deve restituire sempre i dati QoS disponibili più di recente. |
      | `getCurrentPlaybackTime()` | Restituisce la posizione corrente dell&#39;indicatore di riproduzione. Per il tracciamento VOD, il valore è specificato in secondi dall&#39;inizio dell&#39;elemento multimediale. Per il tracciamento LIVE/LIVE, il valore viene specificato in secondi dall&#39;inizio del programma. |

   * Un oggetto di configurazione facoltativo che espone queste proprietà:

      | Proprietà | Descrizione | Obbligatorio |
      | :--- | :--- | :--- |
      | Online Video Provider | Nome della piattaforma video online tramite la quale il contenuto è distribuito. | No. Se presente, sostituisce il valore definito durante la configurazione dell&#39;estensione. |
      | Player Name | Nome del lettore multimediale in uso (ad esempio &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) | No. Se presente, sostituisce il valore definito durante la configurazione dell&#39;estensione. |
      | Channel | Proprietà nome canale | No. Se presente, sostituisce il valore definito durante la configurazione dell&#39;estensione. |
   **Valore restituito:** una promessa che risolve con un&#39;istanza `MediaHeartbeat` o rifiuta con un messaggio di errore.

1. **Accesso a costanti MediaHeartbeat:** `media-heartbeat` modulo condiviso

   Questo modulo espone tutte le costanti e i metodi statici di questa classe: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

1. Crea l&#39;istanza di tracciamento MediaHeartbeat come segue:

   ```javascript
   var getMediaHeartbeatInstance =
     turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   
   var MediaHeartbeat =
     turbine.getSharedModule('adobe-video-analytics', 'media-heartbeat');
     ...
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   }
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   }
   ...
   
   var self = this;
   getMediaHeartbeatInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       ...
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   
   ...
   ```

1. Utilizzando l’istanza Media Heartbeat, segui la [documentazione JS Media SDK](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-javascript/set-up-js-2.html?lang=it) e la [documentazione API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html) per implementare il tracciamento multimediale.

>[!NOTE]
>
>**Test:** per questa versione, per testare l’estensione devi caricarla in [Platform](../../../extension-dev/submit/upload-and-test.md), dove puoi accedere a tutte le estensioni dipendenti.


<!--
## Leveraging the sample HTML5 player

You can obtain the MA extension sample HTML5 player here: [HTML5 Sample Player](https://github.com/adobe/reactor-adobe-va-sample-player). The sample player acts as a reference to create video player extensions and to showcase using the MA extension to support media tracking.

### Sample player extension action types

This section describes the action types available in the Sample Player extension.

#### Open Video

The _Open Video_ action provides various configurations for creating and customizing an HTML5 player, providing a video to play and enabling/disabling Adobe Video Analytics tracking.

**Action Configuration / Player Settings:** Note the CSS Selector setting which specifics the `<div>` in the web page where the player is added. Note also that the _Enable Adobe Analytics_ checkbox is checked in the Analytics Settings pane.

![Player Extension Action Configuration](../../../images/ext-va-sp-action.png)

![Player Extension Action Configuration](../../../images/ext-va-sp-action1.png)

* [\[...\]/openVideo/openVideo.jsx](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/view/actions/openVideo/openVideo.jsx) -

  UI Code to configure the Action is defined here.

* [\[...\]/actions/openVideo.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/actions/openVideo.js) - This file exports a function that gets executed when the Action is triggered as part of the tag rule.

  This is a code snippet from `openVideo.js` where the `openVideo` Action is executed:

  ```javascript
    function openVideo(settings) {
        let player;
        try {
            Logger.info(LOG_TAG, `Executing action with ${JSON.stringify(settings)}`);

            player = new PlayerFacade(settings);
            PlayerStore.registerPlayer(player);
            player.load(settings.media);
        } catch (ex) {
            Logger.error(LOG_TAG, `Creating player for action openVideo failed with error ${ex.message}`);

            // Cleanup from DOM.
            if (player) {
                player.destroy();
            }
        }
    }
    ...
  ```

* [\[...\]/analytics/adobeAnalyticsProvider.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/helpers/analytics/adobeAnalyticsProvider.js) - This file implements Video Analytics tracking by using Shared Modules exposed by the VA extension.

### Sample player extension basic deployment

Once the Sample Player extension is installed, you'll need to create at least one rule to properly deploy it. The Image below shows a sample rule that opens the specified video when the core extension fires the `DOMLoaded` event.

![Player Extension Sample Rule](../../../images/ext-va-sp-rule.png)

After you have saved this rule, you will need to add it to a Library, and then build and deploy so that you can test the behavior.

-->
