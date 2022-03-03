---
title: Classe di prodotto
description: Questo documento fornisce una panoramica della classe Product in Experience Data Model (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 9%

---

# [!UICONTROL Prodotto] Classe

In Experience Data Model (XDM), l’ [!UICONTROL Prodotto] acquisisce il set minimo di proprietà che definiscono un prodotto.

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

Adobe fornisce diversi gruppi di campi standard da utilizzare con [!DNL XDM Individual Profile] classe. Di seguito è riportato un elenco di alcuni gruppi di campi di uso comune per la classe:

* [[!UICONTROL Catalogo dei prodotti]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Categoria di prodotti]](../field-groups/product/product-category.md)
