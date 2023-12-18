---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;
solution: Experience Platform
title: Gruppo di campi schema dettagli canale
description: Scopri il gruppo di campi dello schema Dettagli canale.
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# [!UICONTROL Dettagli canale] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Vedi il documento su [aggiornamenti nome gruppo di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli canale] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilizzato per descrivere informazioni sul canale come ID, tipo di canale, tipo di supporto e tipo di posizione.

![](../../images/field-groups/channel-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `channel` | [Canale esperienza](../../data-types/experience-channel.md) | Oggetto che descrive le restituzioni dei prodotti, la registrazione della garanzia e i processi relativi a carrello acquisti e ordini. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
