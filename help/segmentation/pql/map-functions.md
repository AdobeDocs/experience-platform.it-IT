---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni mappa;mappa;
solution: Experience Platform
title: Funzioni Mappa PQL
description: Il Profile Query Language (PQL) offre funzioni per facilitare l’interazione con le mappe.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---

# Mappare le funzioni

[!DNL Profile Query Language] (PQL) offre funzioni che facilitano l’interazione con le mappe. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella sezione [[!DNL Profile Query Language] panoramica](./overview.md).

## Ottenere

La `get` viene utilizzata per recuperare il valore di una mappa per una determinata chiave.

**Formato**

```sql
{MAP}.get({STRING})
```

**Esempio**

La seguente query PQL ottiene il valore della mappa di identità per la chiave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Chiavi

La `keys` viene utilizzata per recuperare tutte le chiavi di una determinata mappa.

**Formato**

```sql
{MAP}.keys()
```

**Esempio**

La seguente query PQL ottiene tutte le chiavi per la mappa `identityMap`.

```sql
identityMap.keys()
```

## Valori

La `values` viene utilizzata per recuperare tutti i valori di una data mappa.

**Formato**

```sql
{MAP}.values()
```

**Esempio**

La seguente query PQL ottiene tutti i valori per la mappa `identityMap`.

```sql
identityMap.values()
```

## Passaggi successivi

Dopo aver appreso le funzioni della mappa, puoi utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere il [Panoramica della lingua della query del profilo](./overview.md).
