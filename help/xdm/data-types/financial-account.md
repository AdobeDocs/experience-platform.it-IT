---
title: Tipo di dati del conto finanziario
description: Scopri il tipo di dati XDM dell’account finanziario.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 8%

---

# [!UICONTROL Conto finanziario] tipo di dati

[!UICONTROL Conto finanziario] è un tipo di dati XDM standard che descrive i dettagli di un conto finanziario, tra cui il tipo, il proprietario e il saldo corrente.

![](../images/data-types/financial-account.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Valuta]](./currency.md) | Saldo corrente del conto. |
| `financialAccountId` | [!UICONTROL Stringa] | Un ID univoco per l’account. |
| `financialAccountName` | [!UICONTROL Stringa] | Nome assegnato all’account. |
| `financialAccountType` | [!UICONTROL Stringa] | Tipo di conto finanziario, ad esempio conto corrente, conto di risparmio o pensione. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
