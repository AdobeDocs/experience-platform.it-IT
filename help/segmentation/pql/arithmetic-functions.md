---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni aritmetiche;aritmetica;
solution: Experience Platform
title: Funzioni aritmetiche PAL
description: Le funzioni aritmetiche vengono utilizzate per eseguire calcoli di base sui valori in Profile Query Language (PQL).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# Funzioni aritmetiche

Le funzioni aritmetiche vengono utilizzate per eseguire calcoli di base sui valori in [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella sezione [[!DNL Profile Query Language] panoramica](./overview.md).

## Add

La `+` (aggiunta) viene utilizzata per trovare la somma di due espressioni di argomento.

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

La `*` (moltiplicazione) viene utilizzata per trovare il prodotto di due espressioni di argomento.

**Formato**

```sql
{NUMBER} * {NUMBER}
```

**Esempio**

La seguente query PQL individua il prodotto dell&#39;inventario e il prezzo di un prodotto per trovare il valore lordo del prodotto.

```sql
product.inventory * product.price
```

## Sottrai

La `-` (sottrazione) viene utilizzata per trovare la differenza tra due espressioni di argomento.

**Formato**

```sql
{NUMBER} - {NUMBER}
```

**Esempio**

La seguente query PQL trova la differenza di prezzo tra due prodotti diversi.

```sql
product1.price - product2.price
```

## Dividi

La `/` (divisione) viene utilizzato per trovare il quoziente di due espressioni di argomento.

**Formato**

```sql
{NUMBER} / {NUMBER}
```

**Esempio**

La seguente query PQL trova il quoziente tra il totale dei prodotti venduti e il totale del denaro guadagnato per vedere il costo medio per articolo.

```sql
totalProduct.price / totalProduct.sold
```

## Resto

La `%` (modulo/rest) viene utilizzato per trovare il resto dopo aver diviso le due espressioni di argomento.

**Formato**

```sql
{NUMBER} % {NUMBER}
```

**Esempio**

La seguente query PQL controlla se l&#39;età della persona è divisibile per cinque anni.

```sql
person.age % 5 = 0
```

## Passaggi successivi

Ora che hai imparato le funzioni aritmetiche, puoi utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere il [Panoramica della lingua della query del profilo](./overview.md).
