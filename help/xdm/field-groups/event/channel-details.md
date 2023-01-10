---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo campi schema dettagli canale
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli canale .
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# [!UICONTROL Dettagli canale] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli canale] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md), utilizzato per descrivere le informazioni sul canale come ID, tipo di canale, tipo di supporto e tipo di posizione.

![](../../images/field-groups/channel-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `channel` | [Canale esperienza](../../data-types/experience-channel.md) | Oggetto che descrive le restituzioni dei prodotti, la registrazione della garanzia e i processi relativi al carrello o all&#39;ordine. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
