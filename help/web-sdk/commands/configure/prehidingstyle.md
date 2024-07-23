---
title: prehidingStyle
description: Crea una definizione CSS che consenta il caricamento di contenuto personalizzato senza sfarfallio.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

La proprietà `prehidingStyle` ti consente di definire un selettore CSS per nascondere il contenuto personalizzato fino al caricamento. Questa proprietà è utile nelle implementazioni sincrone dell’SDK web per evitare sfarfallii. L&#39;Adobe consiglia di utilizzare il [frammento di pre-hiding](../../personalization/manage-flicker.md) per le implementazioni asincrone di Web SDK.

I selettori CSS definiti in questa proprietà iniziano a nascondere il contenuto quando si esegue il primo comando [`sendEvent`](../sendevent/overview.md) su una pagina. Il contenuto viene reso visibile quando viene ricevuta una risposta da un Adobe, che in genere include contenuti personalizzati. Il contenuto è visibile anche se il comando `sendEvent` non riesce o si interrompe.

Se si includono sia `prehidingStyle` che il frammento pre-hiding nell&#39;implementazione, il frammento pre-hiding ha la priorità rispetto a questa proprietà di configurazione.

## Prehiding dello stile tramite l’estensione tag Web SDK

Selezionare il pulsante **[!UICONTROL Fornisci stile di pre-hiding]** durante [la configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione [!UICONTROL Personalization], quindi seleziona il pulsante **[!UICONTROL Fornisci stile di pre-hiding]**.
1. Questo pulsante apre una finestra modale con un editor CSS. Inserisci il selettore CSS e il blocco di dichiarazione desiderati, quindi fai clic su **[!UICONTROL Salva]** per chiudere la finestra modale.
1. Fai clic su **[!UICONTROL Salva]** in Impostazioni estensione, quindi pubblica le modifiche.

## Prehiding dello stile tramite la libreria JavaScript dell&#39;SDK Web

Impostare la stringa `prehidingStyle` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione dell&#39;SDK Web, non verrà nascosto nulla durante l&#39;esecuzione del primo comando `sendEvent` su una pagina. Imposta questo valore sul selettore CSS e sul blocco di dichiarazione desiderati per le librerie caricate in modo sincrono.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```
