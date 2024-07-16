---
title: Raccogliere informazioni su prodotti e ordini tramite Adobe Experience Platform Web SDK
description: Scopri come aggiungere dati relativi a prodotti o a un carrello utilizzando Adobe Experience Platform Web SDK.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 2%

---

# Raccogliere informazioni su prodotti e ordini

Se la tua organizzazione vende prodotti o servizi, puoi utilizzare questa pagina come guida su come tracciare tali prodotti e servizi.

In questa pagina viene utilizzato il gruppo di campi [Schema Commerce](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md) XDM.

Questo gruppo di campi è costituito da due parti principali:

* Oggetto `commerce`. Questo oggetto consente di indicare quali azioni vengono eseguite sull&#39;array `productListItems`.
* Array `productListItems`.

>[!TIP]
>
>Se si ha familiarità con Adobe Analytics, l&#39;oggetto `commerce` contiene dati simili agli eventi commerce nella variabile `events`. L&#39;array di oggetti `productListItems` contiene dati simili alla variabile `products`.

## Oggetto `commerce` {#commerce-object}

Questa sezione descrive i campi disponibili nell&#39;oggetto `commerce`.

>[!TIP]
>
>Una misura ha due campi: `id` e `value`. Nella maggior parte dei casi si utilizza solo il campo `value` (ad esempio `'value':1`). Il campo `id` consente di impostare un identificatore univoco per il tracciamento al momento dell&#39;invio della misura. Per ulteriori informazioni, consulta la documentazione XDM per [Measure](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md).

| Misura | Consiglio | Descrizione |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Facoltativo | Un carrello non è più accessibile o acquistabile dall’utente. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Altamente consigliato | Un utente non cerca più prodotti, ma sta acquistando un prodotto. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Altamente consigliato | Un prodotto viene aggiunto a un elenco. Assicurarsi di impostare il prodotto in `productListItems` contemporaneamente. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Facoltativo | Viene creato un nuovo elenco di prodotti. Ad esempio, viene creato un nuovo carrello. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Altamente consigliato | Un prodotto viene rimosso da un elenco di prodotti. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Facoltativo | Un elenco di prodotti viene riattivato dall’utente. Questa azione si verifica spesso nelle campagne di remarketing. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Altamente consigliato | Viene visualizzato un elenco di prodotti. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Altamente consigliato | Si è verificata una visualizzazione di un prodotto. Assicurarsi di impostare il prodotto visualizzato in `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Altamente consigliato | Un ordine è accettato. Deve avere un elenco di prodotti. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Facoltativo | Un prodotto viene salvato per un utilizzo futuro. |

{style="table-layout:auto"}

### `Commerce` esempi di oggetti

Espandere la sezione seguente per visualizzare un esempio di un comando Web SDK che utilizza un campo dell&#39;oggetto `commerce`.

+++`productViews`

Una chiamata Web SDK di base `sendEvent` che imposta il campo `productViews` su `1`:

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

## Oggetto `order` {#order-object}

L&#39;oggetto `commerce` contiene un oggetto dedicato per la raccolta dei dettagli dell&#39;ordine. Questo è denominato oggetto `order`.

Questa sezione descrive tutti i campi supportati dall&#39;oggetto `order`.

| Campo | Opzione | Consiglio | Descrizione |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | Valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) per il totale dell&#39;ordine. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | Elenco dei pagamenti in un ordine. Un oggetto [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) include quanto segue. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Facoltativo | La valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) per questo metodo di pagamento. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Altamente consigliato | Il valore del pagamento nel codice valuta specificato. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Altamente consigliato | Tipo di pagamento (ad esempio `credit_card`, `gift_card`, `paypal`). Per ulteriori informazioni, vedere l&#39;elenco di [valori noti](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values). |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Facoltativo | Un ID univoco per questa transazione di pagamento. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Altamente consigliato | Totale per questo ordine dopo l&#39;applicazione di tutti gli sconti e le imposte. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Altamente consigliato | L&#39;identificatore univoco assegnato dal venditore per questo acquisto. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Facoltativo | Un identificatore univoco assegnato dall’acquirente a questo acquisto. |

### Esempi di oggetti dell’ordine

Espandere la sezione seguente per visualizzare un esempio di un comando Web SDK che utilizza l&#39;oggetto `commerce`.

+++`Order` esempio di oggetto

Una chiamata SDK Web `sendEvent` che imposta l&#39;oggetto `order` che si applica a più prodotti nell&#39;array `productListItems`:

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
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Facoltativo | La valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) per il prodotto. Questo campo si applica in genere solo quando nell’elenco dei prodotti sono presenti più prodotti con codici di valuta diversi. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Altamente consigliato | Imposta questo campo solo se applicabile. Ad esempio, potrebbe non essere possibile impostare sull&#39;evento `productView` perché diverse varianti del prodotto possono avere prezzi diversi ma su un evento `productListAdds`. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Altamente consigliato | L’ID XDM del prodotto. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Altamente consigliato | Il metodo utilizzato dal visitatore per aggiungere un elemento di prodotto all’elenco. Impostato con `productListAdds` misure e utilizzato solo quando un prodotto viene aggiunto all&#39;elenco. Gli esempi includono `add to cart button`, `quick add` e `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Altamente consigliato | Il nome visualizzato o leggibile del prodotto. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Altamente consigliato | Il numero di unità del prodotto che il cliente ha indicato di richiedere. Deve essere impostato su `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` e così via. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Altamente consigliato | Conservare l&#39;unità. È l’identificatore univoco del prodotto. |

### Esempi di elenco dei prodotti

Espandere le sezioni seguenti per visualizzare esempi di comandi Web SDK che utilizzano l&#39;oggetto `productListItems`.

+++`productListItems` esempio

Una chiamata SDK Web `sendEvent` che imposta `productViews` per più prodotti nell&#39;array `productListItems`:

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

Una chiamata SDK Web `sendEvent` che imposta l&#39;evento `productListAdds` per più prodotti nell&#39;array `productListItems`:

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

Una chiamata SDK Web `sendEvent` che imposta l&#39;evento `checkouts` per più prodotti nell&#39;array `productListItems`:

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
