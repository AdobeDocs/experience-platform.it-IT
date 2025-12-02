---
title: orgId
description: La proprietà orgId è una stringa che indica ad Adobe a quale organizzazione vengono inviati i dati.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# `orgId`

La proprietà `orgId` è una stringa che indica ad Adobe a quale organizzazione vengono inviati i dati. **Questa proprietà è obbligatoria per tutti i dati inviati tramite Web SDK.**

Per individuare `orgID`:

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. In qualsiasi punto del Adobe Experience Cloud, premere **`[Ctrl]`** + **`[I]`**. Viene visualizzata una finestra [!UICONTROL User Data Debugger].
1. Fai clic su **[!UICONTROL Copy]** ![Copia](../../assets/copy.png) accanto a [!UICONTROL Current Org ID] oppure fai clic sulla scheda **[!UICONTROL Assigned Orgs]** per visualizzare altri ID organizzazione a cui puoi accedere.
1. Dopo aver individuato le informazioni desiderate, fare clic su **[!UICONTROL Close]**.

Gli ID organizzazione sono sempre stringhe alfanumeriche di 24 caratteri e terminano sempre in `@AdobeOrg`.

Impostare la stringa `orgId` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione del Web SDK, il Web SDK genera un errore della console e i dati non vengono inviati ad Adobe.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## Impostare l’ID organizzazione utilizzando l’estensione tag Web SDK

Questa impostazione può essere configurata nell&#39;estensione tag Web SDK utilizzando [le impostazioni di configurazione dell&#39;istanza di SDK](/help/tags/extensions/client/web-sdk/configure/general.md). Il campo viene popolato automaticamente in base all’organizzazione in cui è stata creata la proprietà tag.
