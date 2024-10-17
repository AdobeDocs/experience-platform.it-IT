---
solution: Experience Platform
title: Funzioni filtro PQL
description: Le funzioni di filtro vengono utilizzate per filtrare i dati all’interno di array in Profile Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 7c282594e66c8c7700471a94947448fd91596814
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 2%

---

# Funzioni filtro

Le funzioni di filtro vengono utilizzate per filtrare i dati all&#39;interno di array in [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Filtro

La funzione `[]` (filtro) consente l&#39;applicazione di filtri a un array e la restituzione di un sottoinsieme dell&#39;array corrispondente alla condizione specificata. Di conseguenza, questa funzione restituisce un array.

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

L&#39;operatore `^` (attivo) consente di fare riferimento alle proprietà nei livelli superiori dei filtri.

**Formato**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argomento | Descrizione |
| -------- | ----------- |
| `{ARRAY}` | Array che viene filtrato. |
| `{FILTER_1}` | Livello esterno del filtro. |
| `{FILTER_2}` | Livello interno del filtro |
| `^{PROPERTY}` | La proprietà su cui viene filtrato anche. A causa di `^`, sta controllando una proprietà in base al filtro1. |

**Esempio**

La seguente query PQL ottiene tutti gli eventi che hanno almeno un elemento prodotto con uno SKU uguale a &quot;PS&quot; **o** hanno una persona il cui genere è femmina.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Passaggi successivi

Ora che hai imparato le funzioni filtro, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
