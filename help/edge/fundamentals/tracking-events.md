---
title: Tracciare gli eventi utilizzando l’SDK per web di Adobe Experience Platform
description: Scopri come tenere traccia degli eventi dell’SDK Web per Adobe Experience Platform.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentSloading;document Unloading;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# Tracciare gli eventi

Per inviare dati evento a Adobe Experience Cloud, utilizza la `sendEvent` comando. La `sendEvent` è il modo principale per inviare dati a [!DNL Experience Cloud]e per recuperare contenuti, identità e destinazioni personalizzate.

I dati inviati a Adobe Experience Cloud rientrano in due categorie:

* Dati XDM
* Dati non XDM

## Invio di dati XDM

I dati XDM sono oggetti il cui contenuto e la cui struttura corrispondono a uno schema creato in Adobe Experience Platform. [Ulteriori informazioni su come creare uno schema.](../../xdm/tutorials/create-schema-ui.md)

Eventuali dati XDM che desideri includere nelle analisi, nella personalizzazione, nel pubblico o nelle destinazioni devono essere inviati utilizzando `xdm` opzione .


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

Un certo tempo può passare tra quando `sendEvent` viene eseguito e quando i dati vengono inviati al server (ad esempio, se la libreria SDK per web non è completamente caricata o non è ancora stato ricevuto il consenso). Se si intende modificare una qualsiasi parte del `xdm` dopo l&#39;esecuzione dell&#39;oggetto `sendEvent` è consigliabile duplicare il comando `xdm` oggetto _prima_ esecuzione `sendEvent` comando. Esempio:

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

In questo esempio, il livello dati viene clonato serializzandolo in JSON e quindi deserializzandolo. Successivamente, il risultato clonato viene trasmesso nel `sendEvent` comando. In questo modo si assicura che il `sendEvent` ha un&#39;istantanea del livello dati così come esisteva quando `sendEvent` è stato eseguito in modo che le modifiche successive all&#39;oggetto livello dati originale non vengano riportate nei dati inviati al server. Se utilizzi un livello dati basato su eventi, è probabile che la duplicazione dei dati sia già gestita automaticamente. Ad esempio, se utilizzi il [Livello dati client di Adobe](https://github.com/adobe/adobe-client-data-layer/wiki), `getState()` fornisce un&#39;istantanea calcolata e clonata di tutte le modifiche precedenti. Questa operazione viene gestita automaticamente anche se utilizzi l’estensione tag Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Esiste un limite di 32 KB per i dati che possono essere inviati in ogni evento nel campo XDM.


## Invio di dati non XDM

I dati che non corrispondono a uno schema XDM devono essere inviati utilizzando `data` opzione `sendEvent` comando. Questa funzione è supportata nelle versioni 2.5.0 e successive dell’SDK per web.

Questa opzione è utile se devi aggiornare un profilo Adobe Target o inviare attributi Recommendations di Target. [Ulteriori informazioni su queste funzionalità di Target.](../personalization/adobe-target/target-overview.md#single-profile-update)

In futuro, potrai inviare il livello di dati completo sotto il `data` e mapparla su lato server XDM.

**Come inviare gli attributi Profilo e Recommendations ad Adobe Target:**

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

Negli schemi ExperienceEvent XDM, è disponibile un `eventType` campo . Contiene il tipo di evento principale per il record. L’impostazione di un tipo di evento può essere utile per distinguere tra i diversi eventi che invierai. XDM fornisce diversi tipi di evento predefiniti che è possibile utilizzare oppure è sempre possibile creare tipi di evento personalizzati per i casi d’uso. Fai riferimento alla documentazione XDM per un [elenco di tutti i tipi di evento predefiniti](../../xdm/classes/experienceevent.md#eventType).

Questi tipi di evento vengono visualizzati in un elenco a discesa se utilizzi l’estensione tag oppure puoi sempre trasmetterli senza tag . Possono essere trasferiti come parte del `xdm` opzione .


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

In alternativa, il `eventType` può essere passato al comando evento utilizzando `type` opzione . Dietro le quinte, questo viene aggiunto ai dati XDM. Avere `type` come opzione consente di impostare più facilmente la variabile `eventType` senza dover modificare il payload XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Sovrascrittura dell’ID del set di dati

In alcuni casi d’uso, potrebbe essere utile inviare un evento a un set di dati diverso da quello configurato nell’interfaccia utente di configurazione. Per questo è necessario impostare il `datasetId` l&#39;opzione `sendEvent` comando:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Aggiunta di informazioni sull&#39;identità

È inoltre possibile aggiungere all’evento informazioni di identità personalizzate. Vedi [Recupero ID Experience Cloud](../identity/overview.md).

## Utilizzo dell’API sendBeacon

Può essere difficile inviare i dati dell’evento immediatamente prima che l’utente della pagina web se ne vada. Se la richiesta richiede troppo tempo, il browser potrebbe annullare la richiesta. Alcuni browser hanno implementato un’API web standard denominata `sendBeacon` per consentire una raccolta più semplice dei dati in questo periodo di tempo. Quando utilizzi `sendBeacon`, il browser effettua la richiesta web nel contesto di navigazione globale. Questo significa che il browser effettua la richiesta beacon in background e non blocca la navigazione delle pagine. Per comunicare a Adobe Experience Platform [!DNL Web SDK] utilizzare `sendBeacon`, aggiungi l’opzione `"documentUnloading": true` al comando evento .  Ecco un esempio:


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

I browser hanno imposto limiti alla quantità di dati che possono essere inviati con `sendBeacon` una volta sola. In molti browser, il limite è di 64K. Se il browser rifiuta l’evento perché il payload è troppo grande, Adobe Experience Platform [!DNL Web SDK] torna a utilizzare il suo metodo di trasporto normale (ad esempio, fetch).

## Gestione delle risposte dagli eventi

Se desideri gestire una risposta da un evento, puoi ricevere le seguenti notifiche di un successo o di un errore:


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


### La `result` oggetto

La `sendEvent` restituisce una promessa risolta con un `result` oggetto. La `result` l&#39;oggetto contiene le proprietà seguenti:

**proposizioni**: Le offerte di personalizzazione per le quali il visitatore si è qualificato. [Ulteriori informazioni sulle proposte.](../personalization/rendering-personalization-content.md#manually-rendering-content)

**decisioni**: Questa proprietà è obsoleta. Utilizza piuttosto `propositions`.

**destinazioni**: Segmenti da Adobe Experience Platform che possono essere condivisi con piattaforme di personalizzazione esterne, sistemi di gestione dei contenuti, server di annunci e altre applicazioni in esecuzione sui siti web dei clienti. [Ulteriori informazioni sulle destinazioni.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

**deduzioni**: Informazioni sull’apprendimento automatico in tempo reale. [Ulteriori informazioni sull&#39;apprendimento automatico in tempo reale.](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/real-time-machine-learning/home.html?lang=en)

>[!WARNING]
>
>`inferences` è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.



## Modifica degli eventi a livello globale {#modifying-events-globally}

Se desideri aggiungere, rimuovere o modificare i campi dall’evento globalmente, puoi configurare un `onBeforeEventSend` callback.  Questo callback viene chiamato ogni volta che viene inviato un evento.  Questo callback viene passato in un oggetto evento con un `xdm` campo .  Modifica `content.xdm` per modificare i dati inviati con l’evento.


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

`xdm` i campi sono impostati in questo ordine:

1. Valori passati come opzioni al comando evento `alloy("sendEvent", { xdm: ... });`
2. Valori raccolti automaticamente.  (Vedi [Informazioni automatiche](../data-collection/automatic-information.md).)
3. Le modifiche apportate nel `onBeforeEventSend` callback.

Alcune note sul `onBeforeEventSend` callback:

* L&#39;evento XDM può essere modificato durante il callback. Dopo la restituzione del callback, tutti i campi e i valori modificati degli oggetti content.xdm e content.data vengono inviati con l’evento .

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Se il callback genera un&#39;eccezione, l&#39;elaborazione per l&#39;evento viene interrotta e l&#39;evento non viene inviato.
* Se il callback restituisce il valore booleano di `false`, l’elaborazione dell’evento viene interrotta senza un errore e l’evento non viene inviato. Questo meccanismo consente di ignorare facilmente alcuni eventi esaminando i dati dell’evento e restituendo `false` se l’evento non deve essere inviato.

   >[!NOTE]
   >Presta attenzione a evitare di restituire false sul primo evento su una pagina. La restituzione di false sul primo evento può avere un impatto negativo sulla personalizzazione.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Qualsiasi valore restituito diverso da booleano `false` consentirà all’evento di elaborare e inviare dopo il callback.

* Gli eventi possono essere filtrati esaminando il tipo di evento (vedi [Tipi di eventi](#event-types).):

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

## potenziali errori utilizzabili

Quando si invia un evento, potrebbe essere generato un errore se i dati inviati sono troppo grandi (oltre 32 KB per la richiesta completa). In questo caso, devi ridurre la quantità di dati inviati.
