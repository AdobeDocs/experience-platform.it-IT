---
title: Variabili mappate automaticamente in  Analytics
seo-title: Variabili mappate automaticamente in  Analytics con  Adobe Experience Platform Web SDK
description: Scopri quali variabili vengono mappate automaticamente in  Analytics con  Experience Platform Web SDK
seo-description: Scopri quali variabili vengono mappate automaticamente in  Analytics con  Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: a7c8830c5c8152b1f21373a506b2fff97d43c40a
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---


# Variabili mappate automaticamente in  Analytics

Di seguito è riportato un elenco di variabili che il  Adobe Experience Platform Edge Network mappa automaticamente in  Analytics.

| Percorso campo XDM |  Stringa query Analytics / Intestazione HTTP | Descrizione |
| ---------- | ------------------------- | -------- |
| `commerce.order.purchaseID` | `pi` | Mappatura del parametro query AppMeasurement PURCHASEID. |
| `commerce.order.currencyCode` | `cc` | Mappatura del parametro della query AppMeasurement CURRENCY. |
| `commerce.purchases.value` | `events` | Parametro query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_ACQUISTO, utilizzando un delimitatore `,`. |
| `commerce.productViews.value` | `events` | Mappatura EVENT_LIST_FULL del parametro di query AppMeasurement con conversione COMMERCE_PROD_VIEW, utilizzando il delimitatore `,`. |
| `commerce.productListOpens.value` | `events` | Parametro della query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_OPEN, utilizzando il delimitatore `,`. |
| `commerce.productListViews.value` | `events` | Parametro della query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_VIEW, utilizzando il delimitatore `,`. |
| `commerce.checkouts.value` | `events` | Parametro della query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_CHECKOUT, utilizzando il delimitatore `,`. |
| `commerce.productListAdds.value` | `events` | Parametro della query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_ADD, utilizzando il delimitatore `,`. |
| `commerce.productListRemovals.value` | `events` | Parametro query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_REMOVE, utilizzando il delimitatore `,`. |
| `commerce.productViews.id` | `events` | `prodView` Serializzazione degli eventi. |
| `commerce.productListOpens.id` | `events` | `scOpen` Serializzazione degli eventi. |
| `commerce.productListViews.id` | `events` | `scView` Serializzazione degli eventi. |
| `commerce.productListAdds.id` | `events` | `scAdd` Serializzazione degli eventi. |
| `commerce.productListRemovals.id` | `events` | `scRemove` Serializzazione degli eventi. |
| `commerce.checkouts.id` | `events` | `scCheckout` Serializzazione degli eventi. |
| `device.screenHeight` | `s` | Mappatura risoluzione schermo del parametro query AppMeasurement. |
| `device.screenWidth` | `s` | Mappatura risoluzione schermo del parametro query AppMeasurement. |
| `productlistitems.[N].lineitemid` | `products` | Mappatura categoria prodotti del parametro query AppMeasurement. |
| `productlistitems.[N].name` | `products` | Mappatura Nome prodotto del parametro query AppMeasurement. |
| `productlistitems.[N].quantity` | `products` | Parametro query AppMeasurement Mappatura quantità prodotti. |
| `productlistitems.[N].pricetotal` | `products` | Parametro query AppMeasurement Mappatura prezzo prodotti. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Dati contestuali AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Dati contestuali AppMeasurement. |
| `environment.browserDetails.userAgent` | `User-Agent` | Si tratta di una mappatura intestazione HTTP, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Si tratta di una mappatura intestazione HTTP, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | Mappatura del parametro di query AppMeasurement COOKIES con conversione BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | Mappatura del parametro di query AppMeasurement J_JSCRIPT. |
| `environment.browserDetails.javaEnabled` | `v` | Mappatura del parametro di query AppMeasurement JAVA_ENABLED con conversione BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | Mappatura del parametro query AppMeasurement BROWSER_HEIGHT. |
| `environment.browserDetails.viewportWidth` | `bw` | Mappatura del parametro query AppMeasurement BROWSER_WIDTH. |
| `environment.connectionType` | `ct` | Mappatura del parametro query AppMeasurement CT_CONNECT_TYPE. |
| `device.colorDepth` | `c` | Mappatura del parametro di query AppMeasurement C_COLOR. |
| `placeContext.geo.stateProvince` | `state` | Mappatura STATE del parametro della query AppMeasurement. |
| `placeContext.geo.postalCode` | `zip` | Mappatura ZIP del parametro query AppMeasurement. |
| `placeContext.geo.latitude` | `lat` | Mappatura del parametro LATITUDE della query AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Mappatura del parametro query AppMeasurement LONGITUDE. |
| `web.webPageDetails.server` | `sv` | Mappatura USER_SERVER del parametro query AppMeasurement. |
| `web.webPageDetails.name` | `gn` | Mappatura PAGENAME del parametro della query AppMeasurement. |
| `web.webPageDetails.URL` | `g` | Mappatura del parametro della query AppMeasurement PAGE_URL. |
| `web.webPageDetails.homePage` | `hp` | Mappatura HOMEPAGE del parametro di query AppMeasurement con conversione BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | Mappatura REFERRER del parametro della query AppMeasurement. |
| `web.webInteraction.type` | `pe` | Mappatura del parametro della query AppMeasurement PAGE_EVENT con conversione CLICK_MAP_TYPE. |
| `web.webInteraction.URL` | `pev1` | Mappatura del parametro query AppMeasurement PAGE_EVENT_VAR1. |
| `web.webInteraction.name` | `pev2` | Mappatura del parametro query AppMeasurement PAGE_EVENT_VAR2. |
| `web.webPageDetails.siteSection` | `ch` | Mappatura CANALE del parametro della query AppMeasurement. |
| `web.webPageDetails.errorPage` | `pageType` | Parametro della query AppMeasurement PAGE_TYPE_FULL con la conversione ERROR_PAGE_TYPE. |
| `application.id` | `c.a.appid` | Mappatura dei dati contestuali AppMeasurement. `c.a.appid` |
| `application.launches.value` | `c.a.launches` | Mappatura dei dati contestuali AppMeasurement. `c.a.launches` |
| `marketing.trackingCode` | `v0` | Mappatura del parametro di query AppMeasurement CAMPAIGN. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Mappatura dei dati contestuali AppMeasurement. `a.media.name` |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.length` |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Mappatura dei dati contestuali AppMeasurement. `c.a.contentType` |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.playerName` |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.channel` |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.segment` |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.friendlyName` |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.sdkVersion` |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.show` |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.format` |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.season` |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.episode` |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.network` |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Mappatura dei dati contestuali AppMeasurement con conversione VEDIO_SHOW_TYPE. `c.a.media.type` |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.feed` |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.timePlayed` |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.totalTimePlayed` |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.federated` |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.pauseCount` |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.pauseTime` |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Mappatura dei dati contestuali AppMeasurement. `c.a.media.resume` |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Mappatura dei dati contestuali AppMeasurement con conversione VIDEO_SHOW_TYPE. `c.a.media.type` |
| `identityMap.ECID.[0].id` | `mid` | MID del parametro query AppMeasurement. |
