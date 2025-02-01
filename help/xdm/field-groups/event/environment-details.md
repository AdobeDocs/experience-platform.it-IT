---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;environment;environment details;
solution: Experience Platform
title: Gruppo di campi schema Dettagli ambiente
description: Scopri il gruppo di campi schema Dettagli ambiente ExperienceEvent.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 2%

---


# [!UICONTROL Dettagli ambiente] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [](../name-updates.md).

[!UICONTROL Dettagli ambiente] è un gruppo di campi dello schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzata per acquisire informazioni sui dettagli dell&#39;ambiente relativi a un evento esperienza, ad esempio i dettagli del dispositivo, le informazioni del browser, l&#39;ora locale e altre informazioni geografiche.

![](../../images/field-groups/environment-details.png){width=500}

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Descrive un dispositivo identificato, un’applicazione o un’istanza del browser del dispositivo che è tracciabile nelle sessioni, normalmente tramite i cookie. |
| `environment` | [Ambiente](../../data-types/environment.md) | Descrive informazioni sul contesto situazionale dell’osservazione dell’evento, specificando informazioni transitorie come la rete o le versioni del software. |
| `placeContext` | [Inserisci contesto](../../data-types/place-context.md) | Descrive le circostanze transitorie relative all’osservazione dell’evento. Alcuni esempi includono informazioni specifiche per le impostazioni locali come meteo, ora locale, traffico, giorno della settimana, giorno lavorativo o festivo e orario di lavoro. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
