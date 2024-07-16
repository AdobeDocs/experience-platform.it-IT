---
title: Gestione delle risposte ai comandi
description: Gestisci le risposte dai comandi utilizzando le promesse di JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Gestione delle risposte ai comandi

Alcuni comandi dell’SDK web possono restituire un oggetto contenente dati potenzialmente utili per l’organizzazione. Puoi scegliere cosa fare con quei dati, se lo desideri. Le risposte ai comandi sono utili per proposte e destinazioni, in quanto richiedono dati Edge Network per funzionare in modo efficace.

Le risposte ai comandi utilizzano [promesse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) di JavaScript, che fungono da proxy per un valore non noto al momento della creazione della promessa. Una volta che il valore è noto, la promessa viene &quot;risolta&quot; con il valore.

## Gestire le risposte ai comandi tramite l’estensione tag Web SDK

Crea una regola che sottoscrive l&#39;evento **[!UICONTROL Invia evento completato]** come parte di una regola.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Eventi], seleziona un evento esistente o creane uno.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo evento] su **[!UICONTROL Invia evento completato]**.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

Puoi quindi includere le azioni **[!UICONTROL Applica proposte]** o **[!UICONTROL Applica risposta]** a questa regola.

1. Quando visualizzi la regola creata o modificata in precedenza, seleziona un’azione esistente o crea un’azione.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Applica proposte]** o **[!UICONTROL Applica risposta]**, a seconda del comportamento desiderato.
1. Imposta i campi desiderati dell&#39;azione, quindi fai clic su **[!UICONTROL Mantieni modifiche]**.

## Gestire le risposte dei comandi tramite la libreria JavaScript dell’SDK per web

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
