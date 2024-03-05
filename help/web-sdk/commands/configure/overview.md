---
title: Configurare Adobe Experience Platform Web SDK
description: Utilizza il comando configure per impostare le impostazioni richieste quando utilizzi l’SDK per web.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Configurare Adobe Experience Platform Web SDK

La configurazione per l’SDK per web viene eseguita con `configure` comando. La configurazione dell’SDK per web è un passaggio fondamentale e obbligatorio che deve verificarsi ogni volta che viene utilizzata la libreria o l’estensione tag.

## Impostazioni di configurazione tramite l’estensione tag Web SDK

Accedi a [pagina di configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.

Queste impostazioni di configurazione vengono impostate ogni volta che utilizzi l’estensione per inviare dati ad Adobe.

## Impostazioni di configurazione tramite la libreria JavaScript dell’SDK web

Esegui il `configure` comando. Questo comando è necessario prima di poter chiamare qualsiasi altro comando Web SDK, ad esempio [`sendEvent`](../sendevent/overview.md). Le proprietà [`edgeConfigId`](edgeconfigid.md) e [`orgId`](orgid.md) sono obbligatori. Tutte le altre proprietà sono facoltative, a seconda dei requisiti di implementazione dell’organizzazione.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false,
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  "debugEnabled": true,
  "defaultConsent": "pending",
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  "edgeBasePath": "ee",
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "edgeDomain": "data.example.com",
  "idMigrationEnabled": false,
  "onBeforeEventSend": function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  "onBeforeLinkClickSend": function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  "prehidingStyle": "#container { opacity: 0 !important }",
  "targetMigrationEnabled": true,
  "thirdPartyCookiesEnabled": false
});
```
