---
title: Garanzie delle prestazioni per API server di rete Edge
description: Scopri come utilizzare l’API server in protezioni delle prestazioni ottimali.
keywords: raccolta dati;raccolta;rete Edge;api;sla;slt;livelli di servizio
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---

# Garanzie delle prestazioni per API server di rete Edge

## Panoramica {#overview}

Le protezioni delle prestazioni definiscono i limiti di utilizzo relativi ai casi di utilizzo dell’API server. Il superamento dei limiti di prestazione descritti in questo articolo potrebbe comportare un degrado delle prestazioni.

L&#39;Adobe non è responsabile del deterioramento delle prestazioni causato da limiti di utilizzo superati. I clienti che superano costantemente le protezioni delle prestazioni possono richiedere una capacità di elaborazione aggiuntiva per evitare il deterioramento delle prestazioni.

## Definizioni

* **Disponibilità** viene calcolato per ogni intervallo di cinque minuti come percentuale delle richieste elaborate da Experience Platform Edge Network che non generano errori e si riferiscono solo alle API di rete Edge fornite. Se un tenant non ha effettuato richieste in un determinato intervallo di cinque minuti, tale intervallo è considerato disponibile al 100%.
* **Percentuale mensile di uptime** per una determinata regione è calcolata come la media della disponibilità per tutti gli intervalli di cinque minuti in un mese.
* Un **a monte** è un servizio dietro la rete Edge, abilitato per un datastream specifico, ad esempio Adobe Server Side Forwarding, Adobe Edge Segmentation o Adobe Target.
* A **unità di richiesta** corrisponde a un frammento di 8 KB di una richiesta e a monte configurato per un datastream.
* A **richiesta** è un singolo messaggio inviato da un&#39;applicazione di proprietà del cliente al [!DNL Server API]. Una richiesta può contenere una o più unità di richiesta.
* Un **errore** è qualsiasi richiesta che non riesce a causa di una rete Edge [errore del servizio interno](error-handling.md).

## Limiti di servizio

Tutti i datastreams applicano determinati limiti di utilizzo, che controllano principalmente quanti eventi possono essere inviati contemporaneamente, le loro dimensioni e il numero di servizi upstream a cui tali richieste vengono indirizzate.

### Unità di richiesta

Tutti i limiti vengono applicati e normalizzati su un **unità di richiesta (RU)**, definito come **Frammento da 8 KB** di una richiesta indirizzata a un servizio upstream configurato in un datastream.

#### Esempi

| Aggiornamenti configurati per ogni datastream | Dimensione media della richiesta | Unità di richiesta |
| --- | --- | --- |
| 1 (piattaforma Adobe) | 8 KB (1 frammento) | 1 |
| 2 (Adobe Platform, Adobe Target) | 8 KB (1 frammento) | 2 |
| 2 (Adobe Platform, Adobe Target) | 16 KB (2 frammenti) | 4 |
| 2 (Adobe Platform, Adobe Target) | 64 KB (8 frammenti) | 16 |

### Limiti delle unità di richiesta

La tabella seguente mostra i valori limite predefiniti. Se hai bisogno di limiti di unità di richiesta più elevati, contatta il rappresentante del tuo account.

| Endpoint | Richieste di unità al secondo |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### Limite di dimensione della richiesta HTTP

| Formato payload | Dimensione massima per una richiesta | Frammenti di richiesta max 8 KB |
| --- | --- | --- |
| Testo normale JSON | 64 KB | 8 |


>[!NOTE]
>
>A seconda del payload stesso, i formati binari sono generalmente più compatti del 20-40%, consentendo di inviare più dati rispetto a JSON in formato testo normale. Contatta il tuo rappresentante dell’Assistenza clienti se hai bisogno di una maggiore capacità per i tuoi datastreams.
