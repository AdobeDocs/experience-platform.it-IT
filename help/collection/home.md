---
keywords: Experience Platform;home;argomenti popolari;raccolta dati;launch;web sdk
solution: Experience Platform
title: Panoramica sulla raccolta dati
description: Scopri le varie tecnologie coinvolte nella raccolta di dati sulle esperienze dei clienti in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 5%

---

# Panoramica sulla raccolta dati

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente da origini lato client e inviarli all’Edge Network di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli in pochi secondi a destinazioni Adobe o non Adobe.

La raccolta dei dati è supportata per le seguenti origini lato client:

* Applicazioni basate sul Web
* Applicazioni mobile native
* Applicazioni over-the-top (OTT)

La raccolta dei dati si concentra sulla reperibilità e sull’accessibilità dei set di dati acquisiti, tra cui:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Tag](../tags/home.md)
* [Stream di dati](../datastreams/overview.md)
* [Inoltro eventi](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../web-sdk/home.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)
* [API del server di rete Edge](../server-api/overview.md)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


Questa guida fornisce un’introduzione di alto livello alla raccolta dei dati e spiega come funziona l’invio di dati a prodotti Adobe Experience Cloud e applicazioni non Adobe tramite Experience Platform Edge Network.

## Tag, Web SDK e Mobile SDK

Experience Platform Web SDK e Experience Platform Mobile SDK comprimono tutte le librerie di prodotti Adobe in un unico kit di sviluppo, rispettivamente per le piattaforme web e mobili. Questi possono essere implementati utilizzando codice non elaborato o utilizzando [tag](../tags/home.md) tramite l&#39;interfaccia utente di Data Collection o Adobe Experience Platform.

La compressione di queste librerie velocizza la raccolta dei dati e consolida le operazioni in un unico flusso dai dispositivi lato client all’Edge Network di Experience Platform.

![Tag, Web SDK, SDK mobile](./images/home/tags-sdks.png)

## Experience Platform Edge Network e flussi di dati {#edge}

Experience Platform Edge Network è una rete di server distribuita a livello globale, veloce e affidabile, in grado di ricevere ed elaborare dati su vasta scala. Utilizzando i tag, puoi impostare [datastream](../datastreams/overview.md) per prodotti come Adobe Target, Adobe Audience Manager e Adobe Analytics, che ti consentono di attivare questi prodotti sul lato server senza modificare il codice lato client.

Inoltre, gli stream di dati sono integrati con diverse funzionalità di Experience Platform che garantiscono che tutti i dati sensibili che invii siano gestiti in modo appropriato rispetto a politiche organizzative e normative legali. Per ulteriori informazioni, consulta la sezione sulla gestione di [dati sensibili](../datastreams/overview.md#sensitive) nella documentazione dei flussi di dati.

![Flussi di dati e soluzioni Adobe](./images/home/adobe-solutions.png)

## Inoltro eventi

[L&#39;inoltro degli eventi](../tags/ui/event-forwarding/overview.md) può toccare qualsiasi flusso di dati di Experience Platform, consentendoti di trasformare, arricchire e inviare dati a qualsiasi destinazione non Adobe con latenza estremamente bassa e senza aggiungere codice di terze parti al dispositivo client.

![Inoltro eventi](./images/home/event-forwarding.png)

>[!NOTE]
>
>L’inoltro di eventi è una funzione a pagamento inclusa nelle offerte Adobe Real-Time Customer Data Platform Connections, Prime o Ultimate.

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello sul funzionamento della raccolta dei dati per automatizzare il processo di invio dei dati raccolti sull’esperienza del cliente ai prodotti Adobe e alle destinazioni di terze parti.

![Framework raccolta dati](./images/home/collection.png)

Per ulteriori informazioni sul flusso di lavoro generale coinvolto nell&#39;invio di dati evento tramite Edge Network, consulta la [panoramica end-to-end](./e2e.md).
