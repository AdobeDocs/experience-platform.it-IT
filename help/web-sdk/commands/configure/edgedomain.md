---
title: edgeDomain
description: Determina il dominio principale a cui desideri inviare i dati.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

La proprietà `edgeDomain` consente di modificare il dominio in cui l&#39;SDK Web invia i dati. Questa proprietà viene spesso utilizzata dalle organizzazioni che utilizzano [cookie di prime parti](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=it). I dati vengono inviati al dominio dell’organizzazione, quindi un record CNAME li inoltra ad Adobe.

La tua organizzazione determina il valore corretto per questa proprietà durante la configurazione di [cookie di prime parti](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=it). A questo scopo, un’organizzazione utilizza in genere un sottodominio dedicato. Se ad esempio si utilizza il dominio `example.com`, è possibile impostare cookie di prime parti in `data.example.com`.

## Configurare un dominio edge tramite l’estensione tag Web SDK

Imposta il campo di testo **[!UICONTROL Dominio Edge]** durante la [configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Individua il campo di testo **[!UICONTROL dominio Edge]**, quindi immetti il valore desiderato.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Configurare un dominio Edge tramite la libreria JavaScript dell’SDK Web

Impostare la stringa `edgeDomain` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione dell&#39;SDK, per impostazione predefinita viene impostato su `edge.adobedc.net`. Imposta questo valore se desideri escludere il dominio a cui l’SDK Web invia i dati.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```
