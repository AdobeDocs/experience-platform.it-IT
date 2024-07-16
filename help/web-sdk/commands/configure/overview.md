---
title: Configurare Adobe Experience Platform Web SDK
description: Utilizza il comando configure per impostare le impostazioni richieste quando utilizzi l’SDK per web.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 1c614ef525d55d7476d037c6838b35c3471e4501
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Configurare Adobe Experience Platform Web SDK

La configurazione per l&#39;SDK Web viene eseguita con il comando `configure`. La configurazione dell’SDK per web è un passaggio fondamentale e obbligatorio che deve verificarsi ogni volta che viene utilizzata la libreria o l’estensione tag.

## Configurare l’SDK web utilizzando l’estensione tag {#configure-tag-extension}

Segui i passaggi seguenti per configurare Web SDK tramite l’estensione tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Per informazioni dettagliate su tutte le opzioni di configurazione, vai alla [pagina di configurazione dell&#39;estensione tag Web SDK](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

Queste impostazioni di configurazione vengono impostate ogni volta che utilizzi l’estensione per inviare dati ad Adobe.

## Configurare l’SDK web utilizzando la libreria JavaScript {#configure-js}

Eseguire il comando `configure`. Questo comando è necessario prima di poter chiamare qualsiasi altro comando Web SDK, ad esempio [`sendEvent`](../sendevent/overview.md).

Le proprietà [`edgeConfigId`](edgeconfigid.md) e [`orgId`](orgid.md) sono obbligatorie. Tutte le altre proprietà sono facoltative, a seconda dei requisiti di implementazione dell’organizzazione.

Per informazioni dettagliate su ciascuno dei comandi supportati, vedere il sommario di questa guida utente.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
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
  onBeforeLinkClickSend: function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
