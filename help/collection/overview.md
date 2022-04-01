---
title: API server di rete Edge
description: Scopri cos’è l’API di Adobe Experience Platform Edge Network Server e come utilizzarla.
seo-description: Learn what the Adobe Experience Platform Edge Network Server API is and how you can use it.
keywords: raccolta dati;raccolta;Adobe Experience Platform Edge Network;api server;
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Panoramica API server di rete Edge

Adobe Experience Platform Edge Network offre ai clienti un modo ottimizzato di interagire con qualsiasi servizio Adobe Experience Cloud o Adobe Experience Platform Edge.

La [!DNL Edge Network Server API] può essere utilizzato per una varietà di casi d’uso di raccolta dati, personalizzazione, pubblicità e marketing. La [!DNL Server API] può essere utilizzato su server, [!DNL IoT] dispositivi, set-top box e una varietà di altri dispositivi.

Dal momento che [!DNL Server API] non si basa su librerie da caricare, offre un modo rapido e rapido per interagire con Adobe Experience Platform Edge Network e le soluzioni supportate.

I vantaggi [!DNL Server API] l&#39;architettura include:

* Riduzione del tempo di caricamento delle pagine
* Latenza migliorata
* Raccolta di dati di prime parti
* Comunicazione semplificata lato server tra i servizi

La [!DNL Server API] supporta la raccolta di dati interattivi e batch tramite due endpoint dedicati:

1. L’endpoint interattivo supporta la comunicazione con i servizi Adobe Experience Platform e Adobe Experience Cloud che supportano la segmentazione avanzata, la personalizzazione e altri casi d’uso del marketing.
2. L’endpoint batch consentirà l’invio in batch di richieste quando i dati devono essere caricati senza ricevere una risposta dalle applicazioni richiamate.

La [!DNL Server API] supporta il seguente tipo di richieste: La [!DNL Server API] supporta le richieste autenticate tramite [Adobe I/O](https://developer.adobe.com/), utilizzando il nuovo `server.adobedc.net` punto finale.

* Richieste autenticate tramite [Adobe I/O](https://developer.adobe.com/), utilizzando il nuovo `server.adobedc.net` punto finale.
* Richieste non autenticate tramite il `edge.adobedc.net` punto finale.

Questo abilita i casi d’uso che consentono la raccolta sicura e autenticata di dati sensibili, in base alle politiche sulla privacy della tua organizzazione. Oltre all’autenticazione, l’API server supporta il contrassegno dei datastreams per accettare solo le comunicazioni autenticate tramite l’API.

Guarda il video seguente per una panoramica semplificata dell’API server.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)