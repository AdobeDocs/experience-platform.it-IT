---
title: Gruppo di campi dello schema dei dettagli di aggiornamento
description: Scopri il gruppo di campi dello schema Dettagli aggiornamento.
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Aggiorna dettagli] gruppo di campi schema

[!UICONTROL Dettagli aggiornamento] è un gruppo di campi dello schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzata per acquisire informazioni relative a un evento di marketing di aggiornamento, inclusi i dettagli sulla transazione e i diversi modi in cui l&#39;offerta è stata visualizzata a un cliente.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `upgrades`. Le proprietà contenute in questo oggetto sono illustrate di seguito.

![Struttura dettagli aggiornamento](../../images/field-groups/upgrade-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `upgradeImpressions` | Array di [impression](../../data-types/impressions.md) | Un array che elenca le impression registrate (visualizzazioni digitali o impegni con l’offerta di aggiornamento) per il cliente. |
| `upgradeTransaction` | [Transazione](../../data-types/transaction.md) | Descrive la transazione di valuta per l&#39;aggiornamento. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
