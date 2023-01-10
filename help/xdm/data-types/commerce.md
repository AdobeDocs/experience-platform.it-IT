---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;commercio;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati Commerce
description: Questo documento fornisce una panoramica del tipo di dati Commerce Experience Data Model (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 2%

---

# [!UICONTROL Commerce] tipo di dati

[!UICONTROL Commerce] è un tipo di dati XDM (Experience Data Model) standard che descrive i record relativi all’attività di acquisto e vendita.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `order` | [[!UICONTROL Ordine]](./order.md) | Descrive l&#39;ordine inserito per uno o più prodotti. |
| `cartAbandons` | [[!UICONTROL Misura]](./measure.md) | Utilizzato per descrivere quando un elenco di prodotti è stato identificato come non più accessibile o acquistabile dall’utente. |
| `checkouts` | [[!UICONTROL Misura]](./measure.md) | Un’azione durante il processo di pagamento di un elenco di prodotti. Se in un processo di pagamento sono presenti più passaggi, può essere presente più di un evento di pagamento. Se sono presenti più passaggi, le informazioni sull&#39;ora dell&#39;evento e la pagina o l&#39;esperienza di riferimento vengono utilizzate per identificare il passaggio e i singoli eventi rappresentati nell&#39;ordine. |
| `inStorePurchase` | [[!UICONTROL Misura]](./measure.md) | Descrive un valore associato a un acquisto in-store per l&#39;utilizzo di analytics. |
| `productListAdds` | [[!UICONTROL Misura]](./measure.md) | L’aggiunta di un prodotto all’elenco dei prodotti, ad esempio un prodotto che viene aggiunto al carrello. |
| `productListOpens` | [[!UICONTROL Misura]](./measure.md) | Inizializzazioni di un nuovo elenco di prodotti, ad esempio un carrello da creare. |
| `productListRemovals` | [[!UICONTROL Misura]](./measure.md) | Rimozione o rimozione di una voce di prodotto da un elenco di prodotti, ad esempio un prodotto che viene rimosso da un carrello. |
| `productListReopens` | [[!UICONTROL Misura]](./measure.md) | Elenco di prodotti precedentemente abbandonato e riattivato dall&#39;utente. |
| `productListViews` | [[!UICONTROL Misura]](./measure.md) | Descrive quando si è verificata una visualizzazione o una visualizzazione di un elenco di prodotti. |
| `productViews` | [[!UICONTROL Misura]](./measure.md) | Descrive quando si è verificata una visualizzazione o una visualizzazione di un singolo prodotto. |
| `purchases` | [[!UICONTROL Misura]](./measure.md) | Utilizzato per tenere traccia di quando un ordine è stato accettato. L’evento di acquisto è l’unica azione richiesta in una conversione di e-commerce. All&#39;evento di acquisto deve essere fatto riferimento a un elenco di prodotti. |
| `saveForLaters` | [[!UICONTROL Misura]](./measure.md) | Un elenco di prodotti viene salvato per utilizzi futuri, ad esempio un elenco di desideri. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
