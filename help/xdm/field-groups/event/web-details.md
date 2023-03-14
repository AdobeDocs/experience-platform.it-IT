---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;
solution: Experience Platform
title: Gruppo di campi schema Dettagli Web
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema Dettagli Web.
exl-id: eb42606b-ade4-4d72-b601-c560009c98e8
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---

# [!UICONTROL Dettagli web] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Vedi il documento su [aggiornamenti nome gruppo di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli web] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilizzato per descrivere informazioni relative a eventi di dettagli web come interazione, dettagli della pagina e referrer.

![](../../images/field-groups/web-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `web` | [Informazioni web](../../data-types/web-information.md) | Descrive i clic sui collegamenti, i dettagli della pagina web, le informazioni sul referente e i dettagli del browser. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.schema.json)
