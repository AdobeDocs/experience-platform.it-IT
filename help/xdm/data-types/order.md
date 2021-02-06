---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;schemi;ordine;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo dati ordine
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Order Experience Data Model).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 3%

---


# [!UICONTROL Order] tipo di dati

[!UICONTROL Order] è un tipo di dati XDM (Experience Data Model) standard che descrive l&#39;ordine inserito per un elenco di prodotti.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `payments` | Array di [[!UICONTROL Payment Items]](./payment-item.md) | L&#39;elenco dei pagamenti per questo ordine. |
| `currencyCode` | Stringa | Codice valuta ISO 4217 utilizzato per i totali degli ordini. Tutte le istanze devono essere conformi all&#39;espressione regolare `^[A-Z]{3}$`. Gli esempi includono `USD` e `EUR`. |
| `priceTotal` | Doppio | Il prezzo totale di questo ordine dopo che tutti gli sconti e le tasse sono stati applicati. |
| `purchaseID` | Stringa | Identificatore univoco assegnato dal venditore per l&#39;acquisto o il contratto. Poiché questo è definito dal venditore, non vi è alcuna garanzia che l&#39;ID sia univoco. |
| `purchaseOrderNumber` | Stringa | Identificatore univoco assegnato dall&#39;acquirente per l&#39;acquisto o il contratto. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)