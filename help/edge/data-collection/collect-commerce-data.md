---
title: Raccogliere informazioni su prodotti e ordini tramite Adobe Experience Platform Web SDK
description: Scopri come aggiungere dati relativi a prodotti o a un carrello utilizzando Adobe Experience Platform Web SDK.
source-git-commit: cb47f70fe75eb0dfe26fb3c3557658cf6cff5a17
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 1%

---


# Raccogliere informazioni su prodotti e ordini

Se la tua organizzazione vende prodotti o servizi, puoi utilizzare questa pagina come guida su come tracciare tali prodotti e servizi.

Questa pagina utilizza XDM [Schema Commerce](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md) gruppo di campi.

Questo gruppo di campi è costituito da due parti principali:

* Il `commerce` oggetto. Questo oggetto ti consente di indicare quali azioni vengono eseguite `productListItems` array.
* Il `productListItems` array.

>[!TIP]
>
>Se hai familiarità con Adobe Analytics, il `commerce` L&#39;oggetto contiene dati simili agli eventi di e-commerce in `events` variabile. Il `productListItems` l&#39;array di oggetti contiene dati simili a `products` variabile.

## Il `commerce` oggetto {#commerce-object}

Questa sezione descrive i campi disponibili nel `commerce` oggetto.

>[!TIP]
>
>Una misura ha due campi: `id` e `value`. Nella maggior parte dei casi, si utilizza solo `value` campo (ad esempio, `'value':1`). Il `id` consente di impostare un identificatore univoco per il tracciamento al momento dell’invio della misura. Consulta la documentazione di XDM per [Misura](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) per ulteriori informazioni.

| Misura | Consiglio | Descrizione |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Facoltativo | Un carrello non è più accessibile o acquistabile dall’utente. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Altamente consigliato | Un utente non cerca più prodotti, ma sta acquistando un prodotto. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Altamente consigliato | Un prodotto viene aggiunto a un elenco. Assicurarsi di impostare il prodotto in `productListItems` contemporaneamente. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Facoltativo | Viene creato un nuovo elenco di prodotti. Ad esempio, viene creato un nuovo carrello. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Altamente consigliato | Un prodotto viene rimosso da un elenco di prodotti. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Facoltativo | Un elenco di prodotti viene riattivato dall’utente. Questa azione si verifica spesso nelle campagne di remarketing. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Altamente consigliato | Viene visualizzato un elenco di prodotti. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Altamente consigliato | Si è verificata una visualizzazione di un prodotto. Assicurati di impostare il prodotto visualizzato in `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Altamente consigliato | Un ordine è accettato. Deve avere un elenco di prodotti. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Facoltativo | Un prodotto viene salvato per un utilizzo futuro. |

{style="table-layout:auto"}

### `Commerce` esempi di oggetti

Espandi la sezione seguente per visualizzare un esempio di comando Web SDK che utilizza un campo del `commerce` oggetto.

+++`productViews`

Un Web SDK di base `sendEvent` chiamata impostazione della `productViews` campo a `1`:

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

+++

## Il `order` oggetto {#order-object}

Il `commerce` L&#39;oggetto contiene un oggetto dedicato per la raccolta dei dettagli dell&#39;ordine. Questa funzione è denominata `order` oggetto.

Questa sezione descrive tutti i campi supportati da `order` oggetto.

| Campo | Opzione | Consiglio | Descrizione |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta per il totale dell’ordine. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | Elenco dei pagamenti in un ordine. A [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) include quanto segue. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Facoltativo | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta per questo metodo di pagamento. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Altamente consigliato | Il valore del pagamento nel codice valuta specificato. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Altamente consigliato | Tipo di pagamento (ad esempio, `credit_card`, `gift_card`, `paypal`). Consulta l’elenco di [valori noti](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) per i dettagli. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Facoltativo | Un ID univoco per questa transazione di pagamento. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Altamente consigliato | Totale per questo ordine dopo l&#39;applicazione di tutti gli sconti e le imposte. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Altamente consigliato | L&#39;identificatore univoco assegnato dal venditore per questo acquisto. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Facoltativo | Un identificatore univoco assegnato dall’acquirente a questo acquisto. |

### Esempi di oggetti dell’ordine

Espandi la sezione seguente per visualizzare un esempio di comando Web SDK utilizzando `commerce` oggetto.

+++`Order` esempio di oggetto

SDK per web `sendEvent` chiamata impostazione della `order` oggetto che si applica a più prodotti nel `productListItems` array:

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

+++

## Oggetto elenco prodotti {#product-list-object}

L’elenco dei prodotti indica quali prodotti sono correlati all’azione corrispondente. È un elenco di [productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). Ogni prodotto ha diversi campi facoltativi.

| Campo | Consiglio | Descrizione |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Facoltativo | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta per il prodotto. Questo campo si applica in genere solo quando nell’elenco dei prodotti sono presenti più prodotti con codici di valuta diversi. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Altamente consigliato | Imposta questo campo solo se applicabile. Ad esempio, potrebbe non essere possibile impostare su `productView` evento perché diverse varianti del prodotto possono avere prezzi diversi, ma su `productListAdds` evento. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Altamente consigliato | L’ID XDM del prodotto. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Altamente consigliato | Il metodo utilizzato dal visitatore per aggiungere un elemento di prodotto all’elenco. Imposta con `productListAdds` e viene utilizzato solo quando un prodotto viene aggiunto all’elenco. Alcuni esempi includono `add to cart button`, `quick add`, e `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Altamente consigliato | Il nome visualizzato o leggibile del prodotto. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Altamente consigliato | Il numero di unità del prodotto che il cliente ha indicato di richiedere. Deve essere impostato su `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`e così via. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Altamente consigliato | Conservare l&#39;unità. È l’identificatore univoco del prodotto. |

### Esempi di elenco dei prodotti

Espandi le sezioni seguenti per visualizzare esempi di comandi Web SDK utilizzando `productListItems` oggetto.

+++`productListItems` esempio

SDK per web `sendEvent` chiamata impostazione della `productViews` per più prodotti in `productListItems` array:

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

+++

+++`productListAdds` esempio

SDK per web `sendEvent` chiamata impostazione della `productListAdds` evento per più prodotti in `productListItems` array:

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

+++

+++`checkouts` esempio

SDK per web `sendEvent` chiamata impostazione della `checkouts` evento per più prodotti in `productListItems` array:

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

+++
