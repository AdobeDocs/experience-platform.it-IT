---
title: Gruppo di campi schema dettagli applicazione
description: Scopri il gruppo di campi dello schema Dettagli applicazione.
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 3%

---

# [!UICONTROL Dettagli applicazione] gruppo di campi dello schema

[!UICONTROL Dettagli applicazione] è un gruppo di campi dello schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo oggetto `application` a uno schema, che acquisisce dettagli relativi all&#39;applicazione come arresti anomali, utilizzo delle funzionalità, avvii e aggiornamenti.

![](../../images/field-groups/application-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `application` | [[!UICONTROL Applicazione]](../../data-types/financial-account.md) | Acquisisce informazioni sull’applicazione relative a un evento, tra cui il nome dell’applicazione, la versione dell’app, le installazioni, i lanci, gli arresti anomali e le chiusure. Potrebbe essere l’applicazione interessata dall’evento (ad esempio, la destinazione per l’invio di una notifica push) o l’applicazione che dà origine all’evento (ad esempio, un clic o un accesso). |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
