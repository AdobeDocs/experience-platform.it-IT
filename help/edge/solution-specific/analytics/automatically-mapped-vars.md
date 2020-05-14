---
title: Variabili mappate automaticamente in Analytics
seo-title: Variabili mappate automaticamente in Analytics con Adobe Experience Platform Web SDK
description: Scopri quali variabili vengono mappate automaticamente in Analytics con l’SDK Web della piattaforma Experience
seo-description: Scopri quali variabili vengono mappate automaticamente in Analytics con l’SDK Web della piattaforma Experience
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Variabili mappate automaticamente in Analytics

Di seguito è riportato un elenco di variabili che Adobe Experience Platform Edge Network mappa automaticamente in Analytics.

| Percorso campo XDM | Stringa query di Analytics / Intestazione HTTP | Descrizione |
| ---------- | ------------------------- | -------- |
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
| `application.id` | `c.a.appid` | Mappatura dei dati contestuali AppMeasurement. `c.a.appid` |
| `application.launches.value` | `c.a.launches` | Mappatura dei dati contestuali AppMeasurement. `c.a.launches` |
| `marketing.trackingCode` | `v0` | Mappatura del parametro di query AppMeasurement CAMPAIGN. |
| `commerce.purchaseID` | `pi` | Mappatura del parametro query AppMeasurement PURCHASEID. |
| `commerce.currencyCode` | `cc` | Mappatura del parametro della query AppMeasurement CURRENCY. |
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
| `identitymap.ecid.[0].id` | `mid` | MID del parametro query AppMeasurement. |
