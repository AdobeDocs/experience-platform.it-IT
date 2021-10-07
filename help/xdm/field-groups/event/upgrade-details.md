---
title: Gruppo campi schema dettagli aggiornamento
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli di aggiornamento.
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---

# [!UICONTROL Aggiorna il gruppo di campi ] Detailsschema

[!UICONTROL Aggiorna ] i dettagli un gruppo di campi dello schema standard per la  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) classe utilizzata per acquisire informazioni su un evento di marketing di aggiornamento, inclusi dettagli sulla transazione e sulle diverse modalità di visualizzazione dell&#39;offerta a un cliente.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `upgrades`. Le proprietà contenute in questo oggetto sono illustrate di seguito.

![Struttura dei dettagli di aggiornamento](../../images/field-groups/upgrade-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `upgradeImpressions` | Array di [Impressioni](../../data-types/impressions.md) | Array che elenca le impression registrate (visualizzazioni digitali o coinvolgimenti nell’offerta di aggiornamento) per il cliente. |
| `upgradeTransaction` | [Transazione](../../data-types/transaction.md) | Descrive la transazione di valuta per l&#39;aggiornamento. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
