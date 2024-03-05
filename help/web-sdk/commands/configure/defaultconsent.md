---
title: defaultConsent
description: Imposta il metodo predefinito di raccolta dei consensi.
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# `defaultConsent`

Il `defaultConsent` determina il modo in cui gestisci il consenso alla raccolta dei dati prima di chiamare [`setConsent`](../setconsent.md) comando. Questa proprietà è utile quando non desideri raccogliere accidentalmente dati da individui residenti in aree in cui è richiesto il consenso prima di raccogliere i dati.

Questa proprietà consente tre valori:

* **In entrata**: la raccolta dei dati procede come di consueto, fino a quando l’utente non rinuncia.
* **Uscita**: i dati vengono eliminati definitivamente fino al consenso dell’utente.
* **In sospeso**: i dati vengono memorizzati localmente fino a quando l’utente non acconsente utilizzando [`setConsent`](../setconsent.md) comando. I dati non persistono tra i caricamenti di pagina.

Se un visitatore non rientra nella giurisdizione del Regolamento generale sulla protezione dei dati (RGPD), il consenso predefinito può essere impostato su `in`. Per i visitatori all’interno della giurisdizione del RGPD il consenso predefinito potrebbe essere impostato su `pending`. La piattaforma di gestione del consenso (CMP) può rilevare l’area geografica del cliente e fornire il flag `gdprApplies` a IAB TCF 2.0. Questo flag può essere utilizzato per impostare il consenso predefinito.

## Impostare il consenso predefinito tramite l’estensione tag Web SDK

Seleziona il pulsante di opzione desiderato in **[!UICONTROL Consenso predefinito]** quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Privacy] , quindi selezionare la sezione desiderata **[!UICONTROL Consenso predefinito]**.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Impostare il consenso predefinito utilizzando la libreria JavaScript di Web SDK

Imposta il `defaultConsent` stringa al livello di consenso desiderato durante l’esecuzione del comando `configure` comando. Questa proprietà distingue tra maiuscole e minuscole e supporta solo i tre valori seguenti: `"in"`, `"out"`, e `"pending"`. Se tenti di utilizzare un altro valore, la libreria genera un errore.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
