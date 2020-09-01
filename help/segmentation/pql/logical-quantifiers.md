---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: Quantificatori logici
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---


# Funzioni quantificatore logiche

I quantificatori logici possono essere utilizzati per affermare condizioni con array in [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Exists

La `exists` funzione determina l&#39;esistenza di un elemento in un array, a condizione che soddisfi la condizione specificata.

**Formato**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argomento | Descrizione |
| ---------- | ----------- |
| `{VARIABLE}` | Nome di una variabile. |
| `{EXPRESSION}` | Matrice da controllare. |
| `{CONDITION}` | Un&#39;espressione facoltativa che filtra i valori nell&#39;array restituito. |

**Esempio**

La seguente query PQL ottiene tutti gli eventi con un prezzo superiore a $50 o con uno SKU di &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Per tutti

La `forall` funzione determina tutti gli elementi di un array che soddisfano tutte le condizioni specificate.

**Formato**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argomento | Descrizione |
| ---------- | ----------- |
| `{VARIABLE}` | Nome di una variabile. |
| `{EXPRESSION}` | Matrice da controllare. |
| `{CONDITION}` | Un&#39;espressione facoltativa che filtra i valori nell&#39;array restituito. |

**Esempio**

La seguente query PQL ottiene tutti gli eventi con un prezzo superiore a $50 e un SKU pari a &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Passaggi successivi

Ora che hai imparato i quantificatori logici, puoi usarli nelle tue query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
