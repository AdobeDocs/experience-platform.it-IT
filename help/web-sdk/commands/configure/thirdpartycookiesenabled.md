---
title: thirdPartyCookiesEnabled
description: Consenti l’utilizzo di cookie di terze parti per identificare i visitatori.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

La proprietà `thirdPartyCookiesEnabled` è un valore booleano che determina se Web SDK imposta i cookie in un contesto di terze parti. L’abilitazione di questa opzione è utile se desideri identificare i visitatori tra i sottodomini o i domini di cui è proprietaria la tua organizzazione. Tuttavia, molti browser moderni limitano l’impostazione e la scadenza dei cookie di terze parti.

La proprietà `thirdPartyCookiesEnabled` controlla inoltre se è possibile richiedere un [`CORE ID`](../../identity/overview.md#tracking-coreid-web-sdk) nelle chiamate di [`getIdentity`](../getidentity.md).

Quando questa opzione è abilitata, l’SDK web utilizza Adobe Audience Manager per identificare un visitatore. Quando questa opzione è disabilitata, la chiamata all’Audience Manager è disabilitata. Per ulteriori informazioni, consulta [Informazioni sulle chiamate al dominio Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=it) nella guida utente di Audience Manager.

## Abilitare i cookie di terze parti tramite l’estensione tag Web SDK

Selezionare la casella di controllo **[!UICONTROL Utilizza cookie di terze parti]** durante la [configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione [!UICONTROL Identity], quindi seleziona la casella di controllo **[!UICONTROL Use third-party cookies]**.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Abilitare i cookie di terze parti tramite la libreria JavaScript dell’SDK per web

Impostare il valore booleano `thirdPartyCookiesEnabled` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione dell&#39;SDK Web, per impostazione predefinita verrà utilizzato `true`. Imposta questo valore su `false` se non desideri che l&#39;SDK Web utilizzi Audience Manager per identificare i visitatori.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```
