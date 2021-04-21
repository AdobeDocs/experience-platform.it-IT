---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;elemento di pagamento;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati elemento di pagamento
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Payment Item Experience Data Model).
exl-id: d25a358b-73c1-468b-a9c5-808385689932
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 3%

---

# [!UICONTROL Payment Item] tipo di dati

[!UICONTROL Payment Item] è un tipo di dati XDM (Experience Data Model) standard che descrive un pagamento associato a un ordine che definisce il tipo di pagamento, l’importo e la valuta associata.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `currencyCode` | Stringa | Codice valuta ISO 4217 utilizzato per i totali dell&#39;ordine. Tutte le istanze devono essere conformi all&#39;espressione regolare `^[A-Z]{3}$`. Gli esempi includono `USD` e `EUR`. |
| `paymentAmount` | Doppio | Valore del pagamento. |
| `paymentType` | Stringa | Modalità di pagamento dell&#39;ordine. I valori enum accettati includono: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Stringa | Identificatore univoco della transazione per l&#39;elemento di pagamento. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
