---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;
solution: Experience Platform
title: Gruppo di campi dello schema dei dettagli di marketing della campagna
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli marketing campagna.
exl-id: be08b38b-68a0-4a74-9b8f-0344a0637395
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 2%

---

# [!UICONTROL Dettagli di marketing della campagna] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Vedi il documento su [aggiornamenti nome gruppo di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli di marketing della campagna] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilizzato per descrivere le informazioni della campagna di marketing come il gruppo della campagna, il nome e il codice di tracciamento.

![](../../images/field-groups/campaign-marketing-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Oggetto che descrive le informazioni della campagna di marketing, ad esempio il gruppo della campagna, il nome e il codice di tracciamento. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
