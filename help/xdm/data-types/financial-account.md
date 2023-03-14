---
title: Tipo di dati del conto finanziario
description: Questo documento fornisce una panoramica del tipo di dati XDM del conto finanziario.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 7%

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
