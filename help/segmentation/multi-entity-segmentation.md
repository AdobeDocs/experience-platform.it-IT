---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentazione multi-entità
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# Segmentazione multi-entità

La segmentazione multi-entità è la capacità di estendere [!DNL Profile] i dati con dati aggiuntivi basati su prodotti, store o altre classi non di profilo. Una volta connessi, i dati provenienti da classi aggiuntive diventano disponibili come se fossero nativi dello [!DNL Profile] schema.

Per saperne di più sulla segmentazione multi-entità, continuate a leggere la documentazione e completate le vostre conoscenze guardando il video sottostante o esplorando la panoramica [della](./home.md)segmentazione.]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei diversi servizi di Adobe Experience Platform  coinvolti nell&#39;utilizzo della segmentazione. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [!DNL Real-time Customer Profile](../profile/home.md): Fornisce un profilo del consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [servizio](./home.md)di segmentazione Adobe Experience Platform: Consente di creare segmenti dal profilo cliente in tempo reale.
- [!DNL Experience Data Model (XDM)](../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.

## Come definire le relazioni XDM

La definizione di relazioni con la struttura degli schemi [!DNL Experience Data Model] (XDM) è una parte importante e integrante della creazione dei segmenti.

Questo processo può essere eseguito utilizzando l&#39; [!DNL Schema Registry] API o l&#39; [!DNL Schema Editor]. Per una guida dettagliata sull&#39;utilizzo dell&#39;API per definire una relazione tra due schemi, leggete [l&#39;esercitazione sulla definizione di una relazione tra due schemi mediante l&#39;API](../xdm/tutorials/relationship-api.md). Per una guida dettagliata sull&#39;utilizzo [!DNL Schema Editor] per definire una relazione tra due schemi, vedere [l&#39;esercitazione sulla definizione di una relazione tra due schemi che utilizza l&#39;Editor](../xdm/tutorials/relationship-ui.md)di schema.

## Come creare segmenti che utilizzano relazioni XDM

Una volta definite le relazioni XDM, potete utilizzare l&#39; [!DNL Segmentation Service] API per creare un segmento.

Questo processo può essere eseguito utilizzando l&#39; [!DNL Segmentation] API o l&#39;interfaccia [!DNL Segment Builder] utente. Per una guida dettagliata sull&#39;utilizzo dell&#39;API per creare un segmento, leggete [l&#39;esercitazione sulla creazione di un segmento tramite l&#39;API](./tutorials/create-a-segment.md)di segmentazione. Per una guida dettagliata sull’utilizzo del Generatore di segmenti per creare un segmento, consulta [la guida](./ui/overview.md)utente di Segment Builder (Generatore di segmenti).

## Come valutare e accedere ai segmenti per segmenti con più entità

Dopo aver creato un segmento, puoi valutare e accedere ai risultati del segmento utilizzando l&#39; [!DNL Segmentation Service] API. La valutazione di un segmento con più entità è molto simile alla valutazione di un segmento regolare.

Questo processo può essere eseguito solo tramite l&#39; [!DNL Segmentation Service] API. Per una guida dettagliata sull&#39;utilizzo dell&#39;API per valutare e accedere ai segmenti, consulta l&#39;esercitazione sulla [valutazione e l&#39;accesso ai segmenti](./tutorials/evaluate-a-segment.md).