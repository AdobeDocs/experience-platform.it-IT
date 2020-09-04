---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: Segmentazione multi-entità
topic: overview
description: La segmentazione multi-entità è la capacità di estendere i dati del profilo con dati aggiuntivi basati su prodotti, store o altre classi non di profilo. Una volta connessi, i dati di altre classi diventano disponibili come se fossero nativi dello schema Profilo.
translation-type: tm+mt
source-git-commit: 5dd07bf9afe96be3a4c3f4a4d4e3b23aef4fde70
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---


# Segmentazione multi-entità

La segmentazione multi-entità è una funzione avanzata disponibile come parte di Adobe Experience Platform [!DNL Segmentation Service]. Questa funzione consente di estendere [!DNL Real-time Customer Profile] i dati con dati &quot;non relativi alle persone&quot; aggiuntivi (denominati anche &quot;entità dimensione&quot;) che l&#39;organizzazione può definire, ad esempio dati relativi a prodotti o store. La segmentazione multi-entità offre flessibilità nella definizione dei segmenti di pubblico in base ai dati pertinenti alle esigenze aziendali specifiche e può essere eseguita senza disporre di competenze nella creazione di query sui database. Con la segmentazione multi-entità, puoi aggiungere dati chiave ai tuoi segmenti senza dover apportare costose modifiche ai flussi di dati o aspettare un&#39;unione di dati back-end.

## Introduzione

La segmentazione multi-entità richiede una conoscenza approfondita dei vari servizi Adobe Experience Platform coinvolti nella segmentazione. Prima di continuare con questa guida, consulta la seguente documentazione:

* [!DNL Real-time Customer Profile](../profile/home.md): Fornisce un profilo del consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
   * [Profili](../profile/guardrails.md)profilo: Procedure ottimali per la creazione di modelli di dati supportati da [!DNL Profile].
* [!DNL Adobe Experience Platform Segmentation Service](./home.md): Consente di creare segmenti dai [!DNL Real-time Customer Profile] dati.
* [!DNL Experience Data Model (XDM)](../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../xdm/schema/composition.md#union)dello schema: Scoprite le procedure ottimali per la composizione degli schemi da utilizzare  Experience Platform.

## Casi di utilizzo

Per illustrare il valore della segmentazione multi-entità, prendete in considerazione tre casi d’uso standard di marketing che illustrano le sfide presenti nella maggior parte delle applicazioni di marketing:

### Combinazione di dati di acquisto online e offline

Un esperto di marketing che crea una campagna e-mail potrebbe aver tentato di creare un segmento per un pubblico target utilizzando gli acquisti recenti da parte dell&#39;archivio clienti negli ultimi tre mesi. Idealmente, questo segmento richiederebbe sia il nome dell&#39;articolo che il nome dello store in cui è stato effettuato l&#39;acquisto. In precedenza, la sfida consisteva nell&#39;acquisire l&#39;identificatore dello store dall&#39;evento di acquisto e assegnarlo a un profilo cliente singolo.

### Ritargeting e-mail per l&#39;abbandono del carrello

Spesso è complesso creare e qualificare gli utenti in segmenti che puntano all&#39;abbandono del carrello. Per sapere quali prodotti includere in una campagna di retargeting personalizzata è necessario disporre di dati sui prodotti abbandonati da ogni singolo utente. Questi dati sono legati a eventi commerciali che prima erano difficili da monitorare ed estrarre dati.

## Creazione di segmenti con più entità

Per creare un segmento con più entità è innanzitutto necessario definire le relazioni tra gli schemi prima di utilizzare l&#39;interfaccia utente [!DNL Segmentation] API o Generatore di segmenti per creare la definizione del segmento.

### Definizione delle relazioni

La definizione di relazioni all&#39;interno della struttura degli schemi del modello dati esperienza (XDM) è parte integrante della creazione di segmenti multi-entità. Questo processo può essere eseguito utilizzando l&#39;API del Registro di sistema dello schema o l&#39;Editor schema. Per i passaggi dettagliati che mostrano come definire una relazione tra due schemi, scegliete una delle seguenti esercitazioni:

* [Definizione di una relazione tra due schemi mediante l&#39;API](../xdm/tutorials/relationship-api.md)
* [Definizione di una relazione tra due schemi utilizzando l&#39;interfaccia utente dell&#39;Editor di schema](../xdm/tutorials/relationship-ui.md)

### Creazione di un segmento con più entità

Una volta definite le relazioni XDM necessarie, potete iniziare a creare un segmento con più entità. Questo processo può essere eseguito utilizzando l&#39;API di segmentazione o l&#39;interfaccia utente di Generatore di segmenti. Per ulteriori informazioni, scegliete una delle seguenti guide:

* [Creazione di un segmento tramite l’API di segmentazione](./tutorials/create-a-segment.md)
* [Creazione di un segmento mediante l’interfaccia utente di Generatore di segmenti](./ui/overview.md)

## Valutazione e accesso a segmenti con più entità

Dopo aver creato un segmento, puoi valutare e accedere ai risultati del segmento utilizzando l&#39;API di segmentazione. La valutazione di un segmento con più entità è molto simile alla valutazione di un segmento standard. Questo processo può essere eseguito solo tramite l&#39;API di segmentazione. Per una guida dettagliata che mostra come utilizzare l&#39;API per valutare e accedere ai segmenti, consulta l&#39;esercitazione sulla [valutazione e l&#39;accesso ai segmenti](./tutorials/evaluate-a-segment.md) .
