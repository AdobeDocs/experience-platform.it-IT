---
title: edgeDomain
description: Determina il dominio principale a cui desideri inviare i dati.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

Il `edgeDomain` consente di modificare il dominio in cui l’SDK web invia i dati. Questa proprietà viene spesso utilizzata dalle organizzazioni che utilizzano [cookie di prima parte](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=it). I dati vengono inviati al dominio dell’organizzazione, quindi un record CNAME li inoltra ad Adobe.

La tua organizzazione determina il valore corretto per questa proprietà durante la configurazione [cookie di prima parte](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=it). A questo scopo, un’organizzazione utilizza in genere un sottodominio dedicato. Ad esempio, se utilizzi il dominio `example.com`, puoi impostare i cookie di prime parti su `data.example.com`.

## Configurare un dominio edge tramite l’estensione tag Web SDK

Imposta il **[!UICONTROL Dominio Edge]** campo di testo quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Individuare il campo di testo **[!UICONTROL Dominio Edge]**, quindi inserisci il valore desiderato.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Configurare un dominio edge utilizzando la libreria JavaScript dell’SDK Web

Imposta il `edgeDomain` stringa durante l&#39;esecuzione di `configure` comando. Se ometti questa proprietà durante la configurazione dell’SDK, per impostazione predefinita viene `edge.adobedc.net`. Imposta questo valore se desideri escludere il dominio a cui l’SDK Web invia i dati.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
