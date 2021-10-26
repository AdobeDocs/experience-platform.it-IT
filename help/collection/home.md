---
keywords: Experience Platform;home;argomenti popolari;raccolta dati;lancio;sdk web
solution: Experience Platform
title: Panoramica sulla raccolta dati
topic-legacy: overview
description: Scopri le varie tecnologie coinvolte nella raccolta di dati sulle esperienze dei clienti in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 0926f0a6dc005b1bf278e7a0fa0afe4296d8ad80
workflow-type: tm+mt
source-wordcount: '458'
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
* [Datastream](../edge/fundamentals/datastreams.md)
* [Inoltro eventi](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Debugger Adobe Experience Platform](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Data Model (XDM)](../xdm/home.md)
* [Servizio Adobe Experience Platform Identity](../identity-service/home.md)

Questa guida fornisce un’introduzione di alto livello al framework di raccolta dati e illustra come funziona per inviare dati a prodotti Adobe Experience Cloud e applicazioni non Adobe tramite Platform Edge Network.

## Tag, SDK per web e SDK per dispositivi mobili

L’SDK per web di Platform e l’SDK per dispositivi mobili di Platform comprimono e comprimono tutte le librerie di prodotti Adobe in un unico kit di sviluppo rispettivamente per le piattaforme web e mobili. Questi possono essere implementati utilizzando codice non elaborato o utilizzando [tag](../tags/home.md) tramite l’interfaccia utente di raccolta dati.

La compressione di queste librerie velocizza la raccolta dei dati e consolida le operazioni in un unico flusso da dispositivi lato client a Platform Edge Network.

![Tag, SDK web, SDK mobile](./images/home/tags-sdks.png)

## Rete e datastreams di Platform Edge {#edge}

Platform Edge Network è una rete di server distribuita a livello globale, rapida e affidabile in grado di ricevere ed elaborare dati su vasta scala. Utilizzando i tag, puoi configurare [datastreams](../edge/fundamentals/datastreams.md) per prodotti come Adobe Target, Adobe Audience Manager e Adobe Analytics, che consentono di attivare questi prodotti sul lato server senza modificare il codice lato client.

![Datastreams e soluzioni Adobe](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Per un’introduzione di alto livello a Platform Edge Network, consulta quanto segue [presentazione interattiva dei prodotti](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Inoltro eventi

[Inoltro eventi](../tags/ui/event-forwarding/overview.md) può accedere a qualsiasi archivio dati di Experience Platform, consentendoti di trasformare, arricchire e inviare dati a qualsiasi destinazione non Adobe con latenza estremamente bassa e senza aggiungere codice di terze parti al dispositivo client.

![Inoltro eventi](./images/home/event-forwarding.png)

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello del funzionamento delle tecnologie di raccolta dati di Platform per automatizzare il processo di invio dei dati sulla customer experience raccolti ai prodotti Adobe e alle destinazioni di terze parti.

![Framework di raccolta dati](./images/home/collection.png)

Per ulteriori informazioni sul flusso di lavoro generale coinvolto nell’invio dei dati dell’evento tramite la rete Edge, consulta [panoramica completa della raccolta dati](./e2e.md).
