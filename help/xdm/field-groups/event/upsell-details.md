---
title: Gruppo campi schema dettagli di upselling
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli di upselling .
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---

# [!UICONTROL Gruppo di campi ] Detailsschema di upselling

[!UICONTROL Upselling ] Details è un gruppo di campi di schema standard per la  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) classe utilizzato per acquisire informazioni relative a un evento di marketing di upselling, con dettagli sulla transazione e sui diversi modi in cui l’offerta è stata visualizzata a un cliente.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `upsells`. Le proprietà contenute in questo oggetto sono illustrate di seguito.

![Struttura dei dettagli di upselling](../../images/field-groups/upsell-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `upsellImpressions` | Array di [Impressioni](../../data-types/impressions.md) | Array che elenca le impression registrate (visualizzazioni digitali o coinvolgimenti nell’offerta di upselling) per il cliente. |
| `upsellTransaction` | [Transazione](../../data-types/transaction.md) | Descrive la transazione di valuta per l&#39;upselling. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
