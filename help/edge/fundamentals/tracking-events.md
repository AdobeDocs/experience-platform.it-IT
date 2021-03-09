---
title: Tracciare gli eventi utilizzando l’SDK per web di Adobe Experience Platform
description: Scopri come tenere traccia degli eventi dell’SDK Web per Adobe Experience Platform.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentSloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 25cf425df92528cec88ea027f3890abfa9cd9b41
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---


# Tracciare gli eventi

Per inviare i dati dell’evento a Adobe Experience Cloud, utilizza il comando `sendEvent` . Il comando `sendEvent` è il modo principale per inviare dati a [!DNL Experience Cloud] e per recuperare contenuti personalizzati, identità e destinazioni di pubblico.

I dati inviati a Adobe Experience Cloud rientrano in due categorie:

* Dati XDM
* Dati non XDM (attualmente non supportati)

## Invio di dati XDM

I dati XDM sono oggetti il cui contenuto e la cui struttura corrispondono a uno schema creato in Adobe Experience Platform. [Ulteriori informazioni su come creare uno schema.](../../xdm/tutorials/create-schema-ui.md)

Eventuali dati XDM che desideri far parte di analisi, personalizzazione, pubblico o destinazioni devono essere inviati utilizzando l’opzione `xdm` .


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

È possibile che passi un certo tempo tra l’esecuzione del comando `sendEvent` e l’invio dei dati al server (ad esempio, se la libreria SDK web non è stata completamente caricata o se il consenso non è ancora stato ricevuto). Se si intende modificare una parte qualsiasi dell&#39;oggetto `xdm` dopo l&#39;esecuzione del comando `sendEvent`, è consigliabile clonare l&#39;oggetto `xdm` _prima_ eseguendo il comando `sendEvent`. Esempio:

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

In questo esempio, il livello dati viene clonato serializzandolo in JSON e quindi deserializzandolo. Successivamente, il risultato clonato viene passato nel comando `sendEvent` . In questo modo il comando `sendEvent` dispone di un&#39;istantanea del livello dati come era presente quando è stato eseguito il comando `sendEvent` in modo che le modifiche successive all&#39;oggetto livello dati originale non vengano riportate nei dati inviati al server. Se utilizzi un livello dati basato su eventi, è probabile che la duplicazione dei dati sia già gestita automaticamente. Ad esempio, se utilizzi [Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer/wiki), il metodo `getState()` fornisce un&#39;istantanea calcolata e clonata di tutte le modifiche precedenti. Questa operazione viene gestita automaticamente anche se utilizzi l’estensione Adobe Experience Platform Web SDK in Adobe Experience Platform Launch.

>[!NOTE]
>
>Esiste un limite di 32 KB per i dati che possono essere inviati in ogni evento nel campo XDM.

### Invio di dati non XDM

Al momento, l’invio di dati che non corrispondono a uno schema XDM non è supportato. Il supporto è pianificato per una data futura.

### Impostazione `eventType` {#event-types}

In un evento di esperienza XDM, è disponibile un campo facoltativo `eventType` . Contiene il tipo di evento principale per il record. L’impostazione di un tipo di evento può essere utile per distinguere tra i diversi eventi che invierai. XDM fornisce diversi tipi di evento predefiniti che è possibile utilizzare oppure è sempre possibile creare tipi di evento personalizzati per i casi d’uso. Di seguito è riportato un elenco di tutti i tipi di evento predefiniti forniti da XDM. [Ulteriori informazioni sono disponibili nel repository](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values) pubblico XDM.


| **Tipo evento:** | **Definizione:** |
| ---------------------------------- | ------------ |
| advertising.completes | Indica se una risorsa multimediale temporizzata è stata guardata al completamento - questo non significa necessariamente che il visualizzatore ha guardato l&#39;intero video; il visualizzatore avrebbe potuto saltare in avanti |
| advertising.timePlayed | Descrive il tempo trascorso da un utente su una specifica risorsa multimediale temporizzata |
| advertising.federated | Indica se è stato creato un evento esperienza tramite la federazione di dati (condivisione di dati tra i clienti) |
| advertising.clicks | Azioni di clic su un annuncio |
| advertising.conversions | Azioni predefinite del cliente che attivano un evento per la valutazione delle prestazioni |
| advertising.firstQuartiles | Un annuncio video digitale ha riprodotto fino al 25% della sua durata a velocità normale |
| advertising.impressions | Impressioni di un annuncio pubblicitario per un utente finale con il potenziale di essere visualizzato |
| advertising.midpoints | Un annuncio video digitale ha riprodotto fino al 50% della sua durata a velocità normale |
| advertising.starts | La riproduzione di un annuncio video digitale è iniziata |
| advertising.thirdQuartiles | Un annuncio video digitale ha riprodotto fino al 75% della sua durata a velocità normale |
| web.webpagedetails.pageViews | Visualizzazione di una pagina Web |
| web.webinteraction.linkClicks | Si è verificato un clic su un collegamento web |
| commerce.checkouts | Un’azione durante un processo di pagamento di un elenco di prodotti può essere eseguita con più di un evento di pagamento se sono presenti più passaggi in un processo di pagamento. Se sono presenti più passaggi, le informazioni sull&#39;ora dell&#39;evento e la pagina o l&#39;esperienza a cui si fa riferimento vengono utilizzate per identificare il passaggio che singoli eventi rappresentano nell&#39;ordine |
| commerce.productListAdds | Aggiunta di un prodotto all’elenco dei prodotti. Esempio di aggiunta di un prodotto a un carrello |
| commerce.productListOpens | Inizializzazioni di un nuovo elenco di prodotti. Esempio di creazione di un carrello |
| commerce.productListRemovals | Rimozione di una voce di prodotto da un elenco di prodotti. Esempio di rimozione di un prodotto da un carrello |
| commerce.productListReopens | Un elenco di prodotti non più accessibile (abbandonato) è stato riattivato dall’utente. Esempio tramite un’attività di remarketing |
| commerce.productListViews | Visualizzazione/e di un elenco di prodotti |
| commerce.productViews | Visualizzazione/e di un prodotto |
| commerce.purchases | Un ordine è stato accettato. Acquisto è l’unica azione richiesta in una conversione di e-commerce. L&#39;acquisto deve avere un elenco di prodotti a cui fare riferimento |
| commerce.saveForLaters | L’elenco dei prodotti viene salvato per un utilizzo futuro. Esempio di elenco dei desideri di un prodotto |
| delivery.feedback | Eventi di feedback per una consegna. Esempio di eventi di feedback per una consegna e-mail |


Questi tipi di evento verranno visualizzati in un elenco a discesa se utilizzi l’estensione Adobe Experience Platform Launch o puoi sempre trasmetterli senza Experience Platform Launch. Possono essere passati come parte dell&#39;opzione `xdm` .


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

In alternativa, è possibile passare il `eventType` nel comando dell&#39;evento utilizzando l&#39;opzione `type`. Dietro le quinte, questo viene aggiunto ai dati XDM. Avere come opzione `type` consente di impostare più facilmente il `eventType` senza dover modificare il payload XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Sovrascrittura dell’ID del set di dati

In alcuni casi d’uso, potrebbe essere utile inviare un evento a un set di dati diverso da quello configurato nell’interfaccia utente di configurazione. Per questo è necessario impostare l&#39;opzione `datasetId` sul comando `sendEvent`:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Aggiunta di informazioni sull&#39;identità

È inoltre possibile aggiungere all’evento informazioni di identità personalizzate. Consulta [Recupero ID Experience Cloud](../identity/overview.md).

## Utilizzo dell’API sendBeacon

Può essere difficile inviare i dati dell’evento immediatamente prima che l’utente della pagina web se ne vada. Se la richiesta richiede troppo tempo, il browser potrebbe annullare la richiesta. Alcuni browser hanno implementato un’API web standard denominata `sendBeacon` per consentire una raccolta più semplice dei dati durante questo periodo di tempo. Quando utilizzi `sendBeacon`, il browser effettua la richiesta web nel contesto di navigazione globale. Questo significa che il browser effettua la richiesta beacon in background e non blocca la navigazione delle pagine. Per indicare a Adobe Experience Platform [!DNL Web SDK] di utilizzare `sendBeacon`, aggiungi l&#39;opzione `"documentUnloading": true` al comando dell&#39;evento.  Ecco un esempio:


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

I browser hanno imposto limiti alla quantità di dati che possono essere inviati contemporaneamente con `sendBeacon` . In molti browser, il limite è di 64K. Se il browser rifiuta l’evento perché il payload è troppo grande, Adobe Experience Platform [!DNL Web SDK] torna a utilizzare il normale metodo di trasporto (ad esempio, fetch).

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
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Modifica degli eventi a livello globale {#modifying-events-globally}

Se desideri aggiungere, rimuovere o modificare i campi dall’evento a livello globale, puoi configurare un callback `onBeforeEventSend`.  Questo callback viene chiamato ogni volta che viene inviato un evento.  Questo callback viene passato in un oggetto evento con un campo `xdm` .  Modifica `content.xdm` per modificare i dati inviati con l’evento.


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

1. Valori passati come opzioni al comando dell&#39;evento `alloy("sendEvent", { xdm: ... });`
2. Valori raccolti automaticamente.  (Vedere [Informazioni automatiche](../data-collection/automatic-information.md).)
3. Le modifiche apportate nel callback `onBeforeEventSend` .

Alcune note sul callback `onBeforeEventSend`:

* L&#39;evento XDM può essere modificato durante il callback. Dopo la restituzione del callback, eventuali campi e valori modificati di
gli oggetti content.xdm e content.data vengono inviati con l’evento .

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Se il callback genera un&#39;eccezione, l&#39;elaborazione per l&#39;evento viene interrotta e l&#39;evento non viene inviato.
* Se il callback restituisce il valore booleano di `false`, l&#39;elaborazione dell&#39;evento viene interrotta,
senza un errore e l’evento non viene inviato. Questo meccanismo consente di ignorare facilmente alcuni eventi da
esamina i dati dell’evento e restituisce `false` se l’evento non deve essere inviato.

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

Qualsiasi valore restituito diverso dal valore booleano `false` consentirà all’evento di elaborare e inviare dopo il callback.

* Gli eventi possono essere filtrati esaminando il tipo di evento (consulta [Tipi di eventi](#event-types)):

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
