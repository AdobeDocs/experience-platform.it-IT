---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni booleane;booleano;
solution: Experience Platform
title: Funzioni booleane PQL
topic-legacy: developer guide
description: Le funzioni booleane vengono utilizzate per eseguire la logica booleana su diversi elementi in Profile Query Language (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# Funzioni booleane

Le funzioni booleane vengono utilizzate per eseguire la logica booleana su diversi elementi in [!DNL Profile Query Language] (PQL).  Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## E

La funzione `and` viene utilizzata per creare una congiunzione logica.

**Formato**

```sql
{QUERY} and {QUERY}
```

**Esempio**

La seguente query PQL restituirà tutte le persone con il paese di origine come Canada e l&#39;anno di nascita del 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Oppure

La funzione `or` viene utilizzata per creare una disgiunzione logica.

**Formato**

```sql
{QUERY} or {QUERY}
```

**Esempio**

La seguente query PQL restituirà tutte le persone con il paese di origine come Canada o l&#39;anno di nascita del 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Non

La funzione `not` (o `!`) viene utilizzata per creare una negazione logica.

**Formato**

```sql
not ({QUERY})
!({QUERY})
```

**Esempio**

La seguente query PQL restituirà tutte le persone che non hanno il proprio paese di origine come Canada.

```sql
not (homeAddress.countryISO = "CA")
```

## Se

La funzione `if` viene utilizzata per risolvere un&#39;espressione a seconda che una condizione specificata sia vera o meno.

**Formato**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | Espressione booleana in fase di test. |
| `{TRUE_EXPRESSION}` | L&#39;espressione il cui valore verrà utilizzato se `{TEST_EXPRESSION}` è true. |
| `{FALSE_EXPRESSION}` | L&#39;espressione il cui valore verrà utilizzato se `{TEST_EXPRESSION}` è false. |

**Esempio**

La seguente query PQL imposta il valore come `1` se il paese di origine è Canada e `2` se il paese di origine non è Canada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Passaggi successivi

Dopo aver appreso le funzioni booleane, puoi utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consulta la [Panoramica di Profile Query Language](./overview.md).
