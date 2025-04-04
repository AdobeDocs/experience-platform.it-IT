---
solution: Experience Platform
title: Confronto tra rete Edge e hub
description: Scopri i diversi percorsi di elaborazione disponibili per Adobe Experience Platform.
exl-id: 3e9c63d2-c798-44b4-870d-bf1551f29690
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 3%

---

# Confronto tra rete Edge e hub

Adobe Experience Platform è il sistema più potente, flessibile e aperto sul mercato per la creazione e la gestione di soluzioni complete che guidano la customer experience. Puoi utilizzare Experience Platform per centralizzare e standardizzare i dati e i contenuti dei clienti da qualsiasi sistema e applicare tecniche di data science e apprendimento automatico al fine di migliorare la progettazione e la consegna di esperienze personalizzate. Di conseguenza, Experience Platform dispone di diversi modi per elaborare i dati, consentendo di valutarli nel miglior modo possibile.

## Tipi di server

Su Experience Platform, i dati possono essere elaborati in due percorsi diversi: Adobe Experience Platform hub per flussi di lavoro in batch e in streaming e Edge Network per esperienze in tempo reale.

### Hub Adobe Experience Platform

L’hub è un centro dati principale che si trova a livello centrale e contiene tutti i dati storici e il contesto dei profili avanzati raccolti in Adobe Experience Platform. Questo ti consente di inviare e ricevere dati più solidi e completi ai servizi a valle. Di conseguenza, hub deve essere utilizzato in scenari in cui la **accuratezza** dei dati è più importante.

I servizi disponibili su hub includono:

- Segmentazione in batch
- Segmentazione in streaming
- Profili
- Destinazioni
- Grafo delle identità
- Data Distiller - Query Service
- Connettori Source

### Experience Platform Edge Network

Edge Network è un server fisicamente più vicino a posizioni geografiche diverse. Questi data center elaborano tutti i dati raccolti tramite le estensioni SDK e le API Edge Network. Gli unici dati che risiedono in Edge Network sono le appartenenze a un pubblico, le identità di profilo e gli attributi necessari per la personalizzazione.

Edge Network ti consente di inviare e ricevere dati ai clienti più rapidamente a causa della loro vicinanza all’utente finale. Inoltre, puoi utilizzare Edge Network per elaborare le richieste di inoltro degli eventi e le richieste di gestione dei tag. Tuttavia, Edge Network elabora solo i dati **comportamentali**. Di conseguenza, Edge Network dovrebbe essere utilizzato in scenari in cui la **velocità** dei dati è più importante.

I servizi disponibili su Edge Network includono:

- Segmentazione Edge
- Profili Edge
- Destinazioni di Edge
- Raccolta dati
- Estensioni SDK

## Posizioni

Nella sezione seguente sono elencate le posizioni sia per l’hub che per Edge Network.

![Diagramma che elenca le diverse posizioni per i server hub e Edge Network.](./images/servers/platform-server-locations.png)

**Hub**

- VA7 (Virginia, Stati Uniti)
- NLD2 (Paesi Bassi)
- AUS5 (Australia)
- CAN2 (Canada)
- GBR9 (Regno Unito)
- IND1 (India)

**Edge Network**

- OR2 (Oregon, Stati Uniti)
- VA6 (Virginia, USA)
- IRL1 (Irlanda)
- IND1 (India)
- SGP3 (Singapore)
- AUS3 (Australia)
- JPN3 (Giappone)

Ulteriori informazioni dettagliate sui percorsi server disponibili sono disponibili nella [panoramica su più cloud](./multi-cloud.md#available-cloud-regions).

## Passaggi successivi

Dopo aver letto questa panoramica, ora comprendi le differenze tra l’elaborazione dei dati sull’hub Adobe Experience Platform e Adobe Experience Platform Edge Network.

## Appendice

Nella sezione seguente sono elencate informazioni supplementari sull’elaborazione dei dati in Adobe Experience Platform.

### Domande frequenti

Nella sezione seguente sono elencate le domande frequenti su hub e Edge Network:

#### Quali scenari sono più appropriati per l&#39;hub?

L&#39;hub è più adatto negli scenari in cui la **accuratezza** dei dati è più importante. Ad esempio, supponiamo che tu voglia creare una campagna di marketing per indirizzare tutti i clienti che hanno abbandonato i carrelli. In questo caso d’uso, puoi utilizzare la segmentazione batch, creando un pubblico che corrisponda agli utenti del carrello abbandonati ed esportarlo in una destinazione batch.

#### Quali scenari sono più appropriati per Edge Network?

Edge Network è ideale per scenari in cui **la velocità** dei dati è più importante. Ad esempio, supponiamo che tu debba creare una vendita flash limitata per eseguire il targeting di un cliente che sta navigando sul tuo sito con un prodotto nel carrello. In questo caso d’uso, puoi utilizzare la segmentazione Edge, consentendoti di eseguire immediatamente il targeting e inviare una notifica personalizzata agli utenti con un prodotto nel carrello con una &quot;vendita flash&quot;.

#### Quali dati passano dall’hub ad Edge Network?

Dall’hub ad Edge Network vengono caricati solo i dati necessari per fornire esperienze in tempo reale ai server Edge di. Questi dati vengono inviati automaticamente dall’hub ad Edge Network per mantenerli infine coerenti e vengono conservati solo per un massimo di 14 giorni. Tuttavia, **not** significa che i dati sono perfettamente sincronizzati con i dati nell&#39;hub. Di conseguenza, potrebbero esserci differenze nei dati disponibili tra hub e Edge Network.
