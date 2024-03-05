---
title: thirdPartyCookiesEnabled
description: Consenti l’utilizzo di cookie di terze parti per identificare i visitatori.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

Il `thirdPartyCookiesEnabled` proprietà booleana che determina se Web SDK imposta i cookie in un contesto di terze parti. L’abilitazione di questa opzione è utile se desideri identificare i visitatori tra i sottodomini o i domini di cui è proprietaria la tua organizzazione. Tuttavia, molti browser moderni limitano l’impostazione e la scadenza dei cookie di terze parti.

Quando questa opzione è abilitata, l’SDK web utilizza Adobe Audience Manager per identificare un visitatore. Quando questa opzione è disabilitata, la chiamata all’Audience Manager è disabilitata. Consulta [Informazioni sulle chiamate al dominio Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=it) per ulteriori informazioni, consulta la guida utente di Audienci Manager.

## Abilitare i cookie di terze parti tramite l’estensione tag Web SDK

Seleziona la **[!UICONTROL Utilizzare i cookie di terze parti]** casella di controllo [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Identità] , quindi selezionare la casella di controllo **[!UICONTROL Utilizzare i cookie di terze parti]**.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Abilitare i cookie di terze parti utilizzando la libreria JavaScript dell’SDK per web

Imposta il `thirdPartyCookiesEnabled` booleano quando si esegue `configure` comando. Se ometti questa proprietà durante la configurazione dell’SDK web, per impostazione predefinita `true`. Imposta questo valore su `false` se non desideri che l’SDK per web utilizzi Audienci Manager per identificare i visitatori.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
