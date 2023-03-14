---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;commerce;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati Commerce
description: Questo documento fornisce una panoramica del tipo di dati Commerce Experience Data Model (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 1%

---

# [!UICONTROL Commerce] tipo di dati

[!UICONTROL Commerce] è un tipo di dati Experience Data Model (XDM) standard che descrive i record relativi all’attività di acquisto e vendita.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `order` | [[!UICONTROL Ordine]](./order.md) | Descrive l’ordine effettuato per uno o più prodotti. |
| `cartAbandons` | [[!UICONTROL Misura]](./measure.md) | Utilizzato per descrivere quando un elenco di prodotti è stato identificato come non più accessibile o acquistabile dall’utente. |
| `checkouts` | [[!UICONTROL Misura]](./measure.md) | Azione durante il processo di pagamento di un elenco di prodotti. Ci può essere più di un evento di pagamento se ci sono più passaggi in un processo di pagamento. Se sono presenti più passaggi, le informazioni sull’ora dell’evento e la pagina o l’esperienza di riferimento vengono utilizzate per identificare il passaggio e i singoli eventi rappresentati nell’ordine. |
| `inStorePurchase` | [[!UICONTROL Misura]](./measure.md) | Descrive un valore associato a un acquisto in-store per l’utilizzo in Analytics. |
| `productListAdds` | [[!UICONTROL Misura]](./measure.md) | L’aggiunta di un prodotto all’elenco dei prodotti, ad esempio un prodotto che viene aggiunto a un carrello. |
| `productListOpens` | [[!UICONTROL Misura]](./measure.md) | Inizializzazioni di un nuovo elenco di prodotti, ad esempio la creazione di un carrello. |
| `productListRemovals` | [[!UICONTROL Misura]](./measure.md) | La rimozione o la rimozione di una voce di prodotto da un elenco di prodotti, ad esempio un prodotto rimosso da un carrello. |
| `productListReopens` | [[!UICONTROL Misura]](./measure.md) | Un elenco di prodotti precedentemente abbandonato che è stato riattivato dall’utente. |
| `productListViews` | [[!UICONTROL Misura]](./measure.md) | Descrive quando si è verificata una o più visualizzazioni di un elenco di prodotti. |
| `productViews` | [[!UICONTROL Misura]](./measure.md) | Descrive quando si sono verificate una o più visualizzazioni di un singolo prodotto. |
| `purchases` | [[!UICONTROL Misura]](./measure.md) | Utilizzato per tenere traccia di quando un ordine è stato accettato. L’evento di acquisto è l’unica azione richiesta in una conversione commerce. L’evento di acquisto deve fare riferimento a un elenco di prodotti. |
| `saveForLaters` | [[!UICONTROL Misura]](./measure.md) | Un elenco di prodotti viene salvato per un utilizzo futuro, ad esempio una lista dei desideri. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
