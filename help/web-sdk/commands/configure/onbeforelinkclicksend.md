---
title: onBeforeLinkClickSend
description: Callback eseguito immediatamente prima dell'invio dei dati di tracciamento dei collegamenti.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Questo callback è obsoleto. Utilizza invece [`filterClickDetails`](clickcollection.md).

Il callback `onBeforeLinkClickSend` consente di registrare una funzione di JavaScript che può modificare i dati di tracciamento dei collegamenti inviati immediatamente prima dell&#39;invio dei dati ad Adobe. Questo callback consente di manipolare l&#39;oggetto `xdm` o `data`, inclusa la possibilità di aggiungere, modificare o rimuovere elementi. Puoi anche annullare completamente l’invio di dati in modo condizionale, ad esempio con il traffico bot lato client rilevato. È supportato dall’SDK web 2.15.0 o versione successiva.

Questo callback viene eseguito solo quando [`clickCollectionEnabled`](clickcollectionenabled.md) è abilitato e [`filterClickDetails`](clickcollection.md) non contiene una funzione registrata. Se `clickCollectionEnabled` è disabilitato o se `filterClickDetails` contiene una funzione registrata, il callback non viene eseguito. Se `onBeforeEventSend` e `onBeforeLinkClickSend` contengono entrambi funzioni registrate, `onBeforeLinkClickSend` viene eseguito per primo.

>[!WARNING]
>
>Questo callback consente l’utilizzo di codice personalizzato. Se un codice incluso nel callback genera un&#39;eccezione non rilevata, l&#39;elaborazione per l&#39;evento si interrompe. I dati non vengono inviati ad Adobe.

## Configurare prima del collegamento fai clic su Invia callback utilizzando l’estensione tag Web SDK {#tag-extension}

Seleziona il pulsante **[!UICONTROL Fornisci prima del collegamento, invia codice di callback dell&#39;evento clic]** quando [configura l&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Questo pulsante apre una finestra modale in cui puoi inserire il codice desiderato.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione [!UICONTROL Raccolta dati], quindi seleziona la casella di controllo **[!UICONTROL Abilita raccolta dati su clic]**.
1. Selezionare il pulsante con l&#39;etichetta **[!UICONTROL Fornisci prima del collegamento codice di callback di invio evento clic]**.
1. Questo pulsante apre una finestra modale con un editor di codice. Inserisci il codice desiderato, quindi fai clic su **[!UICONTROL Salva]** per chiudere la finestra modale.
1. Fai clic su **[!UICONTROL Salva]** in Impostazioni estensione, quindi pubblica le modifiche.

Nell’editor di codice puoi accedere alle seguenti variabili:

* **`content.clickedElement`**: elemento DOM su cui è stato fatto clic.
* **`content.xdm`**: payload XDM per l&#39;evento.
* **`content.data`**: payload dell&#39;oggetto dati per l&#39;evento.
* **`return true`**: uscire immediatamente dal callback con i valori della variabile corrente. Il callback `onBeforeEventSend` viene eseguito se contiene una funzione registrata.
* **`return false`**: uscire immediatamente dal callback e interrompere l&#39;invio di dati all&#39;Adobe. Il callback `onBeforeEventSend` non è eseguito.

È possibile utilizzare qualsiasi variabile definita al di fuori di `content`, ma non è inclusa nel payload inviato a Adobe.

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

Analogamente a [`onBeforeEventSend`](onbeforeeventsend.md), è possibile `return true` per completare immediatamente la funzione o `return false` per interrompere l&#39;invio di dati all&#39;Adobe. Se si interrompe l&#39;invio di dati in `onBeforeLinkClickSend` quando sia `onBeforeEventSend` che `onBeforeLinkClickSend` contengono funzioni registrate, la funzione `onBeforeEventSend` non viene eseguita.

## Configurare su prima del collegamento fare clic su Invia callback utilizzando la libreria JavaScript dell&#39;SDK Web {#library}

Registra il callback `onBeforeLinkClickSend` durante l&#39;esecuzione del comando `configure`. È possibile modificare il nome della variabile `content` in qualsiasi valore desiderato modificando la variabile di parametro all&#39;interno della funzione in linea.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
