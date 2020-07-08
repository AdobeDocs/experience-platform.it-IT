---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Campo mappatura destinazione
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Campi di mappatura di destinazione

 Adobe Experience Platform consente di acquisire  dati di Adobe Target attraverso il connettore di origine Target. Quando si utilizza il connettore, tutti i dati provenienti dai campi Target devono essere mappati ai campi [Experience Data Model (XDM)](../../../../xdm/home.md) associati alla classe XDM ExperienceEvent.

La tabella seguente illustra i campi di uno schema Evento esperienza (campo *ExperienceEvent* XDM) e i campi Target a cui devono essere mappati (campo *Richiesta* Target). Sono inoltre disponibili note aggiuntive per alcune mappature.

>[!NOTE]
>
>Scorrere a sinistra/destra per visualizzare il contenuto completo della tabella.

| Campo ExperienceEvent XDM | Campo richiesta Target | Note |
| ------------------------- | -------------------- | ----- |
| **`id`** | Un unico identificatore di richiesta |
| **`dataSource`** |  | Configurato su &quot;1&quot; per tutti i client. |
| `dataSource._id` | Valore generato dal sistema che non può essere trasmesso con la richiesta. | L&#39;ID univoco di questa origine dati. Questo viene fornito dal singolo o dal sistema che ha creato l&#39;origine dati. |
| `dataSource.code` | Valore generato dal sistema che non può essere trasmesso con la richiesta. | Scelta rapida per l&#39;intero @id. È possibile utilizzare almeno uno del codice o @id. A volte, questo codice viene definito codice di integrazione dell&#39;origine dati. |
| `dataSource.tags` | Valore generato dal sistema che non può essere trasmesso con la richiesta. | I tag sono utilizzati per indicare come gli alias rappresentati da una data origine dati devono essere interpretati dalle applicazioni che utilizzano tali alias.<br><br>Esempi:<br><ul><li>`isAVID`: Origini dati che rappresentano  ID visitatore Analytics.</li><li>`isCRSKey`: Origini dati che rappresentano alias da utilizzare come chiavi in CRS.</li></ul>I tag vengono impostati al momento della creazione dell&#39;origine dati, ma vengono anche inclusi nei messaggi della pipeline quando si fa riferimento a una determinata origine dati. |
| **`timestamp`** | Timestamp evento |
| **`channel`** | `context.channel` | Funziona solo con la distribuzione della vista. Le opzioni sono &quot;web&quot; e &quot;mobile&quot;, con &quot;web&quot; come impostazione predefinita. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | È stato risolto il nome del vettore mobile in base all&#39;indirizzo IP della richiesta. |
| `environment.ipV4` | `mboxRequest.ipAddress` (se in formato V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (se in formato V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Mappatura interna Target per ambienti definiti dal cliente (ad esempio dev, qa o prod). |
| `experience.target.supplementalDataID` | Identificatore utilizzato per unire eventi Target con  eventi Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Elenco (array) di attività per le quali il visitatore si è qualificato |
| `experience.target.activities[i].activityID` | L&#39;ID di ogni attività per la quale il visitatore ha qualificato |
| `experience.target.activities[i].version` | La versione di una determinata attività per la quale il visitatore si è qualificato |
| `experience.target.activities[i].activityEvents` | Include i dettagli degli eventi di attività che l&#39;utente ha toccato con questo evento. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | Una delle seguenti proprietà di `deviceAtlas` (o NULL): <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (stringa vuota) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (stringa vuota) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | UUID casuale (obbligatorio) |
| `placeContext.geo.city` | Il nome della città è stato risolto in base all&#39;indirizzo IP della richiesta. |
| `placeContext.geo.countryCode` | È stato risolto il codice del paese in base all&#39;indirizzo IP della richiesta. |
| `placeContext.geo.dmaId` | È stato risolto il codice dell&#39;area di mercato designata in base all&#39;indirizzo IP della richiesta. |
| `placeContext.geo.postalCode` | È stato risolto il codice postale in base all&#39;indirizzo IP della richiesta. |
| `placeContext.geo.stateProvince` | Stato o provincia risolto in base all&#39;indirizzo IP della richiesta. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | Impostate solo se nella richiesta sono presenti i dettagli dell&#39;ordine. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |
