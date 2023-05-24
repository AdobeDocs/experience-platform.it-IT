---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Espressioni PQL di esempio per attributi calcolati
type: Documentation
description: Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento negli attributi a livello di profilo. Queste funzioni richiedono l’utilizzo di espressioni PQL (Profile Query Language) valide. Questa guida illustra alcune delle espressioni PQL più comunemente utilizzate per gli attributi calcolati.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alfa) Espressioni PQL di esempio per attributi calcolati

>[!IMPORTANT]
>
>La funzionalità degli attributi calcolati è attualmente in formato alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione. Ogni attributo calcolato viene definito con informazioni di base, ad esempio un nome e una descrizione, la classe dello schema e il percorso del campo in cui verrà memorizzato il valore e un&#39;espressione, il cui valore calcolato è il valore che si desidera memorizzare nell&#39;attributo calcolato.

Le espressioni utilizzate negli attributi calcolati vengono create utilizzando [!DNL Profile Query Language] (PQL), un linguaggio di query conforme a Experience Data Model (XDM) progettato per supportare la definizione e l’esecuzione di query per i dati del profilo cliente in tempo reale.

Gli attributi calcolati supportano attualmente le seguenti funzioni: sum, count, min, max e boolean. Questa guida descrive alcune delle espressioni PQL più comunemente utilizzate per definire gli attributi calcolati dell’organizzazione. Per ulteriori informazioni su PQL e collegamenti a ulteriori linee guida sulla formattazione e esempi di query supportate, visita [Panoramica di PQL](../../segmentation/pql/overview.md).

## Espressioni di streaming

La tabella seguente fornisce i dettagli delle espressioni di query di uso comune supportate nella modalità di streaming.

| Descrizione | Espressione PQL | Tipo di input:<br/>Evento profilo o esperienza (EE[]) | Tipo di risultato |
|---|---|---|---|
| Numero di download di immagini negli ultimi 7 giorni. | xEvent[(la marca temporale precede di &lt; 7 giorni), eventType=&quot;download&quot; e contentType = &quot;image&quot;].count() | Profilo e EE[] | Intero |
| Somma della spesa del cliente per articoli sportivi negli ultimi 7 giorni. | xEvent[(la marca temporale è &lt; 7 giorni prima di ora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal) | Profilo e EE[] | Intero o doppio |
| Spesa media del cliente per articoli sportivi negli ultimi 7 giorni.<br/><br/>**Nota:** Richiede la creazione di tre attributi calcolati. | **ca1:** xEvent[(la marca temporale è &lt; 7 giorni prima di ora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(la marca temporale è &lt; 7 giorni prima di ora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].count()<br/><br/>**ca3:** ca1 / ca2 | Profilo e EE[] | Doppio |
| Il cliente ha speso più di 100 dollari in articoli sportivi negli ultimi 7 giorni?<br/><br/>**Nota:** Richiede la creazione di due attributi calcolati. | **ca1:** xEvent[(la marca temporale è &lt; 7 giorni prima di ora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | Profilo e EE[] | Booleano |
| Il cliente ha effettuato un acquisto negli ultimi 7 giorni? | chain(xEvent, timestamp, [A: WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7 giorni prima di ora)]) | Profilo e EE[] | Booleano |
| Spesa minima degli utenti per articoli sportivi negli ultimi 7 giorni. | xEvent[(la marca temporale è &lt; 7 giorni prima di ora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].min(commerce.order.priceTotal) | Profilo e EE[] | Intero o doppio |
| La spesa più elevata per gli articoli sportivi negli ultimi 7 giorni. | xEvent[(la marca temporale è &lt; 7 giorni prima di ora) e eventType=&quot;transaction&quot; e category = &quot;sporting goods&quot;].max(commerce.order.priceTotal) | Profilo e EE[] | Intero o doppio |
| Numero di download di ciascun prodotto scaricato negli ultimi 7 giorni, indicizzato per prodotto. | xEvent[(la marca temporale precede di &lt; 7 giorni) ed eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Profilo e EE[] | Mappa[Stringa, Numero intero] |
| Somma delle proprietà numeriche sui download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzati per prodotto. | xEvent[(la marca temporale precede di &lt; 7 giorni) ed eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))) | Profilo e EE[] | Mappa[Stringa, Numero intero] o mappa[Stringa, Doppia] |
| Media delle proprietà numeriche rispetto ai download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzate per prodotto.<br/><br/>**Nota:** Richiede la creazione di tre attributi calcolati. | **ca1:** xEvent[(la marca temporale precede di &lt; 7 giorni) ed eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(la marca temporale precede di &lt; 7 giorni) ed eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()))<br/><br/>**ca3:** ca2/ca1 | Profilo e EE[] | Mappa[Stringa, Doppia] |
| Numero minimo di proprietà numeriche sui download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzate per prodotto. | xEvent[(la marca temporale precede di &lt; 7 giorni) ed eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal))) | Profilo e EE[] | Mappa[Stringa, Numero intero] o mappa[Stringa, Doppia] |
| Numero massimo di proprietà numeriche sui download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzate per prodotto. | xEvent[(la marca temporale precede di &lt; 7 giorni) ed eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal))) | Profilo e EE[] | Mappa[Stringa, Numero intero] o mappa[Stringa, Doppia] |
| Espressione numerica nel profilo, senza riferimenti a eventi. | if(person.gender = &quot;female&quot;, 60, 65) | Profilo | Intero o doppio |
| Espressione booleana sul profilo, senza riferimenti a eventi. | person.bornYear >= 2000 | Profilo | Booleano |
| Espressione stringa nel profilo, senza riferimenti a eventi. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Profilo | Stringa |

## Espressioni batch

Nella tabella seguente vengono forniti i dettagli delle espressioni di query disponibili solo in modalità batch, ovvero non attualmente disponibili in streaming.

| Descrizione | Espressione PQL | Tipo di input:<br/>Evento profilo o esperienza (EE[]) | Tipo di risultato |
|---|---|---|---|
| Indica se la somma delle espressioni numeriche nei download dei prodotti degli ultimi 7 giorni supera o meno i 100, indicizzata per prodotto. | xEvent[(la marca temporale precede di &lt; 7 giorni) ed eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Profilo e EE[] | Mappa[Stringa, Booleano] |
| Indica se la media delle espressioni numeriche nei download dei prodotti degli ultimi 7 giorni supera o meno i 100, indicizzate per prodotto. | xEvent[(la marca temporale precede di &lt; 7 giorni) ed eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Profilo e EE[] | Mappa[Stringa, Booleano] |
| Accumulo di varie metriche per ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzate per prodotto. | xEvent[(la marca temporale precede di &lt; 7 giorni) ed eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)})) | Profilo e EE[] | Mappa[Stringa, Oggetto] dove Object è un tipo XDM personalizzato |
