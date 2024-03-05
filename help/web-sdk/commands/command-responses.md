---
title: Gestione delle risposte ai comandi
description: Gestisci le risposte dai comandi utilizzando le promesse JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Gestione delle risposte ai comandi

Alcuni comandi dell’SDK web possono restituire un oggetto contenente dati potenzialmente utili per l’organizzazione. Puoi scegliere cosa fare con quei dati, se lo desideri. Le risposte ai comandi sono utili per proposte e destinazioni, in quanto richiedono dati di rete Edge per funzionare in modo efficace.

Le risposte ai comandi utilizzano JavaScript [promesse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), funge da proxy per un valore non noto al momento della creazione della promessa. Una volta che il valore è noto, la promessa viene &quot;risolta&quot; con il valore.

## Gestire le risposte ai comandi tramite l’estensione tag Web SDK

Creare una regola che si abbona al **[!UICONTROL Invio evento completato]** come parte di una regola.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Eventi], seleziona un evento esistente o crea un evento.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di evento] a **[!UICONTROL Invio evento completato]**.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

Puoi quindi includere le azioni **[!UICONTROL Applicare le proposte]** o **[!UICONTROL Applica risposta]** a questa regola.

1. Quando visualizzi la regola creata o modificata in precedenza, seleziona un’azione esistente o crea un’azione.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Applicare le proposte]** o **[!UICONTROL Applica risposta]**, a seconda del comportamento desiderato.
1. Imposta i campi desiderati dell’azione, quindi fai clic su **[!UICONTROL Mantieni modifiche]**.

## Gestire le risposte dei comandi tramite la libreria JavaScript dell’SDK per web

Utilizza il `then` e `catch` metodi per determinare quando un comando ha esito positivo o negativo. È possibile omettere `then` o `catch` se le loro finalità non sono importanti per l’implementazione.

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

Tutte le promesse restituite dai comandi utilizzano un `result` oggetto. Ad esempio, puoi ottenere informazioni sulla libreria di da `result` oggetto utilizzando [`getLibraryInfo`](getlibraryinfo.md) comando:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Il contenuto di questo `result` L&#39;oggetto dipende da una combinazione del comando utilizzato e del consenso dell&#39;utente. Se un utente non ha dato il proprio consenso per uno scopo particolare, l’oggetto di risposta contiene solo informazioni che possono essere fornite nel contesto di ciò a cui l’utente ha acconsentito.
