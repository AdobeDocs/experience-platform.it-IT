---
title: Unione dei dati evento
seo-title: Unione dei dati evento Web SDK di Adobe Experience Platform
description: Scopri come unire i dati dell’evento SDK Web della piattaforma Experience
seo-description: Scopri come unire i dati dell’evento SDK Web della piattaforma Experience
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Unione dei dati evento

>[!IMPORTANT]
>
>Questa funzione è ancora in fase di sviluppo e pertanto non tutte le soluzioni saranno in grado di unire questi dati.

A volte, non tutti i dati sono disponibili quando si verifica un evento. Potrebbe essere utile acquisire i dati _disponibili_ , in modo che non vadano perduti se, ad esempio, l&#39;utente chiude il browser. D&#39;altro canto, è possibile includere anche qualsiasi dato che diventerà disponibile in un secondo momento.

In questi casi, è possibile unire i dati con gli eventi precedenti passando `eventMergeId` come opzione ai `event` comandi come segue:

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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("event", {
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

Trasmettendo lo stesso valore ID unione evento a entrambi i comandi evento in questo esempio, i dati nel secondo comando evento vengono incrementati ai dati precedentemente inviati sul primo comando evento. Un record per ciascun comando di evento viene creato nella piattaforma dati esperienza, ma durante il reporting i record vengono uniti utilizzando l&#39;ID unione evento e visualizzati come un singolo evento.

Se inviate dati su un particolare evento a fornitori terzi, potete includere anche lo stesso ID unione evento con tali dati. Successivamente, se scegli di importare dati di terze parti in Adobe Experience Platform, l&#39;ID unione eventi verrà utilizzato per unire tutti i dati raccolti come risultato dell&#39;evento discreto che si è verificato sulla tua pagina Web.

## Generazione di un ID unione eventi

Il valore ID unione evento può essere una qualsiasi stringa scelta, ma ricordate che tutti gli eventi inviati utilizzando lo stesso ID sono segnalati come un singolo evento, quindi prestate attenzione a imporre l&#39;univocità quando gli eventi non devono essere uniti. Se desiderate che l’SDK generi un ID unione evento univoco per vostro conto (in base alla specifica [UUID v4 più diffusa), potete utilizzare il](https://www.ietf.org/rfc/rfc4122.txt)`createEventMergeId` comando per farlo.

Come per tutti i comandi, viene restituita una promessa perché è possibile eseguire il comando prima che l’SDK abbia terminato il caricamento. La promessa verrà risolta il prima possibile con un ID unione evento univoco. È possibile attendere la risoluzione della promessa prima di inviare dati al server come segue:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("event", {
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

Seguite lo stesso pattern se desiderate accedere all&#39;ID unione eventi per altri motivi (ad esempio, per inviarlo a un provider di terze parti):

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
alloy("event", {
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
