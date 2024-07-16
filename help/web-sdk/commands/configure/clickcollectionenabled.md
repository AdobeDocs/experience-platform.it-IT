---
title: clickCollectionEnabled
description: Scopri come configurare Web SDK per determinare se i dati dei clic di collegamento vengono raccolti automaticamente.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

La proprietà `clickCollectionEnabled` è un valore booleano che determina se Web SDK raccoglie automaticamente i dati di collegamento. Se non si imposta questa variabile, il suo valore predefinito è `true`, il che significa che i dati di tracciamento dei collegamenti vengono raccolti automaticamente per impostazione predefinita. L&#39;impostazione di questa proprietà su `false` è utile nei casi in cui si preferisce tenere traccia manualmente dei dati di collegamento.

Quando `clickCollectionEnabled` è abilitato, i seguenti elementi XDM vengono compilati automaticamente con i dati:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

I collegamenti interni, i collegamenti di download e i collegamenti di uscita vengono tracciati automaticamente per impostazione predefinita quando questo valore booleano è abilitato. Se desideri un maggiore controllo sul tracciamento automatico dei collegamenti, Adobe consiglia di utilizzare l&#39;oggetto [`clickCollection`](clickcollection.md).

## Logica di tracciamento automatico dei collegamenti

Web SDK tiene traccia di tutti i clic sugli elementi HTML `<a>` e `<area>` se non dispone di un attributo `onClick`. I clic vengono acquisiti con un listener di eventi di clic [capture](https://www.w3.org/TR/uievents/#capture-phase) allegato al documento. Quando si fa clic su un collegamento valido, viene eseguita la logica seguente in ordine:

1. Se il collegamento corrisponde ai criteri basati sui valori in [`downloadLinkQualifier`](downloadlinkqualifier.md) o se contiene un attributo HTML `download`, `xdm.web.webInteraction.type` è impostato su `"download"` (se `clickCollection.downloadLinkEnabled` è abilitato).
1. Se il dominio di destinazione del collegamento è diverso dal `window.location.hostname` corrente, `xdm.web.webInteraction.type` è impostato su `"exit"` (se `clickCollection.exitLinkEnabled` è abilitato).
1. Se il collegamento non è idoneo per `"download"` o `"exit"`, `xdm.web.webInteraction.type` è impostato su `"other"`.

In tutti i casi, `xdm.web.webInteraction.name` è impostato sull&#39;etichetta di testo del collegamento e `xdm.web.webInteraction.URL` è impostato sull&#39;URL di destinazione del collegamento. Se desideri impostare anche il nome del collegamento sull&#39;URL, puoi sovrascrivere questo campo XDM utilizzando il callback `filterClickDetails` nell&#39;oggetto `clickCollection`.

## Abilitare il tracciamento automatico dei collegamenti tramite l’estensione tag Web SDK {#tag-extension}

Selezionare la casella di controllo **[!UICONTROL Abilita raccolta dati su clic]** durante la [configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione [!UICONTROL Raccolta dati], quindi seleziona la casella di controllo **[!UICONTROL Abilita raccolta dati su clic]**.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Abilitare il tracciamento automatico dei collegamenti utilizzando la libreria JavaScript dell’SDK per web {#library}

Impostare il valore booleano `clickCollectionEnabled` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione dell&#39;SDK Web, per impostazione predefinita verrà utilizzato `true`. Impostare questo valore su `false` se si preferisce impostare `xdm.web.webInteraction.type` e `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
