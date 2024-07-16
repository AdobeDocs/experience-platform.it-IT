---
title: Tipo di dati articolo rimborso
description: Scopri il tipo di dati Experience Data Model (XDM) per l’elemento di rimborso.
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---

# Tipo di dati [!UICONTROL Elemento di rimborso]

[!UICONTROL L&#39;elemento di rimborso] è un tipo di dati XDM (Experience Data Model) standard che descrive le acquisizioni delle informazioni relative a un rimborso associato a un ordine.

![Diagramma del tipo di dati Elemento di rimborso.](../images/data-types/refund-item.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL ID transazione] | `transactionID` | stringa | L&#39;identificatore univoco della transazione per questo elemento di rimborso. |
| [!UICONTROL Importo rimborso] | `refundAmount` | numero | Il valore del rimborso. |
| [!UICONTROL Motivo rimborso] | `refundReason` | stringa | Motivo per cui è stato emesso un rimborso. |
| [!UICONTROL Tipo di pagamento rimborso] | `refundPaymentType` | stringa | Il metodo di pagamento per questo ordine. Sono consentiti valori personalizzati. |
| [!UICONTROL Codice valuta] | `currencyCode` | stringa | Il codice valuta ISO 4217 utilizzato per questo elemento di rimborso. Ad esempio: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
