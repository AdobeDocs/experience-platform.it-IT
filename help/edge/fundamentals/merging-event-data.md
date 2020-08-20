---
title: Unione dei dati evento
seo-title: Unione dei dati evento Adobe Experience Platform Web SDK
description: Scoprite come unire i dati dell'evento SDK Web  Experience Platform
seo-description: Scoprite come unire i dati dell'evento SDK Web  Experience Platform
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---


# Unione dei dati evento

>[!IMPORTANT]
>
>Questa funzione è ancora in fase di sviluppo. Non tutte le soluzioni saranno in grado di unire i dati dell&#39;evento come descritto in questa pagina.

A volte, non tutti i dati sono disponibili quando si verifica un evento. Potrebbe essere utile acquisire i dati _disponibili_ , in modo che non vadano perduti se, ad esempio, l&#39;utente chiude il browser. D&#39;altro canto, è possibile includere anche qualsiasi dato che diventerà disponibile in un secondo momento.

In questi casi, è possibile unire i dati con gli eventi precedenti passando `eventMergeId` come opzione ai `event` comandi come segue:

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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  }
  "eventMergeId": "ABC123"
});
```

Trasmettendo lo stesso `eventMergeID` valore a entrambi i comandi dell&#39;evento in questo esempio, i dati nel secondo comando dell&#39;evento vengono incrementati ai dati precedentemente inviati sul primo comando dell&#39;evento. Un record per ciascun comando evento viene creato nel [!DNL Experience Data Platform], ma durante il reporting i record vengono uniti utilizzando il comando `eventMergeID` e visualizzati come un singolo evento.

Se inviate dati su un particolare evento a fornitori terzi, potete includere anche gli stessi dati `eventMergeID` con tali dati. Successivamente, se si sceglie di importare dati di terze parti nell&#39;Adobe Experience Platform, `eventMergeID` verrà utilizzato per unire tutti i dati raccolti a seguito dell&#39;evento discreto che si è verificato sulla pagina Web.

## Generazione di un `eventMergeID`

Il `eventMergeID` valore può essere una qualsiasi stringa selezionata, ma ricordate che tutti gli eventi inviati utilizzando lo stesso ID vengono segnalati come un singolo evento, quindi prestate attenzione a imporre l&#39;univocità quando gli eventi non devono essere uniti. Se desideri che l’SDK generi un’univocità `eventMergeID` per tuo conto (in base alla specifica [](https://www.ietf.org/rfc/rfc4122.txt)UUID v4 ampiamente adottata), puoi usare il `createEventMergeId` comando per farlo.

Come per tutti i comandi, viene restituita una promessa perché è possibile eseguire il comando prima che l’SDK abbia terminato il caricamento. La promessa sarà risolta con un unico `eventMergeID` il prima possibile. È possibile attendere la risoluzione della promessa prima di inviare dati al server come segue:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    }
    "mergeId": results.eventMergeId
  });
});
```

Seguire lo stesso pattern se si desidera accedere al modulo `eventMergeID` per altri motivi (ad esempio, per inviarlo a un provider di terze parti):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Nota sul formato XDM

All&#39;interno del comando dell&#39;evento, l&#39;evento `mergeId` viene effettivamente aggiunto al `xdm` payload.  Se lo desiderate, `mergeId` possono essere inviati come parte dell&#39;opzione xdm, come segue:

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
    },
    "eventMergeId": "ABC123"
  }
});
```
