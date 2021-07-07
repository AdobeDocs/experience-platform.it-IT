---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;schema;schema di schema;gruppo di campi;gruppo di campi;ambiente;dettagli ambiente;
solution: Experience Platform
title: Gruppo campi schema dettagli ambiente
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli ambiente ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---


# [!UICONTROL Environment Details] schema field group

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Environment Details] is a standard schema field group for the [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) used to capture information regarding environment details related to an Experience Event such as device details, browser information, local time, and other geographical information.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Descrive un&#39;istanza identificata del browser del dispositivo, dell&#39;applicazione o del dispositivo che può essere monitorata tra sessioni, normalmente tramite cookie. |
| `environment` | [Ambiente](../../data-types/environment.md) | Descrive le informazioni sul contesto situazionale dell&#39;osservazione dell&#39;evento, specificatamente specificando informazioni transitorie come le versioni di rete o software. |
| `placeContext` | [Place context](../../data-types/place-context.md) | Descrive le circostanze transitorie relative all&#39;osservazione dell&#39;evento. Gli esempi includono informazioni specifiche per le impostazioni internazionali, ad esempio il tempo, l’ora locale, il traffico, il giorno della settimana, il giorno lavorativo rispetto a festivo e l’orario di lavoro. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
