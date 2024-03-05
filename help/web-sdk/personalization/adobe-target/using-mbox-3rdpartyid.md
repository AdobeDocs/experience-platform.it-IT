---
title: Sincronizzazione dei profili in tempo reale per mbox3rdPartyId
description: Scopri come utilizzare mbox3rdPartyId con Adobe Experience Platform Web SDK.
keywords: personalizzazione;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 5%

---

# Cos’è `mbox3rdPartyId`

L’ID mbox3rdPartyId in Adobe Target è l’ID visitatore della tua azienda, ad esempio l’ID di iscrizione al programma fedeltà.

Quando un visitatore accede al sito di un’azienda, l’azienda in genere crea un ID associato all’account del visitatore, alla carta fedeltà, al numero di iscrizione o ad altri identificatori applicabili per l’azienda. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html#)


## Come usare `mbox3rdPartyId` con Web SDK

### Passaggio 1: configurare `Target Third Party ID Namespace`

Configurare `Target Third Party ID Namespace` nel tuo [Datastream](../../../datastreams/overview.md), utilizzando l’ID Namespace che desideri utilizzare come ID di terze parti mbox.
[Ulteriori informazioni sugli spazi dei nomi ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it)

![Interfaccia utente di Platform che mostra il campo spazio dei nomi dell’ID di terze parti di Target.](assets/mbox3rdpartyid.png)

### Passaggio 2: inviare `mbox3rdpartyId` a Target

Invia il `mbox3rdpartyId` a Target in `sendEvent` , utilizzando lo spazio dei nomi ID configurato nel passaggio 1.
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
