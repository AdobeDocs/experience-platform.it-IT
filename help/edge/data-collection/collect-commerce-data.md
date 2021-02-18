---
title: Raccolta di informazioni sul commercio e sul prodotto con l'SDK Web per Adobe Experience Platform
description: Scoprite come aggiungere dati relativi a prodotti o carrelli tramite Adobe Experience Platform Web SDK.
keywords: prodotti;commercio;misure;misura;ordine;cartAbandons;checkout;productListAdd;productListOpen;productListRemovals;productListReopen;productListViews;purchase;saveForLaters;currencyCode;payment;paymentAmount;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 3%

---


# Raccolta di informazioni commerciali e sui prodotti

Se sul sito sono presenti prodotti, si tratta di un insieme predefinito di elementi che potreste desiderare inviare per abilitare il maggior numero di funzionalità da  Adobe. Anche se questo è un suggerimento, fornisce una serie molto forte di dati fin dall&#39;inizio.

In questo documento viene utilizzato il mixin [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md). Il mixin `commerce` è suddiviso in due parti: l&#39;oggetto `commerce` e l&#39;array `productListItems`. L&#39;oggetto `commerce` consente di indicare quali azioni vengono eseguite nell&#39;array `productListItems`.

>[!TIP]
>
>Se avete familiarità con  Adobe Analytics, la variabile `commerce` è strettamente correlata alla variabile `events`. La variabile `productListItems` è più strettamente correlata alla variabile `products`.

## Azioni relative ai prodotti

Di seguito è riportato un elenco di `measures` disponibili nell&#39;oggetto `commerce`.

>[!TIP]
>
>Una misura ha due campi: `id` e `value`. Nella maggior parte dei casi, sarà utilizzato solo il campo `value` (ad esempio, `'value':1`). Il campo `id` consente di impostare un identificatore univoco che è possibile utilizzare per tenere traccia di quando la misura è stata inviata. Consulta la documentazione XDM per [Measure](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Misura** | **Consiglio** | **Descrizione** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Facoltativo | Un carrello non è più accessibile o acquistabile dall&#39;utente. |
| [checkout](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Altamente consigliato | Un utente non sta più consultando i prodotti ma sta acquistando un prodotto. |
| [productListAdd](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Altamente consigliato | Un prodotto viene aggiunto a un elenco. Assicurarsi di impostare il prodotto in `productListItems` allo stesso tempo. |
| [productListOpen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Facoltativo | Viene creato un nuovo elenco di prodotti. Ad esempio, viene creato un nuovo carrello. |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Altamente consigliato | Un prodotto viene rimosso da un elenco di prodotti. |
| [productListReopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Facoltativo | Un elenco di prodotti viene riattivato dall&#39;utente. Ciò accade spesso nelle campagne di remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Altamente consigliato | Viene visualizzato un elenco di prodotti. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Altamente consigliato | Vista di un prodotto. Accertatevi di impostare il prodotto visualizzato in `productListItems`. |
| [acquisti](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Altamente consigliato | Un ordine è accettato. Deve avere un elenco di prodotti. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Facoltativo | Un prodotto viene salvato per uso futuro. |

Di seguito è riportato un esempio di come impostare questi `Measures` nell&#39;SDK.

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
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | L&#39;elenco dei pagamenti su un ordine. A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) è incluso quanto segue. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Facoltativo | La valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) per questo metodo di pagamento. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Altamente consigliato | Il valore del pagamento nel codice della valuta specificato. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Altamente consigliato | Il tipo di pagamento (ad esempio, `credit_card`, `gift_card`, `paypal`). Per ulteriori informazioni, vedere l&#39;elenco dei valori [noti](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values). |
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
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Altamente consigliato | Deve essere impostato solo se applicabile. Ad esempio, potrebbe non essere possibile impostare su `productView` perché diverse varianti del prodotto possono avere prezzi diversi ma su un `productListAdds`. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Altamente consigliato | L&#39;ID XDM per il prodotto. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Altamente consigliato | Metodo utilizzato per aggiungere un elemento prodotto all’elenco dal visitatore. Impostato con `productListAdds` misure, e dovrebbe essere utilizzato solo quando un prodotto viene aggiunto all&#39;elenco. Alcuni esempi includono `add to cart button`, `quick add` e `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Altamente consigliato | Questo è impostato sul nome visualizzato o sul nome leggibile del prodotto. |
| [quantità](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Altamente consigliato | Il numero di unità che il cliente ha indicato di aver bisogno del prodotto. Deve essere impostato su `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` e così via. |
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
