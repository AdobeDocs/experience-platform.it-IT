---
title: Gruppo di campi schema dettagli versamento
description: Scopri il gruppo di campi dello schema Dettagli versamento.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 4%

---

# [!UICONTROL Dettagli versamento] gruppo di campi dello schema

[!UICONTROL Dettagli versamento] è un gruppo di campi di schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo campo `personalFinances.deposits` a uno schema, che acquisisce i dettagli di un deposito finanziario.

![](../../images/field-groups/deposit-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `account` | [[!UICONTROL Conto Finanziario]](../../data-types/financial-account.md) | Descrive il conto finanziario associato al deposito. |
| `transaction` | [[!UICONTROL Transazione]](../../data-types/transaction.md) | Descrive la transazione finanziaria associata al deposito. |
| `mobileDeposit` | [!UICONTROL Booleano] | Indica se il versamento è stato effettuato tramite una piattaforma mobile. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
