---
solution: Experience Platform
title: Funzioni di PQL Map
description: Profile Query Language (PQL) offre funzioni per semplificare l’interazione con le mappe.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 6%

---

# Funzioni di mappatura

[!DNL Profile Query Language] (PQL) offre funzioni per semplificare l&#39;interazione con le mappe. Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Ottieni

La funzione `get` viene utilizzata per recuperare il valore di una mappa per una determinata chiave.

**Formato**

```sql
{MAP}.get({STRING})
```

**Esempio**

La seguente query PQL ottiene il valore della mappa identità per la chiave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Chiavi

La funzione `keys` viene utilizzata per recuperare tutte le chiavi per una determinata mappa.

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

La funzione `values` viene utilizzata per recuperare tutti i valori di una determinata mappa.

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

Ora che hai imparato le funzioni mappa, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
