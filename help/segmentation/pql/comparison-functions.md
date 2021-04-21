---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni di confronto;confronto;
solution: Experience Platform
title: Funzioni di confronto PQL
topic-legacy: developer guide
description: Le funzioni di confronto vengono utilizzate per confrontare espressioni e valori diversi e restituiscono di conseguenza "true" o "false".
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# Funzioni di confronto

Le funzioni di confronto vengono utilizzate per confrontare espressioni e valori diversi e restituiscono `true` o `false` di conseguenza. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## È uguale a

La funzione `=` (equals) controlla se un valore o un&#39;espressione è uguale a un altro valore o espressione.

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

La funzione `!=` (non uguale) controlla se un valore o un&#39;espressione è **non** uguale a un altro valore o espressione.

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

La funzione `>` (maggiore di) viene utilizzata per verificare se il primo valore è maggiore del secondo valore.

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

La funzione `>=` (maggiore o uguale a) viene utilizzata per verificare se il primo valore è maggiore o uguale al secondo valore.

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

La funzione di confronto `<` (minore di) viene utilizzata per verificare se il primo valore è minore del secondo valore.

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

La funzione di confronto `<=` (minore o uguale a) viene utilizzata per verificare se il primo valore è minore o uguale al secondo valore.

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

Ora che hai imparato le funzioni di confronto, puoi utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consulta la [Panoramica di Profile Query Language](./overview.md).
