---
solution: Experience Platform
title: Funzioni varie di PQL
description: La funzione seguente è una funzione varia per Profile Query Language (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# Funzioni varie

La funzione seguente è una funzione varia per [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Let

La funzione `let` consente di archiviare un&#39;espressione come variabile da utilizzare successivamente in una query.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Esempio**

La seguente query PQL ottiene tutte le somme dei totali dei prodotti con la transazione in USD dove la somma è maggiore di 100 $ e minore di 1000 $.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Passaggi successivi

Dopo aver appreso le varie funzioni, è possibile utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
