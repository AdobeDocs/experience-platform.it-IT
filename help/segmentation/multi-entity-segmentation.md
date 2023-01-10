---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;servizio segmenti;segmenti;segmenti;multi-entità;segmentazione multi-entità;segmenti multi-entità;
solution: Experience Platform
title: Panoramica sulla segmentazione su più entità
description: La segmentazione su più entità consente di estendere i dati di profilo con dati aggiuntivi basati su prodotti, store o altre classi non di profilo. Una volta connessi, i dati provenienti da classi aggiuntive diventano disponibili come se fossero nativi dello schema Profilo.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Panoramica sulla segmentazione su più entità

La segmentazione su più entità è una funzione avanzata disponibile come parte di Adobe Experience Platform [!DNL Segmentation Service]. Questa funzione consente di estendere [!DNL Real-Time Customer Profile] dati con dati &quot;non personali&quot; aggiuntivi (noti anche come &quot;entità dimensione&quot;) che la tua organizzazione può definire, ad esempio dati relativi a prodotti o store. La segmentazione su più entità offre flessibilità quando si definiscono i segmenti di pubblico in base ai dati pertinenti alle specifiche esigenze aziendali e può essere eseguita senza disporre di esperienza nell’esecuzione di query sui database. Con la segmentazione su più entità, puoi aggiungere dati chiave ai segmenti senza dover apportare modifiche costose ai flussi di dati o attendere un’unione di dati back-end.

## Introduzione

La segmentazione su più entità richiede una comprensione funzionante dei vari servizi Adobe Experience Platform coinvolti nella segmentazione. Prima di continuare con questa guida, consulta la seguente documentazione:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): Fornisce un profilo di consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
   * [Guardrail profilo](../profile/guardrails.md): Best practice per la creazione di modelli di dati supportati da [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ti consente di creare segmenti da [!DNL Real-Time Customer Profile] dati.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../xdm/schema/composition.md#union): Scopri le best practice per la composizione degli schemi da utilizzare in Experience Platform. Per utilizzare al meglio la segmentazione, assicurati che i tuoi dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../xdm/schema/best-practices.md).

## Casi d’uso

Per illustrare il valore della segmentazione su più entità, considera tre casi d’uso standard di marketing che illustrano le sfide presenti nella maggior parte delle applicazioni di marketing:

### Combinazione di dati di acquisto online e offline

Un addetto al marketing che crea una campagna e-mail potrebbe aver tentato di creare un segmento per un pubblico target utilizzando gli acquisti recenti da parte dell’archivio clienti negli ultimi tre mesi. Idealmente, questo segmento richiederebbe sia il nome dell’articolo che il nome dello store in cui è stato effettuato l’acquisto. In precedenza, la sfida consisteva nell’acquisire l’identificatore dello store dall’evento di acquisto e assegnarlo a un singolo profilo cliente.

### Retargeting e-mail per abbandono carrello

Spesso è complesso creare e qualificare gli utenti in segmenti che puntano all’abbandono del carrello. Sapere quali prodotti includere in una campagna di retargeting personalizzata richiede i dati relativi a quali prodotti sono stati abbandonati da ciascun individuo. Questi dati sono legati a eventi di e-commerce che prima erano difficili da monitorare ed estrarre i dati da.

## Creazione di segmenti con più entità

La creazione di un segmento con più entità richiede prima di tutto la definizione di relazioni tra schemi prima di utilizzare il [!DNL Segmentation] Interfaccia utente dell’API o del Generatore di segmenti per creare la definizione del segmento.

### Definire relazioni

La definizione di relazioni all’interno della struttura degli schemi Experience Data Model (XDM) è parte integrante della creazione di segmenti con più entità. Per le relazioni, il campo nella destinazione deve essere contrassegnato come identità principale di tale schema. Un&#39;identità può essere contrassegnata solo sulle stringhe e non può essere contrassegnata sulle matrici. Inoltre, le relazioni non devono necessariamente essere una a una, in quanto puoi collegare profili ed eventi di esperienza a più destinazioni.

La definizione delle relazioni può essere effettuata utilizzando l&#39;API del Registro di sistema dello schema o l&#39;Editor schema. Per passaggi dettagliati che mostrano come definire una relazione tra due schemi, scegli tra le seguenti esercitazioni:

* [Definizione di una relazione tra due schemi utilizzando l’API](../xdm/tutorials/relationship-api.md)
* [Definizione di una relazione tra due schemi tramite l’interfaccia utente dell’Editor di schema](../xdm/tutorials/relationship-ui.md)

### Creare un segmento con più entità

Una volta definite le relazioni XDM necessarie, puoi iniziare a creare un segmento con più entità. Questa operazione può essere eseguita utilizzando l’API Segmentation o l’interfaccia utente del Generatore di segmenti. Per ulteriori informazioni, si prega di scegliere tra le seguenti guide:

* [Creazione di un segmento tramite l’API di segmentazione](./tutorials/create-a-segment.md)
* [Creazione di un segmento tramite l’interfaccia utente del Generatore di segmenti](./ui/overview.md)

## Valutare e accedere a segmenti con più entità

Dopo aver creato un segmento, puoi valutare e accedere ai risultati del segmento utilizzando l’API Segmentazione. La valutazione di un segmento con più entità è molto simile alla valutazione di un segmento standard. Questo processo può essere eseguito solo utilizzando l’API di segmentazione. Per una guida dettagliata su come utilizzare l’API per valutare e accedere ai segmenti, consulta la sezione [valutazione e accesso ai segmenti](./tutorials/evaluate-a-segment.md) esercitazione.
