---
title: idMigrationEnabled
description: Consente al Web SDK di leggere i cookie AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

La proprietà `idMigrationEnabled` consente all&#39;SDK Web di leggere i cookie AMCV impostati da implementazioni Adobe Experience Cloud precedenti. Se l’organizzazione aggiorna l’implementazione a Web SDK, questa impostazione consente una transizione più fluida al servizio Adobe Experience Cloud ID corrente. Questa impostazione è utile per evitare un netto aumento di visitatori univoci durante l’aggiornamento a Web SDK.

Se la tua organizzazione esegue una nuova implementazione di Web SDK, l’abilitazione di questa impostazione non ha alcun impatto sulla raccolta dei dati o sull’identificazione dei visitatori. Non ci sono svantaggi a lasciarla abilitata per tutte le implementazioni.

## Abilitare la migrazione degli ID tramite l’estensione tag Web SDK

Selezionare la casella di controllo **[!UICONTROL Migra ECID da VisitorAPI all&#39;SDK Web]** durante la [configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Individua la sezione [!UICONTROL Identity], quindi seleziona la casella di controllo **[!UICONTROL Migra ECID da VisitorAPI all&#39;SDK Web]**.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Abilitare la migrazione degli ID utilizzando la libreria JavaScript dell’SDK per web

Impostare il valore booleano `idMigrationEnabled` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione dell&#39;SDK Web, per impostazione predefinita verrà utilizzato `true`. Imposta questa proprietà se vuoi disabilitare la capacità di leggere i cookie AMCV impostati dall&#39;API visitatore. La maggior parte delle organizzazioni non deve impostare questa proprietà.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```
