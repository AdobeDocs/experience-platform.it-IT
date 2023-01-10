---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni di confronto;confronto;
solution: Experience Platform
title: Funzioni di confronto PQL
description: Le funzioni di confronto vengono utilizzate per confrontare espressioni e valori diversi e restituiscono di conseguenza "true" o "false".
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# Funzioni di confronto

Le funzioni di confronto vengono utilizzate per confrontare espressioni e valori diversi e restituiscono `true` o `false` di conseguenza. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella sezione [[!DNL Profile Query Language] panoramica](./overview.md).

## È uguale a

La `=` (equals) controlla se un valore o un&#39;espressione è uguale a un altro valore o espressione.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Esempio**

La seguente query PQL controlla se il paese dell&#39;indirizzo di origine è in Canada.

```sql
homeAddress.countryISO = "CA"
```

## Non uguale

La `!=` (diverso da uguale) controlla se un valore o un&#39;espressione è **not** uguale a un altro valore o espressione.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Esempio**

La seguente query PQL controlla se il paese dell&#39;indirizzo di origine non è in Canada.

```sql
homeAddress.countryISO != "CA"
```

## Maggiore di

La `>` (maggiore di) viene utilizzato per verificare se il primo valore è maggiore del secondo valore.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone i cui compleanni non rientrano in gennaio o febbraio.

```sql
person.birthMonth > 2
```

## Maggiore o uguale a

La `>=` (maggiore o uguale a) viene utilizzato per verificare se il primo valore è maggiore o uguale al secondo valore.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone i cui compleanni non rientrano in gennaio o febbraio.

```sql
person.birthMonth >= 3
```

## Minore di

La `<` (minore di) la funzione di confronto viene utilizzata per verificare se il primo valore è minore del secondo valore.

**Formato**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone il cui compleanno è a gennaio.

```sql
person.birthMonth < 2
```

## Minore o uguale a

La `<=` (minore o uguale a) la funzione di confronto viene utilizzata per verificare se il primo valore è minore o uguale al secondo valore.

**Formato**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone il cui compleanno è in gennaio o febbraio.

```sql
person.birthMonth <= 2
```

## Passaggi successivi

Ora che hai imparato le funzioni di confronto, puoi utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere il [Panoramica della lingua della query del profilo](./overview.md).
