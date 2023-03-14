---
title: Gruppo di campi schema trasferimenti saldo
description: Questo documento fornisce una panoramica del gruppo di campi schema Trasferimenti saldo.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 3%

---

# [!UICONTROL Trasferimenti saldo] gruppo di campi schema

[!UICONTROL Trasferimenti saldo] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `personalFinances.balanceTransfers` oggetto a uno schema, che acquisisce i dettagli relativi a un trasferimento del saldo finanziario tra conti.

![](../../images/field-groups/balance-transfers.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Conto finanziario]](../../data-types/financial-account.md) | Descrive il conto finanziario da cui viene trasferito il saldo. |
| `accountTo` | [[!UICONTROL Conto finanziario]](../../data-types/financial-account.md) | Descrive il conto finanziario a cui viene trasferito il saldo. |
| `transaction` | [[!UICONTROL Transazione]](../../data-types/transaction.md) | Descrive la transazione finanziaria associata al trasferimento del saldo. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
