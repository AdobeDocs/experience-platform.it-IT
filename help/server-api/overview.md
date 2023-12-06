---
title: Panoramica API del server di rete Edge
description: Scopri cos’è l’API del server di rete Edge e come utilizzarla.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 5%

---


# Panoramica API del server di rete Edge {#overview}

Adobe Experience Platform Edge Network offre ai clienti un modo ottimizzato di interagire con qualsiasi servizio Adobe Experience Cloud o Adobe Experience Platform Edge.

Il [!DNL Edge Network Server API] può essere utilizzato per vari casi di utilizzo di raccolta dati, personalizzazione, pubblicità e marketing. Il [!DNL Server API] può essere utilizzato sui server, [!DNL IoT] dispositivi, set-top box e vari altri dispositivi.

Poiché il [!DNL Server API] non si basa sul caricamento di librerie, ma offre un modo estremamente veloce di interagire con la rete Edge di Adobe Experience Platform e le soluzioni supportate.

Vantaggi del [!DNL Server API] L&#39;architettura include:

* Tempo di caricamento pagina ridotto
* Latenza migliorata
* Raccolta di dati di prime parti
* Comunicazione lato server tra i servizi semplificata

Il [!DNL Server API] supporta la raccolta interattiva e in batch di dati, tramite due endpoint dedicati:

1. L’endpoint interattivo supporta la comunicazione con i servizi Adobe Experience Platform e Adobe Experience Cloud che supportano la segmentazione avanzata, la personalizzazione e altri casi di utilizzo di marketing.
2. L’endpoint batch consente l’invio in batch di richieste quando i dati devono essere caricati senza ricevere una risposta dalle applicazioni richiamate.

Il [!DNL Server API] supporta i seguenti tipi di richieste:

* Richieste autenticate tramite [Adobe Developer](https://developer.adobe.com/), utilizzando `server.adobedc.net` endpoint.
* Richieste non autenticate tramite `edge.adobedc.net` endpoint.

Questo consente casi d’uso che consentono una raccolta sicura e autenticata di dati sensibili, in base alle politiche sulla privacy della tua organizzazione. Oltre all’autenticazione, l’API server supporta il contrassegno degli stream di dati per accettare solo le comunicazioni autenticate tramite l’API.

Guarda il video seguente per una panoramica semplificata dell’API server.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
