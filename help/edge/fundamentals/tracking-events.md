---
title: Tracciamento degli eventi
seo-title: Tracciamento degli eventi SDK Web per Adobe Experience Platform
description: Scopri come tenere traccia degli eventi SDK Web per la piattaforma Experience
seo-description: Scopri come tenere traccia degli eventi SDK Web per la piattaforma Experience
translation-type: tm+mt
source-git-commit: 3c6f9663ef5b83ceeb93539171017e2b282a613f

---


# Tracciamento degli eventi

>[!IMPORTANT]
>
>L’SDK Web per Adobe Experience Platform è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

Per inviare i dati dell&#39;evento ad Adobe Experience Cloud, usa il `event` comando. Il `event` comando è il modo principale per inviare dati a Experience Cloud e per recuperare contenuti, identità e destinazioni personalizzate.

I dati inviati ad Adobe Experience Cloud sono suddivisi in due categorie:

* Dati XDM
* Dati non XDM (attualmente non supportati)

## Invio di dati XDM

I dati XDM sono un oggetto il cui contenuto e la cui struttura corrispondono a uno schema creato in Adobe Experience Platform. [Ulteriori informazioni sulla creazione di uno schema.](../../xdm/tutorials/create-schema-ui.md)

Eventuali dati XDM che desiderate far parte di analisi, personalizzazione, audience o destinazioni devono essere inviati utilizzando l&#39; `xdm` opzione.

```javascript
alloy("event", {
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

>[!Note]
>Esiste un limite di 32 KB per i dati che possono essere inviati in ogni evento nel campo XDM.

### Invio di dati non XDM

Al momento, l&#39;invio di dati che non corrispondono a uno schema XDM non è supportato. Il supporto è pianificato per una data futura.

### Impostazione `eventType`

In un evento di esperienza XDM, è presente un `eventType` campo. Contiene il tipo di evento principale per il record. Questo può essere trasmesso come parte dell&#39; `xdm` opzione.

```javascript
alloy("event", {
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

In alternativa, `eventType` è possibile passare al comando dell&#39;evento utilizzando l&#39; `type` opzione. Dietro le quinte, questo viene aggiunto ai dati XDM. Questa `type` opzione consente di impostare più facilmente il payload `eventType` senza dover modificare XDM.

```javascript
var myXDMData = { ... };

alloy("event", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Avvio di una visualizzazione

Una volta avviata la visualizzazione, è importante inviare una notifica all’SDK impostando `viewStart` l’opzione all’ `true` interno del `event` comando. Ciò indica, tra l’altro, che l’SDK deve recuperare e rendere il contenuto personalizzato. Anche se al momento non utilizzate la personalizzazione, semplifica notevolmente l&#39;abilitazione della personalizzazione o di altre funzioni in un secondo momento, perché non sarà necessario modificare il codice sulla pagina. Inoltre, il tracciamento delle viste è utile quando si visualizzano i report di analisi dopo la raccolta dei dati.

La definizione di una vista può dipendere dal contesto.

* In un normale sito Web, ogni pagina Web viene generalmente considerata una visualizzazione univoca. In questo caso, un evento con `viewStart` impostato su `true` deve essere eseguito il prima possibile nella parte superiore della pagina.
* In un&#39;applicazione a pagina singola \(SPA\), una vista è meno definita. In genere indica che l&#39;utente ha navigato all&#39;interno dell&#39;applicazione e che la maggior parte del contenuto è cambiata. Per coloro che hanno familiarità con le basi tecniche delle applicazioni a pagina singola, questo è tipicamente quando l&#39;applicazione carica un nuovo percorso. Ogni volta che un utente passa a una nuova vista, tuttavia si sceglie di definire una _vista_, `viewStart` deve essere eseguito un evento con impostato per `true` .

L’evento con `viewStart` impostato su `true` è il meccanismo principale per inviare dati ad Adobe Experience Cloud e richiedere contenuti da Adobe Experience Cloud. È possibile iniziare una visualizzazione nel modo seguente:

```javascript
alloy("event", {
  "viewStart": true,
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

Dopo l&#39;invio dei dati, il server risponde, tra l&#39;altro, con contenuti personalizzati. Questo contenuto personalizzato viene automaticamente visualizzato nella vista. I gestori di collegamenti vengono inoltre collegati automaticamente al contenuto della nuova visualizzazione.

## Utilizzo dell&#39;API sendBeacon

Può essere difficile inviare i dati dell&#39;evento subito prima che l&#39;utente della pagina Web se ne vada. Se la richiesta richiede troppo tempo, il browser potrebbe annullare la richiesta. Alcuni browser hanno implementato un&#39;API standard Web chiamata `sendBeacon` per consentire una raccolta più semplice dei dati durante questo periodo. Quando si utilizza `sendBeacon`, il browser effettua la richiesta Web nel contesto di navigazione globale. Questo significa che il browser esegue la richiesta del beacon in background e non blocca la navigazione della pagina. Per comunicare all’SDK Web di Adobe Experience Platform di utilizzarlo `sendBeacon`, aggiungi l’opzione `"documentUnloading": true` al comando dell’evento.  Ecco un esempio:

```javascript
alloy("event", {
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

I browser hanno imposto limiti alla quantità di dati che possono essere inviati `sendBeacon` contemporaneamente. In molti browser, il limite è 64 K. Se il browser rifiuta l’evento perché il payload è troppo grande, Adobe Experience Platform Web SDK torna a utilizzare il suo metodo di trasporto normale (ad esempio, fetch).

## Gestione delle risposte dagli eventi

Se desiderate gestire una risposta da un evento, potete ricevere una notifica di esito positivo o negativo come segue:

```javascript
alloy("event", {
  "viewStart": true,
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
}).then(function() {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Modifica degli eventi a livello globale {#modifying-events-globally}

Se desiderate aggiungere, rimuovere o modificare i campi dall’evento a livello globale, potete configurare un `onBeforeEventSend` callback.  Questa callback viene chiamata ogni volta che un evento viene inviato.  Questo callback viene passato in un oggetto evento con un `xdm` campo.  Modificare `event.xdm` per modificare i dati inviati nell&#39;evento.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
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

1. Valori passati come opzioni al comando evento `alloy("event", { xdm: ... });`
2. Raccolti automaticamente i valori.  Consultate Informazioni [](../reference/automatic-information.md)automatiche.
3. Modifiche apportate al `onBeforeEventSend` callback.

Se il `onBeforeEventSend` callback genera un’eccezione, l’evento viene comunque inviato; tuttavia, nessuna delle modifiche apportate all’interno del callback viene applicata all’evento finale.

## potenziali errori fruibili

Quando si invia un evento, potrebbe essere generato un errore se i dati inviati sono troppo grandi (oltre 32 KB per la richiesta completa). In questo caso, è necessario ridurre la quantità di dati inviati.

Quando il debug è abilitato, il server convalida in modo sincrono i dati dell&#39;evento che vengono inviati in base allo schema XDM configurato. Se i dati non corrispondono allo schema, i dettagli relativi alla mancata corrispondenza vengono restituiti dal server e viene generato un errore. In questo caso, modificare i dati per farli corrispondere allo schema. Se il debug non è abilitato, il server convalida i dati in modo asincrono e, pertanto, non viene generato alcun errore corrispondente.
