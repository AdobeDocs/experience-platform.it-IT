---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;quantificatori logici;quantificatore logico;
solution: Experience Platform
title: Quantificatori logici PQL
topic-legacy: developer guide
description: I quantificatori logici possono essere utilizzati per asserire condizioni con gli array in Profile Query Language (PQL).
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---

# Funzioni quantificatore logico

I quantificatori logici possono essere utilizzati per asserire condizioni con array in [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Esiste

La funzione `exists` determina l&#39;esistenza di un elemento in una matrice, purché soddisfi la condizione specificata.

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

La seguente query PQL ottiene tutti gli eventi con un prezzo superiore a $50 o con SKU di &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Per tutti

La funzione `forall` determina tutti gli elementi di una matrice che soddisfano tutte le condizioni specificate.

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

La seguente query PQL ottiene tutti gli eventi che hanno un prezzo superiore a 50 $ e ha una SKU di &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Passaggi successivi

Ora che hai imparato i quantificatori logici, puoi utilizzarli nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consulta la [Panoramica di Profile Query Language](./overview.md).
