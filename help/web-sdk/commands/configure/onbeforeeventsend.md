---
title: onBeforeEventSend
description: Callback eseguito immediatamente prima dell'invio dei dati.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# `onBeforeEventSend`

Il `onBeforeEventSend` callback consente di registrare una funzione JavaScript che può modificare i dati inviati immediatamente prima che vengano inviati ad Adobe. Questo callback consente di manipolare `xdm` o `data` , inclusa la possibilità di aggiungere, modificare o rimuovere elementi. Puoi anche annullare completamente l’invio di dati in modo condizionale, ad esempio con il traffico bot lato client rilevato.

>[!WARNING]
>
>Questo callback consente l’utilizzo di codice personalizzato. Se un codice incluso nel callback genera un&#39;eccezione non rilevata, l&#39;elaborazione per l&#39;evento si interrompe. I dati non vengono inviati ad Adobe.

## Il prima del callback di invio dell’evento utilizzando l’estensione tag Web SDK

Seleziona la **[!UICONTROL Immetti prima del codice di callback di invio dell&#39;evento]** quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Questo pulsante apre una finestra modale in cui puoi inserire il codice desiderato.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Raccolta dati] , quindi selezionare il pulsante **[!UICONTROL Immetti prima del codice di callback di invio dell&#39;evento]**.
1. Questo pulsante apre una finestra modale con un editor di codice. Inserisci il codice desiderato, quindi fai clic su **[!UICONTROL Salva]** per chiudere la finestra modale.
1. Clic **[!UICONTROL Salva]** in impostazioni estensione, pubblica le modifiche.

Nell’editor di codice puoi aggiungere, modificare o rimuovere elementi all’interno di `content` oggetto. Questo oggetto contiene il payload inviato all’Adobe. Non è necessario definire `content` oggetto o racchiudere qualsiasi codice all&#39;interno di una funzione. Qualsiasi variabile definita al di fuori di `content` possono essere utilizzati, ma non sono inclusi nel payload inviato ad Adobe.

>[!TIP]
>
>Gli oggetti `content.xdm` e `content.data` sono sempre definiti in questo contesto, pertanto non è necessario verificarne l’esistenza. Alcune variabili all’interno di questi oggetti dipendono dall’implementazione e dal livello dati. L’Adobe consiglia di verificare la presenza di valori non definiti all’interno di questi oggetti per evitare errori JavaScript.

Ad esempio, se desideri:

* Aggiungere l’elemento XDM `xdm.commerce.order.purchaseID`
* Forza tutti i caratteri in `xdm.marketing.trackingCode` in minuscolo
* Elimina `xdm.environment.operatingSystemVersion`
* Se un tipo di evento è un clic di collegamento, invia immediatamente i dati indipendentemente dal codice sottostante
* Annulla l’invio dei dati all’Adobe se viene rilevato un bot

Il codice equivalente all’interno della finestra modale è il seguente:

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!NOTE]
>
>Evita di tornare `false` al primo evento di una pagina. Ritorno `false` sul primo evento può avere un impatto negativo sulla personalizzazione.

## Il prima del callback di invio dell’evento utilizzando la libreria JavaScript dell’SDK Web

Registra il `onBeforeEventSend` callback durante l&#39;esecuzione di `configure` comando. È possibile modificare il `content` nome variabile a qualsiasi valore desiderato modificando la variabile di parametro all&#39;interno della funzione in linea.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

È inoltre possibile registrare una propria funzione invece di una funzione in linea.

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": lastChanceLogic
});    
```
