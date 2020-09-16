---
title: Tracciamento degli eventi
seo-title: Tracciamento degli eventi SDK Web per Adobe Experience Platform
description: Scopri come tenere traccia  eventi SDK Web per Experienci Platform
seo-description: Scopri come tenere traccia  eventi SDK Web per Experienci Platform
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 69ddfca041624123b03eb01d0f10a5bdb36cd119
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---


# Tracciamento degli eventi

Per inviare i dati dell&#39;evento all&#39;Adobe Experience Cloud, utilizzate il `sendEvent` comando. Il `sendEvent` comando è il modo principale per inviare i dati al [!DNL Experience Cloud]destinatario e per recuperare contenuti, identità e destinazioni personalizzate.

I dati inviati ad Adobe Experience Cloud rientrano in due categorie:

* Dati XDM
* Dati non XDM (attualmente non supportati)

## Invio di dati XDM

I dati XDM sono un oggetto il cui contenuto e la cui struttura corrispondono a uno schema creato in Adobe Experience Platform. [Ulteriori informazioni sulla creazione di uno schema.](../../xdm/tutorials/create-schema-ui.md)

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
>
>Esiste un limite di 32 KB per i dati che possono essere inviati in ogni evento nel campo XDM.

### Invio di dati non XDM

Al momento, l&#39;invio di dati che non corrispondono a uno schema XDM non è supportato. Il supporto è pianificato per una data futura.

### Impostazione `eventType`

In un evento di esperienza XDM, è presente un `eventType` campo facoltativo. Contiene il tipo di evento principale per il record. L&#39;impostazione di un tipo di evento può facilitare la distinzione tra i diversi eventi da inviare. XDM fornisce diversi tipi di evento predefiniti che è possibile utilizzare oppure creare sempre tipi di evento personalizzati per i casi di utilizzo. Di seguito è riportato un elenco di tutti i tipi di evento predefiniti forniti da XDM.


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


Questi tipi di evento verranno visualizzati in un menu a discesa se si utilizza l&#39;estensione Launch o se è sempre possibile trasmetterli senza Launch. Possono essere passati come parte dell&#39; `xdm` opzione.


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

### Sostituzione dell’ID del set di dati

In alcuni casi d’uso, potrebbe essere utile inviare un evento a un set di dati diverso da quello configurato nell’interfaccia utente di configurazione. Per questo è necessario impostare l&#39; `datasetId` opzione sul `sendEvent` comando:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Aggiunta di informazioni sull&#39;identità

È inoltre possibile aggiungere informazioni sull&#39;identità personalizzata all&#39;evento. Consultate [Recupero dell’ID Experience Cloud](./identity.md)

## Utilizzo dell&#39;API sendBeacon

Può essere difficile inviare i dati dell&#39;evento subito prima che l&#39;utente della pagina Web se ne vada. Se la richiesta richiede troppo tempo, il browser potrebbe annullare la richiesta. Alcuni browser hanno implementato un&#39;API standard Web chiamata `sendBeacon` per consentire una raccolta più semplice dei dati durante questo periodo. Quando si utilizza `sendBeacon`, il browser effettua la richiesta Web nel contesto di navigazione globale. Questo significa che il browser esegue la richiesta del beacon in background e non blocca la navigazione della pagina. Per indicare [!DNL Web SDK] ad Adobe Experience Platform di utilizzare `sendBeacon`, aggiungete l&#39;opzione `"documentUnloading": true` al comando dell&#39;evento.  Ecco un esempio:


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

I browser hanno imposto limiti alla quantità di dati che possono essere inviati `sendBeacon` contemporaneamente. In molti browser, il limite è 64 K. Se il browser rifiuta l’evento perché il payload è troppo grande, Adobe Experience Platform [!DNL Web SDK] torna a utilizzare il suo metodo di trasporto normale (ad esempio, fetch).

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
