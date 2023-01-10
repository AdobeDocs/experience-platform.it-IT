---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;ordine;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati ordine
description: Questo documento fornisce una panoramica del tipo di dati XDM (Order Experience Data Model).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 5%

---

# [!UICONTROL Ordine] tipo di dati

[!UICONTROL Ordine] è un tipo di dati XDM (Experience Data Model) standard che descrive l’ordine inserito per un elenco di prodotti.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `payments` | Array di [[!UICONTROL Elementi di pagamento]](./payment-item.md) | L&#39;elenco dei pagamenti per questo ordine. |
| `currencyCode` | Stringa | Codice valuta ISO 4217 utilizzato per i totali dell&#39;ordine. Tutte le istanze devono essere conformi all&#39;espressione regolare `^[A-Z]{3}$`. Esempi `USD` e `EUR`. |
| `priceTotal` | Doppio | Il prezzo totale di questo ordine dopo che tutti gli sconti e le imposte sono stati applicati. |
| `purchaseID` | Stringa | Identificatore univoco assegnato dal venditore per l&#39;acquisto o il contratto. Poiché questo è definito dal venditore, non vi è alcuna garanzia che l&#39;ID sia univoco. |
| `purchaseOrderNumber` | Stringa | Identificatore univoco assegnato dall&#39;acquirente per l&#39;acquisto o il contratto. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
