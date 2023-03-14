---
title: Raccogliere informazioni su Commerce e prodotto tramite Adobe Experience Platform Web SDK
description: Scopri come aggiungere dati relativi a prodotti o a un carrello utilizzando Adobe Experience Platform Web SDK.
keywords: products;commerce;misure;misura;ordine;cartAbandons;checkout;productListAdds;productListOpens;productListRemovals;productListReopens;productListViews;productViews;purchases;saveForLaters;currencyCode;payments;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 51a18ca3a9d0817eafeecea328900eb2f4d1d9a4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 4%

---

# Raccogliere informazioni su prodotti e commercio

Se sul sito sono presenti prodotti, si tratta di un set predefinito di elementi che potresti voler inviare per abilitare il maggior numero di funzionalità di Adobe. Anche se questo è un suggerimento, fornisce un set molto forte di dati fin dall&#39;inizio.

Questo documento utilizza [Dettagli di ExperienceEvent Commerce](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) gruppo di campi dello schema. Il `commerce` è suddiviso in due parti: `commerce` oggetto e `productListItems` array. Il `commerce` oggetto consente di indicare le azioni che si verificano per `productListItems` array.

>[!TIP]
>
>Se hai familiarità con Adobe Analytics, il `commerce` è strettamente correlato al `events` variabile. Il `productListItems` è più strettamente correlato al `products` variabile.

## Azioni relative ai prodotti

Di seguito è riportato un elenco di `measures` disponibile in `commerce` oggetto.

>[!TIP]
>
>Una misura ha due campi: `id` e `value`. Nella maggior parte dei casi, utilizzerai `value` solo campo (ad esempio, `'value':1`). Il `id` consente di impostare un identificatore univoco da utilizzare per tenere traccia di quando è stata inviata la misura. Consulta la documentazione di XDM per [Misura](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Misura** | **Consiglio** | **Descrizione** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Facoltativo | Un carrello non è più accessibile o acquistabile dall’utente. |
| [checkout](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Altamente consigliato | Un utente non cerca più prodotti, ma sta acquistando un prodotto. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Altamente consigliato | Un prodotto viene aggiunto a un elenco. Assicurarsi di impostare il prodotto in `productListItems` contemporaneamente. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Facoltativo | Viene creato un nuovo elenco di prodotti. Ad esempio, viene creato un nuovo carrello. |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Altamente consigliato | Un prodotto viene rimosso da un elenco di prodotti. |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Facoltativo | Un elenco di prodotti viene riattivato dall’utente. Questo accade spesso nelle campagne di remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Altamente consigliato | Viene visualizzato un elenco di prodotti. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Altamente consigliato | Si è verificata una visualizzazione di un prodotto. Assicurati di impostare il prodotto visualizzato in `productListItems`. |
| [acquisti](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Altamente consigliato | Un ordine è accettato. Deve avere un elenco di prodotti. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Facoltativo | Un prodotto viene salvato per un utilizzo futuro. |

Di seguito è riportato un esempio di impostazione `Measures` nell’SDK.

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

L’oggetto Commerce dispone anche di un campo speciale per la raccolta dei dettagli dell’ordine denominato `order`.

| **Ordine** | **Opzione** | **Consiglio** | **Descrizione** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta per il totale dell’ordine. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | Elenco dei pagamenti in un ordine. A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) include quanto segue. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Facoltativo | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta per questo metodo di pagamento. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Altamente consigliato | Il valore del pagamento nel codice valuta specificato. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Altamente consigliato | Tipo di pagamento (ad esempio, `credit_card`, `gift_card`, `paypal`). Consulta l’elenco di [valori noti](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) per i dettagli. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Facoltativo | Un ID univoco per questa transazione di pagamento. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Altamente consigliato | Totale per questo ordine dopo l&#39;applicazione di tutti gli sconti e le imposte. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Altamente consigliato | L&#39;identificatore univoco assegnato dal venditore per questo acquisto. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Facoltativo | Un identificatore univoco assegnato dall’acquirente a questo acquisto. |

Ecco un esempio di un acquisto tipico nell’SDK.

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

L’elenco dei prodotti indica quali prodotti sono correlati all’azione corrispondente. È un elenco di [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Ogni prodotto dispone di diversi campi facoltativi.

| **Campo** | **Consiglio** | **Descrizione** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Facoltativo | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta per il prodotto. Questa funzione è utile solo quando si possono avere prodotti con codici valuta diversi e quando è applicabile. Ad esempio, in caso di acquisto o di aggiunta al carrello. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Altamente consigliato | Deve essere impostato solo se applicabile. Ad esempio, potrebbe non essere possibile impostare su `productView` evento perché diverse varianti del prodotto possono avere prezzi diversi, ma su `productListAdds` evento. |
| [prodotto](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Altamente consigliato | L’ID XDM del prodotto. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Altamente consigliato | Il metodo utilizzato dal visitatore per aggiungere un elemento di prodotto all’elenco. Imposta con `productListAdds` e devono essere utilizzati solo quando un prodotto viene aggiunto all’elenco. Alcuni esempi includono `add to cart button`, `quick add`, e `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Altamente consigliato | È impostato sul nome visualizzato o sul nome leggibile del prodotto. |
| [quantità](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Altamente consigliato | Il numero di unità del prodotto che il cliente ha indicato di richiedere. Deve essere impostato su `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`e così via. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Altamente consigliato | Conservare l&#39;unità. È l’identificatore univoco del prodotto. |

## Esempi

`productViews` evento

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

`productListAdds` evento

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

`checkouts` evento

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

`order` evento

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
