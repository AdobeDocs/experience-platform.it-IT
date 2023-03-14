---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;segmenti;segmenti;più entità;più entità;più entità;
solution: Experience Platform
title: Panoramica della segmentazione di più entità
description: La segmentazione con più entità consente di estendere i dati del profilo con dati aggiuntivi basati su prodotti, archivi o altre classi non di profilo. Una volta effettuata la connessione, i dati provenienti da classi aggiuntive diventano disponibili come se fossero nativi per lo schema Profilo.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Panoramica sulla segmentazione con più entità

La segmentazione multi-entità è una funzione avanzata disponibile come parte di Adobe Experience Platform [!DNL Segmentation Service]. Questa funzione consente di estendere [!DNL Real-Time Customer Profile] dati con dati aggiuntivi non relativi alle persone (noti anche come &quot;entità dimensione&quot;) che la tua organizzazione può definire, ad esempio dati relativi a prodotti o archivi. La segmentazione multi-entità offre flessibilità quando si definiscono segmenti di pubblico in base a dati rilevanti per le specifiche esigenze aziendali e può essere eseguita senza avere esperienza nell’esecuzione di query sui database. Con la segmentazione con più entità, puoi aggiungere dati chiave ai segmenti senza dover apportare modifiche costose ai flussi di dati o attendere un’unione dati back-end.

## Introduzione

La segmentazione multi-entità richiede una buona comprensione dei vari servizi Adobe Experience Platform coinvolti nella segmentazione. Prima di continuare con questa guida, consulta la seguente documentazione:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): fornisce un profilo consumer unificato in tempo reale, basato su dati aggregati provenienti da più origini.
   * [Guardrail del profilo](../profile/guardrails.md): best practice per la creazione di modelli di dati supportati da [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): consente di creare segmenti da [!DNL Real-Time Customer Profile] dati.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../xdm/schema/composition.md#union): scopri le best practice per la composizione degli schemi da utilizzare in Experience Platform. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../xdm/schema/best-practices.md).

## Casi d’uso

Per illustrare il valore della segmentazione tra più entità, considera tre casi d’uso di marketing standard che illustrano le sfide presenti nella maggior parte delle applicazioni di marketing:

### Combinazione di dati di acquisto online e offline

Un addetto al marketing che crea una campagna e-mail può aver tentato di creare un segmento per un pubblico target utilizzando i recenti acquisti del negozio clienti negli ultimi tre mesi. Idealmente, questo segmento richiederebbe sia il nome dell’articolo che il nome del negozio in cui è stato effettuato l’acquisto. In precedenza, la sfida consisteva nell’acquisire l’identificatore del negozio dall’evento di acquisto e assegnarlo a un singolo profilo cliente.

### Retargeting delle e-mail per abbandono carrello

Spesso è complesso creare e qualificare gli utenti in segmenti destinati all’abbandono del carrello. Per sapere quali prodotti includere in una campagna di retargeting personalizzata sono necessari dati relativi ai prodotti abbandonati da ogni singolo utente. Questi dati sono legati a eventi di e-commerce che in precedenza erano difficili da monitorare ed estrarre dati da.

## Creazione di segmenti con più entità

La creazione di un segmento con più entità richiede innanzitutto la definizione di relazioni tra schemi prima di utilizzare [!DNL Segmentation] API o interfaccia utente di Segment Builder per creare la definizione del segmento.

### Definire le relazioni

La definizione delle relazioni all’interno della struttura degli schemi Experience Data Model (XDM) è parte integrante della creazione di segmenti con più entità. Per le relazioni, il campo nella destinazione deve essere contrassegnato come identità primaria di tale schema. Un’identità può essere contrassegnata solo su stringhe e non può essere contrassegnata su array. Inoltre, non è necessario che le relazioni siano one-to-one, in quanto puoi collegare profili ed eventi di esperienza a più destinazioni.

La definizione delle relazioni può essere eseguita utilizzando l’API Schema Registry o l’Editor di schema. Per i passaggi dettagliati che mostrano come definire una relazione tra due schemi, scegli una delle seguenti esercitazioni:

* [Definizione di una relazione tra due schemi utilizzando l’API](../xdm/tutorials/relationship-api.md)
* [Definizione di una relazione tra due schemi tramite l’interfaccia utente dell’Editor di schema](../xdm/tutorials/relationship-ui.md)

### Creare un segmento con più entità

Dopo aver definito le relazioni XDM necessarie, puoi iniziare a creare un segmento con più entità. Questa operazione può essere eseguita utilizzando l’API di segmentazione o l’interfaccia utente di Segment Builder. Per ulteriori informazioni, scegliere tra le seguenti guide:

* [Creazione di un segmento utilizzando l’API di segmentazione](./tutorials/create-a-segment.md)
* [Creazione di un segmento mediante l’interfaccia utente del Generatore di segmenti](./ui/overview.md)

## Valutare e accedere a segmenti con più entità

Dopo aver creato un segmento, puoi valutare e accedere ai risultati del segmento utilizzando l’API di segmentazione. La valutazione di un segmento con più entità è molto simile alla valutazione di un segmento standard. Questo processo può essere eseguito solo utilizzando l’API di segmentazione. Per una guida dettagliata che mostra come utilizzare l’API per valutare e accedere ai segmenti, leggi la [valutazione e accesso ai segmenti](./tutorials/evaluate-a-segment.md) esercitazione.
