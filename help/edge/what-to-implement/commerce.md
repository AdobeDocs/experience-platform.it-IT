---
title: Prodotti
seo-title: Supporto di prodotti con  Adobe Experience Platform Web SDK
description: Scoprite come aggiungere dati in caso di prodotti o di un carrello con  Experience Platform Web SDK
seo-description: Scoprite come aggiungere dati in caso di prodotti o di un carrello con  Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 4%

---


# Prodotti

Se sul sito sono presenti prodotti, si tratta di un insieme predefinito di elementi che potreste desiderare inviare per abilitare il maggior numero di funzionalità da Adobe. Anche se questo è un suggerimento, fornisce una serie molto forte di dati fin dall&#39;inizio.

In questo documento viene utilizzato il mixin [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) . La `commerce` miscelazione è suddivisa in due parti: l&#39; `commerce` oggetto e l&#39; `productListItems` array. L&#39; `commerce` oggetto consente di indicare quali azioni vengono eseguite sull&#39; `productListItems` array.

>[!Tip]
>
>
>Se avete familiarità con Adobe  Analytics, la variabile `commerce` è maggiormente correlata alla `events` variabile. La variabile `productListItems` è più strettamente correlata alla `products` variabile.

## Azioni relative ai prodotti

Di seguito è riportato un elenco di `measures` elementi disponibili nell&#39; `commerce` oggetto.

>[!Tip]
>
>
>Una misura ha due campi: `id` e `value`. Nella maggior parte dei casi, sarà utilizzato solo il `value` campo (ad esempio, `'value':1`). Il `id` campo consente di impostare un identificatore univoco che consente di tenere traccia di quando la misura è stata inviata. Consulta la documentazione XDM per [Measure](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Misura** | **Consiglio** | **Descrizione** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Facoltativo | Un carrello non è più accessibile o acquistabile dall&#39;utente. |
| [checkout](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Altamente consigliato | Un utente non sta più consultando i prodotti ma sta acquistando un prodotto. |
| [productListAdd](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Altamente consigliato | Un prodotto viene aggiunto a un elenco. Assicuratevi di impostare il prodotto nello `productListItems` stesso momento. |
| [productListOpen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Facoltativo | Viene creato un nuovo elenco di prodotti. Ad esempio, viene creato un nuovo carrello. |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Altamente consigliato | Un prodotto viene rimosso da un elenco di prodotti. |
| [productListReopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Facoltativo | Un elenco di prodotti viene riattivato dall&#39;utente. Ciò accade spesso nelle campagne di remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Altamente consigliato | Viene visualizzato un elenco di prodotti. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Altamente consigliato | Vista di un prodotto. Accertatevi di impostare il prodotto visualizzato nel `productListItems`. |
| [acquisti](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Altamente consigliato | Un ordine è accettato. Deve avere un elenco di prodotti. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Facoltativo | Un prodotto viene salvato per uso futuro. |

Di seguito è riportato un esempio di come impostare questi valori `Measures` nell’SDK.

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

L&#39;oggetto commerce dispone anche di un campo speciale per la raccolta dei dettagli dell&#39;ordine denominato `order`.

| **Ordine** | **Opzione** | **Consiglio** | **Descrizione** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | La valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) per il totale dell&#39;ordine. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | L&#39;elenco dei pagamenti su un ordine. Un oggetto [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) include quanto segue: |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Facoltativo | La valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) per questo metodo di pagamento. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Altamente consigliato | Il valore del pagamento nel codice della valuta specificato. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Altamente consigliato | Tipo di pagamento (ad esempio, `credit_card`, `gift_card`, `paypal`). Per informazioni dettagliate, consultate l&#39;elenco dei valori [](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) noti. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Facoltativo | Un ID univoco per questa transazione di pagamento. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Altamente consigliato | Totale per questo ordine dopo che tutti gli sconti e le imposte sono stati applicati. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Altamente consigliato | Identificatore univoco assegnato dal venditore per l&#39;acquisto. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Facoltativo | Identificatore univoco assegnato dall&#39;acquirente per l&#39;acquisto. |

Esempio di acquisto tipico nell’SDK.

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```

## Elenchi di prodotti

L&#39;elenco dei prodotti indica quali prodotti sono correlati all&#39;azione corrispondente. È un elenco di [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Ogni prodotto ha una serie di campi opzionali.

| **Campo** | **Consiglio** | **Descrizione** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Facoltativo | La valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) per il prodotto. Questa funzione è utile solo quando è possibile avere prodotti con codici valuta diversi e quando viene applicata. Ad esempio, in caso di acquisto o aggiunta al carrello. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Altamente consigliato | Deve essere impostato solo se applicabile. Ad esempio, potrebbe non essere possibile impostare `productView` perché diverse variazioni del prodotto possono avere prezzi diversi ma su un `productListAdds`. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Altamente consigliato | L&#39;ID XDM per il prodotto. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Altamente consigliato | Metodo utilizzato per aggiungere un elemento prodotto all’elenco dal visitatore. Impostato con `productListAdds` misure, e dovrebbe essere utilizzato solo quando un prodotto viene aggiunto all&#39;elenco. Esempi includono `add to cart button`, `quick add`e `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Altamente consigliato | Questo è impostato sul nome visualizzato o sul nome leggibile del prodotto. |
| [quantità](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Altamente consigliato | Il numero di unità che il cliente ha indicato di aver bisogno del prodotto. Deve essere impostato su `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`e così via. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Altamente consigliato | Unità di conservazione dello store. È l’identificatore univoco del prodotto. |

## Esempi

`productView` event

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

`productView` event

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

`checkout` event

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

`purchase` event

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```
