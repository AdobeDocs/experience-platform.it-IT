---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;durata;ttl;time-to-live;
solution: Experience Platform
title: Scadenze degli eventi esperienza
description: Questo documento fornisce indicazioni generali sulla configurazione dei tempi di scadenza per singoli eventi esperienza all’interno di un set di dati di Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '855'
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

Per mantenere accurati i risultati, è necessario assicurarsi che gli intervalli di lookback per i tipi di pubblico rientrino nei limiti di scadenza dei relativi set di dati dipendenti. Ad esempio, se applichi un valore di scadenza di 30 giorni e un pubblico tenta di visualizzare i dati relativi a un massimo di 45 giorni fa, il pubblico risultante potrebbe non essere accurato.

Pertanto, se possibile, devi mantenere lo stesso valore di scadenza dell’evento esperienza per tutti i set di dati, per evitare l’impatto di valori di scadenza diversi tra set di dati diversi nella logica di segmentazione.

## Domande frequenti {#faq}

Nella sezione seguente sono elencate le domande frequenti relative alla scadenza dei dati di Experience Event:

### Quali sono le differenze tra la scadenza dei dati di Experience Event e la scadenza dei dati di profilo pseudonimo?

La scadenza dei dati di Experience Event e la scadenza dei dati del profilo pseudonimo sono funzioni complementari.

#### Granularità

La scadenza dei dati di Experience Event funziona su un **set di dati** livello. Di conseguenza, ogni set di dati può avere un’impostazione di scadenza dati diversa.

La scadenza dei dati del profilo pseudonimo funziona su una **sandbox** livello. Di conseguenza, la scadenza dei dati influirà su tutti i profili nella sandbox.

#### Tipi di identità

La scadenza dei dati dell’evento esperienza rimuove gli eventi **solo** in base alla marca temporale del record evento. Gli spazi dei nomi delle identità inclusi sono **ignorato** a scopo di scadenza.

Scadenza dati profilo pseudonimo **solo** considera i profili con grafici di identità contenenti spazi dei nomi di identità selezionati dal cliente, ad esempio `ECID`, `AAID`, o altri tipi di cookie. Se il profilo contiene **qualsiasi** spazio dei nomi di identità aggiuntivo **non** nell’elenco selezionato del cliente, il profilo **non** essere soppressa.

#### Elementi rimossi

Scadenza dati evento esperienza **solo** rimuove eventi e non **non** rimuovere i dati della classe di profilo. I dati della classe profilo vengono rimossi solo quando tutti i dati vengono rimossi in **tutto** set di dati e sono **no** record della classe di profilo rimanenti per il profilo.

La scadenza dei dati del profilo pseudonimo rimuove **entrambi** record di eventi e profili. Di conseguenza, verranno rimossi anche i dati della classe di profilo.

### In che modo la scadenza dei dati di profilo pseudonimo può essere utilizzata insieme alla scadenza dei dati di Experience Event?

La scadenza dei dati del profilo pseudonimo e la scadenza dei dati dell’evento esperienza possono essere utilizzate per completarsi a vicenda.

Dovresti **sempre** imposta la scadenza dei dati Experience Event nei set di dati, in base alle tue esigenze di conservazione dei dati sui tuoi clienti noti. Una volta impostata la scadenza dei dati di Experience Event, puoi utilizzare la scadenza dei dati di profilo pseudonimo per rimuovere automaticamente i profili pseudonimi. In genere, il periodo di scadenza dei dati per i profili pseudonimi è inferiore al periodo di scadenza dei dati per gli eventi esperienza.

Per un caso d’uso tipico, puoi impostare la scadenza dei dati Experience Event in base ai valori dei dati utente noti e impostare la scadenza dei dati del profilo pseudonimo su una durata molto più breve per limitare l’impatto dei profili pseudonimi sulla conformità della licenza di Platform.
