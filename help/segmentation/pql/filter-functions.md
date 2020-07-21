---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni filtro
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 4%

---


# Funzioni filtro

Le funzioni filtro vengono utilizzate per filtrare i dati all&#39;interno di array in [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella panoramica [Lingua query](./overview.md)profilo.

## Filtro

La funzione `[]` (filtro) consente l&#39;applicazione di filtri a un array e restituisce un sottoinsieme dell&#39;array che corrisponde alla condizione specificata.

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

L&#39;operatore `^` (up) consente di fare riferimento a proprietà nei livelli superiori dei filtri.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argomento | Descrizione |
| -------- | ----------- |
| `{ARRAY}` | Matrice da filtrare. |
| `{FILTER_1}` | Lo strato esterno del filtro. |
| `{FILTER_2}` | Livello interno del filtro |
| `^{PROPERTY}` | Proprietà su cui viene applicato il filtro. A causa di `^`, controlla una proprietà basata su filter1. |

**Esempio**

La seguente query PQL ottiene tutti gli eventi che hanno almeno un elemento prodotto con uno SKU uguale a &quot;PS&quot; **o hanno** una persona il cui genere è femminile.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Passaggi successivi

Dopo aver appreso le funzioni filtro, potete utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
