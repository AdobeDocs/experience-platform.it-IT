---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;ora di vita;ttl;time-to-live;
solution: Experience Platform
title: Time-to-live sui set di dati
description: Questo documento fornisce indicazioni generali sul time-to-live (TTL) per i set di dati nell’archivio profili per Adobe Experience Platform.
source-git-commit: 878c04c688268f8cf1850c3e8d40f958a6d2d69b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# Time-to-live (TTL) del servizio profili

Il Servizio profili consente agli utenti di applicare il TTL (time-to-live) ai dati nell’archivio profili. TTL è un meccanismo che limita la quantità di tempo in cui i dati risiedono all’interno di un set di dati. Ciò ti consente di rimuovere automaticamente dall’archivio profili i dati che non sono più utili per i tuoi casi d’uso.

Attualmente, il profilo supporta solo l’opzione TTL dell’evento esperienza.

## TTL Evento esperienza

Il TTL dell’evento esperienza consente di applicare il TTL ai set di dati abilitati per il profilo cliente in tempo reale per rimuovere dall’archivio profili i dati che non sono più validi.

>[!NOTE]
>
>Per abilitare il TTL di Experience Event nei set di dati, contatta il supporto.

Dopo aver abilitato il TTL di Experience Event su un set di dati abilitato per il profilo, Platform applicherà automaticamente il valore di scadenza TTL sui dati di Experience Event in un processo in due fasi:

1. Tutti i nuovi dati acquisiti nel set di dati avranno il valore di scadenza TTL applicato al momento dell’acquisizione.
2. Tutti i dati esistenti nel set di dati avranno il valore di scadenza TTL applicato retroattivamente come processo di backfill del sistema una tantum. Una volta che il valore di scadenza TTL è stato inserito nel set di dati, gli eventi che sono più vecchi del valore di scadenza TTL verranno eliminati immediatamente non appena il processo di sistema viene eseguito. Tutti gli altri eventi verranno eliminati non appena raggiungono i loro valori di scadenza TTL dalla marca temporale dell’evento.

>[!NOTE]
>
>Una volta applicato il TTL, tutti i dati precedenti al numero di giorni del TTL verranno **eliminati in modo permanente** e non potranno essere ripristinati.
> 
>Inoltre, assicurati che l’intervallo di lookback per il segmento sia all’interno del limite TTL. In caso contrario, i risultati del segmento potrebbero diventare errati dopo l’applicazione del TTL. Ad esempio, se applichi un TTL di 30 giorni e avessi un segmento che tentava di visualizzare i dati da un massimo di 45 giorni fa, il segmento genererebbe profili errati.
> 
>Di conseguenza, dovresti mantenere lo stesso TTL per tutti i set di dati, se possibile, per evitare l’impatto di diversi valori TTL tra diversi set di dati nella logica di segmentazione.

Ad esempio, se hai applicato un valore TTL di 30 giorni il 15 maggio, si verificheranno i seguenti passaggi:

1. Per tutti i nuovi eventi viene applicato un valore TTL di 30 giorni durante l’acquisizione.
2. Tutti gli eventi esistenti con una marca temporale precedente al 15 aprile verranno eliminati immediatamente con il processo di sistema.
3. Tutti gli eventi esistenti con una marca temporale più recente del 15 aprile avranno un valore di scadenza TTL 30 giorni dopo la marca temporale dell’evento. Quindi, se un evento ha una marca temporale del 18 aprile, verrà eliminato trenta giorni dopo la data di tale marca temporale, che sarebbe il 18 maggio.

