---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Espressioni PQL di esempio per gli attributi calcolati
topic: guida
type: Documentazione
description: Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni richiedono l'uso di espressioni PQL (Profile Query Language) valide. Questa guida descrive alcune delle espressioni PQL più utilizzate per gli attributi calcolati.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 1%

---


# (Alfa) Espressioni PQL di esempio per gli attributi calcolati

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione. Ogni attributo calcolato è definito con informazioni di base, come un nome e una descrizione, la classe e il percorso dello schema del campo in cui il valore sarà tenuto, e un&#39;espressione, il cui valore calcolato è il valore che si desidera memorizzare nell&#39;attributo calcolato.

Le espressioni utilizzate negli attributi calcolati vengono create utilizzando [!DNL Profile Query Language] (PQL), un linguaggio di query compatibile con Experience Data Model (XDM), progettato per supportare la definizione e l&#39;esecuzione di query per i dati del profilo cliente in tempo reale.

Gli attributi calcolati al momento supportano le seguenti funzioni: sum, count, min, max e booleano. Questa guida descrive alcune delle espressioni PQL più comunemente utilizzate per la definizione degli attributi calcolati per l&#39;organizzazione. Per ulteriori informazioni su PQL e collegamenti ad altre linee guida di formattazione ed esempi di query supportate, visitare la [panoramica PQL](../../segmentation/pql/overview.md).

## Espressioni in streaming

Nella tabella seguente sono riportati i dettagli per le espressioni di query comunemente utilizzate supportate in modalità di streaming.

| Descrizione | Espressione PQL | Tipo di input:<br/>Profilo o Evento esperienza (EE[]) | Tipo di risultato |
|---|---|---|---|
| Conteggio dei download delle immagini negli ultimi 7 giorni. | xEvent[(timestamp &lt; 7 giorni prima di ora), eventType=&quot;download&quot; e contentType = &quot;image&quot;].count() | Profilo ed EE[] | Intero |
| Somma della spesa dei clienti per le merci sportive negli ultimi 7 giorni. | xEvent[(marca temporale si verifica &lt; 7 giorni prima di ora) ed eventType=&quot;transaction&quot; e category = &quot;portali&quot;].sum(commerce.order.priceTotal) | Profilo ed EE[] | Numero intero o doppio |
| Spesa media dei clienti per le merci sportive negli ultimi 7 giorni.<br/><br/>**Nota:** richiede la creazione di tre attributi calcolati. | **ca1:** xEvent[(marca temporale si verifica  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(marca temporale si verifica  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.count()<br/><br/>**ca3:** ca1 / ca2]] | Profilo ed EE[] | Doppio |
| Il cliente ha speso più di 100 dollari per i prodotti sportivi negli ultimi 7 giorni?<br/><br/>**Nota:** richiede la creazione di due attributi calcolati. | **ca1:** xEvent[(marca temporale si verifica  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | Profilo ed EE[] | Booleano |
| Il cliente ha effettuato un acquisto negli ultimi 7 giorni? | chain(xEvent, timestamp, [A: What(eventType = &quot;transaction&quot;) WHEN(&lt; 7 giorni prima di ora)] | Profilo ed EE[] | Booleano |
| Gli utenti più bassi spendono in prodotti sportivi negli ultimi 7 giorni. | xEvent[(marca temporale si verifica &lt; 7 giorni prima di ora) ed eventType=&quot;transaction&quot; e category = &quot;portali&quot;].min(commerce.order.priceTotal) | Profilo ed EE[] | Numero intero o doppio |
| Gli utenti più in alto spendono in prodotti sportivi negli ultimi 7 giorni. | xEvent[(marca temporale si verifica &lt; 7 giorni prima di ora) ed eventType=&quot;transaction&quot; e category = &quot;portali&quot;].max(commerce.order.priceTotal) | Profilo ed EE[] | Numero intero o doppio |
| Numero di download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzati per prodotto. | xEvent[(timestamp che si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()) | Profilo ed EE[] | Map[String, Integer] |
| Somma delle proprietà numeriche sui download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzata per prodotto. | xEvent[(timestamp &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)) | Profilo ed EE[] | Mappa[Stringa, Intero] o Mappa[Stringa, Double] |
| Media delle proprietà numeriche rispetto ai download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzata per prodotto.<br/><br/>**Nota:** richiede la creazione di tre attributi calcolati. | **ca1:** xEvent[(marca temporale si verifica  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(marca temporale si verifica  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map(K, G) => mapEntry(K, G.count())<br/><br/>**ca3:** ca2 / ca1]] | Profilo ed EE[] | Map[String, Double] |
| Minimo di proprietà numerica rispetto ai download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzati per prodotto. | xEvent[(timestamp &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal)) | Profilo ed EE[] | Mappa[Stringa, Intero] o Mappa[Stringa, Double] |
| Massimo di proprietà numeriche rispetto ai download di ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzati per prodotto. | xEvent[(timestamp &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal)) | Profilo ed EE[] | Mappa[Stringa, Intero] o Mappa[Stringa, Double] |
| Espressione numerica sul profilo, non facendo riferimento a eventi. | if(Person.gender = &quot;femmina&quot;, 60, 65) | Profilo | Numero intero o doppio |
| Espressione booleana sul profilo, non facendo riferimento a eventi. | Person.bornYear >= 2000 | Profilo | Booleano |
| Espressione stringa sul profilo, non facendo riferimento a eventi. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Profilo | Stringa |

## Espressioni batch

Nella tabella seguente sono riportati i dettagli delle espressioni di query disponibili solo in modalità batch, il che significa che al momento non sono disponibili in streaming.

| Descrizione | Espressione PQL | Tipo di input:<br/>Profilo o Evento esperienza (EE[]) | Tipo di risultato |
|---|---|---|---|
| Se la somma di espressione numerica nei download dei prodotti negli ultimi 7 giorni supera o meno 100, indicizzata per prodotto. | xEvent[(timestamp che si verifica &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Profilo ed EE[] | Map[String, Boolean] |
| Indica se la media di espressione numerica sui download dei prodotti negli ultimi 7 giorni supera o meno 100, indicizzata per prodotto. | xEvent[(timestamp &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100) | Profilo ed EE[] | Map[String, Boolean] |
| Accumulo di varie metriche per ciascun prodotto scaricato, negli ultimi 7 giorni, indicizzate per prodotto. | xEvent[(timestamp &lt; 7 giorni prima di ora) e eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Profilo ed EE[] | Map[String, Object] dove Object è un tipo XDM personalizzato |