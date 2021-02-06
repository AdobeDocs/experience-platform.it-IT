---
keywords: ' Experience Platform;home;temi comuni;schema;schema;XDM;campi;schemi;elemento di pagamento;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo dati elemento pagamento
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Payment Item Experience Data Model).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 3%

---


# [!UICONTROL Payment Item] tipo di dati

[!UICONTROL Payment Item] è un tipo di dati XDM (Experience Data Model) standard che descrive un pagamento associato a un ordine che definisce il tipo di pagamento, l&#39;importo e la valuta associata.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `currencyCode` | Stringa | Codice valuta ISO 4217 utilizzato per i totali degli ordini. Tutte le istanze devono essere conformi all&#39;espressione regolare `^[A-Z]{3}$`. Gli esempi includono `USD` e `EUR`. |
| `paymentAmount` | Doppio | Valore del pagamento. |
| `paymentType` | Stringa | Metodo di pagamento per questo ordine. I valori enum accettati includono: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Stringa | Identificatore univoco della transazione per questo elemento di pagamento. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)