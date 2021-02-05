---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segmentation Service;pql;PQL;Profile Query Language;funzioni varie;misc;'
solution: Experience Platform
title: Funzioni varie PQL
topic: developer guide
description: La seguente funzione è una funzione diversa per la lingua query profilo (PQL, Profile Query Language).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---


# Funzioni varie

La seguente funzione è una funzione diversa per [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Lascia

La funzione `let` consente di memorizzare un&#39;espressione come variabile da utilizzare successivamente in una query.

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

Ora che avete appreso le varie funzioni, potete utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere la [Panoramica del linguaggio di query profilo](./overview.md).
