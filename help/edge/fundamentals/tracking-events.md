---
title: Tracciare gli eventi utilizzando Adobe Experience Platform Web SDK
description: Scopri come tenere traccia degli eventi di Adobe Experience Platform Web SDK.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---


# Tracciare gli eventi

Per inviare i dati evento a Adobe Experience Cloud, utilizza `sendEvent` comando. Il `sendEvent` è il modo principale per inviare dati al [!DNL Experience Cloud]e per recuperare contenuti, identità e destinazioni di pubblico personalizzati.

I dati inviati a Adobe Experience Cloud si dividono in due categorie:

* Dati XDM
* Dati non XDM

## Invio di dati XDM

I dati XDM sono un oggetto il cui contenuto e la cui struttura corrispondono a uno schema creato in Adobe Experience Platform. [Scopri come creare uno schema.](../../xdm/tutorials/create-schema-ui.md)

Tutti i dati XDM che desideri far parte di analisi, personalizzazione, pubblico o destinazioni devono essere inviati utilizzando `xdm` opzione.


```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Un certo periodo di tempo può trascorrere tra `sendEvent` viene eseguito e quando i dati vengono inviati al server (ad esempio, se la libreria SDK Web non è stata completamente caricata o il consenso non è ancora stato ricevuto). Se si desidera modificare una parte del `xdm` oggetto dopo l&#39;esecuzione di `sendEvent` è consigliabile clonare il comando `xdm` oggetto _prima di_ esecuzione di `sendEvent` comando. Ad esempio:

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

In questo esempio, il livello dati viene clonato serializzandolo in JSON, quindi deserializzandolo. Successivamente, il risultato clonato viene trasmesso nel `sendEvent` comando. In questo modo si assicura che `sendEvent` il comando ha un’istantanea del livello dati così come esisteva quando `sendEvent` Il comando è stato eseguito in modo che le modifiche successive all’oggetto livello dati originale non vengano applicate ai dati inviati al server. Se utilizzi un livello dati basato su eventi, la clonazione dei dati probabilmente è già gestita automaticamente. Ad esempio, se utilizzi il [Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer/wiki), il `getState()` Il metodo fornisce un&#39;istantanea clonata e calcolata di tutte le modifiche precedenti. Questo viene gestito automaticamente anche se utilizzi l’estensione tag Adobe Experience Platform Web SDK.

>[!NOTE]
>
>È previsto un limite di 32 KB per i dati che possono essere inviati in ogni evento nel campo XDM.


## Invio di dati non XDM

I dati che non corrispondono a uno schema XDM devono essere inviati utilizzando `data` opzione del `sendEvent` comando. Questa funzione è supportata nelle versioni 2.5.0 e successive di Web SDK.

Questa funzione è utile se devi aggiornare un profilo Adobe Target o inviare gli attributi Recommendations di Target. [Ulteriori informazioni su queste funzioni di Target.](../personalization/adobe-target/target-overview.md#single-profile-update)

In futuro, potrai inviare l’intero livello di dati sotto `data` e mapparlo sul lato server XDM.

**Come inviare attributi di profilo e Recommendations ad Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### Impostazione `eventType` {#event-types}

Negli schemi ExperienceEvent XDM, è disponibile un `eventType` campo. Contiene il tipo di evento principale per il record. L’impostazione di un tipo di evento può aiutarti a distinguere tra i diversi eventi che stai inviando. XDM fornisce diversi tipi di evento predefiniti che è possibile utilizzare o creare sempre tipi di evento personalizzati per i casi d’uso. Consulta la documentazione XDM per un [elenco di tutti i tipi di evento predefiniti](../../xdm/classes/experienceevent.md#eventType).

Questi tipi di evento vengono visualizzati in un elenco a discesa se utilizzi l’estensione tag oppure puoi sempre trasmetterli senza tag. Possono essere trasmesse come parte del `xdm` opzione.


```javascript
alloy("sendEvent", {
  "xdm": {
    "eventType": "commerce.purchases",
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

In alternativa, `eventType` può essere passato nel comando evento utilizzando `type` opzione. Dietro le quinte, questo viene aggiunto ai dati XDM. Avere `type` come opzione consente di impostare più facilmente il `eventType` senza dover modificare il payload XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Sovrascrittura dell’ID del set di dati

>[!IMPORTANT]
>
>Il `datasetId` opzione supportata da `sendEvent` il comando è stato dichiarato obsoleto. Per ignorare un ID di set di dati, utilizza [sostituzioni di configurazione](../../datastreams/overrides.md) invece.

In alcuni casi d’uso, potrebbe essere utile inviare un evento a un set di dati diverso da quello configurato nell’interfaccia utente di configurazione. Per questo è necessario impostare `datasetId` opzione sul `sendEvent` comando:



```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Aggiunta di informazioni di identità

All’evento è inoltre possibile aggiungere informazioni di identità personalizzate. Consulta [Recupero ID Experience Cloud](../identity/overview.md).

## Utilizzo dell’API sendBeacon

Può essere difficile inviare i dati dell’evento subito prima che l’utente della pagina web si sia allontanato. Se la richiesta richiede troppo tempo, il browser potrebbe annullarla. Alcuni browser hanno implementato un’API standard web denominata `sendBeacon` per consentire una più agevole raccolta dei dati in questo lasso di tempo. Quando si utilizza `sendBeacon`, il browser effettua la richiesta web nel contesto di navigazione globale. Ciò significa che il browser effettua la richiesta beacon in background e non blocca la navigazione della pagina. Per comunicare a Adobe Experience Platform [!DNL Web SDK] da utilizzare `sendBeacon`, aggiungi l’opzione `"documentUnloading": true` al comando evento.

**Esempio**

```javascript
alloy("sendEvent", {
  "documentUnloading": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

I browser hanno imposto limiti alla quantità di dati che possono essere inviati con `sendBeacon` contemporaneamente. In molti browser, il limite è di 64 KB. Se il browser rifiuta l’evento perché il payload è troppo grande, Adobe Experience Platform [!DNL Web SDK] utilizza di nuovo il suo normale metodo di trasporto (ad esempio, fetch).

## Gestione delle risposte dagli eventi

Se desideri gestire una risposta da un evento, puoi ricevere la notifica di un successo o un errore come segue:


```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### Il `result` oggetto

Il `sendEvent` Il comando restituisce una promessa risolta con un `result` oggetto. Il `result` L&#39;oggetto contiene le seguenti proprietà:

| Proprietà | Descrizione |
|---------|----------|
| `propositions` | Le offerte di personalizzazione per le quali il visitatore si è qualificato. [Ulteriori informazioni sulle proposte.](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| `decisions` | Proprietà obsoleta. Al suo posto, utilizza `propositions`. |
| `destinations` | Tipi di pubblico da Adobe Experience Platform che possono essere condivisi con piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sui siti web dei clienti. [Ulteriori informazioni sulle destinazioni.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html) |

>[!WARNING]
>
>Il `destinations` proprietà in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Modifica degli eventi a livello globale {#modifying-events-globally}

Se desideri aggiungere, rimuovere o modificare campi dall’evento a livello globale, puoi configurare un’ `onBeforeEventSend` callback. Questo callback viene chiamato ogni volta che viene inviato un evento. Questo callback viene passato in un oggetto evento con un `xdm` campo. Per modificare i dati inviati con l’evento, modifica `content.xdm`.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` I campi sono impostati in questo ordine:

1. Valori passati come opzioni al comando evento `alloy("sendEvent", { xdm: ... });`.
2. Valori raccolti automaticamente. Consulta [Informazione automatica](../data-collection/automatic-information.md).
3. Le modifiche apportate in `onBeforeEventSend` callback.

Alcune note sulla `onBeforeEventSend` callback:

* L’XDM dell’evento può essere modificato durante il callback. Una volta restituito il callback, tutti i campi e i valori modificati degli oggetti content.xdm e content.data vengono inviati con l&#39;evento.

  ```javascript
  onBeforeEventSend: function(content){
    //sets a query parameter in XDM
    const queryString = window.location.search;
    const urlParams = new URLSearchParams(queryString);
    content.xdm.marketing.trackingCode = urlParams.get('cid')
  }
  ```

* Se il callback genera un&#39;eccezione, l&#39;elaborazione dell&#39;evento viene interrotta e l&#39;evento non viene inviato.
* Se il callback restituisce il valore booleano di `false`, l’elaborazione degli eventi viene interrotta senza errori e l’evento non viene inviato. Questo meccanismo consente di ignorare facilmente alcuni eventi esaminando i dati dell’evento e restituendoli `false` se l’evento non deve essere inviato.

  >[!NOTE]
  >Fai attenzione a evitare di restituire false al primo evento di una pagina. La restituzione di false sul primo evento può influire negativamente sulla personalizzazione.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Qualsiasi valore restituito diverso dal valore booleano `false` consentirà all&#39;evento di elaborare e inviare dopo il callback.

* Gli eventi possono essere filtrati esaminando il tipo di evento (vedi [Tipi di evento](#event-types).):

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## Potenziali errori utilizzabili

Quando si invia un evento, è possibile che venga generato un errore se i dati inviati sono troppo grandi (oltre 32 KB per la richiesta completa). In questo caso, devi ridurre la quantità di dati inviati.
