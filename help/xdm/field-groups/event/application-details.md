---
title: Gruppo campi schema dettagli applicazione
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli applicazione.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 4%

---

# [!UICONTROL Dettagli applicazione] gruppo di campi schema

[!UICONTROL Dettagli applicazione] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `application` a uno schema che acquisisce i dettagli relativi all&#39;applicazione quali arresti anomali, utilizzo di funzioni, avvii e aggiornamenti.

![](../../images/field-groups/application-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `application` | [[!UICONTROL Applicazione]](../../data-types/financial-account.md) | Acquisisce le informazioni relative all’applicazione relative a un evento, tra cui il nome dell’applicazione, la versione dell’app, le installazioni, gli avvii, gli arresti e le chiusure. Potrebbe essere l’applicazione oggetto dell’evento (ad esempio la destinazione per una notifica push inviata) o l’applicazione che ha generato l’evento (ad esempio un clic o un accesso). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
