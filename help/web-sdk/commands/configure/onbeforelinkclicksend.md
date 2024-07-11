---
title: onBeforeLinkClickSend
description: Callback eseguito immediatamente prima dell'invio dei dati di tracciamento dei collegamenti.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Questo callback è obsoleto. Utilizzare [`filterClickDetails`](clickcollection.md) invece.

Il `onBeforeLinkClickSend` callback consente di registrare una funzione JavaScript che può modificare i dati di tracciamento dei collegamenti inviati immediatamente prima che tali dati vengano inviati ad Adobe. Questo callback consente di manipolare `xdm` o `data` , inclusa la possibilità di aggiungere, modificare o rimuovere elementi. Puoi anche annullare completamente l’invio di dati in modo condizionale, ad esempio con il traffico bot lato client rilevato. È supportato dall’SDK web 2.15.0 o versione successiva.

Questo callback viene eseguito solo quando [`clickCollectionEnabled`](clickcollectionenabled.md) è abilitato e [`filterClickDetails`](clickcollection.md) non contiene una funzione registrata. Se `clickCollectionEnabled` è disabilitato o se `filterClickDetails` contiene una funzione registrata, quindi il callback non viene eseguito. Se `onBeforeEventSend` e `onBeforeLinkClickSend` entrambi contengono funzioni registrate, `onBeforeLinkClickSend` viene eseguito per primo.

>[!WARNING]
>
>Questo callback consente l’utilizzo di codice personalizzato. Se un codice incluso nel callback genera un&#39;eccezione non rilevata, l&#39;elaborazione per l&#39;evento si interrompe. I dati non vengono inviati ad Adobe.

## Configurare prima del collegamento fai clic su Invia callback utilizzando l’estensione tag Web SDK {#tag-extension}

Seleziona la **[!UICONTROL Fornisci su prima del collegamento clic evento invia codice di callback]** quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Questo pulsante apre una finestra modale in cui puoi inserire il codice desiderato.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Raccolta dati] , quindi selezionare la casella di controllo **[!UICONTROL Abilita raccolta dati di clic]**.
1. Seleziona il pulsante etichettato **[!UICONTROL Fornisci su prima del collegamento clic evento invia codice di callback]**.
1. Questo pulsante apre una finestra modale con un editor di codice. Inserisci il codice desiderato, quindi fai clic su **[!UICONTROL Salva]** per chiudere la finestra modale.
1. Clic **[!UICONTROL Salva]** in impostazioni estensione, pubblica le modifiche.

Nell’editor di codice puoi accedere alle seguenti variabili:

* **`content.clickedElement`**: elemento DOM su cui è stato fatto clic.
* **`content.xdm`**: payload XDM per l’evento.
* **`content.data`**: payload dell’oggetto dati per l’evento.
* **`return true`**: chiude immediatamente il callback con i valori della variabile corrente. Il `onBeforeEventSend` callback eseguito se contiene una funzione registrata.
* **`return false`**: chiudi immediatamente il callback e interrompi l’invio di dati all’Adobe. Il `onBeforeEventSend` callback non eseguito.

Qualsiasi variabile definita al di fuori di `content` possono essere utilizzati, ma non sono inclusi nel payload inviato ad Adobe.

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

Simile a [`onBeforeEventSend`](onbeforeeventsend.md), è possibile `return true` per completare immediatamente la funzione, oppure `return false` per interrompere l’invio di dati ad Adobe. Se interrompi l’invio di dati in `onBeforeLinkClickSend` quando entrambi `onBeforeEventSend` e `onBeforeLinkClickSend` contengono funzioni registrate, `onBeforeEventSend` La funzione non viene eseguita.

## Configurare su prima del collegamento fare clic su Invia callback utilizzando la libreria JavaScript dell&#39;SDK Web {#library}

Registra il `onBeforeLinkClickSend` callback durante l&#39;esecuzione di `configure` comando. È possibile modificare il `content` nome variabile a qualsiasi valore desiderato modificando la variabile di parametro all&#39;interno della funzione in linea.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

È inoltre possibile registrare una propria funzione invece di una funzione in linea.

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
