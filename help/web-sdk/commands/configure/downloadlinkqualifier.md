---
title: downloadLinkQualifier
description: Consente di determinare in che modo il tracciamento automatico dei collegamenti qualifica i collegamenti di download.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Se abiliti il tracciamento automatico dei collegamenti utilizzando [`clickCollectionEnabled`](clickcollectionenabled.md), il `downloadLinkQualifier` Questa proprietà consente di determinare i criteri in base ai quali un URL deve essere considerato un collegamento di download.

Questa proprietà è una stringa regex. Se l’URL su cui è stato fatto clic corrisponde a questo regex, `xdm.web.webInteraction.type` è impostato su `"download"`. Anche i collegamenti sono immediatamente classificati come collegamenti di download se includono un `download` Attributo HTML. Se `clickCollectionEnabled` non è abilitato, questa proprietà non esegue alcuna operazione.

## Scaricare il qualificatore di collegamento utilizzando l’estensione tag Web SDK

Abilita **[!UICONTROL Abilita raccolta dati di clic]** , quindi immettere il testo desiderato in **[!UICONTROL Qualificatore collegamento di download]** quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Raccolta dati] , quindi selezionare la casella di controllo **[!UICONTROL Abilita raccolta dati di clic]**.
1. Una volta abilitata, la funzione **[!UICONTROL Qualificatore collegamento di download]** viene visualizzata la casella di testo. Immetti il valore desiderato. Sono inoltre disponibili pulsanti per testare il regex e ripristinare il valore predefinito.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Scaricare il qualificatore di collegamento utilizzando la libreria JavaScript dell’SDK per web

Imposta il `downloadLinkQualifier` stringa durante l&#39;esecuzione di `configure` comando. Se si omette questa proprietà, verrà utilizzato il valore predefinito seguente:

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
