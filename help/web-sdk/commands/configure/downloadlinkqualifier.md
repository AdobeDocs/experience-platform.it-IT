---
title: downloadLinkQualifier
description: Consente di determinare in che modo il tracciamento automatico dei collegamenti qualifica i collegamenti di download.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Se si abilita il tracciamento automatico dei collegamenti utilizzando [`clickCollectionEnabled`](clickcollectionenabled.md), la proprietà `downloadLinkQualifier` consente di determinare i criteri in base ai quali un URL può essere considerato un collegamento di download.

Questa proprietà è una stringa regex. Se l&#39;URL su cui è stato fatto clic corrisponde a questo regex, `xdm.web.webInteraction.type` è impostato su `"download"`. Se includono un attributo HTML `download`, i collegamenti vengono immediatamente classificati come collegamento di download. Se `clickCollectionEnabled` non è abilitato, questa proprietà non esegue alcuna operazione.

## Scaricare il qualificatore di collegamento utilizzando l’estensione tag Web SDK

Abilita la casella di controllo **[!UICONTROL Abilita raccolta dati su clic]**, quindi immetti il testo desiderato in **[!UICONTROL Scarica qualificatore collegamento]** durante la [configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione [!UICONTROL Raccolta dati], quindi seleziona la casella di controllo **[!UICONTROL Abilita raccolta dati su clic]**.
1. Una volta abilitata, viene visualizzata la casella di testo **[!UICONTROL Qualificatore collegamento di download]**. Immetti il valore desiderato. Sono inoltre disponibili pulsanti per testare il regex e ripristinare il valore predefinito.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Scaricare il qualificatore di collegamento utilizzando la libreria JavaScript dell’SDK per web

Impostare la stringa `downloadLinkQualifier` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà, verrà utilizzato il valore predefinito seguente:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Se desideri utilizzare criteri diversi per qualificare i collegamenti di download, imposta questa proprietà sul valore regex desiderato.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
