---
title: prehidingStyle
description: Crea una definizione CSS che consenta il caricamento di contenuto personalizzato senza sfarfallio.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

Il `prehidingStyle` consente di definire un selettore CSS per nascondere il contenuto personalizzato fino al suo caricamento. Questa proprietà è utile nelle implementazioni sincrone dell’SDK web per evitare sfarfallii. L’Adobe consiglia di utilizzare [frammento pre-hiding](../../personalization/manage-flicker.md) per le implementazioni asincrone di Web SDK.

I selettori CSS definiti in questa proprietà iniziano a nascondere il contenuto quando esegui il primo [`sendEvent`](../sendevent/overview.md) su una pagina. Il contenuto viene reso visibile quando viene ricevuta una risposta da un Adobe, che in genere include contenuti personalizzati. Il contenuto viene mostrato anche se `sendEvent` comando non riuscito o timeout.

Se includi entrambi `prehidingStyle` e il frammento pre-hiding nell&#39;implementazione, il frammento pre-hiding ha priorità rispetto a questa proprietà di configurazione.

## Prehiding dello stile tramite l’estensione tag Web SDK

Seleziona la **[!UICONTROL Fornisci stile pre-hiding]** quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Personalizzazione] , quindi selezionare il pulsante **[!UICONTROL Fornisci stile pre-hiding]**.
1. Questo pulsante apre una finestra modale con un editor CSS. Inserisci il selettore CSS e il blocco di dichiarazione desiderati, quindi fai clic su **[!UICONTROL Salva]** per chiudere la finestra modale.
1. Clic **[!UICONTROL Salva]** in impostazioni estensione, pubblica le modifiche.

## Prehiding dello stile tramite la libreria JavaScript di Web SDK

Imposta il `prehidingStyle` stringa durante l&#39;esecuzione di `configure` comando. Se ometti questa proprietà durante la configurazione dell’SDK per web, quando esegui il primo comando non viene nascosto nulla `sendEvent` su una pagina. Imposta questo valore sul selettore CSS e sul blocco di dichiarazione desiderati per le librerie caricate in modo sincrono.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
