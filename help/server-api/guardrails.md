---
title: Accordi e obiettivi a livello di servizio
description: Scopri come configurare l’autenticazione per l’API server di rete Edge
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: raccolta dati;raccolta;rete Edge;api;sla;slt;livelli di servizio
hide: true
hidefromtoc: true
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# Guardrail

## Panoramica {#overview}

L&#39;Adobe utilizzerà gli sforzi commercialmente rilevanti per fare [!DNL Server API] disponibile entro una percentuale mensile di uptime di almeno il 99,9% per ogni regione, durante qualsiasi ciclo di fatturazione mensile.

## Definizioni

* **Disponibilità** viene calcolato per ogni intervallo di cinque minuti come percentuale delle richieste elaborate da Experience Adobe Experience Platform Edge Network che non generano errori e si riferiscono solo alle API di rete Adobe Experience Platform Edge fornite. Se un tenant non ha effettuato richieste in un determinato intervallo di cinque minuti, tale intervallo è considerato disponibile al 100%.
* **Percentuale mensile di uptime** per una determinata regione è calcolata come la media della disponibilità per tutti gli intervalli di cinque minuti in un mese.
* Un **a monte** è un servizio dietro la rete Adobe Edge, abilitato per un datastream specifico, come Adobe Server Side Forwarding, Adobe Edge Segmentation o Adobe Target.
* A **richiesta** inviato all&#39;API server è definito come una o più unità di richiesta.
* A **unità di richiesta** corrisponde a un frammento di 8 KB di una richiesta e a monte configurato per un datastream.
* Un **errore** è qualsiasi richiesta che non riesce a causa di una rete Adobe Experience Platform Edge [errore del servizio interno](error-handling.md).

## Obiettivi interni

I team tecnici di Adobe implementano procedure di telemetria in tempo reale, monitoraggio e scalabilità per garantire i seguenti obiettivi:

* Meno dell&#39;1% delle richieste HTTP restituite `5xx` errori negli ultimi cinque minuti
* Meno dell’1% delle connessioni a monte restituiscono un errore negli ultimi cinque minuti
* La capacità del tenant viene raddoppiata in meno di 10 minuti dal momento in cui viene raggiunto un limite.

## Esclusioni degli accordi a livello di servizio

L’impegno a livello di servizio descritto sopra non si applica ad eventuali problemi di indisponibilità o prestazioni causati dai seguenti eventi:

* Fattori al di fuori del nostro ragionevole controllo, compreso l’accesso a Internet o problemi correlati al di fuori dell’infrastruttura di Adobe.
* Qualsiasi abuso del [!DNL Server API], come definito dai limiti indicati di seguito.

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

