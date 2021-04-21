---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Espressioni PQL di esempio per gli attributi calcolati
topic-legacy: guide
type: Documentation
description: Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Queste funzioni richiedono l’uso di espressioni PQL (Profile Query Language) valide. Questa guida descrive alcune delle espressioni PQL più comunemente utilizzate per gli attributi calcolati.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 1%

---

# (Alfa) Espressioni PQL di esempio per gli attributi calcolati

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione. Ogni attributo calcolato viene definito con informazioni di base, ad esempio un nome e una descrizione, la classe di schema e il percorso del campo in cui verrà tenuto il valore, e un&#39;espressione il cui valore calcolato è il valore che si desidera memorizzare nell&#39;attributo calcolato.

Le espressioni utilizzate negli attributi calcolati vengono create utilizzando [!DNL Profile Query Language] (PQL), un linguaggio di query conforme a Experience Data Model (XDM) progettato per supportare la definizione e l’esecuzione di query per i dati del profilo cliente in tempo reale.

Gli attributi calcolati supportano attualmente le seguenti funzioni: sum, count, min, max e booleano. Questa guida illustra alcune delle espressioni PQL più comunemente utilizzate che puoi utilizzare quando definisci i tuoi attributi calcolati per la tua organizzazione. Per ulteriori informazioni su PQL e collegamenti ad ulteriori linee guida di formattazione e esempi di query supportate, visita la [Panoramica PQL](../../segmentation/pql/overview.md).

## Espressioni in streaming

La tabella seguente fornisce dettagli sulle espressioni di query comunemente utilizzate supportate in modalità streaming.

| Descrizione | Espressione PQL | Tipo di input:<br/>Profilo o evento esperienza (EE[]) | Tipo di risultato |
|---|---|---|---|
| Numero di download delle immagini negli ultimi 7 giorni. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot; e contentType = &quot;image&quot;].count() | Profilo ed EE[] | Intero |
| Somma della spesa dei clienti per i prodotti sportivi negli ultimi 7 giorni. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;transaction&quot; e category = &quot;sporting Goods&quot;].sum(commerce.order.priceTotal) | Profilo ed EE[] | Intero o doppio |
| Spesa media dei clienti per prodotti sportivi negli ultimi 7 giorni.<br/><br/>**Nota:** richiede la creazione di tre attributi calcolati. | **ca1:** xEvent[ (la marca temporale si verifica  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(la marca temporale si verifica  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.count()<br/><br/>**ca3:** ca1 / ca2]] | Profilo ed EE[] | Doppio |
| Il cliente ha speso più di 100 dollari per articoli sportivi negli ultimi 7 giorni?<br/><br/>**Nota:** richiede la creazione di due attributi calcolati. | **ca1:** xEvent[ (la marca temporale si verifica  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | Profilo ed EE[] | Booleano |
| Il cliente ha effettuato un acquisto negli ultimi 7 giorni? | chain(xEvent, timestamp, [A: What(eventType = &quot;transaction&quot;) WHEN(&lt; 7 giorni prima di ora)]) | Profilo ed EE[] | Booleano |
| Gli utenti più bassi spendono in prodotti sportivi negli ultimi 7 giorni. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;transaction&quot; e category = &quot;sporting Goods&quot;].min(commerce.order.priceTotal) | Profilo ed EE[] | Intero o doppio |
| La spesa più elevata degli utenti per i prodotti sportivi negli ultimi 7 giorni. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;transaction&quot; e category = &quot;sporting Goods&quot;].max(commerce.order.priceTotal) | Profilo ed EE[] | Intero o doppio |
| Numero di download di ogni prodotto scaricato, negli ultimi 7 giorni, indicizzati per prodotto. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Profilo ed EE[] | Mappa[Stringa, Intero] |
| Somma delle proprietà numeriche rispetto ai download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzata per prodotto. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))) | Profilo ed EE[] | Mappa[Stringa, Intero] o Mappa[Stringa, Doppio] |
| Media delle proprietà numeriche rispetto ai download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzata per prodotto.<br/><br/>**Nota:** richiede la creazione di tre attributi calcolati. | **ca1:** xEvent[(timestamp exists  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))))<br/><br/>**ca2:** xEvent[(timestamp before  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.count())<br/><br/>**ca3:** ca2 / ca1]] | Profilo ed EE[] | Map[Stringa, Double] |
| Minimo della proprietà numerica rispetto ai download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzato per prodotto. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal))) | Profilo ed EE[] | Mappa[Stringa, Intero] o Mappa[Stringa, Doppio] |
| Massimo della proprietà numerica rispetto ai download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzato per prodotto. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal))) | Profilo ed EE[] | Mappa[Stringa, Intero] o Mappa[Stringa, Doppio] |
| Espressione numerica nel profilo, senza riferimento a eventi. | if(person.gender = &quot;femmina&quot;, 60, 65) | Profilo | Intero o doppio |
| Espressione booleana nel profilo, senza riferimento a eventi. | person.bornYear >= 2000 | Profilo | Booleano |
| Espressione stringa sul profilo, senza riferimento a eventi. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Profilo | Stringa |

## Espressioni batch

La tabella seguente fornisce dettagli sulle espressioni di query disponibili solo in modalità batch, il che significa che non sono attualmente disponibili in streaming.

| Descrizione | Espressione PQL | Tipo di input:<br/>Profilo o evento esperienza (EE[]) | Tipo di risultato |
|---|---|---|---|
| Se la somma di espressioni numeriche rispetto ai download dei prodotti negli ultimi 7 giorni supera o meno 100, indicizzata per prodotto. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Profilo ed EE[] | Mappa[Stringa, booleano] |
| Se la media di espressioni numeriche rispetto ai download dei prodotti negli ultimi 7 giorni supera o meno 100, indicizzata per prodotto. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Profilo ed EE[] | Mappa[Stringa, booleano] |
| Cumulo di varie metriche per ogni prodotto scaricato, negli ultimi 7 giorni, indicizzato per prodotto. | xEvent[(la marca temporale si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Profilo ed EE[] | Map[String, Object] dove Object è un tipo XDM personalizzato |
