---
solution: Experience Platform
title: PAL Funzioni aritmetiche
description: Le funzioni aritmetiche vengono utilizzate per eseguire calcoli di base sui valori in Profile Query Language (PQL).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---

# Funzioni aritmetiche

Le funzioni aritmetiche vengono utilizzate per eseguire calcoli di base sui valori in [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Add

La funzione `+` (addizione) viene utilizzata per trovare la somma di due espressioni di argomento come numero.

**Formato**

```sql
{NUMBER} + {NUMBER}
```

**Esempio**

La seguente query PQL somma il prezzo di due prodotti diversi.

```sql
product1.price + product2.price
```

## Moltiplica

La funzione `*` (moltiplicazione) viene utilizzata per trovare il prodotto di due espressioni di argomento come numero.

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

La funzione `-` (sottrazione) viene utilizzata per trovare la differenza di due espressioni di argomento come numero.

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

La funzione `/` (divisione) viene utilizzata per trovare il quoziente di due espressioni di argomento come numero.

**Formato**

```sql
{NUMBER} / {NUMBER}
```

**Esempio**

La seguente query PQL trova il quoziente tra il totale dei prodotti venduti e il totale del denaro guadagnato per visualizzare il costo medio per articolo.

```sql
totalProduct.price / totalProduct.sold
```

## Rimanente

La funzione `%` (modulo/resto) viene utilizzata per trovare il resto dopo aver diviso le due espressioni di argomento come numero.

**Formato**

```sql
{NUMBER} % {NUMBER}
```

**Esempio**

La seguente query PQL controlla se l’età della persona è divisibile di cinque.

```sql
person.age % 5 = 0
```

## Passaggi successivi

Ora che hai imparato le funzioni aritmetiche, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
