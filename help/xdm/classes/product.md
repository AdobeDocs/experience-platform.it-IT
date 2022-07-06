---
title: Classe di prodotto
description: Questo documento fornisce una panoramica della classe Product in Experience Data Model (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 9%

---

# [!UICONTROL Prodotto] Classe

In Experience Data Model (XDM), l’ [!UICONTROL Prodotto] acquisisce il set minimo di proprietà che definiscono un prodotto di vendita al dettaglio.

![](../images/classes/product.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `productListPrice` | [Valuta](../data-types/currency.md) | Descrive il prezzo predefinito del prodotto prima delle vendite e degli sconti. |
| `_id` | Stringa | Identificatore stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, evitare la duplicazione dei dati e per cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non viene fornito un valore esplicito durante l’inserimento dei dati. Tuttavia, se lo desideri, puoi comunque scegliere di fornire i tuoi valori ID univoci. |
| `productDescription` | Stringa | Una descrizione del prodotto. |
| `productID` | Stringa | Identificatore univoco per il prodotto. |
| `productLastModifiedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) marca temporale dell’ultima modifica apportata al prodotto per eventuali aggiornamenti. |
| `productManufacturedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) marca temporale di quando è stato creato questo prodotto. |
| `productName` | Stringa | Nome del prodotto. |
| `productRating` | Stringa | Valutazione del prodotto da parte del cliente. |

{style=&quot;table-layout:auto&quot;}

## Gruppi di campi compatibili {#field-groups}

Adobe fornisce diversi gruppi di campi standard da utilizzare con [!UICONTROL Prodotto] classe. Di seguito è riportato un elenco di alcuni gruppi di campi di uso comune per la classe:

* [[!UICONTROL Catalogo dei prodotti]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Categoria di prodotti]](../field-groups/product/product-category.md)
