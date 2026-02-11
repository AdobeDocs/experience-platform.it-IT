---
title: Configurare Adobe Experience Platform Web SDK
description: Utilizzare il comando configure per impostare le impostazioni richieste quando si utilizza il Web SDK.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Configurare Adobe Experience Platform Web SDK

La configurazione per il Web SDK viene eseguita con il comando **`configure`**. Questo comando è necessario per ogni caricamento di pagina prima di chiamare altri comandi Web SDK, ad esempio [`sendEvent`](../sendevent/overview.md).

**Le proprietà [`datastreamId`](datastreamid.md) e [`orgId`](orgid.md) sono obbligatorie.** Tutte le altre proprietà sono facoltative, a seconda dei requisiti di implementazione dell&#39;organizzazione. L&#39;esempio seguente mostra un oggetto di configurazione che utilizza la maggior parte delle proprietà disponibili:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    filterClickDetails: function(content) {
      content.linkUrl = "https://example.com/current.html";
    },
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints", "oneTimeAnalyticsReferrer"],
  debugEnabled: true,
  defaultConsent: "pending",
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  edgeBasePath: "ee",
  edgeConfigOverrides: { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  edgeDomain: "data.example.com",
  idMigrationEnabled: false,
  onBeforeEventSend: function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  conversation: {
    stickyConversationSession: false
  },
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
