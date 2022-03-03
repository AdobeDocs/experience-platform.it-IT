---
title: Gruppo campi schema dettagli depositi
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli depositi.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 5%

---

# [!UICONTROL Dettagli sui depositi] gruppo di campi schema

[!UICONTROL Dettagli sui depositi] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `personalFinances.deposits` a uno schema che acquisisce i dettagli su un deposito finanziario.

![](../../images/field-groups/deposit-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `account` | [[!UICONTROL Conto finanziario]](../../data-types/financial-account.md) | Descrive il conto finanziario associato al deposito. |
| `transaction` | [[!UICONTROL Transazione]](../../data-types/transaction.md) | Descrive la transazione finanziaria associata al deposito. |
| `mobileDeposit` | [!UICONTROL Booleano] | Indica se il deposito è stato effettuato tramite una piattaforma mobile. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
