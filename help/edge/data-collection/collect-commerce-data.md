---
title: Raccogliere informazioni su prodotti e commercio con l’SDK per web di Adobe Experience Platform
description: Scopri come aggiungere dati relativi a prodotti o carrelli utilizzando Adobe Experience Platform Web SDK.
keywords: prodotti;commercio;misure;misura;ordine;cartAbandons;checkout;productListAdd;productListAperture;productListRemovals;productListReopen;productListViews;productViews;acquisti;saveForLaters;currencyCode;pagamenti;importoPagamento;IDTransazione;priceTotal;purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
translation-type: tm+mt
source-git-commit: 7d7502b238f96eda1a15b622ba10bbccc289b725
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 3%

---

# Raccogliere informazioni su prodotti e soluzioni commerce

Se sul sito sono presenti prodotti, si tratta di un set predefinito di elementi che puoi inviare per abilitare il maggior numero di funzionalità da Adobe. Anche se questo è un suggerimento, fornisce un set di dati molto forte fin dall&#39;inizio.

In questo documento viene utilizzato il gruppo di campi dello schema [Dettagli commercio esperienza](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md). Il gruppo di campi `commerce` è suddiviso in due parti: l&#39;oggetto `commerce` e l&#39;array `productListItems`. L&#39;oggetto `commerce` ti consente di indicare quali azioni si stanno verificando nell&#39;array `productListItems`.

>[!TIP]
>
>Se hai familiarità con Adobe Analytics, la variabile `commerce` è strettamente correlata alla variabile `events`. La variabile `productListItems` è più strettamente correlata alla variabile `products`.

## Azioni relative ai prodotti

Di seguito è riportato un elenco di `measures` disponibili nell&#39;oggetto `commerce` .

>[!TIP]
>
>Una misura ha due campi: `id` e `value`. Nella maggior parte dei casi, utilizzerai solo il campo `value` (ad esempio, `'value':1`). Il campo `id` ti consente di impostare un identificatore univoco che puoi utilizzare per tenere traccia di quando è stata inviata la misura. Consulta la documentazione XDM per [Measure](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Misura** | **Consiglio** | **Descrizione** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Facoltativo | Un carrello non è più accessibile o acquistabile dall’utente. |
| [checkout](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Altamente consigliato | Un utente non sta più navigando per i prodotti, ma sta acquistando un prodotto. |
| [productListAdd](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Altamente consigliato | Un prodotto viene aggiunto a un elenco. Assicurati di impostare il prodotto in `productListItems` allo stesso tempo. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Facoltativo | Viene creato un nuovo elenco di prodotti. Ad esempio, viene creato un nuovo carrello. |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Altamente consigliato | Un prodotto viene rimosso da un elenco di prodotti. |
| [productListReopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Facoltativo | Un elenco di prodotti viene riattivato dall’utente. Questo accade spesso nelle campagne di remarketing. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Altamente consigliato | Viene visualizzato un elenco di prodotti. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Altamente consigliato | Visualizzazione di un prodotto. Assicurati di impostare il prodotto visualizzato in `productListItems`. |
| [acquisti](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Altamente consigliato | Un ordine è accettato. Deve avere un elenco di prodotti. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Facoltativo | Un prodotto viene salvato per un utilizzo futuro. |

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
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | L&#39;elenco dei pagamenti su un ordine. Un [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) include quanto segue. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Facoltativo | La valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) per questo metodo di pagamento. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Altamente consigliato | Valore del pagamento nel codice valuta specificato. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Altamente consigliato | Il tipo di pagamento (ad esempio, `credit_card`, `gift_card`, `paypal`). Per ulteriori informazioni, vedere l&#39;elenco dei valori [noti](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) . |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Facoltativo | Un ID univoco per questa transazione di pagamento. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Altamente consigliato | Totale per l&#39;ordine dopo l&#39;applicazione di tutti gli sconti e le imposte. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Altamente consigliato | Identificatore univoco assegnato dal venditore per l&#39;acquisto. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Facoltativo | Identificatore univoco assegnato dall&#39;acquirente per l&#39;acquisto. |

Ecco un esempio di acquisto tipico nell&#39;SDK.

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

## Elenco dei prodotti

L’elenco dei prodotti indica quali prodotti sono correlati all’azione corrispondente. È un elenco di [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Ogni prodotto dispone di una serie di campi facoltativi.

| **Campo** | **Consiglio** | **Descrizione** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Facoltativo | La valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) per il prodotto. Questa funzione è utile solo quando è possibile avere prodotti con diversi codici di valuta e quando viene applicata. Ad esempio, quando esiste un acquisto o aggiungi al carrello. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Altamente consigliato | Deve essere impostato solo se applicabile. Ad esempio, potrebbe non essere possibile impostare su `productView` perché diverse varianti del prodotto possono avere prezzi diversi ma su un `productListAdds`. |
| [prodotto](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Altamente consigliato | ID XDM per il prodotto. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Altamente consigliato | Il metodo utilizzato dal visitatore per aggiungere un elemento prodotto all’elenco. Impostato con le misure `productListAdds` e deve essere utilizzato solo quando un prodotto viene aggiunto all’elenco. Gli esempi includono `add to cart button`, `quick add` e `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Altamente consigliato | Questo è impostato sul nome visualizzato o il nome leggibile dall&#39;utente del prodotto. |
| [quantità](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Altamente consigliato | Il numero di unità che il cliente ha indicato di aver bisogno del prodotto. Deve essere impostato su `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` e così via. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Altamente consigliato | Archivia unità di conservazione. È l’identificatore univoco del prodotto. |

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
