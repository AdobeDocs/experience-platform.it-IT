---
title: targetMigrationEnabled
description: Consenti al Web SDK di leggere e scrivere i cookie di Adobe Target.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

Il `targetMigrationEnabled` La proprietà è booleana e consente al Web SDK di leggere e scrivere i cookie mbox e mboxEdgeCluster utilizzati dalle librerie Adobe Target 1.x e 2.x. Questa opzione consente di mantenere il profilo visitatore tra le pagine che utilizzano le implementazioni Adobe Target precedenti e le pagine che utilizzano l’SDK per web.

## Abilitare la migrazione di Target da at.js utilizzando l’estensione tag Web SDK

Seleziona la **[!UICONTROL Migrare Target da at.js a Web SDK]** casella di controllo [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Personalizzazione] , quindi selezionare la casella di controllo **[!UICONTROL Migrare Target da at.js a Web SDK]**.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Abilitare la migrazione di Target da at.js utilizzando la libreria JavaScript dell’SDK web

Imposta il `targetMigrationEnabled` booleano quando si esegue `configure` comando. Se ometti questa proprietà durante la configurazione dell’SDK web, per impostazione predefinita `false`. Imposta questo valore su `true` se alcune pagine utilizzano ancora le librerie Adobe Target 1.x o 2.x.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
