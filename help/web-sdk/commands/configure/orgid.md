---
title: orgId
description: La proprietà orgId è una stringa che indica all’Adobe a quale organizzazione vengono inviati i dati.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

Il `orgId` proprietà è una stringa che indica all’Adobe a quale organizzazione vengono inviati i dati. **Questa proprietà è obbligatoria per tutti i dati inviati tramite Web SDK.**

Per individuare `orgID`:

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. In qualsiasi punto del Adobe Experience Cloud, premere **`[Ctrl]`** + **`[I]`**. A [!UICONTROL Debugger dati utente] viene visualizzata la finestra.
1. Clic **[!UICONTROL Copia]** ![Copia](../../assets/copy.png) accanto al [!UICONTROL ID organizzazione corrente], oppure fai clic su **[!UICONTROL Organizzazioni assegnate]** per visualizzare altri ID organizzazione a cui puoi accedere.
1. Una volta individuate le informazioni desiderate, fare clic su **[!UICONTROL Chiudi]**.

Gli ID organizzazione sono sempre stringhe alfanumeriche di 24 caratteri e terminano sempre con `@AdobeOrg`.

## Configurare un `orgID` utilizzo dell’estensione tag Web SDK

Inserisci l’ID organizzazione nel **[!UICONTROL ID organizzazione IMS]** campo di testo quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Inserisci l’ID organizzazione desiderato nella [!UICONTROL ID organizzazione IMS] campo di testo nella parte superiore.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Configurare un `orgID` utilizzo della libreria JavaScript dell’SDK web

Imposta il `orgId` stringa durante l&#39;esecuzione di `configure` comando. Se ometti questa proprietà durante la configurazione dell’SDK per web, l’SDK per web genera un errore della console e i dati non vengono inviati a Adobe.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
