---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;elemento di pagamento;tipo dati;tipo dati;tipo dati;tipo dati;home;popular topic;schema;Schema;XDM;fields;schemas;Schemas;payment item;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati elemento di pagamento
description: Scopri il tipo di dati XDM (Payment Item Experience Data Model).
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 14%

---

# Tipo di dati [!UICONTROL Elemento pagamento]

[!UICONTROL Elemento pagamento] è un tipo di dati XDM (Experience Data Model) standard che descrive un pagamento associato a un ordine che definisce il tipo di pagamento, l&#39;importo e la valuta associata.

![immagine elemento pagamento](../images/data-types/payment-item.PNG){width=400}

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `currencyCode` | Stringa | Il codice valuta ISO 4217 utilizzato per i totali dell’ordine. Tutte le istanze devono essere conformi all&#39;espressione regolare `^[A-Z]{3}$`. Gli esempi includono `USD` e `EUR`. |
| `paymentAmount` | Doppio | Il valore del pagamento. |
| `paymentType` | Stringa | Il metodo di pagamento per questo ordine. I valori enum accettati includono: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Stringa | L’identificatore univoco di transazione per questo elemento di pagamento. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
