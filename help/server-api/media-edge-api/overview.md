---
keywords: Experience Platform;media edge;argomenti popolari;intervallo di date
solution: Experience Platform
title: API Media Edge
description: Panoramica delle API Media Edge.
exl-id: null
source-git-commit: f040ba6d1403da4212fe279e32316bac995905b2
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 5%

---


# Panoramica API di Media Edge

Le API Media Edge sono basate su Adobe Experience Platform (AEP) per fornire dati di tracciamento degli eventi multimediali nel framework di [Schemi XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Per i clienti Media Analytics, questo rende disponibili le seguenti funzioni:

* Con [Customer Journey Analytics (CJA)](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it), i clienti possono ottenere dettagli granulari sulla durata, avvii e arresti in tempo reale da valutare e combinare per le metriche dei contenuti multimediali. I clienti che eseguono la migrazione da Adobe Analytics dispongono di tutte le metriche di reporting disponibili in CJA.

* Con [Adobe Real-time Customer Data Platform (CDP)](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=it), i clienti possono arricchire i loro profili in tempo reale con i dati sul consumo di contenuti multimediali.

* Con [Adobe Journey Optimizer (AJO)](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en), i clienti possono ottimizzare le campagne omnicanale e automatizzare i percorsi con i segnali di consumo dei contenuti multimediali.


## Ottimizzazione dei flussi di dati di tracciamento dei contenuti multimediali

Entrambi [Media Collection](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) API e API Media Edge forniscono dati di tracciamento dei contenuti multimediali come servizi RESTful. Tuttavia, l’utilizzo del servizio Media Edge offre i seguenti vantaggi:

* È il modo più semplice per incorporare schemi XDM nel flusso di dati.

* Le chiamate vengono indirizzate da un lettore multimediale direttamente al [Rete Experience Edge Platform](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* Tiene traccia degli eventi multimediali nel modo più efficiente.

La tabella seguente presenta il miglior servizio API di Adobe per vari casi di analisi dei contenuti multimediali:

| Caso d’uso | Piattaforma | Servizio API |
| -------- | ------ | ---------- |
| CJA | AEP | Media Edge |
| CDP + CJA | AEP | Media Edge |
| Analytics + CJA | AEP | Media Edge |
| Analisi legacy | N/D | Media Collection |

>[!NOTE]
>
> Il servizio API Media Collection per Analytics riceve ancora dati XDM, ma non è ottimizzato per esso nella misura in cui il servizio Media Edge lo è. A seconda dei dati inviati dal lettore multimediale, alcuni dati solo Analytics possono essere instradati anche tramite il servizio API Media Edge.

L’immagine seguente mostra i flussi di dati per i due servizi API:


![Flussi di dati di analisi dei contenuti multimediali](../assets/edge-api-dataflow.png)


Per ulteriori informazioni sull’utilizzo delle API Media Edge, consulta la documentazione introduttiva.

Per ulteriori informazioni sull’utilizzo di Platform Edge, consulta [Installazione di Media Analytics con Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).




