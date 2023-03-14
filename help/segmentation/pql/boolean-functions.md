---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;pql;PQL;Profile Query Language;boolean functions;boolean;
solution: Experience Platform
title: Funzioni Boolean PQL
description: Le funzioni booleane vengono utilizzate per eseguire la logica booleana su diversi elementi in PQL (Profile Query Language).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# Funzioni booleane

Le funzioni booleane vengono utilizzate per eseguire la logica booleana su elementi diversi in [!DNL Profile Query Language] (PQL)  Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## E

Il `and` per creare una congiunzione logica.

**Formato**

```sql
{QUERY} and {QUERY}
```

**Esempio**

La seguente query PQL restituirà tutte le persone con paese di origine come Canada e anno di nascita 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Oppure

Il `or` viene utilizzata per creare una disgiunzione logica.

**Formato**

```sql
{QUERY} or {QUERY}
```

**Esempio**

La seguente query PQL restituirà tutte le persone con paese di origine come Canada o anno di nascita 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## No

Il `not` (o `!`) viene utilizzata per creare una negazione logica.

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

Il `if` La funzione viene utilizzata per risolvere un&#39;espressione a seconda che una condizione specificata sia vera.

**Formato**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | L’espressione booleana in fase di test. |
| `{TRUE_EXPRESSION}` | Espressione il cui valore verrà utilizzato se `{TEST_EXPRESSION}` è vero. |
| `{FALSE_EXPRESSION}` | Espressione il cui valore verrà utilizzato se `{TEST_EXPRESSION}` è false. |

**Esempio**

La seguente query PQL imposterà il valore come `1` se il paese di origine è il Canada e `2` se il paese di origine non è il Canada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Passaggi successivi

Ora che hai imparato le funzioni booleane, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
