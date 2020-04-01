---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni varie
topic: developer guide
translation-type: tm+mt
source-git-commit: d7ec6240864916d3b54db8bd641f4917a38f9480

---


# Funzioni varie

La seguente funzione è una funzione diversa per la lingua query profilo (PQL, Profile Query Language). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella panoramica [Lingua query](./overview.md)profilo.

## Lascia

La `let` funzione consente di memorizzare un&#39;espressione come variabile da utilizzare successivamente in una query.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Esempio**

La seguente query PQL ottiene tutte le somme dei totali di prodotto con la transazione in USD, dove la somma è maggiore di $100 e inferiore a $1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Passaggi successivi

Ora che avete appreso le varie funzioni, potete utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
