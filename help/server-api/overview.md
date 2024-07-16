---
title: Panoramica dell’API di Edge Network Server
description: Scopri cos’è l’API del server di rete Edge e come utilizzarla.
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: 041a1782442df5f08bb52e4e450734a51c7781ea
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 5%

---

# Panoramica dell’API di Edge Network Server {#overview}

L’Edge Network di Adobe Experience Platform offre ai clienti un modo ottimizzato di interagire con qualsiasi servizio Edge di Adobe Experience Cloud o Adobe Experience Platform.

[!DNL Edge Network Server API] può essere utilizzato per vari casi di utilizzo di raccolta dati, personalizzazione, pubblicità e marketing. [!DNL Server API] può essere utilizzato su server, dispositivi [!DNL IoT], set-top box e vari altri dispositivi.

Poiché [!DNL Server API] non si basa su librerie da caricare, offre un modo estremamente veloce di interagire con l&#39;Edge Network di Adobe Experience Platform e le soluzioni supportate.

I vantaggi dell&#39;architettura [!DNL Server API] includono:

* Tempo di caricamento pagina ridotto
* Latenza migliorata
* Raccolta di dati di prime parti
* Comunicazione lato server tra i servizi semplificata

[!DNL Server API] supporta la raccolta di dati in batch e interattivi tramite due endpoint dedicati:

1. L’endpoint interattivo supporta la comunicazione con i servizi Adobe Experience Platform e Adobe Experience Cloud che supportano la segmentazione avanzata, la personalizzazione e altri casi di utilizzo di marketing.
2. L’endpoint batch consente l’invio in batch di richieste quando i dati devono essere caricati senza ricevere una risposta dalle applicazioni richiamate.

[!DNL Server API] supporta il seguente tipo di richieste:

* Richieste autenticate tramite [Adobe Developer](https://developer.adobe.com/), utilizzando l&#39;endpoint `server.adobedc.net`.
* Richieste non autenticate tramite l&#39;endpoint `edge.adobedc.net`.

Questo consente casi d’uso che consentono una raccolta sicura e autenticata di dati sensibili, in base alle politiche sulla privacy della tua organizzazione. Oltre all’autenticazione, l’API server supporta il contrassegno degli stream di dati per accettare solo le comunicazioni autenticate tramite l’API.

Guarda il video seguente per una panoramica semplificata dell’API server.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
