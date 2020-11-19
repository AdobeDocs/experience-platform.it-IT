---
title: Unione dei dati evento
seo-title: Unione dei dati evento Adobe Experience Platform Web SDK
description: Scoprite come unire i dati dell'evento SDK Web  Experience Platform
seo-description: Scoprite come unire i dati dell'evento SDK Web  Experience Platform
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Unione dei dati evento

>[!IMPORTANT]
>
>Questa funzione è ancora in fase di sviluppo. Non tutte le soluzioni saranno in grado di unire i dati dell&#39;evento come descritto in questa pagina.

A volte, non tutti i dati sono disponibili quando si verifica un evento. Potrebbe essere utile acquisire i dati che si dispone, in modo che non vadano persi se, ad esempio, l&#39;utente chiude il browser. D&#39;altro canto, è possibile includere anche qualsiasi dato che diventerà disponibile in un secondo momento.

In questi casi, è possibile unire i dati con gli eventi precedenti passando `mergeId` come opzione ai `event` comandi come segue:

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
  },
  "mergeId": "ABC123"
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
  },
  "mergeId": "ABC123"
});
```

Trasmettendo lo stesso valore per l&#39; `mergeId` opzione a entrambi i comandi dell&#39;evento in questo esempio, i dati nel secondo comando dell&#39;evento vengono incrementati ai dati precedentemente inviati sul primo comando dell&#39;evento. Un record per ciascun comando evento viene creato nel [!DNL Experience Data Platform], ma durante il reporting i record vengono uniti utilizzando l&#39;ID unione evento e visualizzati come un singolo evento.

Se inviate dati su un particolare evento a fornitori terzi, potete includere anche lo stesso ID unione evento con tali dati. Successivamente, se si sceglie di importare dati di terze parti in Adobe Experience Platform, l&#39;ID unione eventi verrà utilizzato per unire tutti i dati raccolti a seguito dell&#39;evento discreto che si è verificato sulla pagina Web.

## Generazione di un ID unione eventi

L&#39;ID unione eventi può essere una qualsiasi stringa scelta, ma ricordate che tutti gli eventi inviati utilizzando lo stesso ID sono segnalati come un singolo evento, quindi prestate attenzione a imporre l&#39;univocità quando gli eventi non devono essere uniti. Se desiderate che l’SDK generi un ID unione evento univoco per vostro conto (in base alla specifica [UUID v4 più diffusa), potete utilizzare il](https://www.ietf.org/rfc/rfc4122.txt)`createEventMergeId` comando per farlo.

Come per tutti i comandi, viene restituita una promessa perché è possibile eseguire il comando prima che l’SDK abbia terminato il caricamento. La promessa verrà risolta il prima possibile con un ID unione evento univoco. È possibile attendere la risoluzione della promessa prima di inviare dati al server come segue:

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
    },
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
    },
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

All&#39;interno del comando dell&#39;evento, l&#39;ID unione evento viene aggiunto al `xdm` payload nella posizione corretta per conto dell&#39;utente.  Se lo desiderate, l&#39;ID unione evento può essere inviato come parte dell&#39; `xdm` opzione, come segue:

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

Quando si aggiunge direttamente l&#39;ID unione eventi all&#39; `xdm` oggetto, si noti che il nome `eventMergeID` è utilizzato invece di `mergeId`.
