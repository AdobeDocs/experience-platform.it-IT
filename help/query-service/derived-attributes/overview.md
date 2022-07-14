---
title: Attributi derivati
description: Gli attributi derivati forniscono un mezzo utile per generare attributi a tua scelta che possono essere aggiornati a cadenza regolare ed eventualmente pubblicati nei dati del Profilo cliente in tempo reale. Questo documento fornisce una panoramica sull’utilizzo di Query Service per creare attributi derivati da utilizzare con i dati del profilo.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 61e0895484b8005e2109056d51557f609fecaf97
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Attributi derivati

La funzione degli attributi derivati fornisce un mezzo pratico per generare attributi di tua scelta da altre informazioni disponibili nel data lake. Questi attributi possono essere aggiornati a cadenza regolare ed eventualmente pubblicati nei dati del Profilo cliente in tempo reale. Gli attributi derivati rispondono alla necessità di creare attributi complessi come decile, percentile e quartile su attributi più semplici come max, count e media. Questi attributi possono essere calcolati specificatamente per un singolo utente o per un&#39;entità aziendale. Questo consente di derivare gli attributi che possono essere accreditati direttamente in un identificatore, come indirizzi e-mail, ID dispositivo e numeri di telefono, nonché gli attributi che sono indirettamente associati a tale utente o profilo aziendale.

Gli attributi derivati sono necessari per diversi casi d’uso quando i dati vengono analizzati sul data lake. Questi dati possono quindi essere contrassegnati per l’utilizzo in Profilo cliente in tempo reale e utilizzati in casi d’uso a valle, come la creazione di tipi di pubblico altamente mirati. Alcuni potenziali casi d’uso per questa funzione possono includere:

* Identificare il 10% più basso di abbonati in base al pubblico per canale. In questo modo, gli esperti di marketing possono eseguire il targeting di un pubblico specifico e vendere un nuovo pacchetto di abbonati.
* Identificare un pubblico che si trova nel 10% dei volantini più richiesti in base alle miglia totali percorse e con lo stato di &quot;Flyer&quot;. Questo pubblico potrebbe essere utilizzato per indirizzare in modo selettivo la vendita di una nuova offerta di carta di credito.
* Determina il tasso di abbandono in base alla sottoscrizione.
* Identificare l&#39;1% più alto del reddito familiare in una provincia o in uno stato, e fornire una misura del numero di individui che si sono allontanati da quel gruppo collettivo negli ultimi &quot;n&quot; mesi.

## Attributi derivati complessi

Per creare una classificazione basata su una o più metriche (come ricavi, durata della visualizzazione e così via) su una particolare dimensione (categoria), sono necessari attributi derivati complessi. Decili, quartili e percentili consentono flessibilità e precisione nella classificazione dei dati con attributi derivati.

Un decile è un metodo per suddividere un insieme di dati classificati in 10 parti uguali. Quando i dati sono suddivisi in decile, a ogni riga del set di dati viene assegnato un rango di decile. Ciò consente di ordinare i dati in ordine decrescente o crescente.

Un grado di decile organizza i dati in ordine dal più basso al più alto ed è fatto su una scala da 1 a 10 dove ogni numero successivo corrisponde a un aumento di 10 punti percentuali.

I bucket con decibel rappresentano il numero di gruppi con classifica e vengono utilizzati per assegnare una classificazione a una dimensione (categoria) nel set di dati. Il bucket può essere un numero o un&#39;espressione che restituisce un valore intero positivo per ogni partizione. I bucket non devono avere un valore null.

I quartili vengono utilizzati per dividere la distribuzione per quattro e percentili per 100.

## Attributi derivati analitici

Query Service fornisce funzioni integrate come la sessionizzazione e l’ultimo contatto, tra cui, che è possibile applicare a qualsiasi dato di serie temporale per generare attributi derivati correlati al business. Puoi basare questi attributi derivati analitici su una o più identità ed eventualmente pubblicare i dati in Profilo cliente in tempo reale, se necessario.

Alcuni casi d&#39;uso potenziali per questo tipo di attributo derivato possono includere:

* Tracciamento dei prodotti analizzati durante una sessione utente che non erano disponibili.
* Tracciamento delle metriche più comuni, come le dimensioni, il colore o la categoria di prodotto dei prodotti esaminati o acquistati.
* Tracciamento dell’origine della piattaforma che ha portato a un browser di prodotti o a un acquisto.
* Monitoraggio dell’elemento visualizzato più di recente da un’identità.
* Metriche di tracciamento come il numero medio di elementi in un carrello, l’abbandono del carrello o la frequenza media di acquisto.

## Altri attributi derivati

Puoi anche calcolare le metriche aziendali come attributo derivato e utilizzarle in combinazione con attributi semplici come il codice postale o una metrica aggregata come il conteggio totale. Ad esempio, un conteggio totale basato su una città o una provincia, o un conteggio totale basato su una categoria di business e una città/provincia.

## Passaggi successivi e casi di utilizzo

Leggendo questo documento si ha una migliore comprensione di come gli attributi derivati da Query Service facilitano casi d&#39;uso complessi per massimizzare l&#39;utilità dei dati. Successivamente, devi leggere il [caso di utilizzo di attributi derivati basati su decile](./deciles-use-case.md) per vedere come questa funzione viene applicata in uno scenario reale.
