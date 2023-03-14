---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;pql;PQL;Profile Query Language;map functions;map;
solution: Experience Platform
title: Funzioni mappa PQL
description: PQL (Profile Query Language) offre funzioni per semplificare l’interazione con le mappe.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---

# Mappare le funzioni

[!DNL Profile Query Language] (PQL) offre funzioni per semplificare l’interazione con le mappe. Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Ottenere

Il `get` La funzione viene utilizzata per recuperare il valore di una mappa per una determinata chiave.

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

Il `keys` La funzione viene utilizzata per recuperare tutte le chiavi per una data mappa.

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

Il `values` Questa funzione viene utilizzata per recuperare tutti i valori di una data mappa.

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

Ora che hai imparato le funzioni mappa, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
