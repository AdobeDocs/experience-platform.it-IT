---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;commerce;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati Commerce
description: Scopri il tipo di dati Commerce Experience Data Model (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# [!UICONTROL Commerce] tipo di dati

[!UICONTROL Commerce] è un tipo di dati Experience Data Model (XDM) standard che descrive i record relativi all’acquisto e alla vendita.

![Un diagramma del [!UICONTROL Commerce] tipo di dati.](../images/data-types/commerce.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL Ordine] | `order` | [[!UICONTROL Ordine]](./order.md) | Descrive l’ordine effettuato per uno o più prodotti. |
| [!UICONTROL ID promozione] | `promotionID` | [!UICONTROL stringa] | Un identificatore di promozione per l’ordine effettuato, se presente. |
| [!UICONTROL Abbandoni carrello] | `cartAbandons` | [[!UICONTROL Misura]](./measure.md) | Descrive quando un elenco di prodotti è stato identificato come non più accessibile o acquistabile dall’utente. |
| [!UICONTROL Pagamenti] | `checkouts` | [[!UICONTROL Misura]](./measure.md) | Azione durante il processo di pagamento di un elenco di prodotti. Ci può essere più di un evento di pagamento se ci sono più passaggi in un processo di pagamento. Se sono presenti più passaggi, le informazioni sull’ora dell’evento e la pagina o l’esperienza di riferimento vengono utilizzate per identificare il passaggio e i singoli eventi rappresentati nell’ordine. |
| [!UICONTROL Aggiunte a elenco prodotti (carrello)] | `productListAdds` | [[!UICONTROL Misura]](./measure.md) | L’aggiunta di un prodotto all’elenco dei prodotti, ad esempio un prodotto che viene aggiunto a un carrello. |
| [!UICONTROL Aperture elenco prodotti (carrello)] | `productListOpens` | [[!UICONTROL Misura]](./measure.md) | Inizializzazioni di un nuovo elenco di prodotti, ad esempio la creazione di un carrello. |
| [!UICONTROL Rimozioni elenco prodotti (carrello)] | `productListRemovals` | [[!UICONTROL Misura]](./measure.md) | La rimozione o la rimozione di una voce di prodotto da un elenco di prodotti, ad esempio un prodotto rimosso da un carrello. |
| [!UICONTROL Riaperture di elenco prodotti (carrello)] | `productListReopens` | [[!UICONTROL Misura]](./measure.md) | Un elenco di prodotti precedentemente abbandonato che è stato riattivato dall’utente. |
| [!UICONTROL Visualizzazioni elenco prodotti (carrello)] | `productListViews` | [[!UICONTROL Misura]](./measure.md) | Descrive quando si è verificata una o più visualizzazioni di un elenco di prodotti.Visualizzazione o visualizzazioni di un elenco di prodotti. |
| [!UICONTROL Visualizzazioni prodotto] | `productViews` | [[!UICONTROL Misura]](./measure.md) | Descrive quando si sono verificate una o più visualizzazioni di un singolo prodotto. |
| [!UICONTROL Acquisti] | `purchases` | [[!UICONTROL Misura]](./measure.md) | Utilizzato per tenere traccia di quando un ordine è stato accettato. L’evento di acquisto è l’unica azione richiesta in una conversione commerce. L’evento di acquisto deve fare riferimento a un elenco di prodotti. |
| [!UICONTROL Salva per dopo] | `saveForLaters` | [[!UICONTROL Misura]](./measure.md) | Descrive quando un elenco di prodotti viene salvato per un utilizzo futuro, ad esempio una lista dei desideri. |
| [!UICONTROL Acquisto in negozio] | `inStorePurchase` | [[!UICONTROL Misura]](./measure.md) | Indica un acquisto &quot;inStore&quot;. Queste informazioni vengono salvate per l’utilizzo in Analytics. |
| [!UICONTROL Carrello] | `cart` | [[!UICONTROL carrello]](./cart.md) | Le proprietà del carrello che contiene uno o più prodotti. |
| [!UICONTROL Spedizione] | `shipping` | [[!UICONTROL spedizione]](./shipping.md) | I dettagli di spedizione per uno o più prodotti. |
| [!UICONTROL Fatturazione] | `billing` | [[!UICONTROL fatturazione]](#billing) | I dettagli di fatturazione per uno o più pagamenti. |
| [!UICONTROL Acquisto immediato] | `instantPurchase` | [[!UICONTROL Misura]](./measure.md) | Descrive quando un prodotto è stato acquistato immediatamente, saltando potenzialmente il carrello o il pagamento. |
| [!UICONTROL Aperture elenco richieste di acquisto] | `requisitionListOpens` | [[!UICONTROL Misura]](./measure.md) | Indica l&#39;inizializzazione di un nuovo elenco di richieste. |
| [!UICONTROL Eliminazioni elenco richieste di acquisto] | `requisitionListDeletes` | [[!UICONTROL Misura]](./measure.md) | Indica la rimozione dell&#39;elenco di richieste di acquisto. |
| [!UICONTROL Aggiunte a elenco richieste di acquisto] | `requisitionListAdds` | [[!UICONTROL Misura]](./measure.md) | Indica l&#39;aggiunta di uno o più prodotti a un elenco di richieste. |
| [!UICONTROL Rimozioni elenco richieste di acquisto] | `requisitionListRemovals` | [[!UICONTROL Misura]](./measure.md) | Indica la rimozione di uno o più prodotti da un elenco di prodotti della richiesta di acquisto. |
| [!UICONTROL Elenco richieste] | `requisitionList` | [[!UICONTROL elenco richieste]](./requisition-list.md) | Proprietà dell&#39;elenco di richieste di acquisto creato dal cliente. |
| [!UICONTROL Ambito] | `commerceScope` | [[!UICONTROL commerce]](./commerce-scope.md) | Gli identificatori dell’ambito Commerce di dove si è verificato un evento (visualizzazione store, store, sito web, ecc.). |

{style="table-layout:auto"}

## [!UICONTROL fatturazione] tipo di dati {#billing}

[!UICONTROL fatturazione] è un tipo di dati Experience Data Model (XDM) standard che contiene informazioni sui dettagli di fatturazione. In particolare, si concentra sull’indirizzo di fatturazione.

![Un diagramma del tipo di dati di fatturazione.](../images/data-types/billing.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL Indirizzo di fatturazione] | `address` | [[!UICONTROL Indirizzo postale]](./postal-address.md) | Indirizzo di fatturazione. |

{style="table-layout:auto"}

Per ulteriori dettagli su [!UICONTROL Commerce] tipo di dati, fai riferimento all’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
