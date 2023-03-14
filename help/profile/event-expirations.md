---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;durata;ttl;time-to-live;
solution: Experience Platform
title: Scadenze degli eventi esperienza
description: Questo documento fornisce indicazioni generali sulla configurazione dei tempi di scadenza per singoli eventi esperienza all’interno di un set di dati di Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 0fce883528abc62075914abc4a8f81d2bff8f2e6
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Scadenze degli eventi esperienza

In Adobe Experience Platform, puoi configurare i tempi di scadenza per tutti gli eventi esperienza acquisiti in un set di dati abilitato per [Profilo cliente in tempo reale](./home.md). Questo ti consente di rimuovere automaticamente dall’archivio profili i dati che non sono più validi o utili per i tuoi casi d’uso.

Le scadenze degli eventi esperienza non possono essere configurate tramite l’interfaccia utente o le API di Platform. Al contrario, devi contattare il supporto per abilitare le scadenze degli eventi esperienza nei set di dati richiesti.

>[!IMPORTANT]
>
>Le scadenze degli eventi esperienza non devono essere confuse con le scadenze dei set di dati, che eliminano l’intero set di dati dopo il raggiungimento della data di scadenza. Questi vengono configurati manualmente tramite [Igiene dei dati Adobe Experience Platform](../hygiene/home.md).

## Processo di scadenza automatizzato

Dopo aver abilitato le scadenze degli eventi esperienza in un set di dati abilitato per il profilo, Platform applica automaticamente i valori di scadenza per ogni evento acquisito in un processo in due fasi:

1. A tutti i nuovi dati acquisiti nel set di dati viene applicato il valore di scadenza al momento dell’acquisizione in base alla marca temporale dell’evento.
1. A tutti i dati esistenti nel set di dati viene applicato retroattivamente il valore di scadenza come processo di sistema di backfill una tantum. Una volta inserito il valore di scadenza nel set di dati, gli eventi precedenti al valore di scadenza vengono immediatamente eliminati non appena viene eseguito il processo di sistema. Tutti gli altri eventi verranno eliminati non appena raggiungono i valori di scadenza dalla marca temporale dell’evento. Se tutti gli eventi esperienza sono stati rimossi e il profilo non ha più attributi di profilo, questo non esisterà più.

>[!WARNING]
>
>Una volta applicati, tutti i dati precedenti al numero di giorni assegnati dal valore di scadenza sono **eliminato definitivamente** e non possono essere ripristinati.

Ad esempio, se applicassi un valore di scadenza di 30 giorni il 15 maggio, si verificherebbero i seguenti passaggi:

1. A tutti i nuovi eventi viene applicato un valore di scadenza di 30 giorni durante l’acquisizione.
1. Tutti gli eventi esistenti con una marca temporale precedente al 15 aprile vengono eliminati immediatamente con il processo di sistema.
1. Tutti gli eventi esistenti con una marca temporale più recente del 15 aprile hanno un valore di scadenza 30 giorni dopo la marca temporale dell’evento. Quindi, se un evento ha la marca temporale del 18 aprile, viene eliminato 30 giorni dopo la data di tale marca temporale, che sarebbe il 18 maggio.

## Effetti sulla segmentazione

Per mantenere accurati i risultati, è necessario assicurarsi che gli intervalli di lookback per i segmenti rientrino nei limiti di scadenza dei relativi set di dati dipendenti. Ad esempio, se applichi un valore di scadenza di 30 giorni e disponi di un segmento che tenta di visualizzare i dati risalenti a un massimo di 45 giorni fa, il pubblico risultante sarà probabilmente impreciso.

Pertanto, se possibile, devi mantenere lo stesso valore di scadenza dell’evento esperienza per tutti i set di dati, per evitare l’impatto di valori di scadenza diversi tra set di dati diversi nella logica di segmentazione.
