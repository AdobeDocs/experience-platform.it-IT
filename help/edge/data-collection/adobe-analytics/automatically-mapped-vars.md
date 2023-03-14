---
title: Mappatura automatica delle variabili di Adobe Analytics in Adobe Experience Platform Web SDK
description: Scopri quali variabili vengono mappate automaticamente in Adobe Analytics con Experience Platform Web SDK
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;variabili;analytics;mappa automatica;mappato automaticamente;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 6%

---

# Variabili mappate automaticamente in [!DNL Analytics]

Di seguito è riportato un elenco di variabili mappate automaticamente da Adobe Experience Platform Edge Network in Adobe Analytics. Informazioni dettagliate sui parametri delle query di raccolta dati di Adobe Analytics sono disponibili nella sezione [Guida all’implementazione di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html?lang=it).

>[!NOTE]
>Le informazioni presenti in questa pagina si applicano anche all’SDK di Adobe Mobile.

| Percorso campo XDM | [!DNL Analytics Query String] / Intestazione HTTP | Descrizione |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | Dati contestuali AppMeasurement `c.a.appid` mappatura. |
| application.launches.value | c.a.launches | Dati contestuali AppMeasurement `c.a.launches` mappatura. |
| commerce.checkouts.id | eventi | `scCheckout` serializzazione degli eventi. Se questo campo viene escluso (ad esempio, per gli eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.checkouts.value | eventi | Mappatura del parametro di query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_CHECKOUT, utilizzando il delimitatore `,`. |
| commerce.order.currencyCode | cc | Mappatura VALUTA parametro query AppMeasurement. |
| commerce.order.purchaseID | pi greco | Mappatura ID acquisto del parametro di query AppMeasurement. |
| commerce.productListAdds.id | eventi | `scAdd` serializzazione degli eventi. Se questo campo viene escluso (ad esempio, per gli eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productListAdds.value | eventi | Mappatura del parametro di query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_ADD, utilizzando il delimitatore `,`. |
| commerce.productListOpens.id | eventi | `scOpen` serializzazione degli eventi. Se questo campo viene escluso (ad esempio, per gli eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productListOpens.value | eventi | Mappatura del parametro di query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_OPEN, utilizzando il delimitatore `,`. |
| commerce.productListRemovals.id | eventi | `scRemove` serializzazione degli eventi. Se questo campo viene escluso (ad esempio, per gli eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productListRemovals.value | eventi | Mappatura del parametro di query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_REMOVE, utilizzando il delimitatore `,`. |
| commerce.productListViews.id | eventi | `scView` serializzazione degli eventi. Se questo campo viene escluso (ad esempio, per gli eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productListViews.value | eventi | Mappatura del parametro di query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_SC_VIEW, utilizzando il delimitatore `,`. |
| commerce.productViews.id | eventi | `prodView` serializzazione degli eventi. Se questo campo viene escluso (ad esempio, per gli eventi non serializzati), il sistema genera e assegna il proprio valore ID all’entità. |
| commerce.productViews.value | eventi | Mappatura del parametro di query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_PROD_VIEW, utilizzando il delimitatore `,`. |
| commerce.purchases.value | eventi | Mappatura del parametro di query AppMeasurement EVENT_LIST_FULL con conversione COMMERCE_PURCHASE, utilizzando un delimitatore `,`. |
| device.colorDepth | c | Mappatura C_COLOR del parametro query AppMeasurement. |
| device.screenHeight | s | Mappatura risoluzione schermo del parametro della query AppMeasurement. |
| device.screenWidth | s | Mappatura risoluzione schermo del parametro della query AppMeasurement. |
| environment.browserDetails.acceptLanguage | Accept-Language | Questo è un mapping di intestazione HTTP, HEADER_ACCEPT_LANGUAGE. |
| environment.browserDetails.cookiesEnabled | k | Mappatura dei COOKIE dei parametri di query AppMeasurement con conversione BOOLEAN_TO_YN. |
| environment.browserDetails.javaEnabled | v | Mappatura JAVA_ENABLED del parametro di query AppMeasurement con conversione BOOLEAN_TO_YN. |
| environment.browserDetails.javaScriptVersion | j | Mappatura J_JSCRIPT del parametro di query AppMeasurement. |
| environment.browserDetails.userAgent | Utente-agente | Questo è un mapping di intestazione HTTP, HEADER_USER_AGENT. |
| environment.browserDetails.viewportHeight | bh | Mappatura BROWSER_HEIGHT del parametro query AppMeasurement. |
| environment.browserDetails.viewportWidth | bw | Mappatura BROWSER_WIDTH del parametro query AppMeasurement. |
| environment.connectionType | ct | Mappatura del parametro di query AppMeasurement CT_CONNECT_TYPE. |
| environment.ipV4 | X-Forwarded-For | Mappatura intestazione HTTP, X-FORWARDED-FOR. |
| identityMap.ECID[0].id | mid | Mappatura MID parametro query AppMeasurement. |
| marketing.trackingCode | v0 | Mappatura del parametro di query AppMeasurement per CAMPAIGN. |
| media.mediaTimed.completes.value | c.a.media.complete | Dati contestuali di AppMeasurement. |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | Dati contestuali di AppMeasurement. |
| media.mediaTimed.federated.value | c.a.media.federated | Dati contestuali AppMeasurement `c.a.media.federated` mappatura. |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | Dati contestuali di AppMeasurement. |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | Dati contestuali AppMeasurement `c.a.media.pauseTime` mappatura. |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | Dati contestuali AppMeasurement `c.a.media.pauseCount` mappatura. |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | Dati contestuali AppMeasurement `c.a.media.friendlyName` mappatura. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | Dati contestuali AppMeasurement `c.a.media.episode` mappatura. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | Dati contestuali AppMeasurement `c.a.media.season` mappatura. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | Dati contestuali AppMeasurement `a.media.name` mappatura. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | Dati contestuali AppMeasurement `c.a.media.show` mappatura. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Dati contestuali AppMeasurement `c.a.media.type` mappatura con conversione VEDIO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Dati contestuali AppMeasurement `c.a.media.type` mappatura con video_SHOW_TYPE di conversione. |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | Dati contestuali AppMeasurement `c.a.media.length` mappatura. |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | Dati contestuali di AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | Dati contestuali AppMeasurement `c.a.media.channel` mappatura. |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | Dati contestuali AppMeasurement `c.a.contentType` mappatura. |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | Dati contestuali AppMeasurement `c.a.media.network` mappatura. |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | Dati contestuali AppMeasurement `c.a.media.segment` mappatura. |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | Dati contestuali AppMeasurement `c.a.media.playerName` mappatura. |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | Dati contestuali AppMeasurement `c.a.media.sdkVersion` mappatura. |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | Dati contestuali AppMeasurement `c.a.media.feed` mappatura. |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | Dati contestuali AppMeasurement `c.a.media.format` mappatura. |
| media.mediaTimed.progress10.value | c.a.media.progress10 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.progress95.value | c.a.media.progress95 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.resumes.value | c.a.media.resume | Dati contestuali AppMeasurement `c.a.media.resume` mappatura. |
| media.mediaTimed.starts.value | c.a.media.view | Dati contestuali di AppMeasurement. |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | Dati contestuali di AppMeasurement. |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | Dati contestuali AppMeasurement `c.a.media.timePlayed` mappatura. |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | Dati contestuali AppMeasurement `c.a.media.totalTimePlayed` mappatura. |
| placeContext.geo.latitude | ultimo | Mappatura LATITUDE del parametro di query AppMeasurement. |
| placeContext.geo.longitude | lon | Mappatura LONGITUDINE del parametro della query AppMeasurement. |
| placeContext.geo.postalCode | zip | Mappatura ZIP del parametro di query AppMeasurement. |
| placeContext.geo.stateProvince | Stato | Mappatura STATE del parametro di query AppMeasurement. |
| productListItems[N].lineItemId | products | Mappatura della categoria Prodotti del parametro di query AppMeasurement. |
| productlistitems[N].name | products | Mappatura del nome dei prodotti per il parametro di query AppMeasurement. |
| productlistitems[N].priceTotal | products | Parametro query AppMeasurement: mappatura prezzo prodotti. |
| productlistitems[N].quantità | products | Mappatura della quantità di prodotti mediante query AppMeasurement. |
| web.webInteraction.URL | pev1 | Mappatura del parametro di query AppMeasurement PAGE_EVENT_VAR1. |
| web.webInteraction.name | pev2 | Mappatura del parametro di query AppMeasurement PAGE_EVENT_VAR2. |
| web.webInteraction.type | pe | `web.webInteraction.type=other` a `pe=lnk_o`; `web.webInteraction.type=download` a `pe=lnk_d`; `web.webInteraction.type=exit` a `pe=lnk_e` |
| web.webPageDetails.URL | g | Mappatura PAGE_URL del parametro della query AppMeasurement. |
| web.webPageDetails.errorPage | pageType | Mappatura PAGE_TYPE_FULL del parametro query AppMeasurement con conversione ERROR_PAGE_TYPE. |
| web.webPageDetails.homePage | hp | Mappatura del parametro di query AppMeasurement HOMEPAGE con conversione BOOLEAN_TO_YN. |
| web.webPageDetails.name | gn | Mappatura PAGENAME del parametro di query AppMeasurement. |
| web.webPageDetails.server | sv | Mappatura del parametro di query USER_SERVER di AppMeasurement. |
| web.webPageDetails.siteSection | ch | Mappatura CANALE del parametro di query AppMeasurement. |
| web.webReferrer.URL | r | Mappatura REFERRER del parametro di query AppMeasurement. |

{style="table-layout:auto"}
