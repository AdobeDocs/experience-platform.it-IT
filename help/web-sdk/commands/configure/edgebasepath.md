---
title: edgeBasePath
description: Percorso di base dell’endpoint utilizzato per interagire con i servizi Adobe.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

La proprietà `edgeBasePath` modifica il percorso di destinazione quando si interagisce con i servizi Adobe. La maggior parte delle organizzazioni non deve impostare o modificare questa proprietà.

## Percorso di base di Edge tramite l’estensione tag Web SDK

Immetti il testo desiderato nel campo di testo **[!UICONTROL Percorso base Edge]** durante [la configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione [!UICONTROL Impostazioni avanzate], quindi immetti il valore desiderato nel campo di testo **[!UICONTROL Percorso base Edge]**.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Percorso di base di Edge tramite la libreria JavaScript dell’SDK per web

Impostare il campo di testo `edgeBasePath` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà, verrà utilizzato il valore predefinito `ee`. L’Adobe consiglia di omettere questa proprietà dalla maggior parte delle configurazioni.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
