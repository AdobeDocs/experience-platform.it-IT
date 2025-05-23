---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;durata;ttl;time-to-live;
solution: Experience Platform
title: Scadenze degli eventi esperienza
description: Questo documento fornisce indicazioni generali sulla configurazione dei tempi di scadenza per singoli eventi esperienza all’interno di un set di dati di Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: e85122a0f6acf2f3cb3960d89faa70220692ac23
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# Scadenze degli eventi esperienza

In Adobe Experience Platform puoi configurare i tempi di scadenza per tutti gli eventi esperienza acquisiti in un set di dati abilitato per [Profilo cliente in tempo reale](./home.md). Questo ti consente di rimuovere automaticamente dall’archivio profili i dati che non sono più validi o utili per i tuoi casi d’uso.

Per informazioni su come gestire le scadenze degli eventi esperienza nei set di dati, consulta la [guida dell&#39;interfaccia utente del set di dati](../catalog/datasets/user-guide.md#data-retention-policy).

![Finestra di dialogo che visualizza la conservazione del set di dati e le impostazioni disponibili.](./images/event-expirations/set-data-retention-dialog.png) {width="500" zoomable="yes"}

>[!IMPORTANT]
>
>Le scadenze degli eventi esperienza non devono essere confuse con le scadenze dei set di dati, che eliminano l’intero set di dati dopo il raggiungimento della data di scadenza. Questi sono configurati manualmente tramite [Igiene dei dati di Adobe Experience Platform](../hygiene/home.md).

## Processo di scadenza automatizzato

Dopo aver abilitato le scadenze degli eventi esperienza in un set di dati abilitato per il profilo, Experience Platform applica automaticamente i valori di scadenza per ogni evento acquisito in un processo in due fasi:

1. A tutti i nuovi dati acquisiti nel set di dati viene applicato il valore di scadenza al momento dell’acquisizione in base alla marca temporale dell’evento.
1. A tutti i dati esistenti nel set di dati viene applicato retroattivamente il valore di scadenza come processo di sistema di backfill una tantum. Una volta inserito il valore di scadenza nel set di dati, gli eventi precedenti al valore di scadenza vengono immediatamente eliminati non appena viene eseguito il processo di sistema. Tutti gli altri eventi verranno eliminati non appena raggiungono i valori di scadenza dalla marca temporale dell’evento. Se tutti gli eventi esperienza sono stati rimossi e il profilo non ha più attributi di profilo, questo non esisterà più.

>[!WARNING]
>
>Una volta applicati, i dati precedenti al numero di giorni assegnati dal valore di scadenza sono **eliminati in modo permanente** e non possono essere ripristinati.

Ad esempio, se applicassi un valore di scadenza di 30 giorni il 15 maggio, si verificherebbero i seguenti passaggi:

1. A tutti i nuovi eventi viene applicato un valore di scadenza di 30 giorni durante l’acquisizione.
1. Tutti gli eventi esistenti con una marca temporale precedente al 15 aprile vengono eliminati immediatamente con il processo di sistema.
1. Tutti gli eventi esistenti con una marca temporale più recente del 15 aprile hanno un valore di scadenza 30 giorni dopo la marca temporale dell’evento. Quindi, se un evento ha la marca temporale del 18 aprile, viene eliminato 30 giorni dopo la data di tale marca temporale, che sarebbe il 18 maggio.

## Effetti sulla segmentazione

Per mantenere accurati i risultati, è necessario assicurarsi che gli intervalli di lookback per i tipi di pubblico rientrino nei limiti di scadenza dei relativi set di dati dipendenti. Ad esempio, se applichi un valore di scadenza di 30 giorni e un pubblico tenta di visualizzare i dati relativi a un massimo di 45 giorni fa, il pubblico risultante potrebbe non essere accurato.

Pertanto, se possibile, devi mantenere lo stesso valore di scadenza dell’evento esperienza per tutti i set di dati, per evitare l’impatto di valori di scadenza diversi tra set di dati diversi nella logica di segmentazione.

## Domande frequenti {#faq}

Nella sezione seguente sono elencate le domande frequenti relative alla scadenza dei dati di Experience Event:

### Qual è la durata minima per la quale posso impostare una scadenza dei dati di Experience Event?

La durata minima della scadenza dei dati di un evento esperienza è **un giorno**.

### Quali sono le differenze tra la scadenza dei dati di Experience Event e la scadenza dei dati di profilo pseudonimo?

La scadenza dei dati di Experience Event e la scadenza dei dati del profilo pseudonimo sono funzioni complementari.

#### Granularità

La scadenza dei dati di Experience Event funziona a un livello di **set di dati**. Di conseguenza, ogni set di dati può avere un’impostazione di scadenza dati diversa.

La scadenza dei dati del profilo pseudonimo funziona a un livello **sandbox**. Di conseguenza, la scadenza dei dati influirà su tutti i profili nella sandbox.

#### Tipi di identità

La scadenza dei dati dell&#39;evento esperienza rimuove gli eventi **solo** in base alla marca temporale del record evento. Gli spazi dei nomi di identità inclusi sono **ignorati** a scopo di scadenza.

Scadenza dati profilo pseudonimo **only** considera i profili con grafici di identità contenenti spazi dei nomi di identità selezionati dal cliente, ad esempio `ECID`, `AAID` o altri tipi di cookie. Se il profilo contiene **qualsiasi** spazio dei nomi di identità aggiuntivo **not** nell&#39;elenco selezionato del cliente, il profilo **not** verrà eliminato.

#### Elementi rimossi

La scadenza dei dati di Experience Event **only** rimuove gli eventi e **not** rimuove i dati della classe di profilo. I dati della classe profilo vengono rimossi solo quando tutti i dati vengono rimossi in **tutti** i set di dati e sono presenti **nessun** record della classe profilo rimanenti per il profilo.

La scadenza dei dati del profilo pseudonimo rimuove **sia** record evento che record profilo. Di conseguenza, verranno rimossi anche i dati della classe di profilo.

### In che modo la scadenza dei dati di profilo pseudonimo può essere utilizzata insieme alla scadenza dei dati di Experience Event?

La scadenza dei dati del profilo pseudonimo e la scadenza dei dati dell’evento esperienza possono essere utilizzate per completarsi a vicenda.

Devi **sempre** impostare la scadenza dei dati Experience Event nei set di dati in base alle tue esigenze di conservazione dei dati sui tuoi clienti noti. Una volta impostata la scadenza dei dati di Experience Event, puoi utilizzare la scadenza dei dati di profilo pseudonimo per rimuovere automaticamente i profili pseudonimi. In genere, il periodo di scadenza dei dati per i profili pseudonimi è inferiore al periodo di scadenza dei dati per gli eventi esperienza.

Per un caso d’uso tipico, puoi impostare la scadenza dei dati Experience Event in base ai valori dei dati utente noti e impostare la scadenza dei dati del profilo pseudonimo su una durata molto più breve per limitare l’impatto dei profili pseudonimi sulla conformità della licenza di Experience Platform.
