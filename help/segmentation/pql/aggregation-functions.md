---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni di aggregazione;aggregazione;
solution: Experience Platform
title: Funzioni di aggregazione PQL
description: Le funzioni di aggregazione vengono utilizzate per raggruppare più valori all’interno degli array PQL (Profile Query Language) per creare un singolo valore di riepilogo.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 6%

---

# Funzioni di aggregazione

Le funzioni di aggregazione sono utilizzate per raggruppare più valori all&#39;interno di [!DNL Profile Query Language] (PQL) array per formare un singolo valore di riepilogo. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella sezione [[!DNL Profile Query Language] panoramica](./overview.md).

## Conteggio

La `count` restituisce il numero di elementi all&#39;interno della matrice specificata.

**Formato**

```sql
{ARRAY}.count()
```

**Esempio**

La seguente query PQL restituisce il numero di ordini nell&#39;array.

```sql
orders.count()
```

## Somma

La `sum` restituisce la somma di tutti i valori selezionati all&#39;interno della matrice.

**Formato**

```sql
{ARRAY}.sum()
```

**Esempio**

La seguente query PQL restituisce la somma di tutti i prezzi degli ordini.

```sql
orders.sum(order.price)
```

## Medio

La `average` restituisce la media aritmetica di tutti i valori selezionati all&#39;interno dell&#39;array.

**Formato**

```sql
{ARRAY}.average()
```

**Esempio**

La seguente query PQL restituisce il prezzo medio di tutti gli ordini.

```sql
orders.average(order.price)
```

## Minimo

La `min` restituisce il valore più piccolo tra tutti i valori selezionati all&#39;interno della matrice.

**Formato**

```sql
{ARRAY}.min()
```

**Esempio**

La seguente query PQL restituisce il prezzo più basso di tutti gli ordini.

```sql
orders.min(order.price)
```

## Massimo

La `max` restituisce il valore più grande tra tutti i valori selezionati all&#39;interno dell&#39;array.

**Formato**

```sql
{ARRAY}.max()
```

**Esempio**

La seguente query PQL restituisce il prezzo più alto di tutti gli ordini.

```sql
orders.max(order.price)
```

## Passaggi successivi

Dopo aver appreso le funzioni di aggregazione, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere il [Panoramica della lingua della query del profilo](./overview.md).
