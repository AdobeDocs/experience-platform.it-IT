---
title: conversazione
description: Configurare le impostazioni di chat di Brand Concierge.
exl-id: 0f64c7f1-2c28-4c67-af05-dc9ee688fdc0
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# `conversation`

>[!AVAILABILITY]
>
>Brand Concierge per Web SDK è attualmente in **beta**. La funzionalità e la documentazione sono soggette a modifiche.

L&#39;oggetto `conversation` contiene le opzioni di configurazione per le sessioni di chat di Brand Concierge. Questo oggetto è supportato in Web SDK versione 2.31.0 o successiva.

## Proprietà

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| **`collectSources`** | `boolean` | Determina se Web SDK legge il parametro della stringa di query `adobe_brand_concierge_source` e lo include in `xdm.channel.referringSource`. Impostazione predefinita: `false`. |
| **`stickyConversationSession`** | `boolean` | Determina se il Web SDK imposta un cookie di sessione per mantenere le sessioni di chat di Brand Concierge in tutti i caricamenti di pagina. Impostazione predefinita: `false`. Se omesso o impostato su `false`, Brand Concierge chat avvia una nuova sessione a ogni caricamento di pagina. |

## Esempio

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    collectSources: true
    stickyConversationSession: true
  }
});
```

## Configurare le impostazioni di conversazione utilizzando l&#39;estensione tag Web SDK

Queste impostazioni possono essere configurate nell&#39;estensione tag Web SDK utilizzando [Impostazioni Brand Concierge](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
