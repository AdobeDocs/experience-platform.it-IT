---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;pql;PQL;Profile Query Language;filter functions;filter;
solution: Experience Platform
title: Funzioni filtro PQL
description: Le funzioni di filtro vengono utilizzate per filtrare i dati all’interno di array in PQL (Profile Query Language).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# Funzioni filtro

Le funzioni di filtro vengono utilizzate per filtrare i dati all’interno di array in [!DNL Profile Query Language] (PQL) Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Filtro

Il `[]` (filter) consente l’applicazione di filtri a un array e la restituzione di un sottoinsieme dell’array che corrisponde alla condizione specificata.

**Formato**

```sql
{ARRAY}[filter]
```

**Esempio**

La seguente query PQL ottiene tutti gli eventi che hanno almeno un elemento di prodotto con uno SKU uguale a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operatore Up

Il `^` (up) consente di fare riferimento alle proprietà nei livelli superiori dei filtri.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argomento | Descrizione |
| -------- | ----------- |
| `{ARRAY}` | Array che viene filtrato. |
| `{FILTER_1}` | Livello esterno del filtro. |
| `{FILTER_2}` | Livello interno del filtro |
| `^{PROPERTY}` | La proprietà su cui viene filtrato anche. A causa della `^`, sta controllando una proprietà in base al filtro1. |

**Esempio**

La seguente query PQL ottiene tutti gli eventi che hanno almeno un elemento di prodotto con uno SKU uguale a &quot;PS&quot; **o** ha una persona il cui sesso è femminile.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Passaggi successivi

Dopo aver appreso le funzioni filtro, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
