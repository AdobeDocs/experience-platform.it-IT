---
solution: Experience Platform
title: Funzioni di aggregazione PQL
description: Le funzioni di aggregazione vengono utilizzate per raggruppare più valori all’interno di array Profile Query Language (PQL) in modo da formare un unico valore di riepilogo.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---

# Funzioni di aggregazione

Le funzioni di aggregazione vengono utilizzate per raggruppare più valori all&#39;interno di array [!DNL Profile Query Language] (PQL) in modo da formare un unico valore di riepilogo. Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Conteggio

La funzione `count` restituisce il numero di elementi all&#39;interno dell&#39;array specificato come numero.

**Formato**

```sql
{ARRAY}.count()
```

**Esempio**

La query PQL seguente restituisce il numero di ordini nell’array.

```sql
orders.count()
```

## Somma

La funzione `sum` restituisce la somma di tutti i valori selezionati all&#39;interno dell&#39;array come un numero.

**Formato**

```sql
{ARRAY}.sum()
```

**Esempio**

La query PQL seguente restituisce la somma di tutti i prezzi degli ordini.

```sql
orders.sum(order.price)
```

## Medio

La funzione `average` restituisce come numero la media aritmetica di tutti i valori selezionati all&#39;interno dell&#39;array.

**Formato**

```sql
{ARRAY}.average()
```

**Esempio**

La query PQL seguente restituisce il prezzo medio di tutti gli ordini.

```sql
orders.average(order.price)
```

## Minimo

La funzione `min` restituisce come numero il più piccolo di tutti i valori selezionati all&#39;interno dell&#39;array.

**Formato**

```sql
{ARRAY}.min()
```

**Esempio**

La query PQL seguente restituisce il prezzo più basso di tutti gli ordini.

```sql
orders.min(order.price)
```

## Massimo

La funzione `max` restituisce come numero il più grande di tutti i valori selezionati all&#39;interno dell&#39;array.

**Formato**

```sql
{ARRAY}.max()
```

**Esempio**

La query PQL seguente restituisce il prezzo più alto di tutti gli ordini.

```sql
orders.max(order.price)
```

## Passaggi successivi

Ora che hai imparato le funzioni di aggregazione, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
