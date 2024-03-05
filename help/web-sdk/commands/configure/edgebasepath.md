---
title: edgeBasePath
description: Percorso di base dell’endpoint utilizzato per interagire con i servizi Adobe.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

Il `edgeBasePath` modifica il percorso di destinazione quando si interagisce con i servizi Adobe. La maggior parte delle organizzazioni non deve impostare o modificare questa proprietà.

## Percorso di base Edge tramite l’estensione tag Web SDK

Inserisci il testo desiderato nella **[!UICONTROL Percorso base perimetrale]** campo di testo quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Impostazioni avanzate] , quindi immettere il valore desiderato nella sezione **[!UICONTROL Percorso base perimetrale]** campo di testo.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Percorso di base Edge tramite la libreria JavaScript di Web SDK

Imposta il `edgeBasePath` campo di testo durante l&#39;esecuzione di `configure` comando. Se si omette questa proprietà, verrà utilizzato il valore predefinito `ee`. L’Adobe consiglia di omettere questa proprietà dalla maggior parte delle configurazioni.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
