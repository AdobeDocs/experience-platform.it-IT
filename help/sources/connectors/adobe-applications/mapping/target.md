---
keywords: Experience Platform;home;argomenti popolari;mappatura target;mappatura target
solution: Experience Platform
title: Mappatura dei dati degli eventi di Adobe Target su XDM
description: Scopri come mappare i campi evento Adobe Target su uno schema Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# Mappature dei campi di mappatura di destinazione

Adobe Experience Platform consente di acquisire i dati di Adobe Target tramite il connettore di origine di Target. Quando utilizzi il connettore, tutti i dati provenienti dai campi di Target devono essere mappati al [Experience Data Model (XDM)](../../../../xdm/home.md) campi associati alla classe ExperienceEvent XDM.

La tabella seguente illustra i campi di uno schema Evento esperienza (*Campo ExperienceEvent XDM*) e i corrispondenti campi di Target a cui devono essere mappati (*Campo Richiesta Target*). Vengono inoltre fornite note aggiuntive per alcune mappature.

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Campo ExperienceEvent XDM | Campo Richiesta Target | Note |
| ------------------------- | -------------------- | ----- |
| **`id`** | Identificatore univoco della richiesta |
| **`dataSource`** |  | Configurato su &quot;1&quot; per tutti i client. |
| `dataSource._id` | Valore generato dal sistema che non può essere trasmesso con la richiesta. | ID univoco dell&#39;origine dati. Questo viene fornito dall&#39;utente o dal sistema che ha creato l&#39;origine dati. |
| `dataSource.code` | Valore generato dal sistema che non può essere trasmesso con la richiesta. | Una scorciatoia per l&#39;intero @id. È possibile utilizzare almeno uno dei codici o @id. A volte, questo codice è indicato come codice di integrazione dell’origine dati. |
| `dataSource.tags` | Valore generato dal sistema che non può essere trasmesso con la richiesta. | I tag vengono utilizzati per indicare in che modo gli alias rappresentati da una data origine dati devono essere interpretati dalle applicazioni che utilizzano tali alias.<br><br>Esempi:<br><ul><li>`isAVID`: Origini dati che rappresentano gli ID visitatore di Analytics.</li><li>`isCRSKey`: Origini di dati che rappresentano gli alias da utilizzare come chiavi in CRS.</li></ul>I tag vengono impostati quando l’origine dati viene creata, ma vengono inclusi anche nei messaggi della pipeline quando si fa riferimento a una determinata origine dati. |
| **`timestamp`** | Timestamp evento |
| **`channel`** | `context.channel` | Funziona solo con la consegna della visualizzazione. Le opzioni sono &quot;web&quot; e &quot;mobile&quot;, con &quot;web&quot; come impostazione predefinita. |
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
| `experience.target.environmentID` | Mappatura interna di Target per ambienti definiti dal cliente (ad esempio dev, qa o prod). |
| `experience.target.supplementalDataID` | Identificatore utilizzato per unire gli eventi di Target con gli eventi di Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Elenco (array) delle attività per le quali il visitatore si è qualificato |
| `experience.target.activities[i].activityID` | L’ID di qualsiasi attività per la quale il visitatore si è qualificato |
| `experience.target.activities[i].version` | La versione di qualsiasi attività per la quale il visitatore si è qualificato |
| `experience.target.activities[i].activityEvents` | Include i dettagli degli eventi di attività che l’utente ha hit con questo evento. |
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
| `placeContext.geo.countryCode` | Codice paese risolto in base all&#39;indirizzo IP della richiesta. |
| `placeContext.geo.dmaId` | È stato risolto il codice dell’area di mercato designata in base all’indirizzo IP della richiesta. |
| `placeContext.geo.postalCode` | Il codice postale è stato risolto in base all’indirizzo IP della richiesta. |
| `placeContext.geo.stateProvince` | Stato o provincia risolto in base all&#39;indirizzo IP della richiesta. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | Imposta solo se nella richiesta sono presenti i dettagli dell’ordine. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style=&quot;table-layout:auto&quot;}
