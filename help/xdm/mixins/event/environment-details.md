---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;progettazione schema;mixin;mixin;ambiente;dettagli ambiente;
solution: Experience Platform
title: Dettagli ambiente Mixin
topic-legacy: overview
description: Questo documento fornisce una panoramica del mixin Dettagli ambiente ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 2%

---

# [!UICONTROL Environment Details] mescolina

>[!NOTE]
>
>I nomi di diversi mixin sono cambiati. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi mixin](../name-updates.md) .

[!UICONTROL Environment Details] è un mixin standard per la  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) classe utilizzata per acquisire informazioni relative ai dettagli dell’ambiente relativi a un evento di esperienza, come dettagli del dispositivo, informazioni sul browser, ora locale e altre informazioni geografiche.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Descrive un&#39;istanza identificata del browser del dispositivo, dell&#39;applicazione o del dispositivo che può essere monitorata tra sessioni, normalmente tramite cookie. |
| `environment` | [Ambiente](../../data-types/environment.md) | Descrive le informazioni sul contesto situazionale dell&#39;osservazione dell&#39;evento, specificatamente specificando informazioni transitorie come le versioni di rete o software. |
| `placeContext` | [Posizionare il contesto](../../data-types/place-context.md) | Descrive le circostanze transitorie relative all&#39;osservazione dell&#39;evento. Gli esempi includono informazioni specifiche per le impostazioni internazionali, ad esempio il tempo, l’ora locale, il traffico, il giorno della settimana, il giorno lavorativo rispetto a festivo e l’orario di lavoro. |

Per ulteriori dettagli sul mixin, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
