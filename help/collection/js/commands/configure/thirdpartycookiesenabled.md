---
title: thirdPartyCookiesEnabled
description: Consenti l’utilizzo di cookie di terze parti per identificare i visitatori.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

La proprietà `thirdPartyCookiesEnabled` è un valore booleano che determina se Web SDK imposta i cookie in un contesto di terze parti. L’abilitazione di questa opzione è utile se desideri identificare i visitatori tra i sottodomini o i domini di cui è proprietaria la tua organizzazione. Tuttavia, molti browser moderni limitano l’impostazione e la scadenza dei cookie di terze parti. Se il browser di un visitatore non supporta i cookie di terze parti, questa proprietà non esegue alcuna operazione.

La proprietà `thirdPartyCookiesEnabled` controlla inoltre se è possibile richiedere un [`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk) nelle chiamate di [`getIdentity`](../getidentity.md).

Quando questa opzione è abilitata, il Web SDK utilizza Adobe Audience Manager per identificare un visitatore. Quando questa opzione è disabilitata, la chiamata ad Audience Manager è disabilitata. Per ulteriori informazioni, consulta [Informazioni sulle chiamate al dominio Demdex](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=it) nella guida utente di Audience Manager.

Impostare il valore booleano `thirdPartyCookiesEnabled` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione del Web SDK, per impostazione predefinita viene utilizzato `true`. Impostare questo valore su `false` se non si desidera che il Web SDK utilizzi Audience Manager per identificare i visitatori.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## Abilitare i cookie di terze parti tramite l’estensione tag Web SDK

Questa impostazione può essere configurata nell&#39;estensione tag Web SDK utilizzando [Impostazioni di configurazione identità](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies).
