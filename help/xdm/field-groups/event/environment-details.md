---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;schema;schema di schema;gruppo di campi;gruppo di campi;ambiente;dettagli ambiente;
solution: Experience Platform
title: Gruppo campi schema dettagli ambiente
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli ambiente ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---


# [!UICONTROL Environment Details] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Environment Details] è un gruppo di campi di schema standard per la  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) classe utilizzata per acquisire informazioni relative ai dettagli dell’ambiente relativi a un evento esperienza, ad esempio dettagli del dispositivo, informazioni sul browser, ora locale e altre informazioni geografiche.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Descrive un&#39;istanza identificata del browser del dispositivo, dell&#39;applicazione o del dispositivo che può essere monitorata tra sessioni, normalmente tramite cookie. |
| `environment` | [Ambiente](../../data-types/environment.md) | Descrive le informazioni sul contesto situazionale dell&#39;osservazione dell&#39;evento, specificatamente specificando informazioni transitorie come le versioni di rete o software. |
| `placeContext` | [Posizionare il contesto](../../data-types/place-context.md) | Descrive le circostanze transitorie relative all&#39;osservazione dell&#39;evento. Gli esempi includono informazioni specifiche per le impostazioni internazionali, ad esempio il tempo, l’ora locale, il traffico, il giorno della settimana, il giorno lavorativo rispetto a festivo e l’orario di lavoro. |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
