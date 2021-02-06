---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;schemi;commercio;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo dati Commerce
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati Commerce Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# [!UICONTROL Commerce] tipo di dati

[!UICONTROL Commerce] è un tipo di dati XDM (Experience Data Model) standard che descrive i record relativi all&#39;attività di acquisto e vendita.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `order` | [[!UICONTROL Order]](./order.md) | Descrive l&#39;ordine inserito per uno o più prodotti. |
| `cartAbandons` | [[!UICONTROL Measure]](./measure.md) | Utilizzato per descrivere quando un elenco di prodotti è stato identificato come non più accessibile o acquistabile dall&#39;utente. |
| `checkouts` | [[!UICONTROL Measure]](./measure.md) | Un&#39;azione durante il processo di estrazione di un elenco di prodotti. Se in un processo di estrazione sono presenti più passaggi, può verificarsi più di un evento di estrazione. Se sono presenti più passaggi, le informazioni sull&#39;ora dell&#39;evento e la pagina o l&#39;esperienza di riferimento vengono utilizzate per identificare il passaggio e i singoli eventi rappresentati nell&#39;ordine. |
| `inStorePurchase` | [[!UICONTROL Measure]](./measure.md) | Descrive un valore associato a un acquisto in-store per l&#39;uso di analisi. |
| `productListAdds` | [[!UICONTROL Measure]](./measure.md) | L&#39;aggiunta di un prodotto all&#39;elenco dei prodotti, ad esempio un prodotto che viene aggiunto al carrello. |
| `productListOpens` | [[!UICONTROL Measure]](./measure.md) | Inizializzazioni di un nuovo elenco di prodotti, ad esempio un carrello che si sta creando. |
| `productListRemovals` | [[!UICONTROL Measure]](./measure.md) | Rimozione o rimozione di una voce di prodotto da un elenco di prodotti, ad esempio un prodotto che viene rimosso da un carrello. |
| `productListReopens` | [[!UICONTROL Measure]](./measure.md) | Elenco di prodotti precedentemente abbandonato e riattivato dall&#39;utente. |
| `productListViews` | [[!UICONTROL Measure]](./measure.md) | Descrive quando si è verificata una visualizzazione o visualizzazioni di un elenco di prodotti. |
| `productViews` | [[!UICONTROL Measure]](./measure.md) | Descrive quando si è verificata una visualizzazione o visualizzazioni di un singolo prodotto. |
| `purchases` | [[!UICONTROL Measure]](./measure.md) | Utilizzato per tenere traccia di quando un ordine è stato accettato. L&#39;evento acquisto è l&#39;unica azione richiesta in una conversione di commercio. L&#39;evento di acquisto deve avere un elenco di prodotti a cui fare riferimento. |
| `saveForLaters` | [[!UICONTROL Measure]](./measure.md) | Un elenco di prodotti viene salvato per uso futuro, ad esempio un elenco di desideri. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)