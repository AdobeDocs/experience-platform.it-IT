---
title: idMigrationEnabled
description: Consente al Web SDK di leggere i cookie AMCV.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

Il `idMigrationEnabled` consente al Web SDK di leggere i cookie AMCV impostati dalle implementazioni Adobe Experience Cloud precedenti. Se l’organizzazione aggiorna l’implementazione a Web SDK, questa impostazione consente una transizione più fluida al servizio Adobe Experience Cloud ID corrente. Questa impostazione è utile per evitare un netto aumento di visitatori univoci durante l’aggiornamento a Web SDK.

Se la tua organizzazione esegue una nuova implementazione di Web SDK, l’abilitazione di questa impostazione non ha alcun impatto sulla raccolta dei dati o sull’identificazione dei visitatori. Non ci sono svantaggi a lasciarla abilitata per tutte le implementazioni.

## Abilitare la migrazione degli ID tramite l’estensione tag Web SDK

Seleziona la **[!UICONTROL Migrare ECID da VisitorAPI all’SDK per web]** casella di controllo [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Individua il [!UICONTROL Identità] , quindi selezionare la casella di controllo **[!UICONTROL Migrare ECID da VisitorAPI all’SDK per web]**.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Abilitare la migrazione degli ID utilizzando la libreria JavaScript dell’SDK per web

Imposta il `idMigrationEnabled` booleano quando si esegue `configure` comando. Se ometti questa proprietà durante la configurazione dell’SDK web, per impostazione predefinita `true`. Imposta questa proprietà se vuoi disabilitare la capacità di leggere i cookie AMCV impostati dall&#39;API visitatore. La maggior parte delle organizzazioni non deve impostare questa proprietà.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
