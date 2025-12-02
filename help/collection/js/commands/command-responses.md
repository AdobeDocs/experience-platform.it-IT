---
title: Gestione delle risposte ai comandi
description: Gestisci le risposte dai comandi utilizzando le promesse di JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Gestione delle risposte ai comandi

Alcuni comandi di Web SDK possono restituire un oggetto contenente dati potenzialmente utili per l&#39;organizzazione. Puoi scegliere cosa fare con quei dati, se lo desideri. Le risposte ai comandi sono utili per proposte e destinazioni, in quanto richiedono dati di Edge Network per funzionare in modo efficace.

Le risposte ai comandi utilizzano [promesse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) di JavaScript, che fungono da proxy per un valore non noto al momento della creazione della promessa. Una volta che il valore è noto, la promessa viene &quot;risolta&quot; con il valore.

Utilizzare i metodi `then` e `catch` per determinare quando un comando ha esito positivo o negativo. È possibile omettere `then` o `catch` se le loro finalità non sono importanti per l&#39;implementazione.

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
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

Tutte le promesse restituite dai comandi utilizzano un oggetto `result`. Ad esempio, è possibile ottenere informazioni sulla libreria dall&#39;oggetto `result` utilizzando il comando [`getLibraryInfo`](getlibraryinfo.md):

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Il contenuto di questo oggetto `result` dipende dalla combinazione del comando utilizzato e del consenso dell&#39;utente. Se un utente non ha dato il proprio consenso per uno scopo particolare, l’oggetto di risposta contiene solo informazioni che possono essere fornite nel contesto di ciò a cui l’utente ha acconsentito.

## Comando le risposte tramite l&#39;estensione tag Web SDK

L&#39;estensione tag Web SDK equivalente alle risposte ai comandi è una regola che sottoscrive l&#39;evento [**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete). È quindi possibile includere azioni quali [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) o [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) in questa regola.
