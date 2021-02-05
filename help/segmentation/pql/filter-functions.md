---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segmentation Service;pql;PQL;Profile Query Language;filter function;filter;'
solution: Experience Platform
title: Funzioni filtro PQL
topic: developer guide
description: Le funzioni filtro vengono utilizzate per filtrare i dati all'interno degli array in PQL (Profile Query Language).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---


# Funzioni filtro

Le funzioni filtro vengono utilizzate per filtrare i dati all&#39;interno di array in [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Filtro

La funzione `[]` (filter) consente di applicare i filtri a un array e restituisce un sottoinsieme dell&#39;array che corrisponde alla condizione specificata.

**Formato**

```sql
{ARRAY}[filter]
```

**Esempio**

La seguente query PQL ottiene tutti gli eventi che hanno almeno un elemento prodotto con uno SKU uguale a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Up, operatore

L&#39;operatore `^` (su) consente di fare riferimento a proprietà nei livelli superiori dei filtri.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argomento | Descrizione |
| -------- | ----------- |
| `{ARRAY}` | Matrice da filtrare. |
| `{FILTER_1}` | Lo strato esterno del filtro. |
| `{FILTER_2}` | Livello interno del filtro |
| `^{PROPERTY}` | Proprietà su cui viene applicato il filtro. A causa di `^`, sta controllando una proprietà basata su filter1. |

**Esempio**

La seguente query PQL ottiene tutti gli eventi che hanno almeno un elemento prodotto con uno SKU uguale a &quot;PS&quot; **o** con una persona il cui genere è femminile.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Passaggi successivi

Dopo aver appreso le funzioni filtro, potete utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere la [Panoramica del linguaggio di query profilo](./overview.md).
