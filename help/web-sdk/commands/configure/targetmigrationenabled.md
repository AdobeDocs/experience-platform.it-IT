---
title: targetMigrationEnabled
description: Consenti al Web SDK di leggere e scrivere i cookie di Adobe Target.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

La proprietà `targetMigrationEnabled` è booleana e consente all&#39;SDK Web di leggere e scrivere i cookie mbox e mboxEdgeCluster utilizzati dalle librerie Adobe Target 1.x e 2.x. Questa opzione consente di mantenere il profilo visitatore tra le pagine che utilizzano le implementazioni Adobe Target precedenti e le pagine che utilizzano l’SDK per web.

## Abilitare la migrazione di Target da at.js utilizzando l’estensione tag Web SDK

Seleziona la casella di controllo **[!UICONTROL Migra Target da at.js a Web SDK]** quando [configura l&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione [!UICONTROL Personalization], quindi seleziona la casella di controllo **[!UICONTROL Migra Target da at.js a Web SDK]**.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Abilitare la migrazione di Target da at.js utilizzando la libreria Web SDK JavaScript

Impostare il valore booleano `targetMigrationEnabled` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione dell&#39;SDK Web, per impostazione predefinita verrà utilizzato `false`. Imposta questo valore su `true` se alcune pagine utilizzano ancora le librerie Adobe Target 1.x o 2.x.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
