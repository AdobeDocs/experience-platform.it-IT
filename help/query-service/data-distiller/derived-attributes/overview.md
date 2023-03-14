---
title: Attributi derivati
description: Gli attributi derivati forniscono un mezzo pratico per generare attributi a scelta che possono essere aggiornati a qualsiasi cadenza regolare e facoltativamente pubblicati nei dati del Profilo cliente in tempo reale. Questo documento fornisce una panoramica dell’utilizzo di Query Service per creare attributi derivati da utilizzare con i dati del profilo.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Attributi derivati

La funzione attributi derivati consente di generare attributi a scelta tra le altre informazioni disponibili nel data lake. Questi attributi possono essere aggiornati a qualsiasi cadenza regolare e facoltativamente pubblicati nei dati del Profilo cliente in tempo reale. Gli attributi derivati soddisfano la necessità di creare attributi complessi come decile, percentile e quartile rispetto a quelli più semplici come max, count e mean. Questi attributi possono essere calcolati in modo specifico per un singolo utente o per un’entità aziendale. Questo consente di derivare attributi che possono essere direttamente accreditati a un identificatore, come indirizzi e-mail, ID dispositivo e numeri di telefono, e anche attributi che sono indirettamente associati a tale utente o profilo aziendale.

Gli attributi derivati sono necessari per diversi casi d’uso quando i dati vengono analizzati nel data lake. Questi dati possono quindi essere contrassegnati per l’utilizzo in Real-Time Customer Profile e utilizzati in casi di utilizzo a valle, ad esempio per la creazione di tipi di pubblico altamente mirati. Alcuni potenziali casi d’uso per questa funzione potrebbero includere:

* Identificare il 10% più basso degli abbonati in base al pubblico per canale. Questo consentirebbe agli addetti al marketing di rivolgersi a un determinato pubblico e di vendere un nuovo pacchetto di abbonati.
* Identificare un pubblico che rientra nel 10% dei migliori volantini in base al numero totale di miglia percorse e che ha lo stato di &quot;Volantino&quot;. Questo pubblico potrebbe essere utilizzato per indirizzare in modo selettivo la vendita di una nuova offerta di carta di credito.
* Determina la frequenza di abbandono in base alla sottoscrizione.
* Identificare il primo 1% del reddito familiare in una provincia o in uno stato e fornire una misura del numero di individui che si spostano da quel gruppo collettivo negli ultimi &quot;n&quot; mesi.

## Attributi derivati complessi

Per creare una classificazione basata su una o più metriche (ad esempio ricavi, durata del pubblico e così via) per una particolare dimensione (categoria), sono necessari attributi derivati complessi. I decili, i quartili e i percentili consentono flessibilità e precisione durante la classificazione dei dati con attributi derivati.

Un decile è un metodo per suddividere un set di dati classificati in 10 parti uguali. Quando i dati sono divisi in decili, a ogni riga del set di dati viene assegnato un livello decile. Questo consente di ordinare i dati in ordine decrescente o crescente.

Un livello decile dispone i dati in ordine dal più basso al più alto e viene eseguito su una scala da 1 a 10 dove ogni numero successivo corrisponde a un aumento di 10 punti percentuali.

I bucket di decile rappresentano il numero di gruppi classificati e vengono utilizzati per assegnare una classificazione a una dimensione (categoria) nel set di dati. Il bucket può essere un numero o un’espressione che restituisce un valore intero positivo per ogni partizione. I bucket non devono avere un valore null.

I quartili vengono utilizzati per dividere la distribuzione per quattro e percentili per 100.

## Attributi derivati analitici

Query Service fornisce funzioni incorporate, tra cui sessionizzazione e ultimo contatto, che è possibile applicare a qualsiasi serie temporale per generare attributi derivati correlati al business. Puoi basare questi attributi derivati analitici su una o più identità e, facoltativamente, pubblicare i dati su Real-Time Customer Profile se necessario.

Alcuni potenziali casi d’uso per questo tipo di attributo derivato possono includere:

* Tracciamento dei prodotti analizzati durante una sessione utente che erano esauriti.
* Tracciamento delle metriche più comuni, ad esempio dimensioni, colore o categoria di prodotto dei prodotti visualizzati o acquistati.
* Tracciamento dell’origine della piattaforma che ha portato alla navigazione o all’acquisto di un prodotto.
* Tracciamento dell’elemento visualizzato più di recente per identità.
* Metriche di tracciamento come il numero medio di elementi in un carrello, l’abbandono del carrello o la frequenza media di acquisto.

## Altri attributi derivati

Puoi anche calcolare le metriche aziendali come attributo derivato e utilizzarle insieme ad attributi semplici come il codice postale o una metrica aggregata come il conteggio totale. Ad esempio, un conteggio totale basato su una città o una provincia oppure un conteggio totale basato su una categoria aziendale e una città/provincia.

## Passaggi successivi e casi d’uso

La lettura di questo documento consente di comprendere meglio in che modo gli attributi derivati da Query Service facilitano casi d’uso complessi per massimizzare l’utilità dei dati. Quindi, dovresti leggere [caso di utilizzo di attributi derivati basati su decile](../../use-cases/deciles-use-case.md) per vedere come questa funzione viene applicata in uno scenario reale.
