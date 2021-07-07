---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo campi schema dettagli canale
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli canale .
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 3%

---


# [!UICONTROL Gruppo di campi ] Dettaglio canale

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Dettaglio canale ] è un gruppo di campi schema standard per la  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilizzato per descrivere le informazioni sul canale come ID, tipo di canale, tipo di supporto e tipo di posizione.

![](../../images/field-groups/channel-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `channel` | [Canale esperienza](../../data-types/experience-channel.md) | Oggetto che descrive le restituzioni dei prodotti, la registrazione della garanzia e i processi relativi al carrello o all&#39;ordine. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
