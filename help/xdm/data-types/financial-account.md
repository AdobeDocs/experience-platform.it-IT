---
title: Tipo di dati conto finanziario
description: Questo documento fornisce una panoramica del tipo di dati XDM del conto finanziario.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 8%

---

# [!UICONTROL Conto finanziario] tipo di dati

[!UICONTROL Conto finanziario] è un tipo di dati XDM standard che descrive i dettagli di un conto finanziario, inclusi il tipo, il proprietario e il saldo corrente.

![](../images/data-types/financial-account.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Valuta]](./currency.md) | Saldo corrente del conto. |
| `financialAccountId` | [!UICONTROL Stringa] | Un ID univoco per l&#39;account. |
| `financialAccountName` | [!UICONTROL Stringa] | Nome assegnato all&#39;account. |
| `financialAccountType` | [!UICONTROL Stringa] | Tipo di conto finanziario, ad esempio controllo, risparmio o ritiro. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
