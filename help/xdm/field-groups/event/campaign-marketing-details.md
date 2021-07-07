---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Campaign Marketing Details Schema Field Group
topic-legacy: overview
description: This document provides an overview of the Campaign Marketing Details schema field group.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---


# [!UICONTROL Campaign Marketing Details] schema field group

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Campaign Marketing Details] is a standard schema field group for the [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), used to describe marketing campaign information such as campaign group, name, and tracking code.

![](../../images/field-groups/campaign-marketing-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Un oggetto che descrive informazioni sulla campagna di marketing come gruppo di campagne, nome e codice di tracciamento. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
