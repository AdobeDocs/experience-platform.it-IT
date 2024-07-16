---
title: edgeConfigId
description: Determina l’ID dello stream di dati a cui desideri inviare i dati.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

La proprietà `edgeConfigId` è una stringa che determina a quale [flusso di dati](../../../datastreams/overview.md) in Adobe Experience Platform desideri inviare i dati. Questa proprietà è obbligatoria per l’invio di dati ad Adobe.

Per individuare un ID dello stream di dati:

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Flussi dati]**.
1. Utilizza il campo di ricerca per individuare lo stream di dati desiderato, quindi seleziona **[!UICONTROL Copia]** ![Copia](../../assets/copy.png) accanto all&#39;ID dello stream di dati.

Puoi anche selezionare il nome dello stream di dati desiderato e nella colonna di destra verrà visualizzato l’ID dello stream di dati da copiare.

## Seleziona l’ID dello stream di dati utilizzando l’estensione tag Web SDK

Scegli da un elenco di flussi di dati disponibili oppure immetti un ID di flusso di dati direttamente quando [configuri l&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Individua la sezione [!UICONTROL Datastreams], quindi seleziona il metodo desiderato per determinare lo stream di dati.
   * Se scegli da un elenco, seleziona la sandbox e lo stream di dati da ciascun elenco a discesa.
   * Se inserisci dei valori, immetti l’ID dello stream di dati desiderato.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

Puoi inviare dati a diversi flussi di dati per ambienti di tag di produzione, staging e sviluppo.

## Seleziona l’ID dello stream di dati utilizzando la libreria JavaScript dell’SDK per web

Impostare la proprietà stringa `edgeConfigId` durante l&#39;esecuzione del comando `configure`. Questa proprietà è obbligatoria per tutte le implementazioni dell’SDK web. Se ometti questa proprietà, l’SDK web non sa a quale flusso di dati inviare i dati, causandone la perdita permanente.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Se si configurano più istanze dell&#39;SDK Web in una singola pagina, è necessario configurare un `edgeConfigId` diverso per ogni istanza.
