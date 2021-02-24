---
title: Tenere traccia degli eventi mediante l’SDK Web per Adobe Experience Platform
seo-description: Scoprite come tenere traccia degli eventi Adobe Experience Platform Web SDK.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 0%

---


# Tracciare gli eventi

Per inviare i dati dell&#39;evento ad Adobe Experience Cloud, utilizzate il comando `sendEvent`. Il comando `sendEvent` è il modo principale per inviare i dati a [!DNL Experience Cloud] e per recuperare contenuti, identità e destinazioni personalizzate.

I dati inviati ad Adobe Experience Cloud rientrano in due categorie:

* Dati XDM
* Dati non XDM (attualmente non supportati)

## Invio di dati XDM

I dati XDM sono un oggetto il cui contenuto e la cui struttura corrispondono a uno schema creato in Adobe Experience Platform. [Ulteriori informazioni sulla creazione di uno schema.](../../xdm/tutorials/create-schema-ui.md)

Eventuali dati XDM che desiderate far parte di analisi, personalizzazione, audience o destinazioni devono essere inviati utilizzando l&#39;opzione `xdm`.


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

È possibile che passi un certo tempo tra l&#39;esecuzione del comando `sendEvent` e l&#39;invio dei dati al server (ad esempio, se la libreria SDK Web non è stata caricata completamente o se il consenso non è ancora stato ricevuto). Se si intende modificare una parte qualsiasi dell&#39;oggetto `xdm` dopo l&#39;esecuzione del comando `sendEvent`, è consigliabile duplicare l&#39;oggetto `xdm` _prima_ eseguendo il comando `sendEvent`. Esempio:

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

In questo esempio, il livello dati viene clonato serializzandolo in JSON e quindi deserializzandolo. Quindi, il risultato clonato viene passato nel comando `sendEvent`. In questo modo si assicura che il comando `sendEvent` abbia un&#39;istantanea del livello dati così come era presente quando il comando `sendEvent` è stato eseguito, in modo che le modifiche successive all&#39;oggetto livello dati originale non vengano riflesse nei dati inviati al server. Se utilizzate un livello dati basato su eventi, è probabile che la duplicazione dei dati sia già gestita automaticamente. Ad esempio, se si utilizza il [ Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer/wiki), il metodo `getState()` fornisce un&#39;istantanea calcolata e duplicata di tutte le modifiche precedenti. Questo viene gestito automaticamente anche se utilizzi l’estensione Adobe Experience Platform Web SDK in  Adobe Experience Platform Launch.

>[!NOTE]
>
>Esiste un limite di 32 KB per i dati che possono essere inviati in ogni evento nel campo XDM.

### Invio di dati non XDM

Al momento, l&#39;invio di dati che non corrispondono a uno schema XDM non è supportato. Il supporto è pianificato per una data futura.

### Impostazione `eventType`

In un evento di esperienza XDM, è presente un campo facoltativo `eventType`. Contiene il tipo di evento principale per il record. L&#39;impostazione di un tipo di evento può facilitare la distinzione tra i diversi eventi da inviare. XDM fornisce diversi tipi di evento predefiniti che è possibile utilizzare oppure creare sempre tipi di evento personalizzati per i casi di utilizzo. Di seguito è riportato un elenco di tutti i tipi di evento predefiniti forniti da XDM. [Per saperne di più, consulta il repo](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values) pubblico XDM.


| **Tipo evento:** | **Definizione:** |
| ---------------------------------- | ------------ |
| advertising.completes | Indica se una risorsa multimediale temporizzata è stata esaminata per il completamento, il che non significa necessariamente che il visualizzatore abbia guardato l’intero video; il visualizzatore avrebbe potuto essere ignorato |
| advertising.timePlayed | Descrive il tempo trascorso da un utente su una specifica risorsa multimediale temporizzata |
| advertising.federated | Indica se un evento esperienza è stato creato tramite la federazione di dati (condivisione dei dati tra i clienti) |
| advertising.clicks | Azioni di clic su un annuncio pubblicitario |
| advertising.conversions | Azioni predefinite del cliente che attivano un evento per la valutazione delle prestazioni |
| advertising.firstQuartiles | Un annuncio video digitale ha riprodotto fino al 25% della sua durata a velocità normale |
| advertising.impressions | Impression(e) di un annuncio pubblicitario per un utente finale con il potenziale di essere visualizzato |
| advertising.midpoints | Un annuncio video digitale ha riprodotto fino al 50% della sua durata a velocità normale |
| advertising.starts | La riproduzione di un annuncio video digitale è iniziata |
| advertising.thirdQuartiles | Un annuncio video digitale ha riprodotto fino al 75% della sua durata a velocità normale |
| web.webpagedetails.pageViews | Sono state visualizzate le visualizzazioni di una pagina Web |
| web.webinteraction.linkClicks | Si è verificato un clic su un collegamento Web |
| commerce.checkouts | Un&#39;azione durante un processo di estrazione di un elenco di prodotti può verificarsi più di un evento di estrazione se in un processo di estrazione sono presenti più passaggi. Se sono presenti più passaggi, le informazioni sull&#39;ora dell&#39;evento e la pagina o l&#39;esperienza di riferimento vengono utilizzate per identificare il passaggio che i singoli eventi rappresentano nell&#39;ordine |
| commerce.productListAdds | Aggiunta di un prodotto all&#39;elenco dei prodotti. Esempio di un prodotto aggiunto a un carrello |
| commerce.productListOpens | Inizializzazioni di un nuovo elenco di prodotti. Esempio di creazione di un carrello |
| commerce.productListRemovals | Rimozione di una voce di prodotto da un elenco di prodotti. Esempio di un prodotto rimosso da un carrello |
| commerce.productListReopens | Un elenco di prodotti non più accessibile (abbandonato) è stato riattivato dall&#39;utente. Esempio tramite un&#39;attività di remarketing |
| commerce.productListViews | Si sono verificate visualizzazioni di un elenco di prodotti |
| commerce.productViews | Sono state visualizzate le visualizzazioni di un prodotto |
| commerce.purchases | Un ordine è stato accettato. L&#39;acquisto è l&#39;unica azione richiesta in una conversione commerciale. L&#39;acquisto deve avere un elenco di prodotti a cui fare riferimento |
| commerce.saveForLaters | L&#39;elenco dei prodotti viene salvato per un utilizzo futuro. Esempio di elenco di desideri di un prodotto |
| delivery.feedback | Eventi di feedback per una consegna. Esempi di eventi di feedback per la consegna di un&#39;e-mail |


Questi tipi di evento saranno visualizzati in un menu a discesa se utilizzate l&#39;estensione Adobe Experience Platform Launch  oppure potete sempre trasmetterli senza Experience Platform Launch. Possono essere passati come parte dell&#39;opzione `xdm`.


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

In alternativa, è possibile trasmettere il `eventType` al comando dell&#39;evento utilizzando l&#39;opzione `type`. Dietro le quinte, questo viene aggiunto ai dati XDM. L&#39;opzione `type` consente di impostare più facilmente il `eventType` senza dover modificare il payload XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Sostituzione dell’ID del set di dati

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

È inoltre possibile aggiungere informazioni sull&#39;identità personalizzata all&#39;evento. Vedere [Recupero  ID Experience Cloud](../identity/overview.md).

## Utilizzo dell&#39;API sendBeacon

Può essere difficile inviare i dati dell&#39;evento subito prima che l&#39;utente della pagina Web se ne vada. Se la richiesta richiede troppo tempo, il browser potrebbe annullare la richiesta. Alcuni browser hanno implementato un&#39;API standard Web denominata `sendBeacon` per consentire la raccolta dei dati in questo periodo con maggiore facilità. Quando si utilizza `sendBeacon`, il browser effettua la richiesta Web nel contesto di navigazione globale. Questo significa che il browser esegue la richiesta del beacon in background e non blocca la navigazione della pagina. Per indicare ad Adobe Experience Platform [!DNL Web SDK] di utilizzare `sendBeacon`, aggiungere l&#39;opzione `"documentUnloading": true` al comando dell&#39;evento.  Ecco un esempio:


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

I browser hanno imposto limiti alla quantità di dati che è possibile inviare contemporaneamente con `sendBeacon`. In molti browser, il limite è 64 K. Se il browser rifiuta l&#39;evento perché il payload è troppo grande, Adobe Experience Platform [!DNL Web SDK] torna a utilizzare il normale metodo di trasporto (ad esempio, fetch).

## Gestione delle risposte dagli eventi

Se desiderate gestire una risposta da un evento, potete ricevere una notifica di esito positivo o negativo come segue:


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

Se desiderate aggiungere, rimuovere o modificare i campi dall&#39;evento a livello globale, potete configurare un callback `onBeforeEventSend`.  Questa callback viene chiamata ogni volta che un evento viene inviato.  Questo callback viene passato in un oggetto evento con un campo `xdm`.  Modificare `event.xdm` per modificare i dati inviati nell&#39;evento.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` i campi sono impostati in questo ordine:

1. Valori passati come opzioni al comando evento `alloy("sendEvent", { xdm: ... });`
2. Raccolti automaticamente i valori.  (Vedere [Informazioni automatiche](../data-collection/automatic-information.md).)
3. Modifiche apportate al callback `onBeforeEventSend`.

Se il callback `onBeforeEventSend` genera un&#39;eccezione, l&#39;evento viene comunque inviato; tuttavia, nessuna delle modifiche apportate all’interno del callback viene applicata all’evento finale.

## potenziali errori fruibili

Quando si invia un evento, potrebbe essere generato un errore se i dati inviati sono troppo grandi (oltre 32 KB per la richiesta completa). In questo caso, è necessario ridurre la quantità di dati inviati.

Quando il debug è abilitato, il server convalida in modo sincrono i dati dell&#39;evento che vengono inviati in base allo schema XDM configurato. Se i dati non corrispondono allo schema, i dettagli relativi alla mancata corrispondenza vengono restituiti dal server e viene generato un errore. In questo caso, modificare i dati per farli corrispondere allo schema. Se il debug non è abilitato, il server convalida i dati in modo asincrono e, pertanto, non viene generato alcun errore corrispondente.
