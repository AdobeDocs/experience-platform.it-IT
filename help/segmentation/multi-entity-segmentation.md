---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentazione multi-entità
topic: overview
translation-type: tm+mt
source-git-commit: 7110be2654e55ea411580f8c9e2e92bb52badab5
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Segmentazione multi-entità

La segmentazione multi-entità è la capacità di estendere i dati del profilo con dati aggiuntivi basati su prodotti, store o altre classi non di profilo. Una volta connessi, i dati di altre classi diventano disponibili come se fossero nativi dello schema Profilo.

Per saperne di più sulla segmentazione multi-entità, continuate a leggere la documentazione e completate le vostre conoscenze guardando il video sottostante o esplorando la panoramica [della](./home.md)segmentazione.]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei diversi servizi di Adobe Experience Platform  coinvolti nell&#39;utilizzo della segmentazione. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Profilo](../profile/home.md)cliente in tempo reale: Fornisce un profilo del consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [servizio](./home.md)di segmentazione Adobe Experience Platform: Consente di creare segmenti dal profilo cliente in tempo reale.
- [Experience Data Model (XDM)](../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.

## Come definire le relazioni XDM

La definizione di relazioni con la struttura degli schemi Experience Data Model (XDM) è una parte importante e integrante della creazione di segmenti.

Questo processo può essere eseguito utilizzando l&#39;API del Registro di sistema dello schema o l&#39;Editor schema. Per una guida dettagliata sull&#39;utilizzo dell&#39;API per definire una relazione tra due schemi, leggete [l&#39;esercitazione sulla definizione di una relazione tra due schemi mediante l&#39;API](../xdm/tutorials/relationship-api.md). Per una guida dettagliata sull&#39;utilizzo dell&#39;Editor di schema per definire una relazione tra due schemi, vedere [l&#39;esercitazione sulla definizione di una relazione tra due schemi che utilizza l&#39;Editor](../xdm/tutorials/relationship-ui.md)di schema.

## Come utilizzare la creazione di segmenti che utilizzano relazioni XDM

Una volta definite le relazioni XDM, potete utilizzare le API Profilo cliente in tempo reale per creare un segmento.

Questo processo può essere eseguito utilizzando l&#39;API Profilo cliente in tempo reale o il Generatore di segmenti. Per una guida dettagliata sull&#39;utilizzo dell&#39;API per creare un segmento, leggete [l&#39;esercitazione sulla creazione di un segmento tramite l&#39;API](./tutorials/create-a-segment.md)Profilo cliente in tempo reale. Per una guida dettagliata sull’utilizzo del Generatore di segmenti per creare un segmento, consulta [la guida](./ui/overview.md)utente di Segment Builder (Generatore di segmenti).

## Come valutare e accedere ai segmenti per segmenti con più entità

Dopo aver creato un segmento, puoi valutare e accedere ai risultati del segmento utilizzando le API Profilo cliente in tempo reale. La valutazione di un segmento con più entità è molto simile alla valutazione di un segmento regolare.

Questo processo può essere eseguito solo tramite l&#39;API Profilo cliente in tempo reale. Per una guida dettagliata sull&#39;utilizzo dell&#39;API per valutare e accedere ai segmenti, consulta [l&#39;esercitazione sulla valutazione e l&#39;accesso ai segmenti](./tutorials/evaluate-a-segment.md).