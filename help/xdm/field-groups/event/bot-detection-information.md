---
title: Gruppo di campi di rilevamento bot
description: Scopri il gruppo di campi dello schema Gruppo di campi Rilevamento bot (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 4%

---

# [!UICONTROL Rilevamento bot] gruppo di campi

[!UICONTROL Rilevamento bot] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce informazioni sul traffico generato da bot.

![Un diagramma del [!UICONTROL Rilevamento bot] gruppo di campi.](../../images/field-groups/bot-detection-information.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Rilevamento bot] | `botDetection` | oggetto | Fornisce informazioni sul traffico generato da bot. |
| [!UICONTROL Punteggio] | `score` | number | Il punteggio di probabilità bot da zero a uno. Un punteggio pari a zero significa che il traffico non è un bot. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)

