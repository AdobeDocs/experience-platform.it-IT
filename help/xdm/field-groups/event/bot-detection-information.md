---
title: Gruppo di campi di rilevamento bot
description: Scopri il gruppo di campi dello schema Gruppo di campi Rilevamento bot (XDM).
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 7%

---

# [!UICONTROL Gruppo di campi Rilevamento bot]

[!UICONTROL Rilevamento bot] è un gruppo di campi dello schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce informazioni sul traffico generato da bot.

![Diagramma del gruppo di campi [!UICONTROL Rilevamento bot].](../../images/field-groups/bot-detection-information.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Rilevamento bot] | `botDetection` | oggetto | Fornisce informazioni sul traffico generato da bot. |
| [!UICONTROL Punteggio] | `score` | numero | Il punteggio di probabilità bot da zero a uno. Un punteggio pari a zero significa che il traffico non è un bot. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
