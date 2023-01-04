---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;ora di vita;ttl;time-to-live;
solution: Experience Platform
title: Scadenza eventi esperienza
description: Questo documento fornisce indicazioni generali sulla configurazione dei tempi di scadenza per i singoli eventi Experience all’interno di un set di dati Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Scadenza eventi esperienza

In Adobe Experience Platform, puoi configurare i tempi di scadenza per tutti gli eventi Experience che vengono acquisiti in un set di dati abilitato per [Profilo cliente in tempo reale](./home.md). Ciò ti consente di rimuovere automaticamente dall’archivio profili i dati che non sono più validi o utili per i tuoi casi d’uso.

Le scadenze degli eventi di esperienza non possono essere configurate tramite l’interfaccia utente o le API di Platform. Al contrario, devi contattare il supporto per abilitare le scadenze dell’Experience Event sui set di dati richiesti.

>[!IMPORTANT]
>
>Le scadenze degli eventi di esperienza non devono essere confuse con le scadenze dei set di dati, che eliminano l’intero set di dati dopo il raggiungimento della data di scadenza. Sono configurati manualmente tramite [Igiene dei dati Adobe Experience Platform](../hygiene/home.md).

## Processo di scadenza automatizzato

Dopo che le scadenze dell’evento esperienza sono state abilitate in un set di dati abilitato per il profilo, Platform applica automaticamente i valori di scadenza per ogni evento acquisito in un processo in due fasi:

1. Tutti i nuovi dati acquisiti nel set di dati hanno il valore di scadenza applicato al momento dell’acquisizione in base alla marca temporale dell’evento.
1. Tutti i dati esistenti nel set di dati hanno il valore di scadenza applicato retroattivamente come processo di backfill del sistema una tantum. Una volta che il valore di scadenza è stato inserito nel set di dati, gli eventi che sono più vecchi del valore di scadenza verranno eliminati immediatamente non appena il processo di sistema viene eseguito. Tutti gli altri eventi verranno eliminati non appena raggiungono i loro valori di scadenza dalla marca temporale dell’evento.

>[!WARNING]
>
>Una volta applicati, i dati più vecchi del numero di giorni assegnati dal valore di scadenza sono **eliminato definitivamente** e non può essere ripristinato.

Ad esempio, se hai applicato un valore di scadenza di 30 giorni il 15 maggio, si verificheranno i seguenti passaggi:

1. Tutti i nuovi eventi ricevono un valore di scadenza di 30 giorni applicati durante l’acquisizione.
1. Tutti gli eventi esistenti con una marca temporale precedente al 15 aprile vengono eliminati immediatamente con il processo di sistema.
1. Tutti gli eventi esistenti con una marca temporale più recente del 15 aprile hanno un valore di scadenza 30 giorni dopo la marca temporale dell’evento. Quindi, se un evento ha una marca temporale del 18 aprile, viene eliminato 30 giorni dopo la data di tale marca temporale, che sarebbe il 18 maggio.

## Effetti sulla segmentazione

Per mantenere precisi i risultati, devi assicurarti che le finestre di lookback per i segmenti si trovino entro i limiti di scadenza dei set di dati dipendenti. Ad esempio, se applichi un valore di scadenza di 30 giorni e hai un segmento che tenta di visualizzare i dati da un massimo di 45 giorni fa, il pubblico risultante sarà probabilmente impreciso.

Pertanto, dovresti mantenere lo stesso valore di scadenza Experience Event per tutti i set di dati, se possibile, per evitare l’impatto di diversi valori di scadenza tra diversi set di dati nella logica di segmentazione.
