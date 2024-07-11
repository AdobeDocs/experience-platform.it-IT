---
title: clickCollectionEnabled
description: Scopri come configurare Web SDK per determinare se i dati dei clic di collegamento vengono raccolti automaticamente.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

Il `clickCollectionEnabled` La proprietà è un valore booleano che determina se Web SDK raccoglie automaticamente i dati dei collegamenti. Se non imposti questa variabile, il suo valore predefinito è `true` ciò significa che i dati di tracciamento dei collegamenti vengono raccolti automaticamente per impostazione predefinita. Impostazione di questa proprietà su `false` è utile nei casi in cui preferisci tenere traccia manualmente dei dati di collegamento.

Quando `clickCollectionEnabled` è abilitato, i seguenti elementi XDM vengono compilati automaticamente con i dati:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

I collegamenti interni, i collegamenti di download e i collegamenti di uscita vengono tracciati automaticamente per impostazione predefinita quando questo valore booleano è abilitato. Se desideri un maggiore controllo sul tracciamento automatico dei collegamenti, l’Adobe consiglia di utilizzare [`clickCollection`](clickcollection.md) oggetto.

## Logica di tracciamento automatico dei collegamenti

L’SDK per web tiene traccia di tutti i clic su `<a>` e `<area>` elementi HTML se non dispone di un `onClick` attributo. I clic vengono acquisiti con una [acquisire](https://www.w3.org/TR/uievents/#capture-phase) fare clic sul listener di eventi allegato al documento. Quando si fa clic su un collegamento valido, viene eseguita la logica seguente in ordine:

1. Se il collegamento corrisponde ai criteri basati sui valori in [`downloadLinkQualifier`](downloadlinkqualifier.md), o se il collegamento contiene un `download` Attributo HTML, `xdm.web.webInteraction.type` è impostato su `"download"` (se `clickCollection.downloadLinkEnabled` è attivato).
1. Se il dominio di destinazione del collegamento è diverso dal `window.location.hostname`, `xdm.web.webInteraction.type` è impostato su `"exit"` (se `clickCollection.exitLinkEnabled` è attivato).
1. Se il collegamento non è idoneo per nessuno dei due `"download"` o `"exit"`, `xdm.web.webInteraction.type` è impostato su `"other"`.

In tutti i casi, `xdm.web.webInteraction.name` è impostato sull’etichetta di testo del collegamento e `xdm.web.webInteraction.URL` è impostato sull’URL di destinazione del collegamento. Se desideri impostare anche il nome del collegamento sull’URL, puoi sovrascrivere questo campo XDM utilizzando `filterClickDetails` callback in `clickCollection` oggetto.

## Abilitare il tracciamento automatico dei collegamenti tramite l’estensione tag Web SDK {#tag-extension}

Seleziona la **[!UICONTROL Abilita raccolta dati di clic]** casella di controllo [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Raccolta dati] , quindi selezionare la casella di controllo **[!UICONTROL Abilita raccolta dati di clic]**.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Abilitare il tracciamento automatico dei collegamenti utilizzando la libreria JavaScript dell’SDK per web {#library}

Imposta il `clickCollectionEnabled` booleano quando si esegue `configure` comando. Se ometti questa proprietà durante la configurazione dell’SDK web, per impostazione predefinita `true`. Imposta questo valore su `false` se preferisci impostare `xdm.web.webInteraction.type` e `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
