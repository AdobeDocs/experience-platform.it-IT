---
title: downloadLinkQualifier
description: Consente di determinare in che modo il tracciamento automatico dei collegamenti qualifica i collegamenti di download.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

Se si abilita il tracciamento automatico dei collegamenti utilizzando [`clickCollectionEnabled`](clickcollectionenabled.md), la proprietà `downloadLinkQualifier` consente di determinare i criteri in base ai quali un URL può essere considerato un collegamento di download.

Questa proprietà è una stringa regex. Se l&#39;URL su cui è stato fatto clic corrisponde a questo regex, `xdm.web.webInteraction.type` è impostato su `"download"`. Se includono un attributo HTML `download`, i collegamenti vengono immediatamente classificati come collegamento di download. Se `clickCollectionEnabled` non è abilitato, questa proprietà non esegue alcuna operazione.

Impostare la stringa `downloadLinkQualifier` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà, verrà utilizzato il valore predefinito seguente:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Se desideri utilizzare criteri diversi per qualificare i collegamenti di download, imposta questa proprietà sul valore regex desiderato.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

## Scaricare il qualificatore di collegamento utilizzando l’estensione tag Web SDK

L&#39;equivalente dell&#39;estensione tag Web SDK di questo campo si trova in [Impostazioni di configurazione della raccolta dati](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier) durante la configurazione dell&#39;estensione tag.
