---
title: Gruppo di campi schema trasferimenti saldo
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Trasferimento saldi.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 4%

---

# [!UICONTROL Trasferimenti di saldo] gruppo di campi schema

[!UICONTROL Trasferimenti di saldo] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `personalFinances.balanceTransfers` oggetto di uno schema che acquisisce i dettagli relativi a un trasferimento di saldo finanziario tra conti.

![](../../images/field-groups/balance-transfers.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Conto finanziario]](../../data-types/financial-account.md) | Descrive il conto finanziario da cui viene trasferito il saldo. |
| `accountTo` | [[!UICONTROL Conto finanziario]](../../data-types/financial-account.md) | Descrive il conto finanziario a cui viene trasferito il saldo. |
| `transaction` | [[!UICONTROL Transazione]](../../data-types/transaction.md) | Descrive la transazione finanziaria associata al trasferimento del saldo. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
