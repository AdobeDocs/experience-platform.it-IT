---
title: Classe prodotto
description: Scopri la classe prodotto in Experience Data Model (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 5%

---

# [!UICONTROL Prodotto] classe

In Experience Data Model (XDM), la [!UICONTROL Prodotto] Questa classe acquisisce il set minimo di proprietà che definiscono un prodotto di vendita al dettaglio.

![](../images/classes/product.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `productListPrice` | [Valuta](../data-types/currency.md) | Descrive il prezzo predefinito del prodotto prima delle vendite e dello sconto. |
| `_id` | Stringa | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l’inserimento dei dati non viene fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `productDescription` | Stringa | Una descrizione del prodotto. |
| `productID` | Stringa | Un identificatore univoco del prodotto. |
| `productLastModifiedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) la marca temporale dell’ultima modifica apportata al prodotto per eventuali aggiornamenti. |
| `productManufacturedDate` | DateTime | Un [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) timestamp di quando il prodotto è stato creato. |
| `productName` | Stringa | Il nome del prodotto. |
| `productRating` | Stringa | La valutazione del prodotto da parte del cliente. |

{style="table-layout:auto"}

## Gruppi di campi compatibili {#field-groups}

L&#39;Adobe fornisce diversi gruppi di campi standard da utilizzare con [!UICONTROL Prodotto] classe. Di seguito è riportato un elenco di alcuni gruppi di campi comunemente utilizzati per la classe:

* [[!UICONTROL Catalogo prodotti]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Categoria di prodotto]](../field-groups/product/product-category.md)
