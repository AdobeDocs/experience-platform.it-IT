---
title: Gruppo di campi schema trasferimenti saldo
description: Scopri il gruppo di campi dello schema Trasferimenti saldo.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 3%

---

# [!UICONTROL Trasferimenti saldo] gruppo di campi schema

[!UICONTROL Trasferimenti saldo] è un gruppo di campi dello schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo oggetto `personalFinances.balanceTransfers` a uno schema, che acquisisce dettagli su un trasferimento del saldo finanziario tra conti.

![](../../images/field-groups/balance-transfers.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Conto Finanziario]](../../data-types/financial-account.md) | Descrive il conto finanziario da cui viene trasferito il saldo. |
| `accountTo` | [[!UICONTROL Conto Finanziario]](../../data-types/financial-account.md) | Descrive il conto finanziario a cui viene trasferito il saldo. |
| `transaction` | [[!UICONTROL Transazione]](../../data-types/transaction.md) | Descrive la transazione finanziaria associata al trasferimento del saldo. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
