---
title: Classe prodotto
description: Scopri la classe prodotto in Experience Data Model (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 8%

---

# Classe [!UICONTROL Product]

In Experience Data Model (XDM), la classe [!UICONTROL Product] acquisisce il set minimo di proprietà che definiscono un prodotto al dettaglio.

![](../images/classes/product.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `productListPrice` | [Valuta](../data-types/currency.md) | Descrive il prezzo predefinito del prodotto prima delle vendite e dello sconto. |
| `_id` | Stringa | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l&#39;inserimento dei dati non verrà fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `productDescription` | Stringa | Una descrizione del prodotto. |
| `productID` | Stringa | Un identificatore univoco del prodotto. |
| `productLastModifiedDate` | Data e ora | Un timestamp [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) di quando il prodotto è stato modificato per l&#39;ultima volta per qualsiasi aggiornamento. |
| `productManufacturedDate` | Data e ora | Timestamp [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) di quando è stato creato il prodotto. |
| `productName` | Stringa | Il nome del prodotto. |
| `productRating` | Stringa | La valutazione del prodotto da parte del cliente. |

{style="table-layout:auto"}

## Gruppi di campi compatibili {#field-groups}

L&#39;Adobe fornisce diversi gruppi di campi standard da utilizzare con la classe [!UICONTROL Product]. Di seguito è riportato un elenco di alcuni gruppi di campi comunemente utilizzati per la classe:

* [[!UICONTROL Catalogo prodotti]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Categoria di prodotto]](../field-groups/product/product-category.md)
