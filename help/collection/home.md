---
keywords: Experience Platform;home;argomenti popolari;raccolta dati;lancio;sdk web
solution: Experience Platform
title: Panoramica sulla raccolta dati
topic-legacy: overview
description: Scopri le varie tecnologie coinvolte nella raccolta di dati sulle esperienze dei clienti in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 3%

---

# Panoramica sulla raccolta dati

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente da sorgenti lato client e di inviarli ad Adobe Experience Platform Edge Network in modo che possano essere arricchiti, trasformati e distribuiti in destinazioni Adobi o non Adobi in pochi secondi.

La raccolta dati è supportata per le seguenti origini lato client:

* Applicazioni basate sul web
* Applicazioni mobili native
* Applicazioni OTT (Over-the-top)

Le tecnologie di raccolta dati fornite da Experience Platform si concentrano sulla scoperta e l’accessibilità dei set di dati acquisiti. Queste tecnologie comprendono quanto segue:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Adobe Experience Platform Launch](https://adobe.com/go/launch_help_en)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Experience Data Model (XDM)](../xdm/home.md)

![](./images/Collection.png)

## Implementazioni più semplici e prestazioni lato client più veloci

Gli SDK Adobe Experience Platform per web e dispositivi mobili comprimono e comprimono tutte le librerie di prodotti Adobe in un unico kit di sviluppo per le piattaforme web o mobili. La compressione di queste librerie velocizza la raccolta dei dati e consolida le operazioni in un unico flusso da dispositivi lato client a Adobe Experience Platform Edge Network.

## Processo di ribaltamento per l&#39;implementazione della tecnologia Adobe

Platform Edge Network è una rete di server distribuita a livello globale, rapida e affidabile in grado di ricevere ed elaborare dati su vasta scala. Utilizzando il Platform launch, è possibile impostare [configurazioni edge](../edge/fundamentals/edge-configuration.md) per prodotti come Adobe Target, Adobe Audience Manager e Adobe Analytics, che consentono di attivare questi prodotti sul lato server senza modificare il codice lato client.

![](./images/deploy.png)

## Trasforma, arricchisci e invia dati in modo rapido e sicuro

[Adobe Experience Platform Launch Server ](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html) Sidecan può accedere a qualsiasi flusso di dati Platform. Puoi trasformare, arricchire e inviare dati a qualsiasi destinazione non Adobe con latenza estremamente bassa senza aggiungere codice di terze parti al dispositivo client, garantendo una raccolta e una distribuzione dei dati più veloci e sicure.

![](./images/launch.png)
