---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: Quantificatori logici PQL
description: I quantificatori logici possono essere utilizzati per affermare condizioni con gli array in PQL (Profile Query Language).
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---

# Funzioni quantificatrici logiche

I quantificatori logici possono essere utilizzati per affermare le condizioni con gli array in [!DNL Profile Query Language] (PQL) Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Esiste

Il `exists` Questa funzione determina l&#39;esistenza di un elemento in un array, purché soddisfi la condizione specificata.

**Formato**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argomento | Descrizione |
| ---------- | ----------- |
| `{VARIABLE}` | Nome di una variabile. |
| `{EXPRESSION}` | Array che viene controllato. |
| `{CONDITION}` | Espressione facoltativa che filtra i valori nell’array restituito. |

**Esempio**

La seguente query PQL ottiene tutti gli eventi il cui prezzo è superiore a 50 $ o il cui SKU è &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Per tutti

Il `forall` determina tutti gli elementi di un array che soddisfano tutte le condizioni specificate.

**Formato**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argomento | Descrizione |
| ---------- | ----------- |
| `{VARIABLE}` | Nome di una variabile. |
| `{EXPRESSION}` | Array che viene controllato. |
| `{CONDITION}` | Espressione facoltativa che filtra i valori nell’array restituito. |

**Esempio**

La seguente query PQL ottiene tutti gli eventi il cui prezzo è superiore a 50 $ e il cui SKU è &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Passaggi successivi

Ora che hai imparato a utilizzare i quantificatori logici, puoi utilizzarli all’interno delle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
