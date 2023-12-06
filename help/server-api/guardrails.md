---
title: Guardrail delle prestazioni per l’API del server di rete Edge
description: Scopri come utilizzare l’API server all’interno di guardrail di prestazioni ottimali.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---


# Guardrail delle prestazioni per l’API del server di rete Edge

## Panoramica {#overview}

I guardrail delle prestazioni definiscono i limiti di utilizzo relativi ai casi di utilizzo dell’API server. Il superamento dei guardrail delle prestazioni descritti in questo articolo potrebbe causare un peggioramento delle prestazioni.

Adobe non è responsabile del deterioramento delle prestazioni causato dal superamento dei limiti di utilizzo. I clienti che superano costantemente i guardrail delle prestazioni possono richiedere una capacità di elaborazione aggiuntiva per evitare il degrado delle prestazioni.

## Definizioni

* **Disponibilità** viene calcolato per ogni intervallo di cinque minuti come percentuale di richieste elaborate da Experienci Platform Edge Network che non generano errori e si riferiscono solo alle API di Edge Network fornite. Se un tenant non ha effettuato richieste in un determinato intervallo di cinque minuti, tale intervallo viene considerato disponibile al 100%.
* **Percentuale tempo di attività mensile** per una determinata regione viene calcolata come media della disponibilità per tutti gli intervalli di cinque minuti in un mese.
* Un **a monte** è un servizio dietro la rete Edge, abilitato per uno stream di dati specifico, ad esempio Adobe Server Side Forwarding, Adobe Edge Segmentation o Adobe Target.
* A **unità di richiesta** corrisponde a un frammento di 8 KB di una richiesta e uno a monte configurato per uno stream di dati.
* A **richiesta** è un singolo messaggio inviato da un’applicazione di proprietà del cliente al [!DNL Server API]. Una richiesta può contenere una o più unità di richiesta.
* Un **errore** è qualsiasi richiesta non riuscita a causa di una rete Edge [errore del servizio interno](error-handling.md).

## Limiti del servizio

Tutti gli stream di dati applicano determinati limiti di utilizzo, che controllano principalmente il numero di eventi che possono essere inviati contemporaneamente, la loro dimensione e il numero di servizi a monte a cui tali richieste vengono indirizzate.

### Unità di richiesta

Tutti i limiti vengono applicati e normalizzati in un **unità di richiesta (RU)**, definito come **Frammento da 8 KB** di una richiesta indirizzata a un servizio upstream configurato in un flusso di dati.

#### Esempi

| Flussi a monte configurati per flusso di dati | Dimensione media della richiesta | Unità di richiesta |
| --- | --- | --- |
| 1 (piattaforma di Adobe) | 8 KB (1 frammento) | 1 |
| 2 (piattaforma di Adobe, Adobe Target) | 8 KB (1 frammento) | 2 |
| 2 (piattaforma di Adobe, Adobe Target) | 16 KB (2 frammenti) | 4 |
| 2 (piattaforma di Adobe, Adobe Target) | 64 KB (8 frammenti) | 16 |

### Limiti unità di richiesta

La tabella seguente mostra i valori limite predefiniti. Se hai bisogno di limiti di unità di richiesta più elevati, contatta il rappresentante del tuo account.

| Endpoint | Richieste unità al secondo |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### Limite dimensione richiesta HTTP

| Formato payload | Dimensione massima per una richiesta | Massimo 8 KB di frammenti di richiesta |
| --- | --- | --- |
| Testo normale JSON | 64 KB | 8 |


>[!NOTE]
>
>A seconda del payload stesso, i formati binari sono generalmente più compatti del 20-40%, consentendo di inviare più dati di quanti ne avresti in JSON in formato testo normale. Contatta il rappresentante dell’Assistenza clienti se hai bisogno di una capacità più elevata per i flussi di dati.

## Passaggi successivi

Consulta la seguente documentazione per ulteriori informazioni su altri guardrail dei servizi Experienci Platform, informazioni sulla latenza end-to-end e informazioni sulle licenze dai documenti di descrizione del prodotto Real-Time CDP:

* [Guardrail Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammi di latenza end-to-end](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) per vari servizi di Experience Platform.
* [Real-time Customer Data Platform (versione B2C - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
