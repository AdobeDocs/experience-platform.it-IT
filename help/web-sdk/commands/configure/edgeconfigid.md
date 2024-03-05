---
title: edgeConfigId
description: Determina l’ID dello stream di dati a cui desideri inviare i dati.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

Il `edgeConfigId` è una stringa che determina quale [flusso di dati](../../../datastreams/overview.md) in Adobe Experience Platform desideri inviare dati a. Questa proprietà è obbligatoria per l’invio di dati ad Adobe.

Per individuare un ID dello stream di dati:

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Flussi di dati]**.
1. Utilizza il campo di ricerca per individuare lo stream di dati desiderato, quindi seleziona **[!UICONTROL Copia]** ![Copia](../../assets/copy.png) accanto all’ID dello stream di dati.

Puoi anche selezionare il nome dello stream di dati desiderato e nella colonna di destra verrà visualizzato l’ID dello stream di dati da copiare.

## Seleziona l’ID dello stream di dati utilizzando l’estensione tag Web SDK

Scegli da un elenco di flussi di dati disponibili, oppure immetti un ID di flusso di dati direttamente quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Individua il [!UICONTROL Flussi di dati] , quindi seleziona il metodo desiderato per determinare lo stream di dati.
   * Se scegli da un elenco, seleziona la sandbox e lo stream di dati da ciascun elenco a discesa.
   * Se inserisci dei valori, immetti l’ID dello stream di dati desiderato.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

Puoi inviare dati a diversi flussi di dati per ambienti di tag di produzione, staging e sviluppo.

## Seleziona l’ID dello stream di dati utilizzando la libreria JavaScript dell’SDK per web

Imposta il `edgeConfigId` proprietà stringa durante l&#39;esecuzione di `configure` comando. Questa proprietà è obbligatoria per tutte le implementazioni dell’SDK web. Se ometti questa proprietà, l’SDK web non sa a quale flusso di dati inviare i dati, causandone la perdita permanente.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Se configuri più istanze dell’SDK web in una singola pagina, devi configurare un’altra `edgeConfigId` per ogni istanza.
