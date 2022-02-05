---
title: Sincronizzazione dei profili in tempo reale per mbox3rdPartyId
description: Scopri come utilizzare mbox3rdPartyId con Adobe Experience Platform Web SDK.
keywords: personalizzazione;target;adobe target;renderdecisions;sendEvent;mbox3rdPartyId;
exl-id: null
source-git-commit: b02a7a95be33b28ab79afc7418bb3a644c417fc9
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 6%

---


# Che cosa è `mbox3rdPartyId`

L’ID mbox3rdPartyId in Adobe Target è l’ID visitatore della tua azienda, ad esempio l’ID di iscrizione al programma fedeltà.

Quando un visitatore accede al sito di un’azienda, in genere l’azienda crea un ID associato all’account del visitatore, alla carta fedeltà, al numero di iscrizione o ad altri identificatori applicabili per tale azienda. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## Come utilizzare `mbox3rdPartyId` con l’SDK per web

### Passaggio 1: Configura le `Target Third Party ID Namespace`

Configura le `Target Third Party ID Namespace` nel tuo [Datastream](../../fundamentals/datastreams.md), utilizzando lo spazio dei nomi ID che desideri utilizzare come ID di terze parti mbox.
[Ulteriori informazioni sui namespace ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![](assets/mbox3rdpartyid.png)

### Passaggio 2: Invia `mbox3rdpartyId` a Target

Invia `mbox3rdpartyId` a Target nel `sendEvent` utilizzando lo spazio dei nomi ID configurato nel passaggio 1.
[Ulteriori informazioni sull’invio degli ID](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```


