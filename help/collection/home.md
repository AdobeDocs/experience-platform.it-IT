---
keywords: Experience Platform;home;argomenti popolari;raccolta dati;lancio;sdk web
solution: Experience Platform
title: Panoramica sulla raccolta dati
topic-legacy: overview
description: Scopri le varie tecnologie coinvolte nella raccolta di dati sulle esperienze dei clienti in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: bbaf272313d5a8afe33178598063164792f4d8c0
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 6%

---

# Panoramica sulla raccolta dati

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente da sorgenti lato client e di inviarli ad Adobe Experience Platform Edge Network in modo che possano essere arricchiti, trasformati e distribuiti in destinazioni Adobi o non Adobi in pochi secondi.

La raccolta dati è supportata per le seguenti origini lato client:

* Applicazioni basate sul web
* Applicazioni mobili native
* Applicazioni OTT (Over-the-top)

Le tecnologie di raccolta dati fornite da Experience Platform si concentrano sulla scoperta e l’accessibilità dei set di dati acquisiti. Queste tecnologie comprendono quanto segue:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Tag](../tags/home.md)
* [Inoltro eventi](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Debugger Adobe Experience Platform](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Data Model (XDM)](../xdm/home.md)
* [Servizio Adobe Experience Platform Identity](../identity-service/home.md)

<!-- (Outdated terminology)
![](./images/Collection.png)
-->

## Implementazioni più semplici e prestazioni lato client più veloci

Gli SDK Adobe Experience Platform per web e dispositivi mobili comprimono e comprimono tutte le librerie di prodotti Adobe in un unico kit di sviluppo per le piattaforme web o mobili. La compressione di queste librerie velocizza la raccolta dei dati e consolida le operazioni in un unico flusso da dispositivi lato client a Adobe Experience Platform Edge Network.

## Processo di ribaltamento per l&#39;implementazione della tecnologia Adobe {#edge}

Platform Edge Network è una rete di server distribuita a livello globale, rapida e affidabile in grado di ricevere ed elaborare dati su vasta scala. Utilizzando i tag, puoi configurare [datastreams](../edge/fundamentals/datastreams.md) per prodotti come Adobe Target, Adobe Audience Manager e Adobe Analytics, che consentono di attivare questi prodotti sul lato server senza modificare il codice lato client.

<!-- (Outdated terminology)
![](./images/deploy.png)
-->

>[!NOTE]
>
>Per un’introduzione di alto livello a Platform Edge Network, consulta quanto segue [presentazione interattiva dei prodotti](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Trasforma, arricchisci e invia dati in modo rapido e sicuro

[Inoltro di eventi in Adobe Experience Platform](../tags/ui/event-forwarding/overview.md) può accedere a qualsiasi flusso di dati Platform. Puoi trasformare, arricchire e inviare dati a qualsiasi destinazione non Adobe con latenza estremamente bassa senza aggiungere codice di terze parti al dispositivo client, garantendo una raccolta e una distribuzione dei dati più veloci e sicure.

<!-- (Outdated terminology)
![](./images/launch.png)
-->