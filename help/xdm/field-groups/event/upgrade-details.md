---
title: Gruppo di campi dello schema dei dettagli di aggiornamento
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli aggiornamento.
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 2%

---

# [!UICONTROL Dettagli aggiornamento] gruppo di campi schema

[!UICONTROL Dettagli aggiornamento] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzato per acquisire informazioni relative a un evento di marketing di aggiornamento, inclusi dettagli sulla transazione e sulle diverse modalità di visualizzazione dell’offerta a un cliente.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `upgrades`. Le proprietà contenute in questo oggetto sono illustrate di seguito.

![Struttura dei dettagli di aggiornamento](../../images/field-groups/upgrade-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `upgradeImpressions` | Array di [Impression](../../data-types/impressions.md) | Un array che elenca le impression registrate (visualizzazioni digitali o impegni con l’offerta di aggiornamento) per il cliente. |
| `upgradeTransaction` | [Transazione](../../data-types/transaction.md) | Descrive la transazione di valuta per l&#39;aggiornamento. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
