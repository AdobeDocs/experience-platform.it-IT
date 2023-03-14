---
title: Gruppo di campi schema dettagli applicazione
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli applicazione.
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 3%

---

# [!UICONTROL Dettagli applicazione] gruppo di campi schema

[!UICONTROL Dettagli applicazione] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `application` oggetto in uno schema, che acquisisce dettagli relativi all’applicazione come arresti anomali, utilizzo della funzione, avvii e aggiornamenti.

![](../../images/field-groups/application-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `application` | [[!UICONTROL Applicazione]](../../data-types/financial-account.md) | Acquisisce informazioni sull’applicazione relative a un evento, tra cui il nome dell’applicazione, la versione dell’app, le installazioni, i lanci, gli arresti anomali e le chiusure. Potrebbe essere l’applicazione interessata dall’evento (ad esempio, la destinazione per l’invio di una notifica push) o l’applicazione che dà origine all’evento (ad esempio, un clic o un accesso). |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
