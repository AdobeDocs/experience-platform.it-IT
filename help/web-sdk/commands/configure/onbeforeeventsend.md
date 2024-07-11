---
title: onBeforeEventSend
description: Scopri come configurare l’SDK per web per registrare una funzione di JavaScript in grado di modificare i dati inviati immediatamente prima che vengano inviati ad Adobe.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# `onBeforeEventSend`

Il `onBeforeEventSend` callback consente di registrare una funzione di JavaScript che può modificare i dati inviati immediatamente prima che tali dati vengano inviati ad Adobe. Questo callback consente di manipolare `xdm` o `data` , inclusa la possibilità di aggiungere, modificare o rimuovere elementi. Puoi anche annullare completamente l’invio di dati in modo condizionale, ad esempio con il traffico bot lato client rilevato.

>[!WARNING]
>
>Questo callback consente l’utilizzo di codice personalizzato. Se un codice incluso nel callback genera un&#39;eccezione non rilevata, l&#39;elaborazione per l&#39;evento si interrompe. I dati non vengono inviati ad Adobe.

## Configurare su prima del callback di invio dell’evento utilizzando l’estensione tag Web SDK {#tag-extension}

Seleziona la **[!UICONTROL Immetti prima del codice di callback di invio dell&#39;evento]** quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Questo pulsante apre una finestra modale in cui puoi inserire il codice desiderato.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Raccolta dati] , quindi selezionare il pulsante **[!UICONTROL Immetti prima del codice di callback di invio dell&#39;evento]**.
1. Questo pulsante apre una finestra modale con un editor di codice. Inserisci il codice desiderato, quindi fai clic su **[!UICONTROL Salva]** per chiudere la finestra modale.
1. Clic **[!UICONTROL Salva]** in impostazioni estensione, pubblica le modifiche.

Nell’editor di codice puoi accedere alle seguenti variabili:

* **`content.xdm`**: Il [XDM](../sendevent/xdm.md) payload dell’evento.
* **`content.data`**: Il [dati](../sendevent/data.md) payload dell&#39;oggetto per l&#39;evento.
* **`return true`**: chiudi immediatamente il callback e invia i dati all&#39;Adobe con i valori correnti nella `content` oggetto.
* **`return false`**: chiudi immediatamente il callback e interrompi l’invio di dati all’Adobe.

Qualsiasi variabile definita al di fuori di `content` possono essere utilizzati, ma non sono inclusi nel payload inviato ad Adobe.

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

>[!TIP]
>Evita di tornare `false` al primo evento di una pagina. Ritorno `false` sul primo evento può avere un impatto negativo sulla personalizzazione.

## Configurare su prima del callback di invio dell’evento utilizzando la libreria JavaScript dell’SDK web {#library}

Registra il `onBeforeEventSend` callback durante l&#39;esecuzione di `configure` comando. È possibile modificare il `content` nome variabile a qualsiasi valore desiderato modificando la variabile di parametro all&#39;interno della funzione in linea.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
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
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```
