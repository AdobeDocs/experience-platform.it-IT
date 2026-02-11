---
title: conversazione
description: Configurare le impostazioni di chat di Brand Concierge.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 4%

---

# `conversation`

>[!AVAILABILITY]
>
>Brand Concierge per Web SDK è attualmente in **beta**. La funzionalità e la documentazione sono soggette a modifiche.

L&#39;oggetto `conversation` contiene le opzioni di configurazione per le sessioni di chat di Brand Concierge. Questo oggetto è supportato in Web SDK versione 2.31.0 o successiva.

## Proprietà

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| **`stickyConversationSession`** | `boolean` | Determina se il Web SDK imposta un cookie di sessione per mantenere le sessioni di chat di Brand Concierge in tutti i caricamenti di pagina. Impostazione predefinita: `false`. Se omesso o impostato su `false`, Brand Concierge chat avvia una nuova sessione a ogni caricamento di pagina. |

## Esempio

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    stickyConversationSession: true
  }
});
```

## Configurare le impostazioni di conversazione utilizzando l&#39;estensione tag Web SDK

Queste impostazioni possono essere configurate nell&#39;estensione tag Web SDK utilizzando [Impostazioni Brand Concierge](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
