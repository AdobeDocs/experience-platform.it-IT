---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;ordine;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati ordine
description: Questo documento fornisce una panoramica del tipo di dati XDM (Order Experience Data Model).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---

# [!UICONTROL Ordine] tipo di dati

[!UICONTROL Ordine] è un tipo di dati Experience Data Model (XDM) standard che descrive l’ordine effettuato per un elenco di prodotti.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `payments` | Array di [[!UICONTROL Voci di pagamento]](./payment-item.md) | Elenco dei pagamenti per questo ordine. |
| `currencyCode` | Stringa | Il codice valuta ISO 4217 utilizzato per i totali dell’ordine. Tutte le istanze devono essere conformi all&#39;espressione regolare `^[A-Z]{3}$`. Alcuni esempi includono `USD` e `EUR`. |
| `priceTotal` | Doppio | Il prezzo totale dell&#39;ordine dopo l&#39;applicazione di tutti gli sconti e le imposte. |
| `purchaseID` | Stringa | Un identificatore univoco assegnato dal venditore per questo acquisto o contratto. Poiché è definito dal venditore, non c&#39;è garanzia che l&#39;ID sia univoco. |
| `purchaseOrderNumber` | Stringa | L’identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
