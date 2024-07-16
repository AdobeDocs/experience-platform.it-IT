---
title: orgId
description: La proprietà orgId è una stringa che indica all’Adobe a quale organizzazione vengono inviati i dati.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

La proprietà `orgId` è una stringa che indica all&#39;Adobe a quale organizzazione vengono inviati i dati. **Questa proprietà è obbligatoria per tutti i dati inviati tramite Web SDK.**

Per individuare `orgID`:

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. In qualsiasi punto del Adobe Experience Cloud, premere **`[Ctrl]`** + **`[I]`**. Viene visualizzata una finestra di [!UICONTROL User Data Debugger].
1. Fai clic su **[!UICONTROL Copia]** ![Copia](../../assets/copy.png) accanto all&#39;[!UICONTROL ID organizzazione corrente] oppure fai clic sulla scheda **[!UICONTROL Organizzazioni assegnate]** per visualizzare altri ID organizzazione a cui puoi accedere.
1. Dopo aver individuato le informazioni desiderate, fare clic su **[!UICONTROL Chiudi]**.

Gli ID organizzazione sono sempre stringhe alfanumeriche di 24 caratteri e terminano sempre in `@AdobeOrg`.

## Configurare `orgID` utilizzando l&#39;estensione tag Web SDK

Immetti l&#39;ID organizzazione nel campo di testo **[!UICONTROL ID organizzazione IMS]** quando [configuri l&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Inserisci l&#39;ID organizzazione desiderato nel campo di testo [!UICONTROL ID organizzazione IMS] in alto.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Configurare `orgID` utilizzando la libreria JavaScript dell&#39;SDK Web

Impostare la stringa `orgId` durante l&#39;esecuzione del comando `configure`. Se ometti questa proprietà durante la configurazione dell’SDK per web, l’SDK per web genera un errore della console e i dati non vengono inviati a Adobe.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
