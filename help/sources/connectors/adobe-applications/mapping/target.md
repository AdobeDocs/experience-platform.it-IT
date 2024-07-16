---
solution: Experience Platform
title: Mappatura dei dati evento di Adobe Target su XDM
description: Scopri come mappare i campi evento di Adobe Target a uno schema Experience Data Model (XDM) da utilizzare in Adobe Experience Platform.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 81412493b096264ce7a89e3ca2348edb2dcd1798
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Mappature dei campi di mappatura target

La tabella seguente illustra i campi di uno schema Experience Data Model (XDM) e i campi corrispondenti di Adobe Target a cui devono essere mappati. Vengono inoltre fornite note aggiuntive per alcune mappature.

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Campo ExperienceEvent XDM | Campo richiesta target | Note |
| ------------------------- | -------------------- | ----- |
| **`id`** | Un identificatore di richiesta univoco |
| **`dataSource`** | | Configurato su &quot;1&quot; per tutti i client. |
| `dataSource._id` | Valore generato dal sistema che non può essere passato con la richiesta. | ID univoco di questa origine dati. Questo verrebbe fornito dall’individuo o dal sistema che ha creato l’origine dati. |
| `dataSource.code` | Valore generato dal sistema che non può essere passato con la richiesta. | Collegamento all&#39;@id. completa È possibile utilizzare almeno uno dei codici o dei @id. A volte, questo codice viene indicato come codice di integrazione dell’origine dati. |
| `dataSource.tags` | Valore generato dal sistema che non può essere passato con la richiesta. | I tag vengono utilizzati per indicare come gli alias rappresentati da una determinata origine dati devono essere interpretati dalle applicazioni che utilizzano tali alias.<br><br>Esempi:<br><ul><li>`isAVID`: origini dati che rappresentano gli ID visitatore di Analytics.</li><li>`isCRSKey`: origini dati che rappresentano alias da utilizzare come chiavi in CRS.</li></ul>I tag vengono impostati al momento della creazione dell’origine dati, ma sono anche inclusi nei messaggi della pipeline quando si fa riferimento a una determinata origine dati. |
| **`timestamp`** | Timestamp evento |
| **`channel`** | `context.channel` | Funziona solo con la consegna in visualizzazione. Le opzioni sono &quot;web&quot; e &quot;mobile&quot;, con &quot;web&quot; come impostazione predefinita. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | L’ID Experience Cloud (ECID) è noto anche come MCID e continua a essere utilizzato nei namespace. |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | Il nome del gestore di telefonia mobile è stato risolto in base all’indirizzo IP della richiesta. |
| `environment.ipV4` | `mboxRequest.ipAddress` (se in formato V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (se in formato V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Mappatura interna di Target per gli ambienti definiti dal cliente (ad esempio sviluppo, controllo qualità o produzione). |
| `experience.target.supplementalDataID` | Identificatore utilizzato per unire eventi di Target con eventi di Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Elenco (array) di attività per le quali il visitatore si è qualificato |
| `experience.target.activities[i].activityID` | ID di qualsiasi attività per la quale il visitatore si è qualificato |
| `experience.target.activities[i].version` | Versione di qualsiasi attività per la quale il visitatore si è qualificato |
| `experience.target.activities[i].activityEvents` | Include i dettagli degli eventi di attività a cui l’utente ha avuto accesso con questo evento. |
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
| `placeContext.geo.city` | Il nome della città è stato risolto in base all’indirizzo IP della richiesta. |
| `placeContext.geo.countryCode` | Il codice paese è stato risolto in base all’indirizzo IP della richiesta. |
| `placeContext.geo.dmaId` | Il codice dell&#39;area di mercato designata è stato risolto in base all&#39;indirizzo IP della richiesta. |
| `placeContext.geo.postalCode` | Il codice postale è stato risolto in base all’indirizzo IP della richiesta. |
| `placeContext.geo.stateProvince` | Stato o provincia risolto in base all&#39;indirizzo IP della richiesta. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** | | Imposta solo se i dettagli dell’ordine sono presenti nella richiesta. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
