---
solution: Experience Platform
title: API Media Edge
description: Panoramica delle API Media Edge
exl-id: 55c952de-caab-4301-acf2-f7b64cebbb1c
source-git-commit: 034498e662ed55112f22751d44cf3ecf75d38d61
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 3%

---

# Panoramica API di Media Edge

Le API Media Edge sono basate su Adobe Experience Platform per fornire dati di tracciamento degli eventi multimediali nel framework di [Schemi XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Per i clienti Media Analytics, questo rende disponibili le seguenti funzioni:

* Con [Adobe Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it), i clienti possono ottenere dettagli granulari sulla durata, avvii e arresti in tempo reale da valutare e combinare per le metriche dei contenuti multimediali. I clienti che eseguono la migrazione da Adobe Analytics dispongono di tutte le metriche di reporting disponibili in Adobe Customer Journey Analytics.

* Con [Adobe Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=it), i clienti possono arricchire i loro profili in tempo reale con i dati sul consumo di contenuti multimediali.

* Con [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=it), i clienti possono ottimizzare le campagne omnicanale e automatizzare i percorsi con i segnali di consumo dei contenuti multimediali.


## Ottimizzazione dei flussi di dati di tracciamento dei contenuti multimediali

Entrambi [API Media Collection](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html#media-tracking-data-flows) e le API Media Edge forniscono i dati di tracciamento dei contenuti multimediali come servizi RESTful. Tuttavia, l’utilizzo del servizio Media Edge offre i seguenti vantaggi:

* È il modo più semplice per incorporare schemi XDM nel flusso di dati.

* Le chiamate vengono indirizzate da un lettore multimediale direttamente al [Experienci Platform Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=it).

* Tiene traccia degli eventi multimediali in modo efficiente con un minimo di chiamate tra server diversi.

La tabella seguente mostra un possibile servizio API di Adobe per vari casi di analisi dei contenuti multimediali:

| Caso d’uso | Servizio API |
| -------- | ----------- |
| Soluzione Adobe Experience Platform | Media Edge |
| REAL-TIME CDP + CUSTOMER JOURNEY ANALYTICS | Media Edge |
| Soluzione Adobe Analytics + Adobe Experience Platform | Media Edge |
| Solo Adobe Analytics (già tracciamento) | Media Collection |

>[!NOTE]
>
> Il servizio API Media Collection per Analytics riceve ancora dati XDM, ma non è ottimizzato per esso nella misura in cui il servizio Media Edge lo è. A seconda dei dati inviati dal lettore multimediale, alcuni dati solo Analytics possono essere instradati anche tramite il servizio API Media Edge.

L’immagine seguente mostra i flussi di dati per i due servizi API:

![Flussi di dati di analisi dei contenuti multimediali](../assets/edge-api-dataflow.png)

## Passaggi successivi

* Per ulteriori informazioni sull’utilizzo delle API Media Edge, consulta [Documentazione introduttiva](getting-started.md).

* Per ulteriori informazioni sull’utilizzo di Platform Edge, consulta [Installazione di Media Analytics con Experienci Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html).
