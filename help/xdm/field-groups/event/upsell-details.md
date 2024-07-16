---
title: Gruppo di campi dello schema dei dettagli di upselling
description: Scopri il gruppo di campi dello schema Dettagli di vendita in upselling.
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Dettagli di vendita in upselling] gruppo di campi schema

[!UICONTROL Dettagli di vendita in upselling] è un gruppo di campi dello schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzata per acquisire informazioni relative a un evento di marketing di vendita in upselling, inclusi i dettagli sulla transazione e i diversi modi in cui l&#39;offerta è stata visualizzata a un cliente.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `upsells`. Le proprietà contenute in questo oggetto sono illustrate di seguito.

![Struttura dei dettagli della vendita in upselling](../../images/field-groups/upsell-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `upsellImpressions` | Array di [impression](../../data-types/impressions.md) | Un array che elenca le impression registrate (visualizzazioni digitali o impegni con l’offerta di upselling) per il cliente. |
| `upsellTransaction` | [Transazione](../../data-types/transaction.md) | Descrive la transazione di valuta per la vendita in upselling. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
