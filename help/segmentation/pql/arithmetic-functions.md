---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;arithmetic functions;arithmetic;
solution: Experience Platform
title: Funzioni aritmetiche
topic: developer guide
description: Le funzioni aritmetiche vengono utilizzate per eseguire calcoli di base sui valori in PQL (Profile Query Language).
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---


# Funzioni aritmetiche

Le funzioni aritmetiche vengono utilizzate per eseguire calcoli di base sui valori in [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Add

La funzione `+` (addizione) viene utilizzata per trovare la somma di due espressioni di argomento.

**Formato**

```sql
{NUMBER} + {NUMBER}
```

**Esempio**

La seguente query PQL riporta il prezzo di due prodotti diversi.

```sql
product1.price + product2.price
```

## Moltiplica

La funzione `*` (moltiplicazione) viene utilizzata per trovare il prodotto di due espressioni di argomento.

**Formato**

```sql
{NUMBER} * {NUMBER}
```

**Esempio**

La seguente query PQL trova il prodotto dell&#39;inventario e il prezzo di un prodotto per trovare il valore lordo del prodotto.

```sql
product.inventory * product.price
```

## Sottrai

La funzione `-` (sottrazione) viene utilizzata per trovare la differenza tra due espressioni di argomento.

**Formato**

```sql
{NUMBER} - {NUMBER}
```

**Esempio**

La seguente query PQL rileva la differenza di prezzo tra due prodotti diversi.

```sql
product1.price - product2.price
```

## Dividi

La funzione `/` (divisione) viene utilizzata per trovare il quoziente tra due espressioni di argomento.

**Formato**

```sql
{NUMBER} / {NUMBER}
```

**Esempio**

La seguente query PQL trova il quoziente tra il totale dei prodotti venduti e il totale dei soldi guadagnati per vedere il costo medio per articolo.

```sql
totalProduct.price / totalProduct.sold
```

## Resto

La funzione `%` (modulo/rest) viene utilizzata per trovare il resto dopo la divisione delle due espressioni di argomento.

**Formato**

```sql
{NUMBER} % {NUMBER}
```

**Esempio**

La seguente query PQL verifica se l&#39;età della persona è divisibile per cinque anni.

```sql
person.age % 5 = 0
```

## Passaggi successivi

Ora che avete imparato le funzioni aritmetiche, potete usarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
