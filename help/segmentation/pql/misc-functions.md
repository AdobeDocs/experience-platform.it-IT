---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni varie;varie;varie;
solution: Experience Platform
title: Funzioni varie PQL
topic-legacy: developer guide
description: La funzione seguente è una funzione diversa per Profile Query Language (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# Funzioni varie

La funzione seguente è una funzione vari per [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Lasciare

La funzione `let` consente di memorizzare un’espressione come variabile da utilizzare successivamente in una query.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Esempio**

La seguente query PQL ottiene tutte le somme dei totali di prodotto con la transazione in USD dove la somma è maggiore di $100 e inferiore a $1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Passaggi successivi

Dopo aver appreso le varie funzioni, è possibile utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consulta la [Panoramica di Profile Query Language](./overview.md).
