---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni filtro;filtro;
solution: Experience Platform
title: Funzioni filtro PQL
description: Le funzioni filtro vengono utilizzate per filtrare i dati all’interno degli array in Profile Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# Funzioni filtro

Le funzioni filtro vengono utilizzate per filtrare i dati all’interno degli array in [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella sezione [[!DNL Profile Query Language] panoramica](./overview.md).

## Filtro

La `[]` (filter) consente l&#39;applicazione di filtri a una matrice e restituisce un sottoinsieme della matrice corrispondente alla condizione specificata.

**Formato**

```sql
{ARRAY}[filter]
```

**Esempio**

La seguente query PQL ottiene tutti gli eventi che hanno almeno un elemento di prodotto con una SKU uguale a &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Operatore Up

La `^` (su) ti consente di fare riferimento alle proprietà nei livelli superiori dei filtri.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argomento | Descrizione |
| -------- | ----------- |
| `{ARRAY}` | Matrice filtrata. |
| `{FILTER_1}` | Livello esterno del filtro. |
| `{FILTER_2}` | Lo strato interno del filtro |
| `^{PROPERTY}` | Proprietà su cui viene applicato il filtro. A causa del `^`, sta controllando una proprietà basata su filter1. |

**Esempio**

La seguente query PQL ottiene tutti gli eventi che hanno almeno un elemento prodotto con una SKU uguale a &quot;PS&quot; **o** avere una persona il cui genere è femminile.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Passaggi successivi

Dopo aver appreso le funzioni del filtro, puoi utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere il [Panoramica della lingua della query del profilo](./overview.md).
