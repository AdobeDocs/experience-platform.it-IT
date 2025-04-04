---
title: Guardrail delle prestazioni per l’API server di Edge Network
description: Scopri come utilizzare l’API server all’interno di guardrail di prestazioni ottimali.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---


# Guardrail delle prestazioni per l’API server di Edge Network

## Panoramica {#overview}

I guardrail delle prestazioni definiscono i limiti di utilizzo relativi ai casi di utilizzo dell’API server. Il superamento dei guardrail delle prestazioni descritti in questo articolo potrebbe causare un peggioramento delle prestazioni.

Adobe non è responsabile del deterioramento delle prestazioni causato dal superamento dei limiti di utilizzo. I clienti che superano costantemente i guardrail delle prestazioni possono richiedere una capacità di elaborazione aggiuntiva per evitare il degrado delle prestazioni.

>[!IMPORTANT]
>
>Controlla i diritti di licenza nell&#39;ordine di vendita e la corrispondente [descrizione del prodotto](https://helpx.adobe.com/it/legal/product-descriptions.html) sui limiti di utilizzo effettivi, oltre a questa pagina di guardrail.

Tutti i guardrail delle prestazioni descritti in questa pagina si applicano a livello di organizzazione IMS. Per gli utenti con più organizzazioni IMS configurate, ogni organizzazione è soggetta singolarmente ai guardrail delle prestazioni riportati di seguito. Per ulteriori dettagli su [!DNL IMS Organizations], vedere il glossario di [Experience Platform](../landing/glossary.md).

## Definizioni

* **Disponibilità** viene calcolata per ogni intervallo di cinque minuti come percentuale di richieste elaborate da Experience Platform Edge Network che non presentano errori e si riferiscono esclusivamente alle API di Edge Network con provisioning. Se un tenant non ha effettuato richieste in un determinato intervallo di cinque minuti, tale intervallo viene considerato disponibile al 100%.
* **La percentuale di tempo di attività mensile** per una determinata area viene calcolata come media della disponibilità per tutti gli intervalli di cinque minuti in un mese.
* Un **upstream** è un servizio dietro Edge Network, abilitato per uno stream di dati specifico, ad esempio Adobe Server Side Forwarding, Adobe Edge Segmentation o Adobe Target.
* Una **unità di richiesta** corrisponde a un frammento di 8 KB di una richiesta e una a monte configurata per uno stream di dati.
* Una **richiesta** è un singolo messaggio inviato da un&#39;applicazione di proprietà del cliente a [!DNL Server API]. Una richiesta può contenere una o più unità di richiesta.
* Un **errore** è una richiesta non riuscita a causa di un [errore del servizio interno](error-handling.md) di Edge Network.

## Limiti del servizio

Tutti gli stream di dati applicano determinati limiti di utilizzo, che controllano principalmente il numero di eventi che possono essere inviati contemporaneamente, la loro dimensione e il numero di servizi a monte a cui tali richieste vengono indirizzate.

### Unità di richiesta

Tutti i limiti vengono applicati e normalizzati su una **unità di richiesta (RU)**, definita come frammento **8 KB** di una richiesta indirizzata a un servizio upstream configurato in un flusso di dati.

#### Esempi

| Flussi a monte configurati per flusso di dati | Dimensione media della richiesta | Unità di richiesta |
| --- | --- | --- |
| 1 (Adobe Experience Platform) | 8 KB (1 frammento) | 1 |
| 2 (Adobe Experience Platform, Adobe Target) | 8 KB (1 frammento) | 2 |
| 2 (Adobe Experience Platform, Adobe Target) | 16 KB (2 frammenti) | 4 |
| 2 (Adobe Experience Platform, Adobe Target) | 64 KB (8 frammenti) | 16 |

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

Consulta la seguente documentazione per ulteriori informazioni su altri guardrail dei servizi Experience Platform, sulla latenza end-to-end e sulle licenze dai documenti di descrizione del prodotto Real-Time CDP:

* [Guardrail Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammi di latenza end-to-end](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) per vari servizi Experience Platform.
* [Real-Time Customer Data Platform (Edizione B2C - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
