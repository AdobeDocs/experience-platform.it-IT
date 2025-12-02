---
title: Panoramica sull'installazione di Web SDK
description: Scopri come installare Experience Platform Web SDK.
keywords: installazione web sdk;installazione web sdk;internet explorer;promise;npm package
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a490c429047f5e5997d69f30a51e6b78debe2d5d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Panoramica sull&#39;installazione di Web SDK

Sono disponibili tre metodi supportati per utilizzare Adobe Experience Platform Web SDK:

1. **[Estensione tag Web SDK](/help/tags/extensions/client/web-sdk/overview.md)**: Adobe consiglia di utilizzare questo metodo. Installa un caricatore di tag sul sito, quindi utilizza l’interfaccia utente di Adobe Experience Platform Data Collection per configurare la tua implementazione.
1. **[Libreria JavaScript di Web SDK](library.md)**: fai riferimento a un file di libreria ospitato da CDN o ospita il file di libreria utilizzando la tua infrastruttura. Effettua chiamate alla libreria all&#39;interno del codice sul tuo sito.
1. **[NPM](npm.md)**: installare Web SDK nel sito utilizzando Gestione pacchetti NPM.

## Prerequisiti

Prima di utilizzare o installare il Web SDK, è necessario soddisfare i seguenti requisiti:

* L’architettura in Adobe Experience Platform deve prima essere configurata. Queste impostazioni includono tutti gli schemi, le identità e i flussi di dati necessari.
* Devi avere le autorizzazioni giuste configurate per accedere agli strumenti appropriati. Ad esempio, se la tua organizzazione decide di utilizzare l’estensione tag, devi disporre delle autorizzazioni corrette per accedere all’interfaccia utente di Data Collection. Per ulteriori informazioni, vedere [Autorizzazioni per la raccolta dati](../../permissions.md).
* È consigliabile disporre di un dominio di prima parte (CNAME). Se disponi già di un CNAME per Adobe Analytics, puoi utilizzarlo. Il test nello sviluppo funziona senza un CNAME, ma Adobe consiglia di averne uno prima di pubblicarlo in produzione. Per ulteriori informazioni, consulta [ID dispositivo di prime parti](../../use-cases/identity/first-party-device-ids.md).
