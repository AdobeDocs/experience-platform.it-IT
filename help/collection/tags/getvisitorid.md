---
title: getVisitorId
description: Recupera l’istanza dell’estensione tag del servizio ID visitatore di Experience Cloud.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# `getVisitorId()`

Il metodo `_satellite.getVisitorId()` restituisce un&#39;istanza del servizio [Adobe Experience Cloud ID](https://experienceleague.adobe.com/it/docs/id-service/using/home) all&#39;interno della proprietà tag, **if** hai installato e pubblicato l&#39;estensione del servizio ID. Questo metodo è utile quando desideri un accesso diretto all’istanza dell’ID visitatore per l’utilizzo in blocchi di codice personalizzati, nella configurazione avanzata degli elementi dati o nella risoluzione dei problemi di identità del visitatore.

>[!IMPORTANT]
>
>Questo metodo si applica solo alle proprietà che includono l&#39;estensione tag del servizio Experience Cloud ID standalone. Non si applica alle funzionalità implicite del servizio ID disponibili nell’estensione tag Web SDK. Per ottenere un&#39;identità visitatore utilizzando le funzionalità del servizio ID implicito di Web SDK, vedere il comando [`getIdentity`](/help/collection/js/commands/getidentity.md).

Se si chiama questo metodo con l&#39;estensione del servizio ID installata e pubblicata, viene restituito un oggetto simile a quello ottenuto dopo la chiamata al metodo [`Visitor.getInstance()`](https://experienceleague.adobe.com/it/docs/id-service/using/id-service-api/methods/getinstance). Se si chiama questo metodo quando l&#39;estensione del servizio ID non è installata o pubblicata, il metodo restituisce `null`.

```ts
_satellite.getVisitorId(): Visitor | null
```

## Campi e metodi disponibili

Per informazioni sui campi e i metodi disponibili, consulta il servizio Experience Cloud ID [Metodi](https://experienceleague.adobe.com/it/docs/id-service/using/id-service-api/methods/get-set) nella documentazione del servizio ID visitatore di Experience Cloud.

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
