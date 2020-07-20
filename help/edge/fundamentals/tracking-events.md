---
title: Tracciamento degli eventi
seo-title: Tracciamento  eventi SDK Web Adobe Experience Platform
description: Scopri come tenere traccia  eventi SDK Web per Experience Platform
seo-description: Scopri come tenere traccia  eventi SDK Web per Experience Platform
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Tracciamento degli eventi

Per inviare i dati dell&#39;evento ad Adobe Experience Cloud, usa il `sendEvent` comando. Il `sendEvent` comando è il modo principale per inviare i dati al [!DNL Experience Cloud]destinatario e per recuperare contenuti, identità e destinazioni personalizzate.

I dati inviati ad Adobe Experience Cloud sono suddivisi in due categorie:

* Dati XDM
* Dati non XDM (attualmente non supportati)

## Invio di dati XDM

I dati XDM sono un oggetto il cui contenuto e la cui struttura corrispondono a uno schema creato all&#39;interno  Adobe Experience Platform. [Ulteriori informazioni sulla creazione di uno schema.](../../xdm/tutorials/create-schema-ui.md)

Qualsiasi dato XDM che desideri far parte dell&#39;analisi, della personalizzazione, dei tipi di pubblico o delle destinazioni deve essere inviato utilizzando l&#39; `xdm` opzione.

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

>[!NOTE]
>Esiste un limite di 32 KB per i dati che possono essere inviati in ogni evento nel campo XDM.

### Invio di dati non XDM

Al momento, l&#39;invio di dati che non corrispondono a uno schema XDM non è supportato. Il supporto è pianificato per una data futura.

### Impostazione `eventType`

In un evento di esperienza XDM, è presente un `eventType` campo. Contiene il tipo di evento principale per il record. Questo può essere trasmesso come parte dell&#39; `xdm` opzione.

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

In alternativa, `eventType` è possibile passare al comando dell&#39;evento utilizzando l&#39; `type` opzione. Dietro le quinte, questo viene aggiunto ai dati XDM. Questa `type` opzione consente di impostare più facilmente il payload `eventType` senza dover modificare XDM.

```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

## Utilizzo dell&#39;API sendBeacon

Può essere difficile inviare i dati dell&#39;evento subito prima che l&#39;utente della pagina Web se ne vada. Se la richiesta richiede troppo tempo, il browser potrebbe annullare la richiesta. Alcuni browser hanno implementato un&#39;API standard Web chiamata `sendBeacon` per consentire una raccolta più semplice dei dati durante questo periodo. Quando si utilizza `sendBeacon`, il browser effettua la richiesta Web nel contesto di navigazione globale. Questo significa che il browser esegue la richiesta del beacon in background e non blocca la navigazione della pagina. Per indicare  Adobe Experience Platform [!DNL Web SDK] da utilizzare `sendBeacon`, aggiungere l&#39;opzione `"documentUnloading": true` al comando dell&#39;evento.  Ecco un esempio:

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

I browser hanno imposto limiti alla quantità di dati che possono essere inviati `sendBeacon` contemporaneamente. In molti browser, il limite è 64 K. Se il browser rifiuta l&#39;evento perché il payload è troppo grande,  Adobe Experience Platform [!DNL Web SDK] torna a utilizzare il normale metodo di trasporto (ad esempio, fetch).

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

Se desiderate aggiungere, rimuovere o modificare i campi dall’evento a livello globale, potete configurare un `onBeforeEventSend` callback.  Questa callback viene chiamata ogni volta che un evento viene inviato.  Questo callback viene passato in un oggetto evento con un `xdm` campo.  Modificare `event.xdm` per modificare i dati inviati nell&#39;evento.

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
2. Raccolti automaticamente i valori.  Consultate Informazioni [](../reference/automatic-information.md)automatiche.
3. Modifiche apportate al `onBeforeEventSend` callback.

Se il `onBeforeEventSend` callback genera un’eccezione, l’evento viene comunque inviato; tuttavia, nessuna delle modifiche apportate all’interno del callback viene applicata all’evento finale.

## potenziali errori fruibili

Quando si invia un evento, potrebbe essere generato un errore se i dati inviati sono troppo grandi (oltre 32 KB per la richiesta completa). In questo caso, è necessario ridurre la quantità di dati inviati.

Quando il debug è abilitato, il server convalida in modo sincrono i dati dell&#39;evento che vengono inviati in base allo schema XDM configurato. Se i dati non corrispondono allo schema, i dettagli relativi alla mancata corrispondenza vengono restituiti dal server e viene generato un errore. In questo caso, modificare i dati per farli corrispondere allo schema. Se il debug non è abilitato, il server convalida i dati in modo asincrono e, pertanto, non viene generato alcun errore corrispondente.
