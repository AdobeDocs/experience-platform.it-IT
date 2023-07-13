---
solution: Experience Platform
title: PAL Funzioni aritmetiche
description: Le funzioni aritmetiche vengono utilizzate per eseguire calcoli di base sui valori in PQL (Profile Query Language).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 6%

---

# Funzioni aritmetiche

Le funzioni aritmetiche vengono utilizzate per eseguire calcoli di base sui valori in [!DNL Profile Query Language] (PQL) Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Add

Il `+` (addizione) viene utilizzata per trovare la somma di due espressioni di argomento.

**Formato**

```sql
{NUMBER} + {NUMBER}
```

**Esempio**

La query PQL seguente somma il prezzo di due prodotti diversi.

```sql
product1.price + product2.price
```

## Moltiplica

Il `*` (moltiplicazione) viene utilizzata per trovare il prodotto di due espressioni di argomento.

**Formato**

```sql
{NUMBER} * {NUMBER}
```

**Esempio**

La query PQL seguente individua il prodotto dell&#39;inventario e il prezzo di un prodotto per trovare il valore lordo del prodotto.

```sql
product.inventory * product.price
```

## Sottrai

Il `-` (sottrazione) viene utilizzata per trovare la differenza tra due espressioni di argomento.

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

Il `/` (divisione) viene utilizzata per trovare il quoziente di due espressioni di argomento.

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

Il `%` (modulo/resto) viene utilizzata per trovare il resto dopo aver diviso le due espressioni di argomento.

**Formato**

```sql
{NUMBER} % {NUMBER}
```

**Esempio**

La seguente query PQL verifica se l’età della persona è divisibile di cinque.

```sql
person.age % 5 = 0
```

## Passaggi successivi

Ora che hai imparato le funzioni aritmetiche, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
