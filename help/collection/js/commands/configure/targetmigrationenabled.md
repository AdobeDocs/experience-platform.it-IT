---
title: targetMigrationEnabled
description: Consenti al Web SDK di leggere e scrivere i cookie di Adobe Target.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: dade74bf4a5cfd7b60eaf216583deb67b93a61db
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# `targetMigrationEnabled`

La proprietà `targetMigrationEnabled` è un valore booleano che consente al Web SDK di leggere e scrivere i cookie [`mbox` e `mboxEdgeCluster`](https://experienceleague.adobe.com/it/docs/core-services/interface/data-collection/cookies/web-sdk) utilizzati dalle librerie Adobe Target 1.x e 2.x. Questa opzione consente di mantenere il profilo visitatore tra le pagine che utilizzano precedenti implementazioni di Adobe Target e tra le pagine che utilizzano il Web SDK.

Impostare il valore booleano `targetMigrationEnabled` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione del Web SDK, per impostazione predefinita viene utilizzato `false`. Imposta questo valore su `true` se alcune pagine utilizzano ancora le librerie Adobe Target 1.x o 2.x.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## Abilitare la migrazione di Target tramite l’estensione tag Web SDK

Questa impostazione può essere configurata nell&#39;estensione tag Web SDK utilizzando [Impostazioni di configurazione Personalization](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk).
