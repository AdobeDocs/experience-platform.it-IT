---
title: Mappatura automatica delle variabili Adobe Analytics nell’SDK per web Adobe Experience Platform
description: Scopri quali variabili vengono mappate automaticamente in Adobe Analytics con Experience Platform Web SDK
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;variabili;analytics;mappa automatica;mappatura automatica;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: 7809e64abab80f72af979e685f268c0799e74eca
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 5%

---

# Variabili mappate automaticamente in [!DNL Analytics]

Di seguito è riportato un elenco di variabili che Adobe Experience Platform Edge Network mappa automaticamente in Adobe Analytics. Informazioni dettagliate sui parametri delle query di raccolta dati di Adobe Analytics sono disponibili nella [Guida all&#39;implementazione di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html).

| Percorso campo XDM | [!DNL Analytics Query String] / Intestazione HTTP | Descrizione |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | Mappatura dei dati contestuali di AppMeasurement `c.a.appid` . |
| application.launches.value | c.a.launches | Mappatura dei dati contestuali di AppMeasurement `c.a.launches` . |
| commerce.checkouts.id | eventi | `scCheckout` serializzazione degli eventi. Se questo campo viene escluso (ad esempio per eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.checkouts.value | eventi | Mapping del parametro di query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_CHECKOUT, utilizzando il delimitatore `,`. |
| commerce.order.currencyCode | cc | Mappatura del parametro di query AppMeasurement CURRENCY. |
| commerce.order.purchaseID | pi | Mappatura del parametro query AppMeasurement PURCHASEID. |
| commerce.productListAdds.id | eventi | `scAdd` serializzazione degli eventi. Se questo campo viene escluso (ad esempio per eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productListAdds.value | eventi | Parametro query AppMeasurement Mappatura EVENT_LIST_FULL con conversione COMMERCE_SC_ADD, utilizzando delimitatore `,`. |
| commerce.productListOpens.id | eventi | `scOpen` serializzazione degli eventi. Se questo campo viene escluso (ad esempio per eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productListOpens.value | eventi | Parametro query AppMeasurement Mappatura EVENT_LIST_FULL con conversione COMMERCE_SC_OPEN, utilizzando il delimitatore `,`. |
| commerce.productListRemovals.id | eventi | `scRemove` serializzazione degli eventi. Se questo campo viene escluso (ad esempio per eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productListRemovals.value | eventi | Parametro query AppMeasurement Mappatura EVENT_LIST_FULL con conversione COMMERCE_SC_REMOVE, utilizzando il delimitatore `,`. |
| commerce.productListViews.id | eventi | `scView` serializzazione degli eventi. Se questo campo viene escluso (ad esempio per eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productListViews.value | eventi | Parametro query AppMeasurement Mappatura EVENT_LIST_FULL con conversione COMMERCE_SC_VIEW, utilizzando il delimitatore `,`. |
| commerce.productViews.id | eventi | `prodView` serializzazione degli eventi. Se questo campo viene escluso (ad esempio per eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productViews.value | eventi | Mapping del parametro di query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_PROD_VIEW, utilizzando il delimitatore `,`. |
| commerce.purchases.value | eventi | Parametro query AppMeasurement Mappatura EVENT_LIST_FULL con conversione COMMERCE_PURCHASE, utilizzando il delimitatore `,`. |
| device.colorDepth | c | Mappatura del parametro di query AppMeasurement C_COLOR. |
| device.screenHeight | s | Mappatura del parametro di query AppMeasurement Screen Resolution. |
| device.screenWidth | s | Mappatura del parametro di query AppMeasurement Screen Resolution. |
| environment.browserDetails.acceptLanguage | Accept-Language | Si tratta di una mappatura HTTP Header, HEADER_ACCEPT_LANGUAGE. |
| environment.browserDetails.cookiesEnabled | k | Mappatura del parametro di query AppMeasurement COOKIES con conversione BOOLEAN_TO_YN. |
| environment.browserDetails.javaEnabled | v | Mappatura del parametro di query AppMeasurement JAVA_ENABLED con conversione BOOLEAN_TO_YN. |
| environment.browserDetails.javaScriptVersion | j | Mappatura del parametro di query AppMeasurement J_JSCRIPT. |
| environment.browserDetails.userAgent | Utente-agente | Si tratta di una mappatura HTTP Header, HEADER_USER_AGENT. |
| environment.browserDetails.viewportHeight | bh | Mappatura del parametro di query AppMeasurement BROWSER_HEIGHT. |
| environment.browserDetails.viewportWidth | colpo | Mappatura del parametro di query AppMeasurement BROWSER_WIDTH. |
| environment.connectionType | ct | Mappatura del parametro di query AppMeasurement CT_CONNECT_TYPE. |
| environment.ipV4 | X-Forwarded-For | Si tratta di una mappatura HTTP Header, X-FORWARDED-FOR. |
| identityMap.ECID[0].id | mid | Mappatura del parametro MID della query AppMeasurement. |
| marketing.trackingCode | v0 | Mappatura del parametro di query AppMeasurement CAMPAIGN. |
| media.mediaTimed.completes.value | c.a.media.complete | Dati contestuali di AppMeasurement. |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | Dati contestuali di AppMeasurement. |
| media.mediaTimed.federated.value | c.a.media.federated | Mappatura dei dati contestuali di AppMeasurement `c.a.media.federated` . |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | Dati contestuali di AppMeasurement. |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | Mappatura dei dati contestuali di AppMeasurement `c.a.media.pauseTime` . |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | Mappatura dei dati contestuali di AppMeasurement `c.a.media.pauseCount` . |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | Mappatura dei dati contestuali di AppMeasurement `c.a.media.friendlyName` . |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | Mappatura dei dati contestuali di AppMeasurement `c.a.media.episode` . |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | Mappatura dei dati contestuali di AppMeasurement `c.a.media.season` . |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | Mappatura dei dati contestuali di AppMeasurement `a.media.name` . |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | Mappatura dei dati contestuali di AppMeasurement `c.a.media.show` . |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Mappatura dei dati contestuali AppMeasurement `c.a.media.type` con conversione VEDIO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Mappatura dei dati contestuali AppMeasurement `c.a.media.type` con conversione VIDEO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | Mappatura dei dati contestuali di AppMeasurement `c.a.media.length` . |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | Mappatura dei dati contestuali di AppMeasurement `c.a.media.channel` . |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | Mappatura dei dati contestuali di AppMeasurement `c.a.contentType` . |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | Mappatura dei dati contestuali di AppMeasurement `c.a.media.network` . |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | Mappatura dei dati contestuali di AppMeasurement `c.a.media.segment` . |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | Mappatura dei dati contestuali di AppMeasurement `c.a.media.playerName` . |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | Mappatura dei dati contestuali di AppMeasurement `c.a.media.sdkVersion` . |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | Mappatura dei dati contestuali di AppMeasurement `c.a.media.feed` . |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | Mappatura dei dati contestuali di AppMeasurement `c.a.media.format` . |
| media.mediaTimed.progress10.value | c.a.media.progress10 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.progress95.value | c.a.media.progress95 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.resumes.value | c.a.media.resume | Mappatura dei dati contestuali di AppMeasurement `c.a.media.resume` . |
| media.mediaTimed.starts.value | c.a.media.view | Dati contestuali di AppMeasurement. |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | Mappatura dei dati contestuali di AppMeasurement `c.a.media.timePlayed` . |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | Mappatura dei dati contestuali di AppMeasurement `c.a.media.totalTimePlayed` . |
| placeContext.geo.latitude | lat | Mappatura del parametro di query AppMeasurement LATITUDE. |
| placeContext.geo.longitude | lon | Mappatura del parametro di query AppMeasurement LONGITUDE. |
| placeContext.geo.postalCode | zip | Mappatura ZIP del parametro della query AppMeasurement. |
| placeContext.geo.stateProvince | Stato | Mappatura del parametro di query AppMeasurement STATE. |
| productListItems[N].lineItemId | products | Parametro query AppMeasurement Mappatura categoria prodotti. |
| productlistitems[N].name | products | Parametro query AppMeasurement Mappatura del nome dei prodotti. |
| productlistitems[N].priceTotal | products | Parametro della query AppMeasurement Prodotti Mappatura del prezzo. |
| productlistitems[N].Quantity | products | Parametro query AppMeasurement Mappatura della quantità dei prodotti. |
| web.webInteraction.URL | pev1 | Mappatura del parametro di query AppMeasurement PAGE_EVENT_VAR1. |
| web.webInteraction.name | pev2 | Mappatura del parametro di query AppMeasurement PAGE_EVENT_VAR2 . |
| web.webInteraction.type | pe | `web.webInteraction.type=other` a  `pe=lnk_o`;  `web.webInteraction.type=download` a  `pe=lnk_d`;  `web.webInteraction.type=exit` a  `pe=lnk_e` |
| web.webPageDetails.URL | g | Mappatura del parametro di query AppMeasurement PAGE_URL. |
| web.webPageDetails.errorPage | pageType | Mapping del parametro di query AppMeasurement PAGE_TYPE_FULL con la conversione ERROR_PAGE_TYPE. |
| web.webPageDetails.homePage | hp | Mappatura del parametro di query AppMeasurement HOMEPAGE con conversione BOOLEAN_TO_YN. |
| web.webPageDetails.name | firmare | Mappatura del parametro di query AppMeasurement PAGENAME. |
| web.webPageDetails.server | sv | Mappatura del parametro di query AppMeasurement USER_SERVER. |
| web.webPageDetails.siteSection | ch | Mappatura del parametro di query AppMeasurement CHANNEL. |
| web.webReferrer.URL | r | Mappatura REFERRER del parametro di query AppMeasurement. |

{style=&quot;table-layout:auto&quot;}
