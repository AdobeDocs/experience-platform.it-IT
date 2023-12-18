---
title: Tipo di dati articolo rimborso
description: Scopri il tipo di dati Experience Data Model (XDM) per l’elemento di rimborso.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---

# [!UICONTROL Rimborso articolo] tipo di dati

[!UICONTROL Rimborso articolo] è un tipo di dati XDM (Experience Data Model) standard che descrive le informazioni acquisite relative a un rimborso associato a un ordine.

![Diagramma del tipo di dati Articolo di rimborso.](../images/data-types/refund-item.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL ID transazione] | `transactionID` | string | L&#39;identificatore univoco della transazione per questo elemento di rimborso. |
| [!UICONTROL Importo rimborso] | `refundAmount` | number | Il valore del rimborso. |
| [!UICONTROL Motivo rimborso] | `refundReason` | string | Motivo per cui è stato emesso un rimborso. |
| [!UICONTROL Tipo di pagamento rimborso] | `refundPaymentType` | string | Il metodo di pagamento per questo ordine. Sono consentiti valori personalizzati. |
| [!UICONTROL Codice valuta] | `currencyCode` | string | Il codice valuta ISO 4217 utilizzato per questo elemento di rimborso. Ad esempio: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
